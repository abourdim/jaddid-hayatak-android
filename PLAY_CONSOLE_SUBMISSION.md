# Play Console submission — Jaddid Hayatak

Step-by-step submission guide for **jaddid-hayatak-android** to Google Play. Only the in-Play-Console UI bits remain to be done; everything else is shipped.

## ✅ Already done (no action from you)

| | Path |
|---|---|
| Signed release AAB | `releases/jaddid-hayatak-v1.0.aab` (3.0 MB, on the v1.0-debug GitHub Release) |
| Upload keystore | `~/.keys/wdiy-upload.keystore` (validity until 2053-09-11) |
| Privacy policy URL | https://abourdim.github.io/jaddid-hayatak-android/store-assets/privacy.html |
| Feature graphic 1024×500 | `store-assets/feature-graphic.png` (308 KB) |
| App icon 512×512 | `store-assets/play-store-icon-512.png` (151 KB) |
| AR/EN/FR listing copy | `PLAY_STORE_LISTING.md` (paste-ready) |
| GitHub Pages landing | https://abourdim.github.io/jaddid-hayatak-android/ |

## ❌ You need to do (Play Console UI work, ~30 min)

### Step 0 — Register a Play Console developer account ($25 one-time)
1. https://play.google.com/console
2. Sign in with the Google account you want to use as developer-of-record
3. Pay the **$25 one-time** registration fee
4. Verify identity (Google may ask for ID)

### Step 1 — Create the app
1. Play Console → **Create app**
2. App name: **Jaddid Hayatak** (use Arabic name later via translations)
3. Default language: **Arabic (Egypt)** or **English (United States)** — either works as primary
4. App or game: **App**
5. Free or paid: **Free**
6. Tick the two declarations (Developer Program Policies + US export laws)
7. Click **Create app**

### Step 2 — App content (left sidebar → Policy → App content)
For each, click **Start** and fill in:

| Section | What to declare |
|---|---|
| **Privacy policy** | URL → `https://abourdim.github.io/jaddid-hayatak-android/store-assets/privacy.html` |
| **App access** | All functionality available without restrictions |
| **Ads** | No |
| **Content rating** | Start the questionnaire → answer everything **No** (no violence, no crude humor, no sex, no gambling, no drugs) → resulting rating: **Everyone** |
| **Target audience and content** | Age groups: 13+ (or whatever you prefer) |
| **News app** | No |
| **COVID-19 contact tracing** | No |
| **Data safety** | "Data collected" = **No data collected**. "Data shared" = **No data shared** |
| **Government apps** | No |
| **Financial features** | None |
| **Health features** | None |

### Step 3 — Main store listing (left sidebar → Grow → Store presence → Main store listing)
Open `PLAY_STORE_LISTING.md` from this repo. For each language:

1. **Arabic (ar)**
   - App name: `جدد حياتك`
   - Short description: copy from PLAY_STORE_LISTING.md "Arabic (ar) — primary"
   - Full description: copy from PLAY_STORE_LISTING.md
2. **English (en-US)**
   - App name: `Jaddid Hayatak — Renew Your Life`
   - Same — copy from PLAY_STORE_LISTING.md
3. **French (fr-FR)**
   - App name: `Jaddid Hayatak — Renouvelez Votre Vie`
   - Same — copy from PLAY_STORE_LISTING.md

**Graphics** (upload from this repo):
- App icon → `store-assets/play-store-icon-512.png`
- Feature graphic → `store-assets/feature-graphic.png`
- Phone screenshots → **YOU NEED TO CAPTURE THESE** (min 2, recommended 5):
  1. Install the debug APK on your phone (`releases/jaddid-hayatak-v1.0-debug.apk`)
  2. Take screenshots of: home, chapter list, reading mode, theme switch, language switch
  3. Save as PNG at native resolution (e.g. 1080×2340)
  4. Upload to Play Console

### Step 4 — Production release (left sidebar → Production → Releases)
1. Click **Create new release**
2. Upload AAB: `releases/jaddid-hayatak-v1.0.aab`
3. Release name (auto-fills from versionCode/versionName): `1.0`
4. Release notes:
   ```
   First release.
   AR: الإصدار الأول
   FR: Première version
   ```
5. Click **Save** then **Review release**
6. Resolve any "Errors" the Play Console flags (most common: missing translations, missing content rating)
7. Click **Start rollout to production**

### Step 5 — Wait for review
- First-time review: **3–7 days** (longer for new developer accounts)
- After approval: app appears at `https://play.google.com/store/apps/details?id=org.workshopdiy.jaddidhayatak`

## Post-launch checklist

- [ ] App live on Play Store
- [ ] Test downloading from Play Store on a real phone
- [ ] Check that the QR code on `abourdim.github.io/jaddid-hayatak-android/` still works as the GitHub Pages download path (parallel distribution)
- [ ] Save Play Console crashes/ANRs alert email rule
- [ ] Decide whether to repeat for other 46 al-Ghazali books — **WARNING**: Google flags developer accounts with many similar apps as "spam/repetitive content". See `koutoub-android-template/WORKSHOP.html` section 13 for risk mitigation strategies (library-first vs. flagship-only)

## If anything fails

- **AAB upload error: "Bundle is not signed correctly"** → Check `~/.keys/wdiy-upload.env` matches what was used to build. The same upload keystore must sign every future update.
- **"App is using deprecated API level"** → Capacitor 8 targets API 35 — should pass through 2026 reviews. If this triggers, set `targetSdk = 35` in `android/variables.gradle`.
- **"Privacy policy URL doesn't work"** → Verify the URL serves HTTP 200: `curl -sI https://abourdim.github.io/jaddid-hayatak-android/store-assets/privacy.html`
- **"Apps using shared signing certificates may be flagged"** → If you submit multiple wrappers later signed with the SAME keystore (which they all are by design), Google may flag this. Use **internal app sharing** for testing the others before deciding to publish.
