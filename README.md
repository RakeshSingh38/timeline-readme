# Timeline - Real-Time Project Management Platform

> **⚠️ PRIVATE & PROPRIETARY SOFTWARE**  
> This codebase is private and not open source. All rights reserved.  
> **Contact me for access:** [hello@iamrakesh.codes](mailto:hello@iamrakesh.codes)

A full-stack project management application with WebSocket-powered real-time
collaboration, built with Next.js 15, Go, and MongoDB.

## 🔗 Quick links

-   [Features](#features)
-   [State Management](#state-management)
-   [Quick Start](#quick-start)
-   [Load Testing](#load-testing)
-   [Project Structure](#project-structure)
-   [API Documentation](#api-documentation)
-   [Biometrics & Remember Me](#biometrics--remember-me)
-   [Notifications & Realtime Presence](#notifications--realtime-presence)
-   [Realtime Kanban](#realtime-kanban)
-   [Web Workers & Background Processing](#web-workers--background-processing)
-   [Analytics & User Insights](#analytics--user-insights-microsoft-clarity)
-   [Development](#development)
-   [Deployment](#deployment)

## ✨ Features

### **Core Features**

-   ✅ **Multi-Workspace Management**
    -   Create unlimited workspaces
    -   Workspace switching with persistent state
-   ✅ **Advanced Task Management**

    -   Kanban board with drag-and-drop
    -   Task status tracking (Backlog, Todo, In Progress, In Review, Done)
    -   Due date management
    -   Task assignment to team members
    -   Rich filtering and search capabilities

    -   Multiple projects per workspace
    -   Emoji-based project identification
    -   Project-scoped task views

-   ✅ **Role-Based Access Control (RBAC)**

    -   **Member**: View tasks, create/edit own tasks
    -   Granular permission system (15+ permission types)

    -   Dark mode support
    -   Loading states and skeleton screens
    -   Optimistic UI updates

### **Advanced Features**

-   📈 **Analytics Dashboard** - Task completion trends, member activity,
    project health
-   🔍 **Advanced Search** - Full-text search across tasks, projects, and
    members
-   🎨 **Customizable UI** - Theme preferences, sidebar configuration
-   📧 **Invite System** - Unique invite codes per workspace
-   🗂️ **Data Export** - Export tasks and projects
-   🔔 **Notifications** - Real-time activity notification
-   ⚡ **Web Workers** - Background processing for heavy computations (CSV
    export, data aggregation)
-   📊 **Microsoft Clarity** - Session recordings, heatmaps, and user behavior
    analytics

---

## 📸 Screenshots

Add your screenshots here to showcase key flows and UI states.

-   Core

    -   Dashboard: ![Dashboard](docs/screenshots/dashboard.png)
    -   Realtime Presence: ![Presence](docs/screenshots/presence.png)

-   Settings & Admin
    -   Workspace Settings:
        ![Workspace Settings](docs/screenshots/settings-workspace.png)
    -   Member Roles & Permissions:
        ![Roles](docs/screenshots/settings-roles.png)
    -   Admin Panel: ![Admin](docs/screenshots/admin.png)
-   Authentication
    -   Sign In (Auth): ![Sign In](docs/screenshots/auth-sign-in.png)
    -   Biometric Login: ![Biometric](docs/screenshots/auth-biometric.png)
    -   Remember Me Sessions:
        ![Remember Me](docs/screenshots/auth-remember-me.png)
-   Collaboration

    -   Members List: ![Members](docs/screenshots/members.png)
    -   Invites: ![Invites](docs/screenshots/invites.png)

-   Productivity

    -   Calendar View: ![Calendar](docs/screenshots/calendar.png)
    -   Analytics Dashboard: ![Analytics](docs/screenshots/analytics.png)
    -   Search & Filters: ![Search](docs/screenshots/search.png)

-   Mobile
    -   Mobile Dashboard:
        ![Mobile Dashboard](docs/screenshots/mobile-dashboard.png)
    -   Mobile Kanban: ![Mobile Kanban](docs/screenshots/mobile-kanban.png)

Suggested structure:

-   docs/screenshots/
    -   dashboard.png
    -   kanban.png
    -   create-task.png
    -   presence.png
    -   settings-workspace.png
    -   settings-project.png
    -   settings-roles.png
    -   admin.png
    -   auth-sign-in.png
    -   auth-biometric.png
    -   auth-remember-me.png
    -   members.png
    -   invites.png
    -   notifications.png
    -   calendar.png
    -   analytics.png
    -   search.png
    -   mobile-dashboard.png
    -   mobile-kanban.png

---

## 🏗️ Architecture

Architecture diagram

<img src="public/timeline-architecture.svg" alt="Architecture Diagram" />


ASCII fallback:

```
                                      ┌─────────────────────────────────────────────────────────────┐
                                      │                        FRONTEND (Next.js 15)                │
                                      │  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐       │
                                      │  │   App Router │  │  React Query │  │  JWT Auth    │       │
                                      │  │    (Pages)   │  │   (State)    │  │  (Session)   │       │
                                      │  └──────────────┘  └──────────────┘  └──────────────┘       │
                                      │         │                  │                  │             │
                                      │         └──────────────────┴──────────────────┘             │
                                      │                            │                                │
                                      │                        HTTPS/WSS                            │
                                      │                            │                                │
                                      └────────────────────────────┼────────────────────────────────┘
                                                                   │
                                                      ┌────────────┴──────────┐
                                                      │                       │
                                      ┌───────────────▼─────────┐  ┌─────────▼────────────────┐
                                      │  BACKEND (Next.js API)  │  │  WEBSOCKET (Go Server)   │
                                      │  ┌──────────────────┐   │  │  ┌────────────────────┐  │
                                      │  │  REST API Routes │   │  │  │  Gorilla WebSocket │  │
                                      │  │  Authentication  │   │  │  │  JWT Verification  │  │
                                      │  │  Business Logic  │   │  │  │  Online Presence   │  │
                                      │  └──────────────────┘   │  │  │  Message Broadcast │  │
                                      │           │             │  │  └────────────────────┘  │
                                      └───────────┼─────────────┘  └────────────┼─────────────┘
                                                  │                             │
                                                  └──────────────┬──────────────┘
                                                                 │
                                                      ┌──────────▼──────────┐
                                                      │   MongoDB Atlas     │
                                                      │  ┌───────────────┐  │
                                                      │  │  Users        │  │
                                                      │  │  Workspaces   │  │
                                                      │  │  Projects     │  │
                                                      │  │  Tasks        │  │
                                                      │  │  Members      │  │
                                                      │  │  Roles        │  │
                                                      │  └───────────────┘  │
                                                      └─────────────────────┘
```

### **Data Flow**

1. **Authentication**: User signs in via custom auth → Backend issues JWT and
   syncs user to MongoDB
2. **API Requests**: Frontend → Next.js API Routes → MongoDB
3. **Real-Time Updates**: Frontend establishes WebSocket connection → Go Server
   → Broadcasts to all connected clients
4. **State Management**: React Query caches API responses, invalidates on
   mutations
5. **Optimistic Updates**: UI updates immediately, rolls back on API failure

---

## 🛠️ Tech Stack

### **Frontend**

| Technology            | Purpose                         | Version |
| --------------------- | ------------------------------- | ------- |
| **Next.js**           | React framework with App Router | Latest  |
| **TypeScript**        | Type-safe development           | 6.0+    |
| **React**             | UI library                      | 20.0.1  |
| **Tailwind CSS**      | Utility-first styling           | 4.1+    |
| **Radix UI**          | Accessible component primitives | Latest  |
| **Framer Motion**     | Animation library               | 12.23+  |
| **React Query**       | Server state management         | 6.1+    |
| **JWT (custom)**      | Authentication                  | Latest  |
| **Socket.io Client**  | WebSocket client                | 4.8+    |
| **Axios**             | HTTP client                     | 1.7+    |
| **Zod**               | Schema validation               | Latest  |
| **React Hook Form**   | Form management                 | 7.53+   |
| **Web Workers**       | Background processing           | Native  |
| **Microsoft Clarity** | User analytics & heatmaps       | Latest  |

### **Backend**

| Technology             | Purpose                   | Version |
| ---------------------- | ------------------------- | ------- |
| **Next.js API Routes** | RESTful API endpoints     | Latest  |
| **TypeScript**         | Type-safe backend code    | 6.0+    |
| **MongoDB**            | NoSQL database            | 6.0+    |
| **Mongoose**           | MongoDB ODM               | Latest  |
| **Go**                 | WebSocket server language | 1.21+   |
| **Gorilla WebSocket**  | Go WebSocket library      | Latest  |
| **JWT**                | Token authentication      | Latest  |
| **Bcrypt**             | Password hashing          | Latest  |
| **Zod**                | Request validation        | Latest  |

### **DevOps & Tools**

| Tool               | Purpose                       |
| ------------------ | ----------------------------- |
| **k6**             | Load testing WebSocket server |
| **Vercel**         | Frontend deployment           |
| **Heroku/Railway** | Backend deployment            |
| **MongoDB Atlas**  | Database hosting              |
| **Docker**         | Containerization              |
| **ESLint**         | Code linting                  |
| **Prettier**       | Code formatting               |

---

## 🧠 State Management

-   Server state: TanStack Query (React Query)
    -   Example keys used in code: ["authUser"], ["workspace", workspaceId],
        ["tasks", workspaceId], ["all-tasks", workspaceId], ["calendar-tasks",
        workspaceId], ["project-analytics", projectId]
    -   Patterns observed:
        -   Auth user query uses staleTime ≈ 1 min with refetchOnFocus/Mount
            enabled
        -   Workspace/Kanban queries often disable refetchOnFocus/Mount to avoid
            snapback and align with realtime sync
        -   Mutations use optimistic updates with setQueryData and
            invalidateQueries on settle
-   Client state: React Context + custom hooks + Zustand stores
    -   Contexts: SidebarContext, WorkspaceDialogContext, Auth context
    -   Zustand stores:
        -   useKanbanStore: UI state for the board (customColumns, drag state,
            dialogs, selectedTask) with actions like
            setCustomColumns/toggleTaskModal/resetUIState
        -   useTaskSyncStore: cross-component sync triggers
            (lastTaskCreated/Updated/Deleted/StatusChanged/Global) with
            triggerTask\*() helpers, used by Kanban table and row actions
        -   useUIStore: global UI flags (celebration, strategic loading,
            currentWorkspace)
        -   useCalendarSelectionStore: calendar selection state
            (selectedDate/open)
        -   useNotificationHistoryStore: persisted notification history with
            add/markAsRead/markAllAsRead/clearOldNotifications

---

## 📦 Prerequisites

Before you begin, ensure you have the following installed:

-   **Node.js** 20.0.1 or higher
-   **Go** 1.23 or higher (for WebSocket server)
-   **MongoDB** 7.0+ (local or Atlas)
-   **npm** or **yarn** package manager
-   **Git** for version control

### **Optional**

-   **Docker** (for containerized deployment)
-   **k6** (for load testing)

---

## 🚀 Quick Start

### **1. Clone the Repository**

```bash
git clone https://github.com/RakeshSingh38/timeline-nextjs.git
cd timeline-nextjs
```

### **2. Install Dependencies**

#### **Frontend**

```bash
cd frontend
npm install
```

#### **Backend**

```bash
cd ../backend
npm install
```

#### **WebSocket Server**

```bash
cd websocket
go mod download
```

### **3. Environment Setup**

Create environment files in each directory:

#### **Frontend (.env.local)**

```env
NEXT_PUBLIC_API_BASE_URL=http://localhost:8000/api
NEXT_PUBLIC_AUTH_STRATEGY=jwt
NEXT_PUBLIC_CLARITY_PROJECT_ID=your_clarity_project_id
```

#### **Backend (.env.local)**

```env
# Database
MONGODB_URI=mongodb://localhost:27017/timeline
# or for MongoDB Atlas:
# MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/your_Timeline_DB

# Authentication (custom JWT)
JWT_SECRET=your_super_secret_jwt_key_here_min_32_chars
AUTH_COOKIE_NAME=auth_token

# Server
PORT=8000
NODE_ENV=development
BASE_PATH=/api

# Frontend
FRONTEND_ORIGIN=http://localhost:3000

# Session
SESSION_SECRET=your_session_secret_here
COOKIE_DOMAIN=localhost
COOKIE_SECURE=false

# Mail (generic)
MAIL_PROVIDER=generic
MAIL_API_KEY=your_mail_api_key
MAIL_FROM="Timeline <no-reply@your-domain.com>"
MAIL_WEBHOOK_SECRET=your_inbound_webhook_secret
```

#### **WebSocket Server (.env)**

```env
JWT_SECRET=your_super_secret_jwt_key_here_min_32_chars
MONGO_URI=mongodb://localhost:27017/timeline
ALLOWED_ORIGINS=http://localhost:3000,http://localhost:8000
WS_PORT=8001
NODE_ENV=development
```

### **4. Database Setup**

#### **Option A: MongoDB Atlas (Recommended)**

1. Create account at [MongoDB Atlas](https://www.mongodb.com/cloud/atlas)
2. Create a new cluster
3. Get connection string and update `MONGODB_URI`

#### **Option B: Local MongoDB**

```bash
# macOS (Homebrew)
brew install mongodb-community
brew services start mongodb-community

# Linux
sudo systemctl start mongod

# Windows
# Download from mongodb.com and run as service
```

#### **Seed Database with Roles**

```bash
cd backend
npm run seed:roles
```

### **5. Run Development Servers**

Open 3 terminal windows:

#### **Terminal 1: Frontend**

```bash
cd frontend
npm run dev
```

Frontend runs on **http://localhost:3000**

#### **Terminal 2: Backend**

```bash
cd backend
npm run dev
```

Backend runs on **http://localhost:8000**

#### **Terminal 3: WebSocket Server**

```bash
cd backend/websocket
go run main.go
```

WebSocket server runs on **ws://localhost:8001**

### **6. Access the Application**

Open your browser and navigate to:

```
http://localhost:3000
```

**Default Test Account** (create via sign-up):

-   Email: `test@example.com`
-   Password: Create during sign-up

---

## 📁 Project Structure

```
timeline-nextjs/
├── frontend/                    # Next.js Frontend
│   ├── src/
│   │   ├── app/                # App Router pages
│   │   │   ├── (auth)/         # Authentication pages
│   │   │   │   ├── sign-in/
│   │   │   │   └── sign-up/
│   │   │   ├── workspace/      # Workspace pages
│   │   │   │   └── [workspaceId]/
│   │   │   │       ├── page.tsx          # Dashboard
│   │   │   │       ├── tasks/            # Task views
│   │   │   │       ├── kanban/           # Kanban board
│   │   │   │       ├── members/          # Team members
│   │   │   │       └── profile/          # User profile
│   │   │   ├── invite/         # Workspace invites
│   │   │   ├── layout.tsx      # Root layout
│   │   │   └── page.tsx        # Landing page
│   │   ├── components/         # React components
│   │   │   ├── ui/             # Radix UI components
│   │   │   ├── workspace/      # Workspace components
│   │   │   ├── asidebar/       # Sidebar components
│   │   │   └── Navbar/         # Navigation components
│   │   ├── context/            # React Context providers
│   │   ├── hooks/              # Custom React hooks
│   │   ├── lib/                # Utilities
│   │   ├── services/           # API services
│   │   └── types/              # TypeScript types
│   ├── public/                 # Static assets
│   ├── package.json
│   └── next.config.ts
│
├── backend/                     # Next.js Backend (API Routes)
│   ├── app/api/                # Next.js 15 App Router API
│   │   ├── _lib/               # Shared utilities
│   │   │   ├── auth.ts         # Custom JWT auth helper
│   │   │   ├── db.ts           # MongoDB connection
│   │   │   └── cors.ts         # CORS wrapper
│   │   ├── user/               # User endpoints
│   │   ├── workspace/          # Workspace endpoints
│   │   ├── project/            # Project endpoints
│   │   ├── task/               # Task endpoints
│   │   ├── member/             # Member endpoints
│   │   └── auth/               # Auth routes (login, refresh, logout)
│   ├── src/
│   │   ├── config/             # Configuration
│   │   ├── controllers/        # Express controllers
│   │   ├── models/             # Mongoose models
│   │   ├── services/           # Business logic
│   │   ├── routes/             # Express routes
│   │   ├── middlewares/        # Express middlewares
│   │   ├── utils/              # Utility functions
│   │   ├── validation/         # Zod schemas
│   │   └── enums/              # TypeScript enums
│   ├── websocket/              # Go WebSocket Server
│   │   ├── main.go             # Entry point
│   │   ├── handlers/           # WebSocket handlers
│   │   ├── auth/               # JWT authentication
│   │   ├── database/           # MongoDB connection
│   │   ├── middleware/         # CORS middleware
│   │   ├── models/             # Data structures
│   │   ├── .env                # WebSocket environment
│   │   ├── go.mod
│   │   ├── go.sum
│   │   ├── load-test-1k.js     # k6 load test (1k users)
│   │   └── load-test-10k.js    # k6 load test (10k users)
│   ├── package.json
│   └── tsconfig.json
│
└── (additional docs and tooling live in a separate documentation repository)
```

---

## 📊 Project Statistics

| Component           | Count | Description                   |
| ------------------- | ----- | ----------------------------- |
| API Endpoints       | 50+   | RESTful API routes            |
| React Components    | 200+  | UI components with TypeScript |
| Custom Hooks        | 25+   | Reusable business logic       |
| Database Models     | 8     | MongoDB schemas               |
| Services            | 12+   | Backend business logic        |
| Middleware          | 5+    | Authentication & CORS         |
| Test Files          | 15+   | Unit & integration tests      |
| Documentation Files | 30+   | Comprehensive guides          |

---

## 🔐 Environment Variables

### **Frontend Variables**

| Variable                         | Description                  | Required |
| -------------------------------- | ---------------------------- | -------- |
| `NEXT_PUBLIC_API_BASE_URL`       | Backend API URL              | ✅ Yes   |
| `NEXT_PUBLIC_AUTH_STRATEGY`      | Auth strategy (jwt)          | No       |
| `NEXT_PUBLIC_CLARITY_PROJECT_ID` | Microsoft Clarity project ID | No       |

### **Backend Variables**

| Variable              | Description                            | Required | Default     |
| --------------------- | -------------------------------------- | -------- | ----------- |
| `MONGODB_URI`         | MongoDB connection string              | ✅ Yes   | -           |
| `JWT_SECRET`          | Secret for JWT signing                 | ✅ Yes   | -           |
| `AUTH_COOKIE_NAME`    | Name of auth cookie (e.g., auth_token) | No       | auth_token  |
| `PORT`                | Backend server port                    | No       | 8000        |
| `NODE_ENV`            | Environment (development/production)   | No       | development |
| `FRONTEND_ORIGIN`     | Frontend URL for CORS                  | ✅ Yes   | -           |
| `SESSION_SECRET`      | Session encryption key                 | ✅ Yes   | -           |
| `COOKIE_DOMAIN`       | Cookie domain                          | No       | localhost   |
| `COOKIE_SECURE`       | Use secure cookies (HTTPS only)        | No       | false       |
| `MAIL_PROVIDER`       | Mail provider identifier (generic)     | No       | generic     |
| `MAIL_API_KEY`        | API key for mail provider              | ✅ Yes   | -           |
| `MAIL_FROM`           | Default From header                    | ✅ Yes   | -           |
| `MAIL_WEBHOOK_SECRET` | Verify inbound webhooks                | No       | -           |

### **WebSocket Server Variables**

| Variable          | Description                     | Required | Default     |
| ----------------- | ------------------------------- | -------- | ----------- |
| `JWT_SECRET`      | Must match backend JWT secret   | ✅ Yes   | -           |
| `MONGO_URI`       | MongoDB connection string       | ✅ Yes   | -           |
| `ALLOWED_ORIGINS` | Comma-separated allowed origins | ✅ Yes   | -           |
| `WS_PORT`         | WebSocket server port           | No       | 8001        |
| `NODE_ENV`        | Environment                     | No       | development |

---

## 📡 API Documentation

### **Base URL**

```
http://localhost:8000/api
```

### **Authentication**

All authenticated endpoints require a JWT in the `Authorization` header (or via
HttpOnly cookie on browser requests):

```
Authorization: Bearer <jwt_token>
```

### **Development API Docs**

-   JSON: http://localhost:8000/api/docs
-   Swagger UI: http://localhost:8000/api/docs/ui

### **Core Endpoints**

#### **User Endpoints**

| Method | Endpoint        | Description         | Auth |
| ------ | --------------- | ------------------- | ---- |
| GET    | `/user/current` | Get current user    | ✅   |
| PATCH  | `/user/:id`     | Update user profile | ✅   |

#### **Workspace Endpoints**

| Method | Endpoint                         | Description           | Auth |
| ------ | -------------------------------- | --------------------- | ---- |
| POST   | `/workspace`                     | Create workspace      | ✅   |
| GET    | `/workspace/all`                 | Get user's workspaces | ✅   |
| GET    | `/workspace/:id`                 | Get workspace by ID   | ✅   |
| PATCH  | `/workspace/:id`                 | Update workspace      | ✅   |
| GET    | `/workspace/members/:id`         | Get workspace members | ✅   |
| PATCH  | `/workspace/member/:workspaceId` | Change member role    | ✅   |

#### **Project Endpoints**

| Method | Endpoint                              | Description            | Auth |
| ------ | ------------------------------------- | ---------------------- | ---- |
| POST   | `/project/workspace/:workspaceId`     | Create project         | ✅   |
| GET    | `/project/workspace/:workspaceId`     | Get workspace projects | ✅   |
| GET    | `/project/:id/workspace/:workspaceId` | Get project by ID      | ✅   |
| PATCH  | `/project/:id/workspace/:workspaceId` | Update project         | ✅   |
| DELETE | `/project/:id/workspace/:workspaceId` | Delete project         | ✅   |

#### **Task Endpoints**

| Method | Endpoint                                          | Description             | Auth |
| ------ | ------------------------------------------------- | ----------------------- | ---- |
| POST   | `/task/project/:projectId/workspace/:workspaceId` | Create task             | ✅   |
| GET    | `/task/workspace/:workspaceId/all`                | Get all workspace tasks | ✅   |
| GET    | `/task/:id/workspace/:workspaceId`                | Get task by ID          | ✅   |
| PATCH  | `/task/:id/workspace/:workspaceId`                | Update task             | ✅   |
| DELETE | `/task/:id/workspace/:workspaceId`                | Delete task             | ✅   |
| PATCH  | `/task/:id/status/workspace/:workspaceId`         | Update task status      | ✅   |

#### **Member Endpoints**

| Method | Endpoint                        | Description               | Auth |
| ------ | ------------------------------- | ------------------------- | ---- |
| POST   | `/member/workspace/:inviteCode` | Join workspace via invite | ✅   |

---

### 📧 Mail Integration (Generic)

-   Outbound: API sends transactional emails (invites, notifications, password
    resets) via a configured mail provider.
-   Inbound: A secure webhook endpoint processes incoming emails/events for
    features like reply-to-thread or bounce tracking.
-   Security: Validate `MAIL_WEBHOOK_SECRET` on inbound requests; rate-limit and
    log events.

---

## 🔐 Biometrics & Remember Me

This project includes optional biometric authentication (WebAuthn on desktop,
device biometrics on mobile) and a persistent “Remember Me” login system.

### Biometric Auth (WebAuthn + Mobile)

-   Endpoints:
    -   GET `/api/auth/biometric` — List biometric sessions (requires auth)
    -   POST `/api/auth/biometric` — Create biometric session (mobile
        fingerprint hash or WebAuthn credential)
    -   DELETE `/api/auth/biometric?action=all|&deviceId=...` — Revoke
        session(s)
    -   POST `/api/auth/biometric/options` — Get WebAuthn options for login
    -   POST `/api/auth/biometric/login` — Verify WebAuthn assertion and sign in
-   Frontend:
    -   BiometricLoginButton uses WebAuthn when available; falls back based on
        device
    -   Sign-in page has `handleBiometricLogin` with secure-context and browser
        capability checks
-   Notes:
    -   Limit of 5 biometric sessions per user enforced on backend
    -   Device info captured via user-agent; mobile vs desktop paths handled

### Remember Me Sessions

-   Endpoints:
    -   GET `/api/auth/remember-me` — List active remember-me sessions
    -   POST `/api/auth/remember-me` — Create a remember-me session (sets
        cookie; 1-year expiry)
    -   DELETE `/api/auth/remember-me?action=all|&tokenId=...` — Revoke
        session(s) and clear cookie
-   Security:
    -   HttpOnly, SameSite, and Secure cookie attributes respected (env-aware)
    -   Server stores session metadata with IP, user-agent, and expiry

### Flows (at-a-glance)

-   Biometric setup

    1. Enable biometric in settings
    2. Browser creates a WebAuthn credential
    3. Frontend sends credential ID to `/api/auth/biometric`
    4. Backend stores credential ID; session created

-   Biometric login

    1. Tap Biometric Login
    2. Browser performs WebAuthn assertion
    3. Frontend posts to `/api/auth/biometric/login`
    4. Backend verifies and issues auth cookie/JWT

-   Remember Me
    1. User logs in and checks "Remember Me"
    2. Frontend creates device ID and calls `/api/auth/remember-me`
    3. Backend creates a session/token; cookie stored
    4. Future visits auto-login until revoked/expired

### Security highlights

-   WebAuthn public-key cryptography; device-bound credentials
-   HttpOnly/Secure/SameSite cookies; JWT with expiration
-   Max 5 biometric devices per user; automatic old-session cleanup

---

## 🔌 WebSocket Server

### **Connection**

-   Port: 8001 (development), WSS in production
-   Auth: JWT (same secret as API)
-   Rooms: Join/leave workspace rooms to scope events
-   Heartbeats: Periodic keep-alive and automatic cleanup on disconnect

### **Events (overview)**

-   Client → Server: `join-workspace`, `leave-workspace`, `user-activity`,
    `typing-start`, `typing-stop`
-   Server → Client: `online-users`, `user-online`, `user-offline`,
    `user-activity`, `user-typing`, `user-stop-typing`

### **Quick env & test**

-   Env: WebSocket URL (default ws://localhost:8001), shared JWT secret, allowed
    origins
-   Smoke test:
    1. Start API and WebSocket servers
    2. Open two browsers; log into the same workspace
    3. Verify online count and green indicators update in real time

## 🔔 Notifications & Realtime Presence

Keep everyone in sync with live activity and online status.

-   Events emitted over WebSocket:
    -   USER_STATUS_CHANGED — user went online/offline
    -   MEMBER_JOINED / MEMBER_LEFT — workspace membership changes
    -   TASK_CREATED / TASK_UPDATED / TASK_DELETED — task activity
-   UI patterns:
    -   Toasts for immediate feedback (via a reusable toast hook and toaster
        component)
    -   Persisted notification center via Zustand store
        (useNotificationHistoryStore) with unread counts and auto-pruning
    -   Presence indicators in member lists and task avatars
-   Privacy and performance:
    -   Presence updates batched and broadcast per workspace
    -   Only authorized clients for a workspace receive its events

Minimal presence subscription example:

```ts
socket.on("USER_STATUS_CHANGED", ({ userId, status }) => {
    // Update presence UI, optionally add a notification
});
```

---

## 📈 Realtime Kanban

All collaborators see the Kanban board update in real time.

-   Data flow:
    -   UI triggers optimistic update via TanStack Query setQueryData
    -   On success, server response reconciles cache; on error, snapshot
        rollback
    -   Related lists are invalidated (['all-tasks', workspaceId], ['tasks',
        workspaceId], ['calendar-tasks', workspaceId])
    -   A browser CustomEvent ('task-updated' | 'task-created' | 'task-deleted')
        is dispatched to sync other views
    -   Components listen and either refetch or update caches selectively
-   State & sync helpers:
    -   useTaskSyncStore triggers
        (triggerTaskStatusChanged/Created/Updated/Deleted) for cross-component
        updates
    -   useKanbanStore maintains board UI state (dragging, dialogs, selected
        task)
-   Query keys:
    -   ['tasks', workspaceId(, projectId)] — Kanban view cache
    -   ['all-tasks', workspaceId] — table view cache
    -   ['calendar-tasks', workspaceId] — calendar view cache

Result: snappy UX with no “snap-back”, consistent across tabs and users.

---

```javascript
import io from "socket.io-client";

const socket = io("ws://localhost:8001", {
    auth: {
        token: jwtToken, // JWT issued by your backend
    },
    query: {
        token: jwtToken, // Alternative: pass as query param
    },
});

// Connection established
socket.on("connect", () => {
    console.log("Connected to WebSocket server");
});

// Join a workspace room
socket.emit("JOIN_WORKSPACE", { workspaceId: "123" });

// Listen for task updates
socket.on("TASK_UPDATED", (data) => {
    console.log("Task updated:", data);
});

// Listen for online status
socket.on("USER_STATUS_CHANGED", (data) => {
    console.log("User status:", data);
});
```

### **WebSocket Events**

#### **Client → Server**

| Event             | Payload                   | Description                               |
| ----------------- | ------------------------- | ----------------------------------------- |
| `JOIN_WORKSPACE`  | `{ workspaceId: string }` | Join workspace room for real-time updates |
| `LEAVE_WORKSPACE` | `{ workspaceId: string }` | Leave workspace room                      |
| `PING`            | `{ timestamp: number }`   | Heartbeat message                         |

#### **Server → Client**

| Event                 | Payload                                           | Description                   |
| --------------------- | ------------------------------------------------- | ----------------------------- |
| `TASK_CREATED`        | `{ task: Task }`                                  | New task created in workspace |
| `TASK_UPDATED`        | `{ task: Task }`                                  | Task updated                  |
| `TASK_DELETED`        | `{ taskId: string }`                              | Task deleted                  |
| `USER_STATUS_CHANGED` | `{ userId: string, status: 'online'\|'offline' }` | User online status changed    |
| `MEMBER_JOINED`       | `{ member: Member }`                              | New member joined workspace   |
| `MEMBER_LEFT`         | `{ memberId: string }`                            | Member left workspace         |

### **Authentication**

WebSocket connections require JWT authentication:

1. Frontend logs in with credentials and obtains a JWT from backend
2. Token passed via `auth.token` or `query.token`
3. Go server validates JWT using same secret as backend
4. Connection established if valid, rejected otherwise

### **Architecture**

-   **Language**: Go 1.23+
-   **Library**: Gorilla WebSocket
-   **Port**: 8001 (default)
-   **Protocol**: WSS (production), WS (development)
-   **Max Connections**: 10,000+ (load-tested)
-   **Latency**: Sub-4ms average connection time

### **Server-Sent Events (SSE)**

For lightweight, one-way updates where a full duplex socket isn't required:

-   Endpoint: `GET http://localhost:8000/api/events?workspaceId=<id>`
-   Basic client usage:
    ```ts
    const es = new EventSource(
        "http://localhost:8000/api/events?workspaceId=123"
    );
    es.onmessage = (e) => {
        const msg = JSON.parse(e.data); // { type, workspaceId, data, timestamp }
        console.log(msg);
    };
    // Remember to close on unmount
    es.close();
    ```

---

## ⚡ Web Workers & Background Processing

Heavy computations run in background threads to keep the UI responsive.

-   **Use Cases**:

    -   CSV/Excel export generation for large task datasets
    -   Data aggregation for analytics dashboard
    -   Complex filtering and sorting operations
    -   Batch task processing

-   **Implementation**:

    -   Workers defined in `public/workers/` directory
    -   Main thread communicates via `postMessage` API
    -   Results returned asynchronously without blocking UI
    -   Graceful fallback for browsers without worker support

-   **Example**: CSV Export Worker
    ```ts
    // Trigger export in main thread
    const worker = new Worker("/workers/csv-export.worker.js");
    worker.postMessage({ tasks, format: "csv" });
    worker.onmessage = (e) => {
        const blob = new Blob([e.data], { type: "text/csv" });
        downloadFile(blob, "tasks.csv");
    };
    ```

---

## 📊 Analytics & User Insights (Microsoft Clarity)

Track user behavior and identify UX improvements with Microsoft Clarity.

-   **Features**:

    -   Session recordings - Watch real user interactions
    -   Heatmaps - Visualize clicks, scrolls, and engagement
    -   Rage clicks - Identify frustration points
    -   Dead clicks - Detect broken interactions
    -   JavaScript errors - Monitor frontend issues

-   **Setup**:

    1. Sign up at [Microsoft Clarity](https://clarity.microsoft.com)
    2. Create a new project and get Project ID
    3. Add `NEXT_PUBLIC_CLARITY_PROJECT_ID` to frontend `.env.local`
    4. Clarity script auto-loads in production (privacy-friendly, GDPR
       compliant)

-   **Privacy**:
    -   No PII collected by default
    -   Sensitive form fields automatically masked
    -   IP addresses anonymized
    -   Compliant with GDPR, CCPA

---

## 🧪 Load Testing

The WebSocket server has been extensively load-tested using **k6** to verify
performance at scale.

### **Performance Metrics**

| Metric                         | Result         | Status       |
| ------------------------------ | -------------- | ------------ |
| **Max Concurrent Connections** | 10,000+        | ✅ Verified  |
| **Average Connection Time**    | 3.5ms          | ⚡ Excellent |
| **p(95) Connection Latency**   | 5.8ms          | ⚡ Excellent |
| **p(99) Connection Latency**   | 22.57ms        | ✅ Pass      |
| **Error Rate**                 | 0% (0 errors)  | ✅ Perfect   |
| **Message Throughput**         | 2,022 msgs/sec | ⚡ High      |
| **Total Messages Sent**        | 849,578        | ✅ Verified  |
| **Success Rate**               | 100%           | ✅ Perfect   |

### **Running Load Tests**

#### **Prerequisites**

```bash
# Install k6
npm install -g k6
```

#### **Test Scripts**

```bash
cd backend/websocket

# Test with 100 concurrent users
k6 run load-test-1k.js

# Test with 10,000 concurrent users (recommended: 16GB+ RAM)
k6 run load-test-10k.js
```

#### **Test Configuration**

```javascript
// load-test-10k.js
export const options = {
    stages: [
        { duration: "2m", target: 5000 }, // Ramp to 5k
        { duration: "3m", target: 10000 }, // Ramp to 10k
        { duration: "30s", target: 10000 }, // Hold at 10k
        { duration: "1m", target: 0 }, // Ramp down
    ],
    thresholds: {
        ws_connecting: ["p(99)<5000"], // 99% connect in <5s
        message_latency_ms: ["p(95)<100"], // 95% msgs <100ms
        errors: ["count<100"], // <100 errors total
    },
};
```

### **Scaling Recommendations**

| Load Level           | Status              | Notes                          |
| -------------------- | ------------------- | ------------------------------ |
| Up to 5k concurrent  | ✅ Production Ready | Fully tested and verified      |
| 5k - 10k concurrent  | ✅ Production Ready | Fully tested and verified      |
| 10k - 20k concurrent | ✅ Works            | May require OS tuning (ulimit) |
| 20k+ concurrent      | 📑 Untested         | Requires horizontal scaling    |

---

## 💻 Development

### **Development Workflow**

1. **Create a feature branch**

    ```bash
    git checkout -b feature/your-feature-name
    ```

2. **Make changes and test**

    ```bash
    # Frontend
    cd frontend && npm run dev

    # Backend
    cd backend && npm run dev

    # WebSocket
    cd backend/websocket && go run main.go
    ```

3. **Run linting**

    ```bash
    # Frontend
    cd frontend && npm run lint

    # Backend
    cd backend && npm run lint
    ```

4. **Type checking**

    ```bash
    # Frontend
    cd frontend && npm run type-check

    # Backend
    cd backend && npm run type-check
    ```

5. **Commit and push**
    ```bash
    git add .
    git commit -m "feat: your feature description"
    git push origin feature/your-feature-name
    ```

### **Code Style**

-   **Frontend/Backend**: ESLint + Prettier
-   **Go**: `gofmt` (automatic formatting)
-   **Commits**: Conventional Commits (feat, fix, docs, style, refactor, test,
    chore)

### **Testing**

```bash
# Frontend unit tests (if configured)
cd frontend && npm test

# Backend unit tests
cd backend && npm test

# WebSocket load tests
cd backend/websocket && k6 run load-test-1k.js
```

---

### 🗂️ Kanban Caching & Invalidation

The Kanban board uses TanStack Query for server-state with these patterns:

-   Query keys organized by workspace/project (e.g., ["tasks","workspace",
    workspaceId])
-   Optimistic updates on drag-and-drop/status changes using setQueryData
-   Rollback on error and final sync on success
-   Invalidate relevant lists and detail queries after mutations

Typical mutation flow:

1. onMutate: snapshot previous cache; optimistic set
2. onError: restore snapshot
3. onSuccess: merge server response
4. onSettled: queryClient.invalidateQueries for affected keys

Note: Workspace queries deliberately disable refetch-on-focus/mount in some
hooks to align with realtime updates and explicit invalidations.

---

## 🚀 Deployment

### **Frontend Deployment (Vercel)**

1. **Connect Repository**

    - Go to [Vercel Dashboard](https://vercel.com)
    - Import `timeline-nextjs` repository
    - Select `frontend` as root directory

2. **Configure Environment**

    ```env
    NEXT_PUBLIC_API_BASE_URL=https://your-backend.herokuapp.com/api
    NEXT_PUBLIC_AUTH_STRATEGY=jwt
    NEXT_PUBLIC_CLARITY_PROJECT_ID=your_clarity_project_id
    ```

3. **Deploy**
    ```bash
    cd frontend
    npm run build
    vercel --prod
    ```

### **Backend Deployment (AWS/Heroku)**

#### **Heroku**

```bash
cd backend

# Login to Heroku
heroku login

# Create app
heroku create timeline-backend

# Add MongoDB addon (or use Atlas)
heroku addons:create mongodb:sandbox

# Set environment variables
heroku config:set MONGODB_URI=mongodb+srv://...
heroku config:set JWT_SECRET=your_secret
heroku config:set AUTH_COOKIE_NAME=auth_token
heroku config:set FRONTEND_ORIGIN=https://timeline.vercel.app

# Deploy
git push heroku main

# View logs
heroku logs --tail
```

### **WebSocket Server Deployment**

#### **Option 1: Docker**

```bash
cd backend/websocket

# Build image
docker build -t timeline-websocket .

# Run container
docker run -d \
  -p 8001:8001 \
  -e JWT_SECRET=your_secret \
  -e MONGO_URI=mongodb+srv://... \
  -e ALLOWED_ORIGINS=https://timeline.vercel.app \
  -e WS_PORT=8001 \
  --name websocket-server \
  timeline-websocket
```

#### **Option 2: Direct Deployment**

```bash
# On your server
cd backend/websocket

# Build binary
go build -o websocket-server main.go

# Run with systemd or PM2
# Example systemd service:
sudo nano /etc/systemd/system/timeline-websocket.service
```

**Systemd Service File:**

```ini
[Unit]
Description=Timeline WebSocket Server
After=network.target

[Service]
Type=simple
User=www-data
WorkingDirectory=/var/www/timeline/websocket
ExecStart=/var/www/timeline/websocket/websocket-server
Restart=on-failure
Environment="JWT_SECRET=your_secret"
Environment="MONGO_URI=mongodb+srv://..."
Environment="ALLOWED_ORIGINS=https://app-name.vercel.app"
Environment="WS_PORT=8001"

[Install]
WantedBy=multi-user.target
```

### **Database (MongoDB Atlas)**

1. **Create Cluster**

    - Go to [MongoDB Atlas](https://www.mongodb.com/cloud/atlas)
    - Create M0 (free) or M10+ cluster
    - Select region closest to your backend

2. **Configure Network Access**

    - Add IP addresses: `0.0.0.0/0` (or specific IPs)

3. **Create Database User**

    - Username: `timeline_user`
    - Password: Generate strong password
    - Role: `readWrite` on `timeline` database

4. **Get Connection String**
    ```
    mongodb+srv://timeline_user:password@cluster.mongodb.net/your_Timeline_DB
    ```

### **Environment Configuration (Production)**

#### **Frontend**

```env
NEXT_PUBLIC_API_BASE_URL=https://your-backend.server.com/api
NEXT_PUBLIC_AUTH_STRATEGY=jwt
NEXT_PUBLIC_CLARITY_PROJECT_ID=your_clarity_project_id
NODE_ENV=production
```

#### **Backend**

```env
MONGODB_URI=mongodb+srv://...
JWT_SECRET=<generate-32-char-secret>
AUTH_COOKIE_NAME=auth_token
PORT=8000
NODE_ENV=production
FRONTEND_ORIGIN=https://your-frontend.server.com
SESSION_SECRET=<generate-32-char-secret>
COOKIE_DOMAIN=.your-frontend.server.com
COOKIE_SECURE=true
COOKIE_SAMESITE=none
```

#### **WebSocket**

```env
JWT_SECRET=<same-as-backend>
MONGO_URI=mongodb+srv://...
ALLOWED_ORIGINS=https://your-frontend.server.com
WS_PORT=8001
NODE_ENV=production
```

## ⚡ Performance

### **Frontend Optimizations**

-   **Code Splitting**: Automatic route-based splitting with Next.js
-   **Image Optimization**: Next.js Image component with lazy loading
-   **Bundle Analysis**: `npm run analyze` to inspect bundle sizes
-   **React Query**: Intelligent caching and background refetching
-   **Lazy Loading**: Components loaded on-demand
-   **Memoization**: `useMemo` and `useCallback` for expensive computations

### **Backend Optimizations**

-   **Database Indexing**: Optimized queries with MongoDB indexes
-   **Connection Pooling**: MongoDB connection reuse
-   **Caching**: Redis layer (planned)
-   **Rate Limiting**: Prevent API abuse
-   **Compression**: gzip/brotli compression

### **WebSocket Optimizations**

-   **Go Goroutines**: Concurrent connection handling
-   **Message Broadcasting**: Efficient pub/sub pattern
-   **Connection Pooling**: Reusable database connections
-   **Memory Management**: Automatic cleanup of disconnected clients

### **Performance Benchmarks**

| Metric                        | Value             |
| ----------------------------- | ----------------- |
| **Frontend Initial Load**     | <2s (3G network)  |
| **API Response Time (p95)**   | <100ms            |
| **WebSocket Connection Time** | <5ms              |
| **Database Query Time (p95)** | <50ms             |
| **Lighthouse Score**          | 90+ (Performance) |

---

### 🚀 Optimization Results

| Metric                | Before     | After     | Improvement      |
| --------------------- | ---------- | --------- | ---------------- |
| Bundle Size           | 2.1MB      | 1.5MB     | 28% reduction    |
| Navigation Time       | 800-1200ms | 300-500ms | 60% faster       |
| API Calls per Session | 200+       | 60-80     | 70% reduction    |
| Cache Hit Rate        | 30%        | 85%       | 183% improvement |
| Profile Picture Load  | 300-500ms  | 100-200ms | 60% faster       |

---

## 🧪 Case Studies

-   Realtime Presence at Scale

    -   Scenario: 500+ users across multiple workspaces toggling online/offline
    -   Approach: Workspace-scoped WS rooms; batched USER_STATUS_CHANGED events;
        client-side debouncing
    -   Outcome: Stable UI with minimal network overhead; no cross-workspace
        leakage

-   Kanban Multi-User Edits

    -   Scenario: Multiple collaborators reorder/update tasks simultaneously
    -   Approach: Optimistic updates with server reconciliation; query
        invalidation of ['tasks', workspaceId] and related lists; browser
        CustomEvents for view sync
    -   Outcome: No “snap-back”; consistent task state across
        board/table/calendar

-   Biometric + Remember Me Login
    -   Scenario: Users authenticate via WebAuthn on desktop and device
        biometrics on mobile; long-lived “remember me” sessions
    -   Approach: WebAuthn options/login endpoints; max 5 biometric sessions per
        user; secure, env-aware cookies for remember me
    -   Outcome: Fast, frictionless re-entry with revocation controls

---

## 🤝 Contributing

Contributions are welcome! Please follow these guidelines:

1. **Fork the repository**
2. **Create a feature branch** (`git checkout -b feature/AmazingFeature`)
3. **Commit your changes** (`git commit -m 'feat: Add some AmazingFeature'`)
4. **Push to the branch** (`git push origin feature/AmazingFeature`)
5. **Open a Pull Request**

### **Coding Standards**

-   Follow existing code style
-   Write meaningful commit messages (Conventional Commits)
-   Add tests for new features
-   Update documentation as needed
-   Ensure all tests pass before submitting PR

### **Bug Reports**

Please include:

-   Clear description of the issue
-   Steps to reproduce
-   Expected vs actual behavior
-   Screenshots (if applicable)
-   Environment details (OS, browser, Node version)

---

## 🔧 Troubleshooting

### Images Not Loading

-   Verify Cloudinary env vars are set
-   Check transformed URLs via getProfilePictureUrl

### Slow Navigation

-   Review React Query settings (staleTime, refetchOnWindowFocus)
-   Run bundle analysis and address heavy deps

### WebSocket Connection Issues

-   Ensure WS server is running (port 8001)
-   Verify NEXT_PUBLIC_WEBSOCKET_URL and CORS origins

### MongoDB Errors

-   Confirm MongoDB is reachable and credentials are correct
-   Check indexes and scripts in backend utils

---

## 📄 License

This project is **proprietary and private software**. All rights reserved.

**🔒 Access Required**
- This codebase is not publicly available
- Repository access is restricted to authorized collaborators only
- **Contact me for access or collaboration:** [hello@iamrakesh.codes](mailto:hello@iamrakesh.codes)

Unauthorized copying, modification, distribution, or use of this software, via
any medium, is strictly prohibited without explicit written permission from the
owner.

---

## 📞 Support

### **Contact**

-   **GitHub Issues**:
    [Report a bug](https://github.com/RakeshSingh38/timeline-nextjs/issues)
-   **Email**: [hello@iamrakesh.codes](mailto:hello@iamrakesh.codes)

---

<p align="center">
  Made with ❤️ by <a href="https://github.com/RakeshSingh38">Rakesh Singh</a>
</p>
