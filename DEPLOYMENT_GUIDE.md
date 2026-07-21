# Deployment Guide - Job Application Tracker

## Pre-Deployment Checklist

- [ ] All code tested and working locally
- [ ] Environment variables configured
- [ ] Database backup created
- [ ] Frontend builds without errors
- [ ] Backend starts successfully
- [ ] Security review completed
- [ ] Performance optimized
- [ ] HTTPS certificate obtained

## Production Environment Setup

### 1. Backend Deployment

#### Option A: Deploy to Heroku

1. **Create Heroku Account**
   - Go to https://www.heroku.com/
   - Sign up for free account

2. **Install Heroku CLI**
   ```bash
   npm install -g heroku
   heroku login
   ```

3. **Create Heroku App**
   ```bash
   cd backend
   heroku create jobtracker-api
   ```

4. **Set Environment Variables**
   ```bash
   heroku config:set PORT=5000
   heroku config:set MONGODB_URI=mongodb+srv://user:password@cluster.mongodb.net/jobtracker
   heroku config:set JWT_SECRET=your_production_secret_key
   heroku config:set NODE_ENV=production
   ```

5. **Deploy**
   ```bash
   git push heroku main
   ```

#### Option B: Deploy to AWS EC2

1. **Create EC2 Instance**
   - Ubuntu 20.04 LTS
   - t2.micro (free tier eligible)

2. **SSH into Instance**
   ```bash
   ssh -i key.pem ubuntu@your-instance-ip
   ```

3. **Install Node.js**
   ```bash
   curl -sL https://deb.nodesource.com/setup_18.x | sudo -E bash -
   sudo apt-get install -y nodejs
   ```

4. **Install MongoDB**
   ```bash
   sudo apt-get install -y mongodb
   sudo systemctl start mongodb
   ```

5. **Clone Repository**
   ```bash
   git clone your-repo-url
   cd JobTracker/backend
   npm install
   ```

6. **Setup PM2 for Process Management**
   ```bash
   npm install -g pm2
   pm2 start server.js --name "jobtracker-api"
   pm2 startup
   pm2 save
   ```

7. **Configure Nginx as Reverse Proxy**
   ```nginx
   server {
       listen 80;
       server_name your-domain.com;

       location / {
           proxy_pass http://localhost:5000;
           proxy_http_version 1.1;
           proxy_set_header Upgrade $http_upgrade;
           proxy_set_header Connection 'upgrade';
           proxy_set_header Host $host;
       }
   }
   ```

#### Option C: Docker Deployment

1. **Build Docker Image**
   ```bash
   cd backend
   docker build -t jobtracker-backend .
   ```

2. **Run Container**
   ```bash
   docker run -p 5000:5000 \
     -e MONGODB_URI=mongodb://mongo:27017/jobtracker \
     -e JWT_SECRET=your_secret \
     jobtracker-backend
   ```

### 2. Frontend Deployment

#### Option A: Deploy to Vercel

1. **Create Vercel Account**
   - Go to https://vercel.com
   - Connect GitHub account

2. **Import Project**
   - Select frontend folder
   - Configure build settings
   - Set environment variables

3. **Set Environment Variables in Vercel**
   ```
   REACT_APP_API_URL=https://your-api-domain.com
   ```

4. **Deploy**
   - Push to main branch
   - Vercel auto-deploys

#### Option B: Deploy to Netlify

1. **Build Frontend**
   ```bash
   cd frontend
   npm run build
   ```

2. **Drag & Drop Deploy**
   - Go to https://app.netlify.com
   - Drag build folder to deploy

3. **Configure Build Settings**
   - Build command: `npm run build`
   - Publish directory: `build`

4. **Set Environment Variables**
   - Site settings → Build & Deploy → Environment
   - Add `REACT_APP_API_URL`

#### Option C: Deploy to AWS S3 + CloudFront

1. **Build Frontend**
   ```bash
   npm run build
   ```

2. **Create S3 Bucket**
   - Enable static website hosting
   - Upload build folder contents

3. **Create CloudFront Distribution**
   - Set S3 bucket as origin
   - Enable HTTPS

### 3. Database Setup

#### MongoDB Atlas (Cloud)

1. **Create Account**
   - Go to https://www.mongodb.com/cloud/atlas
   - Sign up

2. **Create Cluster**
   - Free tier: 512MB storage
   - Choose region closest to your users

3. **Create Database User**
   - Set username and password
   - Configure IP whitelist

4. **Get Connection String**
   ```
   mongodb+srv://username:password@cluster.mongodb.net/jobtracker
   ```

5. **Update Backend .env**
   ```env
   MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/jobtracker
   ```

### 4. SSL/HTTPS Configuration

#### Using Let's Encrypt (Free)

1. **Install Certbot**
   ```bash
   sudo apt-get install certbot python3-certbot-nginx
   ```

2. **Get Certificate**
   ```bash
   sudo certbot certonly --nginx -d your-domain.com
   ```

3. **Configure Nginx**
   ```nginx
   server {
       listen 443 ssl http2;
       server_name your-domain.com;

       ssl_certificate /etc/letsencrypt/live/your-domain.com/fullchain.pem;
       ssl_certificate_key /etc/letsencrypt/live/your-domain.com/privkey.pem;

       location / {
           proxy_pass http://localhost:5000;
       }
   }

   server {
       listen 80;
       server_name your-domain.com;
       return 301 https://$server_name$request_uri;
   }
   ```

### 5. Environment Variables for Production

#### Backend (.env)
```env
PORT=5000
MONGODB_URI=mongodb+srv://user:password@cluster.mongodb.net/jobtracker
JWT_SECRET=generate_strong_random_key_here
EMAIL_SERVICE=gmail
EMAIL_USER=your_email@gmail.com
EMAIL_PASSWORD=your_app_password
NODE_ENV=production
CORS_ORIGIN=https://your-frontend-domain.com
```

#### Frontend (.env)
```env
REACT_APP_API_URL=https://your-api-domain.com
```

### 6. Domain Configuration

1. **Buy Domain**
   - GoDaddy, Namecheap, Route53, etc.

2. **Update DNS Records**
   - A record → Your server IP
   - CNAME → Your CDN/Load Balancer
   - MX records → Email service

3. **Verify DNS**
   ```bash
   nslookup your-domain.com
   ```

### 7. Monitoring & Logging

#### Backend Monitoring
- Set up error logging (Sentry, Loggly)
- Monitor server performance
- Set up alerts

```bash
npm install sentry-node
```

#### Frontend Monitoring
- Monitor application performance
- Track user analytics
- Monitor JavaScript errors

#### Database Monitoring
- MongoDB Atlas dashboard
- Query performance
- Storage usage

### 8. Backup Strategy

1. **Database Backups**
   - MongoDB Atlas auto-backup
   - Regular manual exports
   - Off-site storage

2. **Code Backups**
   - GitHub repository
   - Weekly backups
   - Version control

3. **Restore Procedure**
   ```bash
   mongorestore --uri="mongodb://..." backup.dump
   ```

### 9. Performance Optimization

1. **Backend**
   - Enable gzip compression
   - Implement caching
   - Optimize database queries
   - Use CDN for static files

2. **Frontend**
   - Minify JavaScript and CSS
   - Optimize images
   - Lazy load components
   - Use service workers

### 10. Security Hardening

1. **Backend Security**
   - Enable HTTPS only
   - Set secure headers
   - Implement rate limiting
   - Validate all inputs
   - Use security.txt

2. **Frontend Security**
   - Remove console logs
   - Implement CSP headers
   - Sanitize HTML
   - Use secure cookies

3. **Database Security**
   - Strong passwords
   - IP whitelist
   - Encryption at rest
   - Regular backups

### 11. CI/CD Pipeline

#### GitHub Actions Example

```yaml
name: Deploy

on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v2

      - name: Setup Node.js
        uses: actions/setup-node@v2
        with:
          node-version: '18'

      - name: Install Dependencies
        run: |
          cd backend && npm install
          cd ../frontend && npm install

      - name: Build Frontend
        run: cd frontend && npm run build

      - name: Deploy to Vercel
        env:
          VERCEL_TOKEN: ${{ secrets.VERCEL_TOKEN }}
        run: vercel --prod

      - name: Deploy to Heroku
        env:
          HEROKU_API_KEY: ${{ secrets.HEROKU_API_KEY }}
        run: heroku deploy
```

### 12. Post-Deployment Testing

- [ ] Frontend loads correctly
- [ ] Backend API responds
- [ ] Authentication works
- [ ] CRUD operations function
- [ ] Reminders work
- [ ] Analytics load
- [ ] Mobile responsive
- [ ] HTTPS working
- [ ] Performance acceptable
- [ ] Error handling works

### 13. Performance Metrics

Monitor these metrics:

```
Frontend:
- Page Load Time: < 3s
- Time to Interactive: < 5s
- Largest Contentful Paint: < 2.5s
- Cumulative Layout Shift: < 0.1

Backend:
- API Response Time: < 500ms
- Database Query Time: < 100ms
- Server Uptime: > 99.9%
- Error Rate: < 0.1%
```

### 14. Scaling Considerations

1. **Horizontal Scaling**
   - Load balancer (Nginx, HAProxy)
   - Multiple backend instances
   - Database replication

2. **Vertical Scaling**
   - Increase server resources
   - Optimize code
   - Cache frequently accessed data

3. **Caching**
   - Redis for session storage
   - CloudFlare for static assets
   - Browser caching policies

### 15. Maintenance

1. **Regular Updates**
   - Node.js updates
   - Dependency updates
   - Security patches

2. **Monitoring**
   - Daily uptime checks
   - Weekly performance reviews
   - Monthly security audits

3. **Backups**
   - Daily database backups
   - Weekly code backups
   - Test restore procedures monthly

## Deployment Summary

| Component | Platform | Cost | Features |
|-----------|----------|------|----------|
| Backend | Heroku | $7-50/month | Easy deployment, auto-scaling |
| Frontend | Vercel/Netlify | Free | Fast, global CDN |
| Database | MongoDB Atlas | Free-100+/month | Cloud managed, scalable |
| Domain | GoDaddy/Route53 | $10-15/year | DNS management |

## Estimated Monthly Cost

- Backend: $10-50
- Frontend: $0-20
- Database: $0-50
- Domain: $1-2
- **Total: $11-122/month**

## Support

For deployment issues:
1. Check provider documentation
2. Review application logs
3. Test locally first
4. Contact provider support

---

**Deployment completed? Great! Your Job Application Tracker is now live! 🎉**
