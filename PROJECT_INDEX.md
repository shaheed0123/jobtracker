# Project Index & File Structure

## Complete File Structure

```
JobTracker/
│
├── README.md                                    # Main project documentation
├── WINDOWS_SETUP.md                             # Windows installation guide
├── docker-compose.yml                           # Docker Compose configuration
│
├── backend/
│   ├── config/
│   │   └── database.js                          # MongoDB connection
│   │
│   ├── models/
│   │   ├── User.js                              # User schema
│   │   ├── Application.js                       # Application schema
│   │   ├── Note.js                              # Note schema
│   │   ├── Reminder.js                          # Reminder schema
│   │   └── Status.js                            # Status schema
│   │
│   ├── controllers/
│   │   ├── authController.js                    # Authentication logic
│   │   ├── userController.js                    # User management logic
│   │   ├── applicationController.js             # Application logic
│   │   ├── noteController.js                    # Note logic
│   │   ├── reminderController.js                # Reminder logic
│   │   ├── statusController.js                  # Status logic
│   │   └── analyticsController.js               # Analytics logic
│   │
│   ├── routes/
│   │   ├── authRoutes.js                        # Auth endpoints
│   │   ├── userRoutes.js                        # User endpoints
│   │   ├── applicationRoutes.js                 # Application endpoints
│   │   ├── noteRoutes.js                        # Note endpoints
│   │   ├── reminderRoutes.js                    # Reminder endpoints
│   │   ├── statusRoutes.js                      # Status endpoints
│   │   └── analyticsRoutes.js                   # Analytics endpoints
│   │
│   ├── middleware/
│   │   └── authMiddleware.js                    # JWT authentication
│   │
│   ├── server.js                                # Express server setup
│   ├── package.json                             # Backend dependencies
│   ├── .env.example                             # Environment variables template
│   ├── .gitignore                               # Git ignore rules
│   ├── Dockerfile                               # Docker configuration
│   └── README.md                                # Backend documentation
│
├── frontend/
│   ├── public/
│   │   └── index.html                           # Main HTML file
│   │
│   ├── src/
│   │   ├── components/
│   │   │   ├── Header.js                        # Header component
│   │   │   ├── Sidebar.js                       # Sidebar navigation
│   │   │   ├── ApplicationCard.js               # Application card display
│   │   │   ├── ApplicationForm.js               # Application form
│   │   │   ├── ReminderForm.js                  # Reminder form
│   │   │   ├── Modal.js                         # Modal dialog
│   │   │   └── styles.css                       # Global styles
│   │   │
│   │   ├── pages/
│   │   │   ├── Login.js                         # Login page
│   │   │   ├── Register.js                      # Registration page
│   │   │   ├── Dashboard.js                     # Dashboard page
│   │   │   ├── Applications.js                  # Applications page
│   │   │   ├── Reminders.js                     # Reminders page
│   │   │   └── Analytics.js                     # Analytics page
│   │   │
│   │   ├── services/
│   │   │   └── api.js                           # API client & services
│   │   │
│   │   ├── utils/
│   │   │   └── helpers.js                       # Utility functions
│   │   │
│   │   ├── App.js                               # Main app component
│   │   └── index.js                             # React entry point
│   │
│   ├── package.json                             # Frontend dependencies
│   ├── .gitignore                               # Git ignore rules
│   ├── Dockerfile                               # Docker configuration
│   ├── nginx.conf                               # Nginx configuration
│   └── README.md                                # Frontend documentation
```

## Key Files Explanation

### Backend Files

| File | Purpose |
|------|---------|
| `server.js` | Main Express server - initializes app and routes |
| `config/database.js` | MongoDB connection configuration |
| `models/*.js` | Mongoose schemas for database collections |
| `controllers/*.js` | API logic for handling requests |
| `routes/*.js` | Express route definitions |
| `middleware/authMiddleware.js` | JWT token validation |
| `package.json` | Dependencies and scripts |
| `.env` | Environment variables (not in git) |

### Frontend Files

| File | Purpose |
|------|---------|
| `App.js` | Main React component with routing |
| `index.js` | React DOM render entry point |
| `components/*.js` | Reusable React components |
| `pages/*.js` | Full page components |
| `services/api.js` | API client with axios |
| `utils/helpers.js` | Utility functions |
| `components/styles.css` | Global CSS styles |
| `package.json` | Dependencies and scripts |

## API Endpoints Summary

### Authentication
```
POST /api/auth/register
POST /api/auth/login
```

### User Management
```
GET  /api/users/profile
PUT  /api/users/profile
```

### Applications (CRUD)
```
POST   /api/applications
GET    /api/applications
GET    /api/applications/:id
PUT    /api/applications/:id
DELETE /api/applications/:id
```

### Reminders
```
POST   /api/reminders
GET    /api/reminders
GET    /api/reminders/application/:applicationId
PUT    /api/reminders/:id
DELETE /api/reminders/:id
```

### Notes
```
POST   /api/notes
GET    /api/notes/:applicationId
PUT    /api/notes/:id
DELETE /api/notes/:id
```

### Status & Analytics
```
GET /api/status/application/:applicationId
GET /api/status/summary/all
GET /api/analytics
```

## Database Collections

### Users
- Stores user account information
- Email is unique identifier
- Password stored as hashed bcrypt

### Applications
- Stores job application records
- Links to User via userId
- Contains job details and current status

### Reminders
- Stores reminder records
- Links to Application and User
- Tracks completion status

### Notes
- Stores application notes
- Links to Application and User
- Rich text content support

### Status
- Tracks status change history
- Links to Application and User
- Timestamps for each change

## Routes Summary

### Frontend Routes
```
/                - Root (redirects to dashboard or login)
/login          - Login page
/register       - Registration page
/dashboard      - Dashboard with statistics
/applications   - List and manage applications
/reminders      - List and manage reminders
/analytics      - View analytics and reports
```

### Backend API Routes
```
/api/auth/*           - Authentication endpoints
/api/users/*          - User management endpoints
/api/applications/*   - Application endpoints
/api/notes/*          - Note endpoints
/api/reminders/*      - Reminder endpoints
/api/status/*         - Status endpoints
/api/analytics/*      - Analytics endpoints
/health               - Health check
```

## Environment Variables

### Backend (.env)
```
PORT                  - Server port (default: 5000)
MONGODB_URI          - MongoDB connection string
JWT_SECRET           - JWT signing secret
EMAIL_SERVICE        - Email provider
EMAIL_USER           - Email address
EMAIL_PASSWORD       - Email password
NODE_ENV             - Environment (development/production)
```

## Development Workflow

1. **Backend Development**
   - Modify files in `backend/` directory
   - Server auto-reloads with nodemon
   - Check console for errors

2. **Frontend Development**
   - Modify files in `frontend/src/` directory
   - App hot-reloads automatically
   - Check browser console for errors

3. **Database Changes**
   - Modify schemas in `backend/models/`
   - Changes reflect on next app restart
   - Use MongoDB shell to verify

4. **Styling**
   - All CSS in `frontend/src/components/styles.css`
   - Classes applied to components
   - Responsive breakpoints at 1024px and 768px

## Testing Checklist

- [ ] User registration works
- [ ] User login works
- [ ] Add application works
- [ ] Edit application works
- [ ] Delete application works
- [ ] Add reminder works
- [ ] Add note works
- [ ] Filter by status works
- [ ] Analytics page loads
- [ ] Dashboard shows correct stats

## Deployment Checklist

- [ ] Update environment variables
- [ ] Build frontend: `npm run build`
- [ ] Test production build
- [ ] Configure MongoDB Atlas
- [ ] Set up HTTPS
- [ ] Configure CORS for production domain
- [ ] Deploy backend
- [ ] Deploy frontend
- [ ] Test deployed application

## Performance Metrics

### Expected Performance
- Page load: < 2 seconds
- API response: < 500ms
- Database query: < 100ms
- Frontend bundle: < 500KB gzipped

## Security Considerations

- ✅ Password hashing with bcryptjs
- ✅ JWT authentication
- ✅ User authorization checks
- ✅ Input validation
- ✅ CORS enabled
- ⚠️ Need: HTTPS in production
- ⚠️ Need: Rate limiting
- ⚠️ Need: SQL injection prevention

## Support & Resources

- [Main README](README.md) - Complete project overview
- [Backend README](backend/README.md) - Backend documentation
- [Frontend README](frontend/README.md) - Frontend documentation
- [Windows Setup](WINDOWS_SETUP.md) - Windows installation guide

## Quick Commands

```bash
# Backend
cd backend && npm install          # Install dependencies
npm run dev                        # Start development server

# Frontend
cd frontend && npm install         # Install dependencies
npm start                          # Start development server
npm run build                      # Build for production

# Docker
docker-compose up                  # Start all services
docker-compose down                # Stop all services
```

---

For detailed information about any component, refer to the specific README file or the comments in the source code.
