# SHAED Documentation Site - Setup & Maintenance Guide

Everything you need to deploy and maintain your password-protected documentation site.

---

## Quick Start: Deploy to Vercel

### Step 1: Create Vercel Account

1. Go to [vercel.com](https://vercel.com)
2. Click **Sign Up**
3. Choose **Continue with GitHub** (easiest—links your repos automatically)
4. Authorize Vercel to access your GitHub

### Step 2: Import Your Repository

1. Once logged in, click **Add New...** → **Project**
2. Find `htmltest` in your repo list and click **Import**
3. Leave all settings as default (Vercel auto-detects static HTML)
4. Click **Deploy**
5. Wait ~30 seconds—done!

### Step 3: Your Site is Live

Vercel gives you a URL like: `htmltest-abc123.vercel.app`

You can access it immediately. The password gate will appear first.

---

## Custom Domain (Optional)

Want to use something like `docs.shaed.io`?

1. In Vercel, go to your project → **Settings** → **Domains**
2. Add your domain (e.g., `docs.shaed.io`)
3. Vercel shows you DNS records to add
4. Go to your domain registrar (Cloudflare, GoDaddy, etc.)
5. Add the DNS records Vercel provides
6. Wait 5-10 minutes for DNS propagation
7. HTTPS is automatic—Vercel handles certificates

---

## Password Protection

Your site uses a JavaScript password gate. Here's how to manage it:

### Changing the Password

1. Open `index.html` in GitHub (or your editor)
2. Find this line near the top:
   ```javascript
   const SITE_PASSWORD = "shaed2025";
   ```
3. Change `shaed2025` to your new password
4. Commit the change
5. Vercel auto-deploys in ~30 seconds

### How the Password Works

- Users enter the password once per browser session
- Closing the browser requires re-entering the password
- The password is stored in the HTML (visible in source code)
- This keeps casual visitors out, but isn't bank-level security

### ⚠️ Important Security Notes

This password gate is **"keep honest people out"** security:
- ✅ Good for: Investor previews, internal docs, client portals
- ❌ Not for: Sensitive data, financial records, PII

If you need real security, consider:
- Vercel Pro ($20/mo) for built-in password protection
- Cloudflare Access (free for 50 users)
- Netlify Identity (free for 5 users)

---

## File Structure

```
htmltest/
├── index.html                 ← Landing page with password gate
├── shaed_eta_tracking.html    ← Your documents (no password on individual files)
├── another_doc.html           
├── MAINTENANCE_GUIDE.md       ← This file
└── README.md
```

**Note:** The password only protects `index.html`. If someone knows a direct URL like `yoursite.com/shaed_eta_tracking.html`, they can access it directly. For most use cases this is fine—you control who gets the links.

---

## File Naming Rules

✅ **Do this:**
- `shaed_eta_tracking.html`
- `dealer-visibility-framework.html`
- `bigquery_schema.html`

❌ **Don't do this:**
- `shaed_eta_tracking (2).html` — no spaces or parentheses
- `My Document.html` — no spaces

---

## Adding a New Document

### Step 1: Upload the HTML file

1. Go to your GitHub repo
2. Click **Add file** → **Upload files**
3. Drag your HTML file in (make sure filename has no spaces!)
4. Commit the change

### Step 2: Add a link in index.html

1. In GitHub, click `index.html` → pencil icon to edit
2. Find the comment `<!-- Add more documents here -->`
3. Paste this template above that comment:

```html
        <!-- YOUR DOCUMENT NAME -->
        <a href="your_filename.html" class="card block bg-slate-800 border border-slate-700 rounded-xl p-6 transition-all duration-200 hover:border-blue-500 hover:bg-slate-750">
          <div class="flex items-start gap-4">
            <div class="w-12 h-12 bg-emerald-600 rounded-lg flex items-center justify-center flex-shrink-0">
              <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" />
            </svg>
            </div>
            <div>
              <h2 class="text-xl font-semibold text-white mb-1">Your Document Title</h2>
              <p class="text-slate-400">Brief description here</p>
              <div class="flex gap-2 mt-3">
                <span class="text-xs bg-emerald-900 text-emerald-300 px-2 py-1 rounded">Tag1</span>
                <span class="text-xs bg-blue-900 text-blue-300 px-2 py-1 rounded">Tag2</span>
              </div>
            </div>
          </div>
        </a>
```

4. Update:
   - `your_filename.html` → actual filename
   - `Your Document Title` → display name
   - `Brief description here` → what it's about
   - Tags as needed

5. Commit changes

### Step 3: Automatic Deploy

Vercel watches your GitHub repo. When you commit:
- Vercel auto-deploys in ~30 seconds
- No action needed from you

---

## Color Options

**Icon backgrounds:**
- `bg-blue-600` — Blue
- `bg-emerald-600` — Green  
- `bg-purple-600` — Purple
- `bg-orange-600` — Orange

**Tag colors:**
- `bg-blue-900 text-blue-300` — Blue
- `bg-emerald-900 text-emerald-300` — Green
- `bg-purple-900 text-purple-300` — Purple
- `bg-orange-900 text-orange-300` — Orange

---

## Updating an Existing Document

1. Upload the new HTML file with the **exact same filename**
2. GitHub replaces the old version
3. Vercel auto-deploys
4. No changes needed to `index.html`

---

## Troubleshooting

### Password not working
- Make sure you're typing the exact password (case-sensitive)
- Check `index.html` for the current password value
- Try a different browser or incognito mode

### Changes not showing up
- Vercel deploys take ~30 seconds
- Hard refresh: `Ctrl+Shift+R` (Windows) or `Cmd+Shift+R` (Mac)
- Check Vercel dashboard for deployment status

### 404 error on a document
- Check filename for spaces or special characters
- Make sure the `href` in index.html matches exactly (case-sensitive)

### Site not deploying
1. Go to [vercel.com](https://vercel.com) → your project
2. Check the **Deployments** tab for errors
3. Make sure your GitHub repo is still connected

---

## Quick Reference

| Task | How |
|------|-----|
| Change password | Edit `SITE_PASSWORD` in index.html |
| Add document | Upload HTML + add card to index.html |
| Update document | Upload same filename—overwrites |
| Check deployment | vercel.com → your project → Deployments |
| Add custom domain | Vercel → Settings → Domains |

---

## Your URLs

After deployment:

- **Vercel URL:** `https://htmltest-[random].vercel.app`
- **Custom domain:** `https://docs.shaed.io` (if you set one up)

---

## Need Help?

Share with me:
1. What you're trying to do
2. Any error messages
3. Screenshot if helpful

Happy documenting! 🚀
