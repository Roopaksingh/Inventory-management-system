# Render Deployment Guide

## Prerequisites

1. **GitHub Account** - Code repository
2. **Render Account** - Sign up at [render.com](https://render.com)
3. **PostgreSQL Database** - Will be created on Render

## Step 1: Push Code to GitHub ✅

You've already done this! Your code is on GitHub.

## Step 2: Create Environment Files

Make sure these files exist in your repository:

- `inventory-management-system/backend/.env.example` - Backend environment template
- `inventory-management-system/frontend/.env.example` - Frontend environment template

## Step 3: Create PostgreSQL Database on Render

1. Go to [Render Dashboard](https://dashboard.render.com)
2. Click **New +** → **PostgreSQL**
3. Configuration:
   - **Name**: `inventory-db`
   - **Region**: Choose your region
   - **PostgreSQL Version**: 15+
4. Click **Create Database**
5. **Copy the External Database URL** (looks like: `postgresql://user:password@host:5432/dbname`)

## Step 4: Deploy Backend

1. In Render Dashboard: **New +** → **Web Service**
2. Connect GitHub repository
3. Configuration:
   - **Name**: `inventory-backend`
   - **Runtime**: Python 3
   - **Root Directory**: `inventory-management-system/backend`
   - **Build Command**: `pip install -r requirements.txt`
   - **Start Command**: `uvicorn app.main:app --host 0.0.0.0 --port 8000`
   - **Region**: Same as database

4. **Environment Variables**:
   - `DATABASE_URL` → Paste the PostgreSQL URL from Step 3
   - `FRONTEND_URL` → You'll set this after deploying frontend

5. Click **Create Web Service**
6. **Copy the backend URL** (e.g., `https://inventory-backend.onrender.com`)

## Step 5: Deploy Frontend

### Option A: Static Site (Recommended for Vite)

1. In Render Dashboard: **New +** → **Static Site**
2. Connect GitHub repository
3. Configuration:
   - **Name**: `inventory-frontend`
   - **Root Directory**: `inventory-management-system/frontend`
   - **Build Command**: `npm install && npm run build`
   - **Publish Directory**: `dist`

4. Click **Create Static Site**
5. **Copy the frontend URL** (e.g., `https://inventory-frontend.onrender.com`)

### Option B: Web Service (If you need Node.js runtime)

1. In Render Dashboard: **New +** → **Web Service**
2. Connect GitHub repository
3. Configuration:
   - **Name**: `inventory-frontend`
   - **Runtime**: Node
   - **Root Directory**: `inventory-management-system/frontend`
   - **Build Command**: `npm install && npm run build`
   - **Start Command**: `npm run preview`

4. **Environment Variables**:
   - `VITE_API_BASE_URL` → Your backend URL (e.g., `https://inventory-backend.onrender.com`)

5. Click **Create Web Service**

## Step 6: Update CORS Configuration

1. Go to your backend service on Render
2. Click **Environment**
3. Update `FRONTEND_URL`:
   ```
   https://inventory-frontend.onrender.com
   ```
4. Save - the service will automatically redeploy

## Step 7: Update Frontend API URL (if using Web Service)

1. Go to your frontend service on Render
2. Click **Environment**
3. Update `VITE_API_BASE_URL`:
   ```
   https://inventory-backend.onrender.com
   ```
4. Save and wait for redeploy

## Step 8: Test Your Deployment

1. Visit: `https://inventory-frontend.onrender.com`
2. Test creating/viewing products, customers, orders
3. Check browser Console for errors (F12)
4. Check Render logs for backend errors

## Troubleshooting

### CORS Errors
- ❌ Problem: "Access to XMLHttpRequest blocked by CORS policy"
- ✅ Solution: Make sure `FRONTEND_URL` environment variable in backend matches your actual frontend URL

### Database Connection Error
- ❌ Problem: "could not connect to server"
- ✅ Solution:
  1. Verify `DATABASE_URL` is correct
  2. Check database status in Render dashboard
  3. Make sure it's a PostgreSQL database

### Build Failed
- ❌ Problem: "npm: command not found" or "pip: command not found"
- ✅ Solution:
  1. Check Root Directory is correct
  2. Verify build command paths
  3. Check that `package.json` or `requirements.txt` exists

### 502 Bad Gateway
- ❌ Problem: "502 Bad Gateway" error
- ✅ Solution:
  1. Check service logs in Render dashboard
  2. Verify Start Command is correct
  3. Check that environment variables are set

### Static Files Not Loading
- ❌ Problem: CSS/JS files return 404
- ✅ Solution (for Static Site):
  1. Verify Publish Directory is `dist`
  2. Run `npm run build` locally to test
  3. Check that `vite.config.js` is correct

## Environment Variables Summary

### Backend Services
```
DATABASE_URL=postgresql://...
FRONTEND_URL=https://your-frontend.onrender.com
```

### Frontend Services
```
VITE_API_BASE_URL=https://your-backend.onrender.com
```

## Useful Links

- [Render Documentation](https://render.com/docs)
- [FastAPI Deployment](https://fastapi.tiangolo.com/deployment/)
- [Vite Deployment](https://vitejs.dev/guide/static-deploy.html)
- [PostgreSQL on Render](https://render.com/docs/databases)

---

**Deployment Complete!** 🎉 Your app is now live on Render.
