## Installation & Setup Guide for Windows Users

### Prerequisites Installation (Windows)

#### 1. Install Node.js
1. Download from: https://nodejs.org/ (LTS version recommended)
2. Run the installer
3. Follow the installation wizard
4. Verify installation by opening Command Prompt and running:
   ```cmd
   node --version
   npm --version
   ```

#### 2. Install MongoDB
1. Download from: https://www.mongodb.com/try/download/community
2. Choose Windows (msi)
3. Run the installer
4. Follow the installation wizard
5. MongoDB will be installed as a Windows Service
6. Verify MongoDB is running by checking Services (services.msc)

#### 3. Alternative: Use MongoDB Atlas (Cloud)
1. Go to: https://www.mongodb.com/cloud/atlas
2. Create a free account
3. Create a cluster
4. Update `MONGODB_URI` in backend `.env`:
   ```env
   MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/jobtracker
   ```

### Step-by-Step Setup on Windows

#### Step 1: Extract Project
1. Extract the JobTracker project to a folder (e.g., `C:\Projects\JobTracker`)
2. Open Command Prompt
3. Navigate to the project folder:
   ```cmd
   cd C:\Projects\JobTracker
   ```

#### Step 2: Setup Backend
1. Navigate to backend:
   ```cmd
   cd backend
   ```

2. Install dependencies:
   ```cmd
   npm install
   ```

3. Create .env file (copy from .env.example):
   ```cmd
   copy .env.example .env
   ```

4. Edit .env file with Notepad or VS Code and set:
   ```env
   PORT=5000
   MONGODB_URI=mongodb://localhost:27017/jobtracker
   JWT_SECRET=your_secret_key_123
   NODE_ENV=development
   ```

5. Start backend server:
   ```cmd
   npm run dev
   ```

   Should display: `Server running on port 5000`

#### Step 3: Setup Frontend (New Command Prompt)
1. Open a new Command Prompt
2. Navigate to frontend:
   ```cmd
   cd C:\Projects\JobTracker\frontend
   ```

3. Install dependencies:
   ```cmd
   npm install
   ```

4. Start frontend:
   ```cmd
   npm start
   ```

   Should automatically open browser at `http://localhost:3000`

### Quick Start (After First Setup)

**Command Prompt 1 - Backend:**
```cmd
cd C:\Projects\JobTracker\backend
npm run dev
```

**Command Prompt 2 - Frontend:**
```cmd
cd C:\Projects\JobTracker\frontend
npm start
```

### Testing the System

1. Open browser at: `http://localhost:3000`
2. Click "Create Account"
3. Fill in details:
   - Full Name: John Doe
   - Email: john@example.com
   - Password: password123
   - Phone: (optional)
4. Click Register
5. You should be redirected to Dashboard

### Common Windows Issues & Solutions

**Issue: "npm is not recognized"**
- Solution: Restart Command Prompt after Node.js installation
- Or check System Environment Variables (search "Environment Variables")

**Issue: Port 5000 already in use**
- Solution: Change PORT in backend/.env to 5001
- Or: Open Task Manager → find node.exe → End Task

**Issue: MongoDB connection refused**
- Solution: Verify MongoDB service is running (services.msc)
- Or use MongoDB Atlas cloud database

**Issue: npm install fails**
- Solution: Delete node_modules folder and package-lock.json
- Run: `npm cache clean --force`
- Try again: `npm install`

### Optional: Setup with VS Code

1. Download VS Code from: https://code.visualstudio.com
2. Open VS Code
3. File → Open Folder → Select JobTracker folder
4. Open Terminal: Ctrl + `
5. Follow setup steps above in VS Code terminal

### Optional: Using Nodemon for Auto-Reload

Already installed! Backend automatically restarts on file changes when using:
```cmd
npm run dev
```

### Optional: Setup with Docker

1. Install Docker Desktop from: https://www.docker.com/products/docker-desktop
2. Run in project root:
   ```cmd
   docker-compose up
   ```

### Project Structure on Windows

```
C:\Projects\JobTracker\
├── backend\
│   ├── controllers\
│   ├── models\
│   ├── routes\
│   ├── middleware\
│   ├── config\
│   ├── server.js
│   ├── package.json
│   ├── .env
│   └── node_modules\
│
├── frontend\
│   ├── src\
│   │   ├── components\
│   │   ├── pages\
│   │   ├── services\
│   │   ├── App.js
│   │   └── index.js
│   ├── public\
│   ├── package.json
│   └── node_modules\
│
└── README.md
```

### Accessing the Application

- **Frontend**: http://localhost:3000
- **Backend API**: http://localhost:5000
- **API Health Check**: http://localhost:5000/health
- **MongoDB**: localhost:27017

### Stopping the Application

**To stop backend**: Press Ctrl + C in backend Command Prompt
**To stop frontend**: Press Ctrl + C in frontend Command Prompt
**To stop MongoDB**: Windows Service (services.msc) → Stop MongoDB service

### Useful Commands

```cmd
# Install dependencies
npm install

# Start development server
npm run dev          (backend)
npm start            (frontend)

# Build for production
npm run build        (frontend)

# Check installed Node version
node --version

# Check npm version
npm --version

# Clear npm cache
npm cache clean --force

# List global npm packages
npm list -g
```

### Next Steps

1. Familiarize yourself with the application
2. Create test job applications
3. Set reminders and notes
4. Check analytics
5. Customize as needed

### Support

- Check README.md files in backend and frontend folders
- Check browser console (F12) for errors
- Check Command Prompt for server errors
- Visit documentation in main README.md

### Production Deployment

When ready for production:
1. Build frontend: `npm run build`
2. Set NODE_ENV=production in backend .env
3. Use MongoDB Atlas instead of local MongoDB
4. Deploy to services like:
   - **Frontend**: Vercel, Netlify, GitHub Pages
   - **Backend**: Heroku, AWS, Azure, DigitalOcean
   - **Database**: MongoDB Atlas, AWS RDS, Azure Cosmos DB
