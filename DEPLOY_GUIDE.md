# Gift Card POS — Deploy Guide (Render)

Your app is ready to deploy. It uses PostgreSQL in the cloud and requires a
staff password to log in. `seed_data.json` is empty by default — the database
starts with zero cards; add your own via Add Card or the Import template.

## Step 1 — Put this folder on GitHub

1. Go to https://github.com and sign in (create a free account if needed).
2. Click **+** (top right) → **New repository**. Name it `giftcard-pos`, set it
   to **Private**, click **Create repository**.
3. On the new repo page, click **uploading an existing file**.
4. Drag ALL files from this folder in (including the `templates`
   folder and `seed_data.json`). Click **Commit changes**.

   *If drag-and-drop won't take the templates folder, install
   [GitHub Desktop](https://desktop.github.com), add this folder, and push.*

## Step 2 — Deploy on Render

1. Go to https://render.com and sign up **using your GitHub account**.
2. Click **New +** → **Blueprint**.
3. Select your `giftcard-pos` repository. Render reads `render.yaml`
   and sets up both the web app and the PostgreSQL database automatically.
4. It will ask for **APP_PASSWORD** — type the login password (e.g. `password123!`).
   The username is `admin` (set by APP_USERNAME in render.yaml; change it there
   or in the dashboard if you want a different one).
5. Click **Apply / Deploy** and wait ~3 minutes.
6. Your site is live at `https://giftcard-pos-XXXX.onrender.com`.
   Bookmark it on the shop computer/tablet.

## Step 3 — First login

Open the URL and sign in with username `admin` and the password you chose.
Everything works like the local version: Charge, Refill, All Cards (with
Remove), Add Card, Import Excel.

## Important notes

- **Free tier sleep:** the free web service sleeps after 15 minutes of no
  traffic; the first page load after that takes ~30-50 seconds. Upgrading to
  the $7/month Starter plan removes this.
- **Free database expires after ~30 days** on Render's free plan. Either
  upgrade the database to the paid tier ($7/month, recommended for real
  business data), or use a permanently-free PostgreSQL from https://neon.tech:
  create a Neon project, copy its connection string, and paste it as the
  `DATABASE_URL` environment variable in your Render web service settings.
- **Changing the password:** Render dashboard → your web service →
  Environment → edit `APP_PASSWORD` → Save (it redeploys automatically).
- **Backups:** All Cards page + Export from your database. On a paid Render
  database, backups are automatic. You can also re-import from Excel anytime.
- **Seed data loads only once** — when the database is empty. After that,
  the database in the cloud is the single source of truth.

## Running locally (optional)

```
pip install -r requirements.txt
python app.py
```
Open http://localhost:5000 — default local login is `admin` / `password123!`
(set the APP_USERNAME / APP_PASSWORD environment variables to change them).
