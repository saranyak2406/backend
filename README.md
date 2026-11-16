# SkillBridge Backend REST API

High-performance, production-ready Node.js & Express REST API for **SkillBridge – Online Learning & Skill Development Platform**, backed by PostgreSQL.

---

## 🚀 Features

- **Authentication & RBAC**: JWT-based authentication with bcrypt password hashing and strict Role-Based Access Control (Admin, Instructor, Student).
- **PostgreSQL Database**: 20 normalized tables with foreign keys, cascaded deletes, and integrity constraints.
- **Course & Curriculum Management**: Full CRUD for courses, sections, and lessons with video streaming support.
- **Examinations & Quizzes**: Automated server-side quiz grading, passing score thresholds, and attempt tracking.
- **Assignments & Submissions**: File uploads via Multer, instructor grading, and feedback system.
- **Certificate Engine**: Real-time PDF certificate streaming using PDFKit with unique certificate IDs and public verification.
- **Analytics & Dashboards**: Role-specific aggregations for Admin, Instructor, and Student metrics.
- **Security & Performance**: Helmet security headers, Express rate limiting, CORS configuration, and Morgan logging.

---

## 🛠 Tech Stack

- **Runtime**: Node.js (v18+)
- **Framework**: Express.js
- **Database**: PostgreSQL (pg / node-postgres)
- **Authentication**: JSON Web Tokens (`jsonwebtoken`), `bcryptjs`
- **File Uploads**: `multer`
- **PDF Generation**: `pdfkit`
- **Security**: `helmet`, `express-rate-limit`, `cors`

---

## 📦 Getting Started

### 1. Prerequisites
- Node.js (v18 or higher)
- PostgreSQL (v14 or higher)

### 2. Installation
```bash
# Clone the repository
git clone https://github.com/saranyak2406/backend.git
cd backend

# Install dependencies
npm install
```

### 3. Environment Variables
Create a `.env` file in the root directory:
```env
PORT=5000
NODE_ENV=development

# Database Connection (Connection URI format)
DATABASE_URL=postgresql://postgres:postgres@localhost:5432/skillbridge_db

# Or individual DB variables:
DB_HOST=localhost
DB_PORT=5432
DB_NAME=skillbridge_db
DB_USER=postgres
DB_PASSWORD=your_postgres_password

# Authentication
JWT_SECRET=super_secret_jwt_key_skillbridge_production_2026
JWT_EXPIRES_IN=7d

# CORS Allowed Origin
CLIENT_URL=http://localhost:5173
```

### 4. Database Setup & Seeding
```bash
# Initialize database tables
npm run db:init

# Seed initial courses, users, and quizzes
npm run db:seed
```

### 5. Running the Server
```bash
# Development mode (with nodemon)
npm run dev

# Production mode
npm start
```

---

## 📡 Core API Endpoints

| Category | Endpoint | Method | Role | Description |
| :--- | :--- | :--- | :--- | :--- |
| **Auth** | `/api/auth/register` | POST | Public | Register student or instructor |
| **Auth** | `/api/auth/login` | POST | Public | Authenticate user & issue JWT |
| **Auth** | `/api/auth/me` | GET | Authenticated | Get current authenticated profile |
| **Users** | `/api/users` | GET | Admin | List all registered users |
| **Courses** | `/api/courses` | GET | Public | Search, filter & paginate courses |
| **Courses** | `/api/courses` | POST | Instructor / Admin | Create new course |
| **Sections** | `/api/courses/:id/sections`| POST | Instructor / Admin | Add section to course |
| **Lessons** | `/api/sections/:id/lessons`| POST | Instructor / Admin | Add lesson with video URL |
| **Enroll** | `/api/enrollments` | POST | Student | Enroll in a course |
| **Progress** | `/api/progress/lessons/:id/complete` | POST | Student | Mark lesson complete |
| **Quizzes** | `/api/quizzes/:id/submit`| POST | Student | Submit quiz for auto-grading |
| **Certificates** | `/api/certificates/:id/download` | GET | Public | Stream PDF certificate |
| **Dashboard** | `/api/dashboard/stats` | GET | Authenticated | Role-tailored analytics |

---

## ☁️ Deploying on Render

1. Create a new **Web Service** on [Render](https://dashboard.render.com).
2. Connect this repository: `https://github.com/saranyak2406/backend.git`.
3. Configure the service settings:
   - **Environment**: `Node`
   - **Build Command**: `npm install`
   - **Start Command**: `npm start`
4. Set Environment Variables:
   - `NODE_ENV`: `production`
   - `PORT`: `5000`
   - `DATABASE_URL`: Your PostgreSQL external connection string (from Render Postgres, Neon, or Supabase)
   - `JWT_SECRET`: *Any strong 32+ character random string*
   - `JWT_EXPIRES_IN`: `7d`
   - `CLIENT_URL`: Your frontend URL (e.g. `https://your-frontend.onrender.com`)

---

## 📄 License
MIT
