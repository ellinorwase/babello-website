# Baby Tracker Landing Page

Simple static landing page for handling email verification and password reset links that redirect to the Baby Tracker mobile app.

## What This Does

When users click on email links (verification emails, password reset emails), this landing page:

1. **On Mobile** 📱: Automatically redirects to the Baby Tracker app with the verification/reset token
2. **On Desktop** 💻: Shows instructions to open the link on their mobile device
3. **Error Handling** ⚠️: Shows clear error messages for invalid or expired links

## Pages

- `/` - Main landing page showcasing the app
- `/verify-email?token=...` - Email verification redirect
- `/reset-password?token=...` - Password reset redirect

## Technology

- Pure HTML/CSS/JavaScript (no build step needed!)
- Mobile/desktop detection
- Deep linking to `bt://` scheme
- Purple branding (#9333ea) matching the app

## Deployment to Vercel (FREE)

### 1. Prerequisites

- Vercel account (free): https://vercel.com/signup
- Vercel CLI installed:
  ```bash
  npm install -g vercel
  ```

### 2. Deploy

```bash
cd /Users/ellinorvase/Ellinors/Project/bt-web
vercel
```

Follow the prompts:
- **Set up and deploy?** → Yes
- **Which scope?** → Your personal account
- **Link to existing project?** → No
- **Project name?** → bt-web (or any name you want)
- **Directory?** → ./ (current directory)
- **Override settings?** → No

Vercel will deploy and give you a URL like: `https://bt-web-xyz.vercel.app`

### 3. Add Custom Domain (babytracker.se)

After deployment:

1. Go to your Vercel dashboard → Project settings → Domains
2. Add your domain: `babytracker.se`
3. Vercel will show you DNS records to add:
   - **Type**: CNAME
   - **Name**: `@` or `www`
   - **Value**: `cname.vercel-dns.com`

4. Add the DNS records to your domain provider (where you bought babytracker.se)
5. Wait 5-10 minutes for DNS to propagate
6. Your site will be live at `https://babytracker.se`! 🎉

### 4. Update Backend Environment Variable

Once deployed, update your Railway backend:

1. Go to Railway → Your backend service → Variables
2. Update or add:
   ```
   WEB_URL=https://babytracker.se
   ```
3. Click **Deploy** to restart the service

## Alternative: Deploy to Netlify

If you prefer Netlify over Vercel:

1. Install Netlify CLI:
   ```bash
   npm install -g netlify-cli
   ```

2. Deploy:
   ```bash
   cd /Users/ellinorvase/Ellinors/Project/bt-web
   netlify deploy --dir=public --prod
   ```

3. Follow similar domain setup as Vercel

## Testing Locally

You can test the pages locally:

```bash
# Simple Python server
cd /Users/ellinorvase/Ellinors/Project/bt-web/public
python3 -m http.server 8000

# Or use npx serve
npx serve public
```

Then visit:
- http://localhost:8000
- http://localhost:8000/verify-email.html?token=test123
- http://localhost:8000/reset-password.html?token=test123

**Note:** Deep linking (`bt://`) won't work in browser on desktop - that's expected!

## How The Redirect Flow Works

### Email Verification Flow:
1. User registers in app
2. Receives email with link: `https://babytracker.se/verify-email?token=abc123`
3. Clicks link on mobile
4. Landing page detects mobile device
5. Redirects to: `bt://auth/verify-email?token=abc123`
6. App opens automatically to verification screen
7. App calls backend API to verify token
8. User is verified! ✅

### Password Reset Flow:
1. User clicks "Forgot Password" in app
2. Receives email with link: `https://babytracker.se/reset-password?token=abc123`
3. Clicks link on mobile
4. Landing page detects mobile device
5. Redirects to: `bt://auth/reset-password?token=abc123`
6. App opens automatically to reset password screen
7. User enters new password
8. App calls backend API to reset password
9. Password is reset! ✅

## File Structure

```
bt-web/
├── public/
│   ├── index.html           # Main landing page
│   ├── verify-email.html    # Email verification redirect
│   └── reset-password.html  # Password reset redirect
├── vercel.json              # Vercel configuration
├── package.json             # Project metadata
└── README.md               # This file
```

## Support

For issues or questions, contact: support@babytracker.se

## Cost

**FREE** ✅
- Vercel free tier includes:
  - Unlimited bandwidth
  - Custom domains
  - Automatic HTTPS
  - Global CDN
  - Perfect for this use case!
