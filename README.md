# InvoiceLens — Setup Guide

## 🚀 Deploy to Netlify in 5 Steps

### Step 1 — Get a new API Key
1. Go to https://console.anthropic.com/settings/keys
2. **Delete** your old exposed key
3. Click **"Create Key"** → copy the new key

---

### Step 2 — Upload to GitHub
1. Create a free account at https://github.com
2. Create a **New Repository** (name it `invoicelens`)
3. Upload ALL these files keeping the folder structure:
   ```
   invoicelens/
   ├── public/
   │   ├── index.html
   │   ├── styles.css
   │   └── app.js
   ├── netlify/
   │   └── functions/
   │       ├── extract-invoice.js
   │       ├── sync-drive.js
   │       └── package.json
   └── netlify.toml
   ```

---

### Step 3 — Deploy on Netlify
1. Go to https://netlify.com → **"Add new site"** → **"Import from Git"**
2. Connect GitHub and select your `invoicelens` repo
3. Click **Deploy site** (Netlify auto-detects the config)

---

### Step 4 — Add Environment Variable (YOUR API KEY)
1. In Netlify → **Site configuration** → **Environment variables**
2. Click **"Add a variable"**:
   - Key: `ANTHROPIC_API_KEY`
   - Value: `sk-ant-your-NEW-key-here`
3. Click **Save** → **Trigger redeploy**

---

### Step 5 — Connect Google Drive (optional)
To auto-save Excel to Drive every 15 minutes:

#### A) Create a Google Service Account:
1. Go to https://console.cloud.google.com
2. Create a project → Enable **Google Drive API**
3. Go to **IAM & Admin** → **Service Accounts** → **Create**
4. Download the JSON key file

#### B) Share your Drive folder:
1. Create a folder in Google Drive
2. Right-click → **Share** → add the service account email (from the JSON)
3. Copy the **folder ID** from the URL: `drive.google.com/drive/folders/**THIS_PART**`

#### C) Connect in the app:
1. Open your deployed app
2. Click **"Connect Google Drive"** in the sidebar
3. Paste the folder ID and service account JSON

---

## 📱 Using the App

- **Upload Invoice**: Drag & drop, browse files, or **Take Photo** on mobile
- **Dashboard**: Auto-updates charts as you add invoices
- **All Invoices**: Filter, sort, search all your expenses
- **Export Excel**: Downloads a 3-sheet Excel (Summary, Line Items, By Vendor)
- **Drive Sync**: Auto-uploads Excel to your Drive every 15 minutes

## 💡 Tips
- Works great on mobile — use "Take Photo" to scan receipts instantly
- All data is saved locally in the browser (localStorage)
- Excel export has 3 tabs: Summary, Line Items, By Vendor

---

## ❓ Troubleshooting

**"Server error 500" on upload**
→ Check that `ANTHROPIC_API_KEY` is set correctly in Netlify env vars

**Drive sync not working**
→ Make sure the service account email has Editor access to your Drive folder

**App won't load**
→ Verify `netlify.toml` is in the root folder and `publish = "public"`
