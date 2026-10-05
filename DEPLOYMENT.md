# GOOT Resorts — Online Demo Deployment

This pack is prepared for deploying the GOOT Resorts Node/Express + PostgreSQL demo to Render.

## 1. Put these files in the project root

Copy:
- `render.yaml`
- `.env.example`
- the contents of `.gitignore.additions` into your existing `.gitignore`

Do NOT upload `.env` or any real password/API/admin key to GitHub.

## 2. Push the complete GOOT project to GitHub

The repository root should contain the existing GOOT files plus:
- `server/`
- frontend files (`index.html`, `admin.html`, assets, css, js, etc.)
- `package.json`
- `render.yaml`

## 3. Create the Render deployment

Open Render and choose:
New → Blueprint

Connect the GitHub repository containing `render.yaml`.

Render will create:
- a Node web service
- a PostgreSQL database

Render Blueprints are designed to define the web service and Postgres database together.

## 4. Set the secrets

During Blueprint setup, Render will ask for values marked `sync: false`.

Set:

ADMIN_KEY
- Create a NEW demo-only admin key.
- Do not reuse a production/local secret if you can avoid it.

ALLOWED_ORIGINS
- First deploy the service.
- Copy the generated Render URL, for example:
  https://goot-resorts-demo.onrender.com
- Put that exact URL into ALLOWED_ORIGINS.
- Redeploy.

If your existing server uses a different environment-variable name for the admin key or allowed origins, keep the existing names used by the application and update `render.yaml` accordingly.

## 5. Verify

Open:

https://YOUR-RENDER-URL.onrender.com/api/health

Expected result should be similar to:

{"ok":true,"db":true}

Then open:

https://YOUR-RENDER-URL.onrender.com/

Admin:

https://YOUR-RENDER-URL.onrender.com/admin.html

## 6. Important production/demo rule

This should be a DEMO database.

Do not connect the public sales demo to your private/local production database.

Use only fake customer/booking data.

## 7. Update the Sales Preview

After Render gives you the real URL, replace the placeholder in:

`GOOT_Resorts_Sales_Preview.html`

with:

https://YOUR-RENDER-URL.onrender.com/

and the admin button with:

https://YOUR-RENDER-URL.onrender.com/admin.html

The preview can then be opened by a buyer on any laptop.

## 8. Custom domain

After the demo is working, you can attach a domain such as:

demo.gootresorts.com

Then the sales preview should use:

https://demo.gootresorts.com/
https://demo.gootresorts.com/admin.html

## 9. Security checklist before sending to buyers

- Use HTTPS.
- Use a separate demo database.
- Use a new demo admin key.
- Never commit `.env`.
- Never expose PostgreSQL credentials.
- Never expose your private production database.
- Keep Helmet/CSP and the existing server-side authentication enabled.
- Test login, bookings, cancellation/deletion, reports and revenue after deployment.
