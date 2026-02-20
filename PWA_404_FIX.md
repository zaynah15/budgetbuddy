# 🔧 Fixing the 404 Error on GitHub Pages

## ✅ What Was Fixed

The 404 error when installing Spendora as a PWA has been **FIXED** with these changes:

### 1. **Relative Paths in Manifest**
```json
{
  "start_url": "./",     // Was "/" - now relative
  "scope": "./",          // Was "/" - now relative
  "icons": [
    {
      "src": "./logo.png"  // Was absolute - now relative
    }
  ]
}
```

### 2. **Relative Paths in HTML**
```html
<link rel="manifest" href="./manifest.json">
<link rel="icon" type="image/png" href="./logo.png">
<link rel="apple-touch-icon" href="./logo.png">
```

### 3. **Service Worker Scope**
```javascript
navigator.serviceWorker.register('./sw.js', { scope: './' })
```

### 4. **Service Worker Cache Paths**
```javascript
const urlsToCache = [
  './',              // Not '/'
  './index.html',    // Not '/index.html'
  './manifest.json', // Not '/manifest.json'
  './logo.png',      // Not '/logo.png'
];
```

---

## 📱 How to Upload to GitHub Pages

### Step 1: Upload Files to Repository ROOT

**Go to:** `https://github.com/zaynah15/budgetbuddy`

**Upload these 4 files to the ROOT** (not in any folder):

1. ✅ `index.html`
2. ✅ `manifest.json`
3. ✅ `logo.png`
4. ✅ `sw.js`

**IMPORTANT:** They must be at:
```
budgetbuddy/
├── index.html     ← Root level
├── manifest.json  ← Root level
├── logo.png       ← Root level
└── sw.js          ← Root level
```

**NOT** like this:
```
budgetbuddy/
└── root/
    ├── index.html  ❌ Wrong! Too deep
    ├── manifest.json
    ├── logo.png
    └── sw.js
```

### Step 2: Enable GitHub Pages

1. Go to **Settings** → **Pages**
2. Source: **Deploy from a branch**
3. Branch: **`main`**
4. Folder: **`/ (root)`** ← Must be root, not `/root` or `/docs`
5. Click **Save**
6. Wait 1-2 minutes

### Step 3: Test the URL

**On your computer:**
1. Visit: `https://zaynah15.github.io/budgetbuddy/`
2. Should see Spendora sign-in screen with the rupee bow logo
3. No 404 error ✅

**On your Android phone:**
1. Open Chrome
2. Visit: `https://zaynah15.github.io/budgetbuddy/`
3. Tap menu (⋮) → **"Install app"** or **"Add to Home Screen"**
4. The app installs successfully ✅
5. Open from home screen → Works perfectly! ✅

---

## 🎯 Why This Fixes the 404

### The Problem Before:

**Absolute paths** like `/manifest.json` work on:
- ✅ `https://spendora.com/manifest.json` (root domain)
- ❌ `https://zaynah15.github.io/budgetbuddy/manifest.json` (subdirectory)

When GitHub Pages serves from `/budgetbuddy/`, it looks for:
- `/manifest.json` → Goes to `https://zaynah15.github.io/manifest.json` ❌ (doesn't exist)

### The Solution:

**Relative paths** like `./manifest.json` work everywhere:
- ✅ `./manifest.json` → `https://zaynah15.github.io/budgetbuddy/manifest.json`
- ✅ Works on any subdirectory
- ✅ Works on custom domains
- ✅ Works locally

---

## 🔍 Verification Checklist

After uploading, check:

- [ ] **Files at repository root** (not in a folder)
- [ ] **GitHub Pages enabled** from `main` branch, `/` folder
- [ ] **Desktop test:** Visit URL, see Spendora logo
- [ ] **Mobile Chrome:** Install app from menu
- [ ] **Home screen:** App icon appears
- [ ] **Open from home screen:** No 404, app loads ✅

---

## 🆘 Troubleshooting

### Still Getting 404?

**Check your file locations:**
```bash
# On GitHub, your repository should look like:
budgetbuddy/
├── FIREBASE_SETUP_GUIDE.md
├── index.html        ← Must be here
├── logo.png          ← Must be here  
├── manifest.json     ← Must be here
└── sw.js             ← Must be here
```

**NOT:**
```bash
budgetbuddy/
├── root/
│   ├── index.html   ❌ Wrong location
│   └── ...
└── README.md
```

### App Installs But Shows Blank Screen?

**Check:**
1. Browser console (F12) for errors
2. Make sure all 4 files uploaded successfully
3. Clear browser cache and try again
4. Check that `logo.png` uploaded correctly

### "Failed to fetch manifest" Error?

**Fix:**
1. Open `manifest.json` on GitHub
2. Make sure it has `"start_url": "./"` (with the dot)
3. Re-upload if needed

---

## ✨ Next Steps

Once the 404 is fixed and the app installs:

1. **Configure Firebase** (see `FIREBASE_SETUP_GUIDE.md`)
2. **Test sign-in** with Google
3. **Enable notifications**
4. **Try dark mode** (moon/sun button)
5. **Start tracking spending!**

---

**🎉 Your Spendora PWA should now install perfectly with no 404 errors!**
