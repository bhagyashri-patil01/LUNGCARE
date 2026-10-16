# Deployment & Setup Guide

## Prerequisites

- **Node.js** (v16+)
- **npm** or **yarn**
- **PostgreSQL** (v12+)
- **Git**

## Environment Variables

### Backend (.env)
```env
PORT=5000
DB_HOST=localhost
DB_PORT=5432
DB_NAME=dashboard_db
DB_USER=postgres
DB_PASSWORD=your_secure_password
JWT_SECRET=your_very_secure_jwt_secret_key_change_this
NODE_ENV=development
FRONTEND_URL=http://localhost:3000
```

### Frontend (.env)
```env
REACT_APP_API_URL=http://localhost:5000
```

## Installation Steps

### 1. Database Setup

```bash
# Create PostgreSQL database
createdb dashboard_db

# Connect and run migrations
psql dashboard_db < database/migrations/schema.sql
```

### 2. Backend Setup

```bash
cd backend
npm install
npm run dev
```

The backend will start on `http://localhost:5000`

### 3. Frontend Setup

```bash
cd frontend
npm install
npm start
```

The frontend will start on `http://localhost:3000`

### 4. Run Both Together

From root directory:
```bash
npm run dev
```

## API Documentation

### Authentication
- `POST /api/auth/register` - Register new user
- `POST /api/auth/login` - User login
- `GET /api/auth/profile` - Get user profile
- `PUT /api/auth/profile` - Update user profile

### Dashboard
- `POST /api/dashboard/data` - Create dashboard data
- `GET /api/dashboard/data` - Get user's data
- `PUT /api/dashboard/data/:id` - Update data
- `DELETE /api/dashboard/data/:id` - Delete data
- `GET /api/dashboard/search?query=...` - Search data

### Notifications
- `GET /api/notifications` - Get all notifications
- `POST /api/notifications` - Create notification
- `PUT /api/notifications/:id` - Mark as read
- `DELETE /api/notifications/:id` - Delete notification

### Files
- `POST /api/files/upload` - Upload file
- `GET /api/files` - Get user files
- `DELETE /api/files/:id` - Delete file

### Users (Admin)
- `GET /api/users` - Get all users (admin only)
- `DELETE /api/users/:id` - Delete user (admin only)

## Docker Setup (Optional)

### Docker Compose
```yaml
version: '3.8'

services:
  db:
    image: postgres:15
    environment:
      POSTGRES_DB: dashboard_db
      POSTGRES_PASSWORD: password
    ports:
      - "5432:5432"
    volumes:
      - ./database/migrations/schema.sql:/docker-entrypoint-initdb.d/schema.sql

  backend:
    build: ./backend
    ports:
      - "5000:5000"
    environment:
      DB_HOST: db
      DB_PASSWORD: password
    depends_on:
      - db

  frontend:
    build: ./frontend
    ports:
      - "3000:3000"
```

Run with: `docker-compose up`

## Features Implemented

✅ **User Management**
- Registration & Login
- JWT Authentication
- User Profiles
- Admin Panel

✅ **Dashboard**
- Real-time Data Visualization
- Multiple Chart Types
- Data Management (CRUD)
- Advanced Search

✅ **Notifications**
- Real-time Notifications (Socket.io)
- Notification History
- Mark as Read

✅ **File Management**
- File Upload
- File Storage
- File History

✅ **Responsive Design**
- Mobile-friendly
- Tablet optimized
- Desktop experience

## Troubleshooting

### Port Already in Use
```bash
# Kill process on port 5000
lsof -ti:5000 | xargs kill -9

# Kill process on port 3000
lsof -ti:3000 | xargs kill -9
```

### Database Connection Error
- Check PostgreSQL is running
- Verify credentials in .env
- Ensure database exists

### CORS Errors
- Check FRONTEND_URL in backend .env
- Verify Express CORS middleware

## Production Deployment

### Backend (Heroku)
```bash
cd backend
heroku create your-app-name
git push heroku main
```

### Frontend (Vercel)
```bash
cd frontend
npm run build
vercel --prod
```

## License

MIT License © 2024
