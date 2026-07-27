# Publishing to the internet (free) + installing as a mobile app

Goal: put both calculators online at **https://tax.myfirsttradingbot.com** using
**GitHub Pages** (free), so they're also installable on your phone as apps (PWA).

Everything below is already prepped in this folder:
- ✅ git repo initialized and all files committed
- ✅ `CNAME` file set to `tax.myfirsttradingbot.com`
- ✅ `.nojekyll` so the `india/` and `usa/` folders are served correctly
- ✅ GitHub CLI (`gh`) installed on this PC (v2.96.0)

---

## ⚠️ Run these in YOUR OWN PowerShell window
Open PowerShell yourself (Start → type "PowerShell" → Enter).
Do NOT use an in-app "Run" button — Step 1 opens your browser to sign in, which only
works in your own terminal. Your password is never shown to anyone.

---

### Step 1 — Sign in to GitHub (one time)
```
gh auth login
```
Answer the prompts:
- **What account?** → `GitHub.com`
- **Preferred protocol?** → `HTTPS`
- **Authenticate Git with your GitHub credentials?** → `Yes`
- **How to authenticate?** → `Login with a web browser`
- Copy the one-time code shown, press **Enter**, approve in the browser that opens.

> If PowerShell says `gh` is not recognized, close and reopen PowerShell so it picks
> up the newly installed CLI, then try again.

---

### Step 2 — Create the repo and publish (one command)
```
cd "C:\Users\k_goy\Desktop\TaxApps"; gh repo create taxapps --public --source=. --remote=origin --push
```
Creates a public repo named `taxapps` under your account and pushes all files.
**This is the actual "publish to the internet" step.**

---

### Step 3 — Turn on GitHub Pages
Open (replace `<your-username>`):
```
https://github.com/<your-username>/taxapps/settings/pages
```
Set:
- **Source:** Deploy from a branch
- **Branch:** `main`  **Folder:** `/ (root)`  → **Save**
- The **Custom domain** field auto-fills with `tax.myfirsttradingbot.com` (from the
  CNAME file). Leave it as-is.

---

### Step 4 — Add ONE DNS record
At whatever service manages DNS for `myfirsttradingbot.com` (the same place you pointed
the domain at your GCP VM), add:

| Type  | Name / Host | Value / Target             | TTL     |
|-------|-------------|----------------------------|---------|
| CNAME | `tax`       | `<your-username>.github.io`| default |

This only ADDS a `tax` subdomain — your existing dashboard on the main domain is
untouched.

> Find your username: it's in your GitHub URL, or run `gh api user -q .login`

---

### Step 5 — Enforce HTTPS (required for the mobile app to install)
Return to the Pages settings page. About 15 minutes after the DNS record is live,
GitHub provisions a free HTTPS certificate — then tick:
- ✅ **Enforce HTTPS**

PWA installation requires HTTPS, so don't skip this.

---

## ✅ Result
- Live at **https://tax.myfirsttradingbot.com**
  - India app:  https://tax.myfirsttradingbot.com/india/
  - USA app:    https://tax.myfirsttradingbot.com/usa/
- On your phone: open the URL → choose an app → browser menu → **Add to Home Screen**
  → it installs like a native app (own icon, full-screen, works offline).
- DNS can take 10 minutes to ~1 hour to propagate the first time.

---

## Updating the apps later
After editing any file in this folder:
```
cd "C:\Users\k_goy\Desktop\TaxApps"; git add -A; git commit -m "Update"; git push
```
GitHub Pages redeploys automatically within a minute or two.

---

## Alternative: instant, no-account option (Netlify Drop)
If you'd rather skip GitHub entirely:
1. Go to **https://app.netlify.com/drop**
2. Drag the whole `TaxApps` folder onto the page.
3. You get a live `https://<name>.netlify.app` URL in seconds (also HTTPS, also
   PWA-installable). You can add a custom domain later in Netlify's settings.
