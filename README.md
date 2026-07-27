# Income Tax Calculators — India 🇮🇳 & USA (Federal + Indiana) 🇺🇸

Two guided, mobile‑installable (PWA) income‑tax **estimators**. All data stays in the
browser (localStorage) — nothing is uploaded anywhere.

> ⚠️ **Educational estimators only.** Not a substitute for official e‑filing
> (Income Tax portal / IRS / Indiana DOR) or advice from a qualified CA / CPA / EA.
> Verify all figures before relying on them.

---

## 📂 Where the applications live

```
C:\Users\k_goy\Desktop\TaxApps\
├─ index.html                         ← landing page (links to both apps)
├─ README.md                          ← this file
│
├─ india\                             🇮🇳 INDIA APP
│   ├─ index.html                     ← open this to run the India calculator
│   ├─ manifest.webmanifest
│   ├─ sw.js
│   └─ icon.svg
│
├─ usa\                               🇺🇸 USA (FEDERAL + INDIANA) APP
│   ├─ index.html                     ← open this to run the USA calculator
│   ├─ manifest.webmanifest
│   ├─ sw.js
│   └─ icon.svg
│
├─ india_income_tax_calculator.html   ← ORIGINAL single-file version (superseded)
└─ us_federal_indiana_tax_calculator.html  ← ORIGINAL single-file version (superseded)
```

**To run locally right now:** double‑click `india\index.html` or `usa\index.html`.
(The guided app works offline as a file; the *installable* PWA + service‑worker
features only activate once the folder is hosted over HTTPS — see Publishing below.)

---

## ✅ Numbers to double‑check before publishing / filing

Every rate lives in one clearly‑commented `TAX_DATA` config block at the top of each
app's `<script>` (search the file for `EDIT RATES HERE`). Any correction is a one‑line edit.

### 🇺🇸 USA app — `usa\index.html`
| Priority | What to verify | Where / notes |
|---|---|---|
| 🔴 HIGH | **All tax‑year 2025 figures are PROVISIONAL** — federal brackets, standard deductions, LTCG/qualified‑dividend breakpoints, Social Security wage base ($176,100) | Confirm against **IRS.gov** once final inflation/legislative numbers are published |
| 🔴 HIGH | **Indiana county tax rate** — you must enter YOUR county's resident rate; it is not built in | Look up on **in.gov/dor** (varies by county, ~1%–3%) |
| 🟠 MED | **Indiana state flat rate 2025 = 3.00%** | Verify on in.gov/dor (rate has been stepping down over recent years) |
| 🟡 LOW | 2023 & 2024 federal brackets / standard deductions | Standard published IRS figures — spot‑check if desired |
| 🟡 LOW | Indiana exemption structure ($1,000 base, +$1,500 dependent child, age/blind add‑ons) | The separate "AGI < $40,000" senior add‑on is **not** implemented |
| ℹ️ NOTE | EITC is a **manual input** field (tables too large to embed); MAGI is approximated as AGI | Enter your EITC from the IRS tables if applicable |

### 🇮🇳 India app — `india\index.html`
| Priority | What to verify | Where / notes |
|---|---|---|
| 🔴 HIGH | **FY 2025‑26 (AY 2026‑27) new‑regime slabs, ₹75,000 std deduction, and the ₹12,00,000 / ₹60,000 rebate 87A** reflect **Budget 2025** | Confirm on **incometax.gov.in** — may change |
| 🟠 MED | Surcharge is applied uniformly on total tax — the **15% surcharge cap on the 111A/112A capital‑gains portion is NOT implemented** | Matters only for very high incomes with large capital gains |
| 🟠 MED | Capital‑gains rate split at **23‑Jul‑2024** (equity STCG 15%→20%, LTCG 10%→12.5%) — enter gains in the correct period bucket | See the in‑app help text on the Capital Gains step |
| 🟡 LOW | Old‑regime slabs are assumed **identical across all three AYs** | Correct as of build, but confirm |
| 🟡 LOW | 80CCD(2) employer‑NPS cap (10%/14% of salary) and exact 80D/80G caps are taken **as entered**, not auto‑capped | Enter eligible amounts only |
| ℹ️ NOTE | Special‑rate CG is taxed flat with no basic‑exemption adjustment for low‑income residents; NRI‑specific rules are shown as a note, not enforced | |

---

## 🌐 Publishing (free) + installing as a mobile app

A PWA must be served over **HTTPS** to install on a phone.

**Fastest (no account):** go to **app.netlify.com/drop** and drag this whole `TaxApps`
folder onto the page → you get a live `https://…netlify.app` URL in seconds. Open it on
your phone → pick an app → browser menu → **Add to Home Screen** → it installs like a
native app (icon, full‑screen, offline).

**Your own domain:** host on **GitHub Pages** (e.g. `tax.myfirsttradingbot.com`) — create
a repo, upload these files, enable Settings → Pages, and add a DNS CNAME.

---

## 🔧 Editing rates later
1. Open `india\index.html` or `usa\index.html` in any text editor.
2. Search for `EDIT RATES HERE`.
3. Change the number in the `TAX_DATA` object, save, refresh. Done.
