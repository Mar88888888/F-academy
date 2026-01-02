# Football Academy Management System

A management system for football academies designed for coaches, players, and parents.

## Description

A web application for managing a football academy that allows:
- Administrators to manage users, groups, and events
- Coaches to plan trainings and matches, track attendance, and evaluate players
- Players to view schedules and their statistics
- Parents to monitor their children's progress

## Features

### Users and Roles
- **Admin** - full access to all features
- **Coach** - management of trainings and matches for their groups
- **Player** - view schedule and personal statistics
- **Parent** - view children's statistics

### Group Management
- Create age groups (U-7, U-9, U-11, etc.)
- Assign head coach and assistants
- Add/remove players

### Trainings
- Schedule trainings with topic and location
- Automatic training generation based on weekly schedule
- Attendance tracking (Present, Late, Absent, Excused)
- Player evaluation by various criteria (1-10)

### Matches
- Schedule matches with opponent and location
- Record results (goals, assists for each player)
- Attendance tracking

### Calendar
- Visual calendar of all events
- Filter by groups
- Quick view of details

### Statistics
- Player statistics: matches, goals, assists, attendance
- Team statistics for coaches
- Parent access to children's statistics

## Technologies

### Backend
- **NestJS** - Node.js framework
- **TypeORM** - ORM for database operations
- **PostgreSQL** - relational database
- **JWT** - authentication
- **bcrypt** - password hashing

### Frontend
- **React 19** - UI library
- **TypeScript** - type safety
- **Vite** - build tool and dev server
- **Tailwind CSS 4** - styling
- **React Router 7** - routing
- **Axios** - HTTP client

### Infrastructure
- **Docker Compose** - service containerization
- **PostgreSQL 15** - database (port 5433)
- **pgAdmin 4** - web interface for DB (port 5050)
- **Redis** - caching (port 6379)

## Installation

### Requirements
- Node.js 18+
- Docker and Docker Compose
- npm or yarn

### 1. Clone the repository
```bash
git clone <repo-url>
cd F-academy
```

### 2. Start Docker services
```bash
docker-compose up -d
```

This will start:
- PostgreSQL on port `5433`
- pgAdmin on port `5050`
- Redis on port `6379`

### 3. Backend Setup
```bash
cd backend
npm install
```

Create a `.env` file:
```env
DATABASE_HOST=localhost
DATABASE_PORT=5433
DATABASE_USER=postgres
DATABASE_PASSWORD=postgres
DATABASE_NAME=football_academy

JWT_SECRET=your-super-secret-jwt-key
JWT_EXPIRES_IN=7d
```

### 4. Frontend Setup
```bash
cd frontend
npm install
```

## Running

### Backend (port 3000)
```bash
cd backend
npm run start:dev
```

### Frontend (port 5173)
```bash
cd frontend
npm run dev
```

## Initial Data

### Create Administrator
```bash
cd backend
npm run seed:admin
```
Creates user:
- Email: `admin@footballacademy.com`
- Password: `admin123`

## API Endpoints

### Auth
- `POST /auth/login` - login

### Users
- `GET /users` - list users (Admin)
- `POST /users` - create user (Admin)
- `PATCH /users/:id` - update (Admin)
- `DELETE /users/:id` - delete (Admin)

### Groups
- `GET /groups` - all groups (Admin)
- `GET /groups/my` - my groups (Coach, Player, Parent)
- `POST /groups` - create (Admin)
- `PATCH /groups/:id` - update (Admin)
- `PATCH /groups/:id/staff` - assign coaches (Admin)
- `POST /groups/:id/players` - add players (Admin)
- `DELETE /groups/:id/players` - remove players (Admin)

### Trainings
- `GET /trainings` - list trainings
- `POST /trainings` - create (Admin, Coach)
- `GET /trainings/:id` - details
- `PATCH /trainings/:id` - update (Admin, Coach)
- `DELETE /trainings/:id` - delete (Admin, Coach)

### Matches
- `GET /matches` - list matches
- `POST /matches` - create (Admin, Coach)
- `GET /matches/:id` - details with results
- `PATCH /matches/:id` - update (Admin, Coach)
- `PUT /matches/:id/goals` - update goals (Admin, Coach)
- `DELETE /matches/:id` - delete (Admin, Coach)

### Attendance
- `GET /attendance/training/:id` - training attendance
- `PUT /attendance/training/:id` - update attendance
- `GET /attendance/match/:id` - match attendance
- `PUT /attendance/match/:id` - update attendance
- `GET /attendance/my/stats` - my statistics (Player)

### Evaluations
- `GET /evaluations/training/:id` - training evaluations
- `PUT /evaluations/training/:id` - update evaluations (Coach)

### Schedules
- `GET /groups/:id/schedule` - group schedule
- `PUT /groups/:id/schedule` - update schedule
- `POST /groups/:id/schedule/generate` - generate trainings
- `DELETE /groups/:id/schedule/trainings` - delete generated

### Players
- `GET /players/stats/my` - my statistics (Player)
- `GET /players/stats/team/:groupId` - team statistics (Coach)
- `GET /players/stats/children` - children statistics (Parent)

### Calendar
- `GET /calendar` - calendar events
