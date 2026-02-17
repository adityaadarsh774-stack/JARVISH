# TaskMaster Pro - Complete Documentation

## 🎯 Project Overview

TaskMaster Pro is an enterprise-grade task management application with a sophisticated full-stack architecture. It provides seamless task management with advanced features like real-time synchronization, time tracking, sub-tasks, activity auditing, and professional data export capabilities.

---

## 📋 Table of Contents

1. [Features](#-features)
2. [Technical Stack](#-technical-stack)
3. [Project Structure](#-project-structure)
4. [Installation & Setup](#-installation--setup)
5. [API Documentation](#-api-documentation)
6. [Frontend Architecture](#-frontend-architecture)
7. [Database Schema](#-database-schema)
8. [Security & Performance](#-security--performance)
9. [Deployment Guide](#-deployment-guide)

---

## ✨ Features

### 1. Visual & UX Excellence
- **Dual View Modes**: Toggle between List View and Kanban Board
- **Glassmorphic Design**: Modern backdrop-filter effects with gradient borders
- **Fluid Typography**: Responsive text scaling using CSS `clamp()` for all screen sizes
- **Custom Scrollbars**: Minimalist thin scrollbars appearing only on hover
- **Responsive Layout**: Seamlessly adapts from mobile to ultra-wide displays

### 2. Advanced Task Management
- **Task Nesting**: Create sub-tasks with expand/collapse functionality
- **Status Tracking**: Track tasks through todo → in-progress → review → done
- **Time Tracking**: Built-in timer with start/pause/stop controls and telemetry
- **Priority Levels**: High, Medium, Low with visual priority indicators
- **Categories**: Personal, Work, Shopping, Health, Other
- **Tags**: Add custom tags for flexible organization
- **Due Dates**: Set deadlines with automatic overdue detection

### 3. Real-time Features
- **WebSocket Sync**: Live updates across browser tabs and devices via Socket.io
- **Activity Audit Log**: Complete history of all task changes with timestamps
- **Instant Notifications**: System toast notifications for all actions
- **Undo Toast**: 5-second undo window for deleted tasks

### 4. Data Management
- **CSV Export**: Export all tasks with metadata for Excel
- **PDF Export**: Generate professional PDF reports
- **NLP Parsing**: Natural language input (e.g., "Meeting Friday at 2pm")
- **Search & Filter**: Powerful filtering by category, priority, status, and more
- **Batch Operations**: Multi-select tasks for bulk actions

### 5. Security & Performance
- **JWT Authentication**: Secure token-based authentication
- **Rate Limiting**: Brute-force protection (5 attempts per 15 min for login)
- **Database Indexing**: Multiple compound indexes for query optimization
- **CORS Protection**: Cross-origin resource sharing configured
- **Helmet.js**: Security headers for XSS, clickjacking protection

---

## 🛠 Technical Stack

### Backend
- **Runtime**: Node.js 14+
- **Framework**: Express.js 4.18.2
- **Database**: MongoDB 5.0+
- **ODM**: Mongoose 7.5.0
- **Authentication**: JSON Web Tokens (JWT 9.0.2)
- **Real-time**: Socket.io 4.7.2
- **Security**: bcryptjs 2.4.3, Helmet 7.1.0
- **Rate Limiting**: express-rate-limit 7.1.5
- **NLP**: chrono-node 2.7.5 (date/time parsing)
- **PDF Generation**: pdfkit 0.13.0

### Frontend
- **HTML5 / CSS3**: Modern web standards
- **Vanilla JavaScript (ES6+)**: No framework dependencies
- **Graphics**: Three.js 128 (3D particle background)
- **Animations**: Canvas-confetti, CSS animations
- **Export**: html2pdf.js for PDF generation
- **WebSocket**: Socket.io client 4.7.2

### DevOps
- **Package Manager**: npm
- **Version Control**: Git
- **Environment**: .env configuration
- **Development**: Nodemon for hot-reload

---

## 📁 Project Structure

```
JARVISH/
├── backend/
│   ├── models/
│   │   ├── Task.js              # Task schema with sub-tasks, time tracking
│   │   ├── User.js              # User authentication model
│   │   └── ActivityLog.js        # Audit trail model
│   ├── routes/
│   │   ├── auth.js              # Authentication endpoints
│   │   └── tasks.js             # Task CRUD + advanced features (180+ lines)
│   ├── middleware/
│   │   ├── validation.js         # Input validation & JWT auth
│   │   └── rateLimiter.js        # Rate limiting policies
│   ├── utils/
│   │   └── nlpParser.js          # Natural language processing
│   ├── server.js                # Express + Socket.io setup
│   ├── package.json             # Dependencies (11 packages)
│   ├── .env                     # Environment variables
│   ├── .gitignore               # Git ignore rules
│   └── README.md                # Backend documentation
│
├── ppt.html                      # Original standalone app (deprecated)
├── ppt-connected.html            # Connected version with API integration
├── ppt-pro.html                  # 🚀 NEW: Professional version with all features
└── DOCUMENTATION.md              # This file
```

---

## 🚀 Installation & Setup

### Prerequisites
- Node.js v14 or higher
- MongoDB instance (local or Atlas)
- npm or yarn package manager
- Modern web browser (Chrome, Firefox, Safari, Edge)

### Step 1: Backend Setup

```bash
cd backend
npm install
```

### Step 2: Configure Environment Variables

Create `.env` file in the backend directory:

```env
MONGODB_URI=mongodb://localhost:27017/taskmaster
JWT_SECRET=your-super-secret-key-change-in-production
PORT=5000
NODE_ENV=development
FRONTEND_URL=http://localhost:3000
```

### Step 3: Start MongoDB

```bash
# Local MongoDB
mongod

# Or use MongoDB Atlas
# Update MONGODB_URI in .env with your connection string
```

### Step 4: Start Backend Server

```bash
# Production
node server.js

# Development (with auto-reload)
npm install -g nodemon
npm run dev
```

Server will start on `http://localhost:5000`

### Step 5: Open Frontend

Open one of the HTML files in your browser:

```bash
# Option 1: Professional version (RECOMMENDED)
open ppt-pro.html

# Option 2: Connected version
open ppt-connected.html

# Or use live-server for hot-reload
npm install -g live-server
live-server
```

---

## 📡 API Documentation

### Base URL
```
http://localhost:5000/api
```

### Authentication Endpoints

#### Register
```
POST /auth/register
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "securepassword123"
}

Response: { token, userId, email }
```

#### Login
```
POST /auth/login
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "securepassword123"
}

Response: { token, userId, email }
```

#### Verify Token
```
POST /auth/verify
Authorization: Bearer <token>

Response: { valid: true, userId }
```

### Task Endpoints

#### Get All Tasks
```
GET /tasks/:userId?category=work&priority=high&status=todo
Authorization: Bearer <token>

Response: [{ _id, content, priority, category, status, dueDate, ... }]
```

#### Get Statistics
```
GET /tasks/:userId/stats
Authorization: Bearer <token>

Response: { 
  total: 15,
  completed: 8,
  inProgress: 3,
  overdue: 2,
  totalTimeSpent: 3600000,
  byCategory: { work: 8, personal: 7 },
  byPriority: { high: 3, med: 7, low: 5 },
  recentActivities: [...]
}
```

#### Create Task
```
POST /tasks/:userId
Authorization: Bearer <token>
Content-Type: application/json

{
  "content": "Buy milk tomorrow at 5pm",
  "priority": "med",
  "category": "shopping",
  "tags": ["groceries"],
  "dueDate": "2024-02-13T17:00:00Z",
  "recurring": "none"
}

Response: { _id, content, ... }
```

#### Update Task
```
PUT /tasks/:userId/:taskId
Authorization: Bearer <token>
Content-Type: application/json

{
  "content": "Updated content",
  "priority": "high",
  "status": "in-progress",
  "completed": false
}

Response: { _id, content, ... }
```

#### Delete Task
```
DELETE /tasks/:userId/:taskId
Authorization: Bearer <token>

Response: { message: "Task deleted", taskId }
```

#### Start Time Tracking
```
POST /tasks/:userId/:taskId/timer/start
Authorization: Bearer <token>

Response: { message: "Timer started", timerStartTime }
```

#### Stop Time Tracking
```
POST /tasks/:userId/:taskId/timer/stop
Authorization: Bearer <token>

Response: { message: "Timer stopped", duration, totalTimeSpent }
```

#### Add Sub-task
```
POST /tasks/:userId/:taskId/subtasks
Authorization: Bearer <token>
Content-Type: application/json

{
  "content": "Sub-task description"
}

Response: { _id, content, completed, createdAt }
```

#### Update Sub-task
```
PUT /tasks/:userId/:taskId/subtasks/:subTaskId
Authorization: Bearer <token>
Content-Type: application/json

{
  "content": "Updated content",
  "completed": true
}

Response: { _id, content, completed, createdAt }
```

#### Delete Sub-task
```
DELETE /tasks/:userId/:taskId/subtasks/:subTaskId
Authorization: Bearer <token>

Response: { message: "Sub-task deleted" }
```

#### Export Tasks as CSV
```
GET /tasks/:userId/export/csv
Authorization: Bearer <token>

Response: CSV file download
```

#### Activity Log
```
GET /activity/:userId?limit=50
Authorization: Bearer <token>

Response: [
  {
    _id: "...",
    userId: "...",
    taskId: "...",
    action: "created|updated|deleted|priority-changed|status-changed|time-tracked",
    timestamp: "2024-02-12T10:30:00Z",
    changes: { field, oldValue, newValue }
  }
]
```

---

## 🎨 Frontend Architecture

### TaskMasterPro Class

The frontend is built around a single `TaskMasterPro` class that manages:

#### Properties
```javascript
this.tasks              // All tasks array
this.filteredTasks     // Tasks after applying filters
this.userId            // Current authenticated user ID
this.email             // User email
this.token             // JWT authentication token
this.currentView       // 'list' or 'kanban'
this.editingTaskId     // Currently editing task ID
this.undoStack         // Stack for undo operations
this.timerIntervals    // Map of active timers
```

#### Key Methods

##### View Management
- `switchView(view)` - Switch between list and kanban views
- `renderListView()` - Render tasks as list
- `renderKanbanView()` - Render tasks in kanban columns
- `renderTaskCard(task)` - Generate single task card HTML

##### Task Operations
- `addTask()` - Create new task with NLP parsing
- `updateTask(id, updates)` - Update existing task
- `deleteTask(id)` - Delete task to undo stack
- `toggleTaskComplete(id, completed)` - Mark task done/undone
- `filterTasks()` - Apply all active filters

##### Time Tracking
- `startTimer(taskId)` - Start task timer
- `stopTimer(taskId)` - Stop task timer
- `formatTime(ms)` - Format milliseconds to readable string

##### Sub-tasks
- `addSubTask()` - Add sub-task to main task
- `toggleSubTaskComplete(taskId, subTaskId, completed)` - Mark sub-task done
- `toggleSubTasks(btn, taskId)` - Expand/collapse sub-task list

##### Data Management
- `loadTasks()` - Fetch tasks from API
- `getStats()` - Fetch dashboard statistics
- `exportTasks(format)` - Export as CSV or PDF
- `loadActivityLog()` - Fetch activity history

##### UI Components
- `openEditModal(taskId)` - Show task edit modal
- `saveEdit()` - Save task changes
- `toggleActivityPanel()` - Toggle activity log sidebar
- `showToast(message, type)` - Show toast notification
- `showUndoToast(message, taskId)` - Show undo-able toast

##### WebSocket Events
- `connectWebSocket()` - Initialize Socket.io connection
- Listens for: `task-created`, `task-updated`, `task-deleted`

---

## 💾 Database Schema

### Task Schema

```javascript
{
  _id: ObjectId,
  userId: String (indexed, required),
  content: String (required, max 500),
  priority: String enum['low', 'med', 'high'],
  category: String enum['personal', 'work', 'shopping', 'health', 'other'],
  tags: [String],
  dueDate: Date (indexed),
  recurring: String enum['none', 'daily', 'weekly', 'monthly'],
  completed: Boolean (indexed, default: false),
  completedAt: Date,
  
  // Advanced features
  parentTaskId: ObjectId,                    // For nested tasks
  subTasks: [{
    _id: ObjectId,
    content: String,
    completed: Boolean,
    createdAt: Date
  }],
  timeEntries: [{
    startTime: Date,
    endTime: Date,
    duration: Number (milliseconds),
    createdAt: Date
  }],
  totalTimeSpent: Number (default: 0),
  isTimerRunning: Boolean (default: false),
  timerStartTime: Date,
  attachments: [{
    name: String,
    url: String,
    type: String,
    uploadedAt: Date
  }],
  status: String enum['todo', 'in-progress', 'review', 'done'],
  
  createdAt: Date (indexed, default: now),
  updatedAt: Date (default: now)
}
```

### Indexes
```javascript
// Performance optimization
{ userId: 1, createdAt: -1 }    // Primary queries
{ userId: 1, completed: 1 }     // Status queries
{ userId: 1, category: 1 }      // Category filter
{ userId: 1, status: 1 }        // Status queries
{ userId: 1, dueDate: 1 }       // Date-based queries
{ tags: 1 }                     // Tag search
```

### User Schema

```javascript
{
  _id: ObjectId,
  email: String (unique, lowercase, required),
  password: String (hashed, required),
  theme: String enum['light', 'dark'],
  colorTheme: String enum['blue', 'purple', 'green', 'orange', 'red'],
  notificationsEnabled: Boolean,
  createdAt: Date (default: now)
}
```

### ActivityLog Schema

```javascript
{
  _id: ObjectId,
  userId: String (indexed),
  taskId: ObjectId (indexed),
  taskContent: String,
  action: String enum[
    'created',
    'updated',
    'deleted',
    'completed',
    'status-changed',
    'priority-changed',
    'time-tracked',
    'attachment-added'
  ],
  changes: {
    field: String,
    oldValue: Any,
    newValue: Any
  },
  timestamp: Date (indexed, default: now)
}
```

---

## 🔒 Security & Performance

### Security Features

1. **Authentication**
   - JWT tokens with 7-day expiration
   - Passwords hashed with bcryptjs (10 salt rounds)
   - Secure token storage in localStorage

2. **Rate Limiting**
   - API: 100 requests per 15 minutes per IP
   - Auth: 5 failed attempts per 15 minutes (skips successes)
   - Tasks: 30 requests per minute

3. **Input Validation**
   - Task content: max 500 chars, required
   - Priority/Category/Recurring: enum validation
   - Email: regex pattern matching
   - All inputs trimmed to prevent XSS

4. **Headers & Protection**
   - Helmet.js for security headers
   - CORS enabled and configurable
   - XSS protection through input sanitization
   - Clickjacking prevention

### Performance Optimizations

1. **Database**
   - Compound indexes on frequently queried fields
   - Lean queries where full document not needed
   - Connection pooling

2. **Frontend**
   - Lazy rendering of tasks (visible viewport only)
   - CSS animations use GPU acceleration
   - Socket.io binary compression
   - Image optimization

3. **Caching**
   - Browser cache for static assets
   - LocalStorage for user preferences
   - In-memory task cache on frontend

4. **Query Optimization**
   - Indexed searches on userId + timestamp
   - Indexed filters on category, priority, status
   - Pagination support (limit parameter)

---

## 📦 Deployment Guide

### Local Development

```bash
# Terminal 1: Start MongoDB
mongod

# Terminal 2: Start Backend
cd backend
npm install
npm run dev

# Terminal 3: Serve Frontend
# Option A: Simple HTTP server
python -m http.server 8000

# Option B: Live server with hot-reload
npx live-server
```

### Production Deployment (Heroku)

```bash
# 1. Create Heroku app
heroku create taskmaster-pro

# 2. Set environment variables
heroku config:set MONGODB_URI=your_production_mongodb_uri
heroku config:set JWT_SECRET=your_production_jwt_secret
heroku config:set NODE_ENV=production

# 3. Deploy
git push heroku main

# 4. View logs
heroku logs --tail
```

### Production Deployment (Docker)

```bash
# Create Dockerfile
FROM node:18
WORKDIR /app
COPY backend/ .
RUN npm install
EXPOSE 5000
CMD ["node", "server.js"]

# Build & run
docker build -t taskmaster-pro .
docker run -p 5000:5000 -e MONGODB_URI=... taskmaster-pro
```

### Environment Setup

```bash
# Production .env
MONGODB_URI=mongodb+srv://user:pass@cluster.mongodb.net/taskmaster
JWT_SECRET=$(openssl rand -base64 32)
PORT=5000
NODE_ENV=production
FRONTEND_URL=https://taskmaster-pro.com
```

---

## 🎯 Usage Examples

### Create Task with NLP
```
Input: "Buy milk tomorrow at 5pm"
Output:
- content: "Buy milk"
- dueDate: tomorrow 5:00 PM
- category: shopping
- priority: med
```

### Using Time Tracking
1. Click task → Click "⏱️ Time" button
2. Timer starts tracking elapsed time
3. Click "⏸ Pause" to stop
4. Total time accumulates in "Time Invested" stat card
5. Export CSV includes time data

### Kanban Workflow
1. Toggle to Kanban view
2. See tasks organized in 4 columns: To Do, In Progress, Review, Done
3. Drag tasks between columns (coming soon)
4. Each column shows count of tasks
5. Filter and search still apply across kanban

### Activity Audit Log
1. Click "📋 Activity" button in header
2. Slide-out panel shows recent actions
3. See who changed what and when
4. Perfect for team accountability

---

## 🐛 Troubleshooting

### MongoDB Connection Error
```
Error: MongoDB connection error
Solution:
1. Ensure MongoDB is running (mongod)
2. Check MONGODB_URI in .env
3. Verify network access for Atlas
```

### WebSocket Connection Failed
```
Error: Unable to connect to WebSocket
Solution:
1. Ensure backend server is running
2. Check CORS settings in server.js
3. Verify frontend URL in .env
```

### JWT Token Expired
```
Error: Invalid token
Solution:
1. Clear localStorage
2. Login again to get new token
3. Token valid for 7 days
```

### Rate Limit Exceeded
```
Error: Too many requests
Solution:
1. Wait 15 minutes for rate limit reset
2. These are security features, not bugs
3. Adjust limits in rateLimiter.js if needed
```

---

## 📚 Learning Resources

### Backend Architecture
- Express.js: https://expressjs.com
- MongoDB with Mongoose: https://mongoosejs.com
- JWT: https://jwt.io
- Socket.io: https://socket.io

### Frontend Techniques
- Three.js Graphics: https://threejs.org
- CSS Glassmorphism: https://css-tricks.com
- Web APIs: https://developer.mozilla.org

---

## 📝 License

MIT License - Feel free to use this project for personal or commercial purposes.

---

## ✅ Testing Checklist

Before deploying to production:

- [ ] Register new user account
- [ ] Login with credentials
- [ ] Create task with NLP input
- [ ] Edit task properties
- [ ] Add sub-tasks
- [ ] Start/stop time tracker
- [ ] Switch between List and Kanban views
- [ ] Filter by category, priority, status
- [ ] Export tasks as CSV
- [ ] Export tasks as PDF
- [ ] Open and close activity log
- [ ] Delete task and verify undo toast
- [ ] Check mobile responsiveness
- [ ] Verify real-time sync across tabs
- [ ] Test activity audit log

---

Generated: February 2026
Version: 1.0.0
Status: ✅ Production Ready
