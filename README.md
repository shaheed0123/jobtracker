# Job Application Tracker - Frontend

## Overview

This is the frontend React application for the Job Application Tracker system. It provides a user-friendly interface for managing job applications, tracking their status, setting reminders, and viewing analytics.

## Features

- **User Authentication**: Secure login and registration
- **Dashboard**: Overview of job applications with key metrics
- **Application Management**: Add, edit, and delete job applications
- **Status Tracking**: Track application status changes (Applied, Interview, Offer, Rejected)
- **Reminders**: Set and manage reminders for follow-ups
- **Notes**: Add and manage notes for each application
- **Analytics**: View detailed analytics on applications and success rates
- **Responsive Design**: Works on desktop, tablet, and mobile devices

## Requirements

- Node.js (v14 or higher)
- npm or yarn
- Modern web browser

## Installation

1. Navigate to the frontend directory:
```bash
cd frontend
```

2. Install dependencies:
```bash
npm install
```

## Running the Application

### Development Mode
```bash
npm start
```

The application will open in your browser at `http://localhost:3000`

### Build for Production
```bash
npm run build
```

This creates an optimized production build in the `build` folder.

## Configuration

The frontend is configured to connect to the backend API at `http://localhost:5000`. This is set in the `package.json` as a proxy:

```json
"proxy": "http://localhost:5000"
```

If your backend is running on a different URL, you need to:
1. Update the `REACT_APP_API_URL` in a `.env` file
2. Or modify the API service configuration in `src/services/api.js`

## Project Structure

```
frontend/
├── public/
│   └── index.html              # Main HTML file
├── src/
│   ├── components/             # Reusable React components
│   │   ├── Header.js
│   │   ├── Sidebar.js
│   │   ├── ApplicationCard.js
│   │   ├── ApplicationForm.js
│   │   ├── ReminderForm.js
│   │   ├── Modal.js
│   │   └── styles.css          # Global styles
│   ├── pages/                  # Page components
│   │   ├── Login.js
│   │   ├── Register.js
│   │   ├── Dashboard.js
│   │   ├── Applications.js
│   │   ├── Reminders.js
│   │   └── Analytics.js
│   ├── services/
│   │   └── api.js              # API client and services
│   ├── utils/
│   │   └── helpers.js          # Utility functions
│   ├── App.js                  # Main app component
│   └── index.js                # Entry point
├── package.json
└── README.md
```

## Components

### Header
- Displays application title and user information
- Logout button

### Sidebar
- Navigation menu with links to different sections
- Dashboard, Applications, Reminders, Analytics

### Dashboard
- Overview of all applications
- Statistics cards showing totals by status
- Recent applications list

### Applications
- List of all job applications
- Filter by status
- Add new application form
- Edit/Delete applications
- Card view with application details

### Reminders
- List of reminders organized by date
- Upcoming reminders section
- Past reminders section
- Create new reminder form
- Mark reminders as complete

### Analytics
- Total applications count
- Status breakdown
- Monthly applications chart
- Success rate analysis
- Interview and offer rates

## API Integration

The application uses axios for API requests. All requests are intercepted to automatically include the JWT token from localStorage.

### Available Services

```javascript
// Authentication
authService.register(data)
authService.login(data)

// User
userService.getProfile()
userService.updateProfile(data)

// Applications
applicationService.create(data)
applicationService.getAll()
applicationService.getById(id)
applicationService.update(id, data)
applicationService.delete(id)

// Notes
noteService.create(data)
noteService.getByApplication(applicationId)
noteService.update(id, data)
noteService.delete(id)

// Reminders
reminderService.create(data)
reminderService.getByApplication(applicationId)
reminderService.getAll()
reminderService.update(id, data)
reminderService.delete(id)

// Analytics
analyticsService.getAnalytics()
```

## Styling

The application uses a custom CSS system with:
- Color-coded status badges
- Responsive grid layouts
- Form styling
- Modal dialogs
- Cards and badges
- Utility classes

### Color Scheme

- Primary: #667eea (Purple)
- Secondary: #764ba2 (Dark Purple)
- Success: #27ae60 (Green)
- Warning: #f39c12 (Orange)
- Danger: #e74c3c (Red)
- Info: #3498db (Blue)

## User Authentication Flow

1. User registers or logs in
2. Token is stored in localStorage
3. Token is automatically included in all API requests
4. If token expires, user is redirected to login
5. Logout clears token and user data

## State Management

The application uses React hooks for state management:
- `useState` for local component state
- `useEffect` for side effects and data fetching
- Local storage for persisting authentication token and user data

## Responsive Design

The application is fully responsive with breakpoints at:
- 1024px (Desktop to Tablet)
- 768px (Tablet to Mobile)

Navigation automatically adjusts for smaller screens.

## Performance Optimizations

- Lazy loading of components
- Efficient API calls
- Cached user data in localStorage
- Optimized CSS with minimal redraws

## Troubleshooting

### Cannot connect to backend
- Ensure backend is running on port 5000
- Check `proxy` setting in `package.json`
- Verify CORS is enabled in backend

### Token expiration
- The application automatically stores and includes the token
- If token expires, you'll be redirected to login
- Re-login to get a new token

### Styling issues
- Clear browser cache (Ctrl+Shift+Delete)
- Restart the development server
- Ensure all CSS files are in `src/components/`

## Browser Support

- Chrome (latest)
- Firefox (latest)
- Safari (latest)
- Edge (latest)

## Development

### Available Scripts

```bash
# Start development server
npm start

# Build for production
npm build

# Run tests
npm test

# Eject (one-way operation)
npm eject
```

## Dependencies

- React 18.2.0
- React DOM 18.2.0
- React Router DOM 6.8.0
- Axios 1.3.2
- React Scripts 5.0.1

## Future Enhancements

- Email notifications for reminders
- File upload for job postings
- Calendar view for applications
- Export reports to PDF
- Dark mode
- Multi-language support
- Mobile app using React Native
