# VectorFly Deployment Guide

## 🚀 Quick Start: Deploy to Vercel

### Prerequisites
- GitHub repository: `VectorFly` (already created ✅)
- Vercel account (free tier works)
- Firebase project (already configured ✅)

---

## Step 1: Import to Vercel

1. **Go to Vercel Dashboard**
   - Visit [vercel.com](https://vercel.com)
   - Click "Add New Project"

2. **Import Repository**
   - Select "Import Git Repository"
   - Choose your `VectorFly` repository
   - Click "Import"

3. **Configure Project**
   - **Framework Preset:** Next.js
   - **Root Directory:** `./` (leave as root)
   - **Build Command:** `turbo run build --filter=web`
   - **Output Directory:** `apps/web/.next`
   - **Install Command:** `npm install`

4. **Add Environment Variables**
   
   Click "Environment Variables" and add these:

   ```
   NEXT_PUBLIC_FIREBASE_API_KEY=<your-firebase-api-key>
   NEXT_PUBLIC_FIREBASE_AUTH_DOMAIN=<your-project>.firebaseapp.com
   NEXT_PUBLIC_FIREBASE_PROJECT_ID=<your-project-id>
   NEXT_PUBLIC_FIREBASE_STORAGE_BUCKET=<your-project>.appspot.com
   NEXT_PUBLIC_FIREBASE_MESSAGING_SENDER_ID=<your-sender-id>
   NEXT_PUBLIC_FIREBASE_APP_ID=<your-app-id>
   NEXT_PUBLIC_APP_URL=https://your-project.vercel.app
   NODE_ENV=production
   ```

   > **Note:** Get Firebase values from your Firebase Console → Project Settings → General

5. **Deploy**
   - Click "Deploy"
   - Wait for build to complete (~2-3 minutes)
   - Your app will be live at `https://your-project.vercel.app`

---

## Step 2: Verify Deployment

### Test These Features:
- ✅ Home page loads
- ✅ Theme toggle works (Sun/Moon icon)
- ✅ Login with Firebase works
- ✅ Search and filters work
- ✅ Profile page displays
- ✅ Theme preference persists after reload

---

## Step 3: Set Up Cloudflare R2 (Optional - For File Uploads)

> **Note:** This is only needed if you want users to upload actual files. Currently, the app uses mock data and localStorage.

### Create R2 Bucket

1. **Go to Cloudflare Dashboard**
   - Visit [dash.cloudflare.com](https://dash.cloudflare.com)
   - Navigate to R2 → Create Bucket

2. **Create Bucket**
   - Name: `vectorfly-assets`
   - Location: Automatic
   - Click "Create Bucket"

3. **Generate API Token**
   - Go to R2 → Manage R2 API Tokens
   - Click "Create API Token"
   - Permissions: Object Read & Write
   - Note: Account ID, Access Key ID, Secret Access Key

4. **Configure CORS**
   - Select your bucket
   - Go to Settings → CORS Policy
   - Add this configuration:
   
   ```json
   [
     {
       "AllowedOrigins": ["https://your-project.vercel.app"],
       "AllowedMethods": ["GET", "PUT", "POST", "DELETE"],
       "AllowedHeaders": ["*"],
       "MaxAgeSeconds": 3600
     }
   ]
   ```

5. **Add R2 Variables to Vercel**
   - Go to Vercel Dashboard → Your Project → Settings → Environment Variables
   - Add:
   
   ```
   R2_ACCOUNT_ID=<your-account-id>
   R2_ACCESS_KEY_ID=<your-access-key>
   R2_SECRET_ACCESS_KEY=<your-secret-key>
   R2_BUCKET_NAME=vectorfly-assets
   NEXT_PUBLIC_R2_PUBLIC_URL=https://<bucket-id>.r2.cloudflarestorage.com
   ```

6. **Redeploy**
   - Go to Deployments → Click "..." → Redeploy

---

## Step 4: Custom Domain (Optional)

1. **Add Domain in Vercel**
   - Go to Settings → Domains
   - Add your domain (e.g., `vectorfly.com`)

2. **Configure DNS**
   - Add CNAME record pointing to `cname.vercel-dns.com`
   - Or use Vercel nameservers

3. **Wait for SSL**
   - Vercel automatically provisions SSL certificate
   - Usually takes 1-2 minutes

---

## 🎯 Current Status

**What Works Now:**
- ✅ Full application deployment
- ✅ Firebase authentication
- ✅ Theme persistence (localStorage)
- ✅ Profile image persistence (localStorage)
- ✅ Uploaded asset persistence (localStorage)
- ✅ All UI components with dark/light theme

**What Needs R2 (Optional):**
- 📁 Actual file uploads to cloud storage
- 📁 Sharing uploaded assets with other users
- 📁 Permanent asset storage beyond localStorage

---

## 📊 Deployment Checklist

- [ ] Import repository to Vercel
- [ ] Add Firebase environment variables
- [ ] Deploy successfully
- [ ] Test authentication
- [ ] Test theme toggle
- [ ] Verify all pages load
- [ ] (Optional) Set up Cloudflare R2
- [ ] (Optional) Configure custom domain

---

## 🆘 Troubleshooting

### Build Fails
- Check build logs in Vercel dashboard
- Verify all environment variables are set
- Test build locally: `npm run build`

### App Doesn't Load
- Check browser console for errors
- Verify Firebase configuration
- Check Vercel deployment logs

### Theme Doesn't Persist
- Check browser localStorage is enabled
- Verify theme toggle component is rendering

---

## 📝 Next Steps After Deployment

1. **Monitor Performance**
   - Enable Vercel Analytics
   - Check Lighthouse scores

2. **Set Up Monitoring**
   - Add error tracking (Sentry)
   - Set up uptime monitoring

3. **Future Enhancements**
   - Implement R2 file uploads
   - Add database for production data
   - Set up CDN caching
   - Implement image optimization

---

## 🎉 You're Done!

Your VectorFly app is now live and accessible to the world! 🚀
