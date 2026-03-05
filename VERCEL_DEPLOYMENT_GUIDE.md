# Vercel Deployment Guide for SabbPe Project

## Overview
This project has two main components:
1. **Frontend** (Vite React app) - Located in `sabbpeapp-main/`
2. **Backend** (Express.js API) - Located in `sabbpeapp-main/backend/`

## Prerequisites
- GitHub account (push your code to GitHub)
- Vercel account (free at vercel.com)
- Node.js v18+ installed locally

## Deployment Steps

### Step 1: Push to GitHub

```bash
# Initialize git repository (if not already done)
git init

# Add all files
git add .

# Commit
git commit -m "Initial commit for Vercel deployment"

# Add remote repository
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO.git

# Push to GitHub
git branch -M main
git push -u origin main
```

### Step 2: Create Vercel Account & Project

1. Go to [vercel.com](https://vercel.com) and sign up
2. Click "Add New" → "Project"
3. Import your GitHub repository
4. Select the repository and click "Import"

### Step 3: Configure Environment Variables in Vercel

In your Vercel project dashboard:
1. Go to Settings → Environment Variables
2. Add all variables from your `.env.local` file:

```
VITE_SUPABASE_PROJECT_ID=cuztcbznvckhubsmcvuj
VITE_SUPABASE_ANON_KEY=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
VITE_SUPABASE_URL=https://cuztcbznvckhubsmcvuj.supabase.co
VITE_BACKEND_URL=https://YOUR_BACKEND_URL (set after backend deployment)
VITE_GOOGLE_VISION_API_KEY=AIzaSyASkZgVQhHqEskA0S3B8BAkTkl8RpAYWnw
VITE_API_URL=https://YOUR_BACKEND_URL/api
VITE_API_BASE_URL=https://cams.sabbpe.com
...
```

#### IMPORTANT: Update Backend URL After Deployment
- First deploy the backend (or update the variable after backend is deployed)
- Update `VITE_BACKEND_URL` to your backend's deployed URL

### Step 4: Root Configuration

The `vercel.json` in the root directory tells Vercel:
- Where to find the main app (sabbpeapp-main)
- How to build it
- What dependencies to install

### Step 5: Deploy Backend (Optional - if you want API on Vercel)

**Option A: Deploy Backend as Separate Vercel Project**

1. Create another Vercel project for the backend
2. Set the root directory to `sabbpeapp-main/backend`
3. Configure environment variables:
   - `SUPABASE_URL`
   - `SUPABASE_KEY`
   - `JWT_SECRET`
   - etc.
4. Get the deployed backend URL (e.g., `https://your-backend.vercel.app`)
5. Update `VITE_BACKEND_URL` in the frontend project

**Option B: Keep Backend Elsewhere (Recommended)**
- Deploy backend to Heroku, Railway, Render, or your own server
- Update `VITE_BACKEND_URL` variable

### Step 6: Update Environment Variables with Backend URL

After backend deployment:
1. Go to Vercel project settings
2. Update these variables:
   - `VITE_BACKEND_URL` = your backend URL
   - `VITE_API_URL` = your backend URL + `/api`
3. Trigger a redeploy (git push or click "Redeploy" in Vercel)

### Step 7: Monitor Deployment

- Check Vercel dashboard for build logs
- Verify your site at `https://YOUR_PROJECT.vercel.app`
- Monitor for any errors in the deployment logs

## Environment Variables Reference

Key variables to configure:

| Variable | Type | Example |
|----------|------|---------|
| VITE_SUPABASE_PROJECT_ID | Public | cuztcbznvckhubsmcvuj |
| VITE_SUPABASE_ANON_KEY | Secret | eyJ... |
| VITE_SUPABASE_URL | Public | https://cuztcbznvckhubsmcvuj.supabase.co |
| VITE_BACKEND_URL | Public | https://your-backend-url.com |
| VITE_GOOGLE_VISION_API_KEY | Secret | AIzaSy... |

## Troubleshooting

### Build Fails
- Check the build logs in Vercel dashboard
- Ensure all dependencies are in package.json
- Verify Node.js version compatibility

### Environment Variables Not Loading
- Ensure variables start with `VITE_` for frontend access
- Redeploy after adding/updating variables
- Check browser console for actual values (run `console.log(import.meta.env)`)

### CORS Issues
- Configure CORS in your backend
- Update allowed origins in backend to include your Vercel URL

### Performance Issues
- Check Vercel Analytics
- Optimize bundle size
- Consider caching strategies

## Rollback

If deployment has issues:
1. Go to Vercel Deployments tab
2. Find the previous successful deployment
3. Click the three dots → "Promote to Production"

## Custom Domain Setup

1. In Vercel project settings → Domains
2. Add your custom domain
3. Follow DNS configuration instructions
4. Update backend URL if using custom domain

## Useful Commands for Local Testing

```bash
# Build locally to test
npm run build

# Preview build locally
npm run preview

# Install Vercel CLI for local deployment testing
npm install -g vercel
vercel
```

## Next Steps

1. Commit this guide to your repo
2. Push to GitHub
3. Connect to Vercel
4. Add environment variables
5. Deploy!

For more info: https://vercel.com/docs
