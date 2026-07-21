# Job Application Tracker - Quick Reference Guide

## 🚀 Quick Start (5 Minutes)

### Prerequisites
- Node.js installed
- MongoDB running on localhost:27017

### Start All Services

**Terminal 1 - Backend:**
```bash
cd backend
npm install
npm run dev
```

**Terminal 2 - Frontend:**
```bash
cd frontend
npm install
npm start
```

Visit: `http://localhost:3000`

## 📋 Application Features

| Feature | Description | Location |
|---------|-------------|----------|
| **Authentication** | Secure login/register | `/login`, `/register` |
| **Dashboard** | Overview & statistics | `/dashboard` |
| **Applications** | Manage job applications | `/applications` |
| **Reminders** | Set follow-up reminders | `/reminders` |
| **Notes** | Add application notes | Application detail |
| **Analytics** | View trends & stats | `/analytics` |

## 🎯 Common Tasks

### Add a Job Application
1. Go to Applications page
2. Click "Add Application"
3. Fill in job details
4. Click "Submit"

### Set a Reminder
1. Go to Reminders page
2. Click "Add Reminder"
3. Select application
4. Set date and title
5. Click "Create Reminder"

### View Analytics
1. Go to Analytics page
2. See application stats
3. View success rates
4. Check monthly trends

## 📊 API Quick Reference

| Method | Endpoint | Purpose |
|--------|----------|---------|
| POST | `/api/auth/login` | User login |
| POST | `/api/auth/register` | User registration |
| POST | `/api/applications` | Create application |
| GET | `/api/applications` | List applications |
| PUT | `/api/applications/:id` | Update application |
| DELETE | `/api/applications/:id` | Delete application |
| POST | `/api/reminders` | Create reminder |
| GET | `/api/reminders` | List reminders |
| POST | `/api/notes` | Create note |
| GET | `/api/analytics` | Get analytics |

## 🔧 Configuration

### Backend .env
```env
PORT=5000
MONGODB_URI=mongodb://localhost:27017/jobtracker
JWT_SECRET=your_secret_key
NODE_ENV=development
```

### Frontend API URL
Update in `frontend/src/services/api.js` if backend is on different port

## 🛠️ Troubleshooting

| Issue | Solution |
|-------|----------|
| MongoDB connection error | Ensure MongoDB is running on port 27017 |
| Port 5000 already in use | Change PORT in backend/.env |
| Blank frontend page | Clear cache, restart both servers |
| "Cannot find module" | Run `npm install` in that directory |
| Styling broken | Clear browser cache (Ctrl+Shift+Delete) |

## 📦 Project Structure

```
JobTracker/
├── backend/          # Express API server
├── frontend/         # React web application
├── README.md         # Main documentation
├── PROJECT_INDEX.md  # File structure reference
└── WINDOWS_SETUP.md  # Windows installation guide
```

## 🎨 Default Colors

- **Primary**: #667eea (Purple)
- **Success**: #27ae60 (Green)
- **Warning**: #f39c12 (Orange)
- **Danger**: #e74c3c (Red)

## 📱 Responsive Breakpoints

- Desktop: > 1024px
- Tablet: 768px - 1024px
- Mobile: < 768px

## 🔐 Security

- ✅ JWT authentication
- ✅ Password hashing
- ✅ User authorization
- ✅ CORS enabled
- ⚠️ Use HTTPS in production

## 📚 Documentation Files

| File | Purpose |
|------|---------|
| `README.md` | Complete project overview |
| `backend/README.md` | Backend API documentation |
| `frontend/README.md` | Frontend setup & features |
| `PROJECT_INDEX.md` | File structure & API reference |
| `WINDOWS_SETUP.md` | Windows installation steps |
| `QUICK_REFERENCE.md` | This file |

## ⚙️ Available NPM Scripts

### Backend
```bash
npm run dev       # Start with auto-reload
npm start         # Start production server
npm test          # Run tests
```

### Frontend
```bash
npm start         # Start development server
npm run build     # Create production build
npm test          # Run tests
```

## 🌐 URLs

| Service | URL |
|---------|-----|
| Frontend | http://localhost:3000 |
| Backend | http://localhost:5000 |
| Health Check | http://localhost:5000/health |
| MongoDB | localhost:27017 |

## 💾 Database Collections

1. **Users** - User accounts
2. **Applications** - Job applications
3. **Reminders** - Follow-up reminders
4. **Notes** - Application notes
5. **Status** - Status history

## 📈 Key Metrics

- Total Applications Count
- Status Breakdown (Applied, Interview, Offer, Rejected)
- Monthly Application Trends
- Offer Rate Percentage
- Interview Rate Percentage

## 🔄 Authentication Flow

1. User registers/logs in
2. JWT token created
3. Token stored in localStorage
4. Token sent with each API request
5. Token validated on backend
6. User redirected to login if token invalid

## 📦 Dependencies

### Backend
- express
- mongoose
- bcryptjs
- jsonwebtoken
- cors
- dotenv

### Frontend
- react
- react-router-dom
- axios
- react-scripts

## 🎓 Learning Resources

- [Express.js Documentation](https://expressjs.com/)
- [MongoDB Documentation](https://docs.mongodb.com/)
- [React Documentation](https://react.dev/)
- [RESTful API Design](https://restfulapi.net/)

## ✅ Pre-Deployment Checklist

- [ ] All environment variables set
- [ ] MongoDB configured
- [ ] Frontend builds without errors
- [ ] Backend starts successfully
- [ ] Can register new user
- [ ] Can create application
- [ ] Can set reminder
- [ ] Can view analytics

## 🚀 Deployment Options

### Backend
- Heroku
- AWS Lambda
- DigitalOcean
- Azure App Service
- Google Cloud Run

### Frontend
- Vercel
- Netlify
- GitHub Pages
- AWS S3 + CloudFront
- Azure Static Web Apps

### Database
- MongoDB Atlas (cloud)
- AWS RDS
- Azure Cosmos DB
- Self-hosted MongoDB

## 📞 Support

- Check README files for detailed docs
- Review browser console (F12) for errors
- Check backend logs in terminal
- Review MongoDB logs for database issues

## 🎯 Next Steps

1. ✅ Run the application
2. ✅ Create test account
3. ✅ Add sample applications
4. ✅ Test all features
5. ✅ Customize styling (optional)
6. ✅ Deploy to production

## 💡 Tips & Tricks

- Use browser DevTools (F12) to debug
- Check network tab for API requests
- Use MongoDB shell (`mongosh`) to query database
- Use Postman to test API endpoints
- Use nodemon for auto-reload during development

## 🔗 Quick Links

- [Express Middleware Guide](https://expressjs.com/en/guide/using-middleware.html)
- [Mongoose Schema Reference](https://mongoosejs.com/docs/schematypes.html)
- [React Hooks Documentation](https://react.dev/reference/react)
- [JWT Introduction](https://jwt.io/introduction)

---

**Last Updated**: May 2026
**Version**: 1.0.0
**License**: MIT

For more information, visit the main README.md file.
