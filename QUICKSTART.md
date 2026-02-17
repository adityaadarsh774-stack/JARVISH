# 🚀 TaskMaster Pro - Quick Start Guide

## 5-Minute Setup

### 1️⃣ Install Backend Dependencies
```bash
cd backend
npm install
```

### 2️⃣ Configure MongoDB
- **Option A (Local)**: Start MongoDB service
  ```bash
  mongod
  ```
- **Option B (Cloud)**: Update `.env` with MongoDB Atlas connection string

### 3️⃣ Set Environment Variables
Create/update `backend/.env`:
```env
MONGODB_URI=mongodb://localhost:27017/taskmaster
JWT_SECRET=dev-secret-change-in-production
PORT=5000
NODE_ENV=development
FRONTEND_URL=http://localhost:3000
```

### 4️⃣ Start Backend
```bash
npm run dev
# or
node server.js
```
✅ Server running on `http://localhost:5000`

### 5️⃣ Open Frontend
In browser, open:
- **Best Experience**: `ppt-pro.html` (Professional version with all features)
- **Alternative**: `ppt-connected.html` (Connected version)
- **Legacy**: `ppt.html` (Standalone version)

---

## 🎯 First Steps

### Create Account
1. Enter email and password
2. Click "Create Account" or "Sign In"
3. JWT token auto-saves to localStorage

### Add Your First Task
1. Type in input: "Buy milk tomorrow at 5pm"
2. Click "+ Add Task"
3. Watch smart NLP parsing extract:
   - ✅ Due date: Tomorrow at 5:00 PM
   - ✅ Category: Shopping
   - ✅ Priority: Medium
   - ✅ Content cleaned up

### Explore Features
- **List View**: See all tasks in a scrollable list
- **Kanban Board**: Organize tasks in 4 columns (To Do → In Progress → Review → Done)
- **Time Tracker**: Click "⏱️ Time" to track how long tasks take
- **Activity Log**: Click "📋 Activity" to see full audit trail
- **Export**: Download tasks as CSV or PDF

---

## 📊 Key Metrics Dashboard

Top-right stats show:
- **Total Tasks**: All tasks created
- **Completed**: % of tasks done
- **In Progress**: Active tasks
- **Overdue**: Tasks past due date
- **Time Invested**: Total hours tracked

---

## 🎮 Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `Enter` | Add new task (when input focused) |
| `Ctrl+F` / `Cmd+F` | Search tasks |

---

## 🛑 Common Issues

### "Cannot connect to server"
- Verify backend is running: `http://localhost:5000/api/health`
- Check MongoDB is running
- Ensure no port conflicts on 5000

### "MongoDB connection failed"
- Start MongoDB: `mongod`
- Or update MONGODB_URI to Atlas

### "WebSocket connection error"
- Backend must be running
- Check browser console for errors
- Refresh page

### Tasks not syncing across tabs?
- Ensure WebSocket is connected (backend running)
- Check browser console for errors

---

## 📁 File Structure

```
JARVISH/
├── ppt-pro.html              # 🌟 USE THIS (Professional UI)
├── ppt-connected.html         # Connected version
├── ppt.html                   # Standalone version
├── DOCUMENTATION.md           # Full documentation
├── QUICKSTART.md              # This file
└── backend/
    ├── server.js              # Main server
    ├── package.json           # Dependencies
    ├── .env                   # Configuration
    ├── models/                # Data schemas
    ├── routes/                # API endpoints
    ├── middleware/            # Auth & validation
    └── utils/                 # Helper functions
```

---

## 🚢 Deploy to Production

### Heroku (Easiest)
```bash
heroku create myapp
heroku config:set MONGODB_URI=your_mongodb_atlas_url
heroku config:set JWT_SECRET=your_secret_key
git push heroku main
```

### DigitalOcean / AWS / Linode
1. Create Node.js app
2. Set environment variables
3. Deploy backend code
4. Host frontend HTML on CDN (Netlify, Vercel)

---

## 💡 Pro Tips

1. **NLP Magic**: Type natural language dates
   - "Do it friday" → Auto-sets Friday's date
   - "urgent" → Sets to High priority
   - "#tag" → Auto-adds tag

2. **Time Tracking**: Perfect for project billing
   - Start timer when task begins
   - Stop when done
   - Export to CSV for invoicing

3. **Sub-tasks**: Break complex tasks
   - Click "Add Sub" button
   - Create 2-5 sub-tasks
   - Track sub-task progress

4. **Kanban Workflow**: Drag tiles between columns
   - To Do → In Progress (when you start)
   - In Progress → Review (when done)
   - Review → Done (after verification)

5. **Activity Audit**: Great for team accountability
   - See who changed what and when
   - Export activity log for reports

---

## 🔐 Security Reminders

⚠️ **Before Going Live**
- [ ] Change JWT_SECRET to a strong random string
- [ ] Use HTTPS in production
- [ ] Set NODE_ENV=production
- [ ] Enable MongoDB authentication
- [ ] Add firewall rules
- [ ] Use environment variables (never hardcode secrets)
- [ ] Enable CORS whitelist for specific domains

---

## 📞 Support

### Check This First
1. Backend running? http://localhost:5000/api/health
2. MongoDB running? Try `mongod` in new terminal
3. Frontend errors? Check browser console (F12)
4. API errors? Check server logs

### Debug Commands
```bash
# Check if port 5000 is in use
lsof -i :5000  # Mac/Linux
netstat -ano | findstr :5000  # Windows

# Test API
curl http://localhost:5000/api/health

# View server logs
npm run dev  # (shows all logs in console)
```

---

## 🎓 Learning Resources

- **Backend**: `backend/README.md` - API documentation
- **Full Docs**: `DOCUMENTATION.md` - Complete reference
- **Code**: Well-commented JavaScript throughout

---

## ✨ What's Included

✅ **Backend** (Production-ready)
- Express.js REST API with 10+ endpoints
- MongoDB database with 3 schemas
- JWT authentication & authorization
- Rate limiting & security headers
- Socket.io for real-time updates
- Natural Language Processing (dates/times)
- Activity audit logging
- CSV/PDF export

✅ **Frontend** (Professional UI)
- Dual view (List & Kanban)
- Glassmorphic design with animations
- Responsive for mobile to ultra-wide
- Time tracking with telemetry
- Sub-tasks with expand/collapse
- Activity audit log panel
- Search & advanced filtering
- Tag & category management

✅ **Deployment Ready**
- Security best practices
- Performance optimizations
- Error handling & logging
- Database indexing
- Rate limiting
- CORS configuration

---

## 🎉 You're Ready!

1. Backend running at `http://localhost:5000`
2. Open `ppt-pro.html` in browser
3. Create account → Add task → Enjoy!

For full documentation, see `DOCUMENTATION.md`

---

**Version**: 1.0.0  
**Last Updated**: February 2026  
**Status**: ✅ Production Ready
