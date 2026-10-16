# LUNGCARE - Lung Cancer Detection System
**Student Name:** Bhagyashri patil
**PRN:** 250105051100

# Dashboard Analytics Application

A full-stack responsive analytics dashboard with user management, real-time notifications, data visualization, and file upload capabilities.

## Tech Stack

- **Frontend**: React 18, Tailwind CSS, Recharts
- **Backend**: Node.js, Express.js
- **Database**: PostgreSQL
- **Real-time**: Socket.io
- **Authentication**: JWT

## Project Structure

```
project2/
├── frontend/              # React application
│   ├── src/
│   │   ├── components/   # Reusable UI components
│   │   ├── pages/        # Page components
│   │   ├── styles/       # Global styles
│   │   ├── utils/        # Utility functions
│   │   ├── App.jsx
│   │   └── index.jsx
│   └── package.json
├── backend/              # Node.js/Express application
│   ├── routes/          # API routes
│   ├── controllers/      # Route handlers
│   ├── models/          # Database models
│   ├── middleware/      # Custom middleware
│   ├── config/          # Configuration files
│   ├── server.js
│   └── package.json
├── database/            # Database scripts
│   └── migrations/      # SQL migration files
└── .env                 # Environment variables
```

## Setup Instructions

### Prerequisites
- Node.js (v16+)
- PostgreSQL (v12+)
- npm or yarn

### Backend Setup

1. Navigate to backend directory:
   ```bash
   cd backend
   npm install
   ```

2. Create `.env` file (copy from `.env.example`)

3. Start the backend server:
   ```bash
   npm run dev
   ```

### Frontend Setup

1. Navigate to frontend directory:
   ```bash
   cd frontend
   npm install
   ```

2. Create `.env` file with API URL

3. Start the development server:
   ```bash
   npm start
   ```

### Database Setup

1. Create PostgreSQL database:
   ```bash
   createdb dashboard_db
   ```

2. Run migrations from `/database/migrations/schema.sql`

## Features

- ✅ User Authentication (Login/Register)
- ✅ User Profiles with avatars
- ✅ Data Visualization & Charts
- ✅ Real-time Notifications (Socket.io)
- ✅ File Upload functionality
- ✅ Advanced Search
- ✅ Admin Dashboard
- ✅ Responsive Design (Mobile, Tablet, Desktop)

## API Endpoints

See `/backend/routes/` for detailed API documentation.

## License

MIT
