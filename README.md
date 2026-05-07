# ⚡ TaskFlow — Team Task Manager

A full-stack web application for managing team projects and tasks with role-based access control (Admin/Member).

---

## 🔗 Live Demo

**🌐 Live URL:** [https://your-app.vercel.app](https://your-app.vercel.app)

### Demo Credentials

| Role | Email | Password |
|------|-------|----------|
| Admin | admin@demo.com | demo1234 |
| Member | member@demo.com | demo1234 |

---

## ✨ Features

### Authentication
- Secure signup and login with JWT tokens
- Password hashing with bcrypt
- Protected routes (redirect to login if not authenticated)
- Persistent sessions via localStorage

### Role-Based Access Control
- **Admin:** Create projects, create/assign tasks, manage team members, delete items
- **Member:** View assigned projects, update task status on assigned tasks

### Project Management
- Create and manage multiple projects
- Add/remove team members per project
- View task count and progress per project

### Task Management
- Create tasks with title, description, priority (low/medium/high)
- Assign tasks to project members
- Set due dates with overdue detection
- Track status: Todo → In Progress → Done
- Filter tasks by status, assigned to me, or overdue

### Dashboard
- Overview stats: Total, Todo, In Progress, Done, Overdue
- Recent tasks table
- Per-project progress bars

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|-----------|
| Frontend | React 18, React Router v6, Axios |
| Backend | Node.js, Express.js |
| Database | PostgreSQL |
| Auth | JWT (jsonwebtoken), bcrypt |
| Deployment | Railway (backend + DB) + Vercel (frontend) |

---

## 📁 Project Structure

```
team-task-manager/
├── server/                     # Node.js + Express backend
│   ├── index.js               # Entry point
│   ├── config/
│   │   ├── db.js              # PostgreSQL connection
│   │   └── schema.sql         # Database schema
│   ├── middleware/
│   │   └── auth.js            # JWT verification, role check
│   └── routes/
│       ├── auth.js            # Login, register, /me
│       ├── projects.js        # Project CRUD + members
│       ├── tasks.js           # Task CRUD + status
│       ├── dashboard.js       # Stats and summary
│       └── users.js           # List all users (admin)
│
└── client/                    # React frontend
    └── src/
        ├── App.js             # Routes
        ├── context/
        │   └── AuthContext.js # Global auth state
        ├── utils/
        │   └── api.js         # Axios instance
        ├── components/
        │   └── Layout.js      # Sidebar + navigation
        └── pages/
            ├── Login.js
            ├── Register.js
            ├── Dashboard.js
            ├── Projects.js
            ├── ProjectDetail.js
            ├── Tasks.js
            └── Team.js
```

---

## 🚀 Local Setup

### Prerequisites
- Node.js v18+
- PostgreSQL (local or Railway)
- Git

### 1. Clone the repository
```bash
git clone https://github.com/YOUR_USERNAME/team-task-manager.git
cd team-task-manager
```

### 2. Setup Backend
```bash
cd server
npm install
cp .env.example .env
# Edit .env with your DATABASE_URL and JWT_SECRET
npm start
```

### 3. Setup Database
Run the SQL from `server/config/schema.sql` in your PostgreSQL database.

### 4. Setup Frontend
```bash
cd client
npm install
# Create .env file:
echo "REACT_APP_API_URL=http://localhost:5000/api" > .env
npm start
```

The app will open at **http://localhost:3000**

---

## ☁️ Deployment

### Backend → Railway
1. Go to [railway.app](https://railway.app) → New Project → Deploy from GitHub
2. Select the `server/` folder (or set root directory to `server`)
3. Add PostgreSQL plugin → copy `DATABASE_URL`
4. Set environment variables: `JWT_SECRET`, `DATABASE_URL`, `NODE_ENV=production`
5. Run schema.sql in the Railway database console

### Frontend → Vercel
1. Go to [vercel.com](https://vercel.com) → New Project → Import from GitHub
2. Set root directory to `client`
3. Add environment variable: `REACT_APP_API_URL=https://your-railway-app.railway.app/api`
4. Deploy!

---

## 📡 API Endpoints

### Auth
| Method | Endpoint | Access | Description |
|--------|----------|--------|-------------|
| POST | /api/auth/register | Public | Create account |
| POST | /api/auth/login | Public | Login, get JWT |
| GET | /api/auth/me | Auth | Get current user |

### Projects
| Method | Endpoint | Access | Description |
|--------|----------|--------|-------------|
| GET | /api/projects | Auth | List projects |
| POST | /api/projects | Admin | Create project |
| PUT | /api/projects/:id | Admin | Update project |
| DELETE | /api/projects/:id | Admin | Delete project |
| GET | /api/projects/:id/members | Auth | List members |
| POST | /api/projects/:id/members | Admin | Add member |
| DELETE | /api/projects/:id/members/:uid | Admin | Remove member |

### Tasks
| Method | Endpoint | Access | Description |
|--------|----------|--------|-------------|
| GET | /api/tasks | Auth | List tasks |
| POST | /api/tasks | Admin | Create task |
| PUT | /api/tasks/:id | Auth | Update task/status |
| DELETE | /api/tasks/:id | Admin | Delete task |

### Dashboard
| Method | Endpoint | Access | Description |
|--------|----------|--------|-------------|
| GET | /api/dashboard | Auth | Stats + recent tasks |

---

## 🎥 Demo Video

[Watch the 3-minute demo on Loom](https://loom.com/your-link)

---

## 👨‍💻 Author

Built for the **Ethara.ai Full-Stack Assessment**

- GitHub: [@YOUR_USERNAME](https://github.com/YOUR_USERNAME)

---

## 📄 License

MIT
