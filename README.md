# SHED — Deploy to Vercel (Step-by-Step)

## What's in this folder

```
shed-production/
├── index.html      ← The full app (single file)
├── api/
│   └── ai.js       ← Serverless proxy (keeps your API key safe)
├── vercel.json     ← Tells Vercel how to run everything
└── README.md       ← This guide
```

---

## STEP 1: Get an Anthropic API Key

1. Go to **https://console.anthropic.com**
2. Sign up or log in
3. Go to **API Keys** in the sidebar
4. Click **Create Key**
5. Copy the key (starts with `sk-ant-...`) — save it somewhere safe
6. Add credit to your account (AI features cost ~$0.01-0.03 per use)

---

## STEP 2: Create a GitHub Account (skip if you have one)

1. Go to **https://github.com**
2. Sign up for free
3. Verify your email

---

## STEP 3: Upload This Project to GitHub

### Option A: Using GitHub Website (Easiest)

1. Go to **https://github.com/new**
2. Repository name: `shed-app`
3. Set it to **Private**
4. Click **Create repository**
5. On the next page, click **"uploading an existing file"**
6. Drag & drop ALL files from this `shed-production` folder:
   - `index.html`
   - `vercel.json`
   - `api/ai.js` (you'll need to create the `api` folder first — click "Add file" > "Create new file" and type `api/ai.js` as the filename, then paste the content)
7. Click **Commit changes**

### Option B: Using Git Command Line

```bash
cd shed-production
git init
git add .
git commit -m "SHED app"
git remote add origin https://github.com/YOUR_USERNAME/shed-app.git
git push -u origin main
```

---

## STEP 4: Deploy on Vercel

1. Go to **https://vercel.com**
2. Click **Sign Up** → choose **Continue with GitHub**
3. Authorize Vercel to access your GitHub
4. Click **"Add New..."** → **Project**
5. Find and select your `shed-app` repository
6. Click **Import**
7. Leave all settings as default
8. Click **Deploy**
9. Wait ~30 seconds — Vercel will build and deploy your app

---

## STEP 5: Add Your API Key (IMPORTANT!)

1. In your Vercel dashboard, click on the `shed-app` project
2. Go to **Settings** tab at the top
3. Click **Environment Variables** in the left sidebar
4. Add a new variable:
   - **Key:** `ANTHROPIC_API_KEY`
   - **Value:** paste your `sk-ant-...` key
   - **Environment:** check all three (Production, Preview, Development)
5. Click **Save**
6. Go to **Deployments** tab
7. Click the **⋮** menu on your latest deployment → **Redeploy**
8. Confirm — this restarts with your API key loaded

---

## STEP 6: Open Your App!

1. After redeployment, click **Visit** or copy your URL
2. Your app is now live at something like: `https://shed-app.vercel.app`
3. Open this URL on your phone's browser

---

## STEP 7: Add to Phone Home Screen

### iPhone:
1. Open the URL in **Safari** (must be Safari, not Chrome)
2. Tap the **Share** button (box with arrow at bottom)
3. Scroll down and tap **"Add to Home Screen"**
4. Name it "SHED" and tap **Add**
5. The app now appears on your home screen like a real app!

### Android:
1. Open the URL in **Chrome**
2. Tap the **⋮** menu (three dots, top right)
3. Tap **"Add to Home screen"**
4. Tap **Add**

---

## How It Works

- **Your data** (weight, logs, etc.) is saved in your phone's browser storage (localStorage). It persists between sessions.
- **AI features** (coach, meal planner, food analyzer, workout generator) route through `/api/ai` on Vercel, which adds your API key server-side. Your key is never exposed to the browser.
- **Daily logs** reset each day automatically.
- **Cost**: AI calls cost roughly $0.01-0.03 each. Normal usage ~$1-3/month.

---

## Troubleshooting

| Problem | Solution |
|---------|----------|
| AI features don't work | Check your API key is set in Vercel Environment Variables, then Redeploy |
| App won't load | Check Vercel deployment logs for errors |
| Data disappeared | Browser storage was cleared. This is per-device, per-browser. |
| Want a custom domain | In Vercel Settings → Domains → add your own (e.g. shed.yourdomain.com) |

---

## Optional: Custom Domain

If you want `shed.leoncheng.com` or similar:
1. Vercel Settings → Domains → Add
2. Type your domain
3. Vercel will give you DNS records to add at your domain registrar
4. Once DNS propagates (~5 min to 24 hours), your custom domain works

---

Built with 🔥 for Leon
