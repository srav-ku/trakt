# Employee Task Tracker - Deployment Guide

## Free Deployment Options

### Option 1: Railway (Recommended - Free Tier Available)
1. Sign up at https://railway.app
2. Create a new project
3. Connect your GitHub repository
4. Railway will auto-detect it as Node.js app
5. Set environment variables in Railway dashboard:
   - `NODE_ENV=production`
   - `PORT=3000` (or Railway's assigned port)
6. Deploy automatically on git push

### Option 2: Render
1. Sign up at https://render.com
2. Create new Web Service
3. Connect GitHub repo
4. Build command: `npm run build`
5. Start command: `npm start`
6. Set Node version to 20
7. Deploy

### Option 3: Fly.io
1. Install Fly CLI
2. Run `flyctl launch` in project root
3. Choose Node.js platform
4. Set `NODE_ENV=production` in fly.toml
5. Run `flyctl deploy`

### Option 4: Heroku (Limited Free Tier)
1. Install Heroku CLI
2. Run `heroku create app-name`
3. Run `git push heroku main`
4. Heroku auto-runs `npm start`

### Option 5: DigitalOcean App Platform (Free Trial)
1. Sign up at https://www.digitalocean.com/
2. Create new App
3. Connect GitHub
4. Select Node.js
5. Build: `npm run build`
6. Run: `npm start`
7. Add environment variables in dashboard

## Pre-Deployment Checklist

- [x] Run `npm run build` locally - verify no errors
- [x] Test production build: `npm start` - verify app works
- [x] Ensure all environment variables are documented
- [x] Database migrations run automatically on startup
- [x] Compression middleware enabled for performance
- [x] Logging disabled in production mode

## Production Environment Variables

```
NODE_ENV=production
PORT=3000
```

Database is automatically created and initialized on first run.

## Post-Deployment Steps

1. Visit your deployed URL
2. Test employee creation
3. Test task creation and filtering
4. Check console for any errors (should be silent in production)
5. Verify database is persisting (refresh page, data should remain)

## Database Backup

SQLite database is stored as a single file (`db.sqlite`). To backup:
- Download the `db.sqlite` file from your server
- Store in secure location
- Can restore by uploading to new deployment

## Troubleshooting

**App won't start:**
- Check logs: `npm start` output
- Verify Node.js version (18+)
- Ensure PORT env var is set

**Database errors:**
- Delete `db.sqlite` to reset (loses all data)
- Migrations run automatically on startup

**Build errors:**
- Run `npm install` locally first
- Verify Node version matches production (20+)
- Check for TypeScript errors: `npm run check`

## Performance Notes

- Gzip compression enabled on all responses
- Frontend built and served as static assets
- Database indexes optimized for common queries
- Consider enabling caching headers in production
