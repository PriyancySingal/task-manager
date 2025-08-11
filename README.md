# Task Manager (Vue + Node/Express + MongoDB Atlas)

## Overview
A simple full-stack Task Manager app built with Vue 3 (Vite) frontend, Node.js + Express backend, and MongoDB Atlas as the database. This project matches the assignment requirements: list tasks, add task, edit, delete, with REST APIs.

## Folder Structure
```
task-manager/
  backend/
  frontend/
  README.md
```

## How to run locally

### Backend
1. cd backend
2. copy `.env.example` to `.env` and set `MONGO_URI`
3. npm install
4. npm run dev
Backend runs on port from `.env` (default 5000)

### Frontend
1. cd frontend
2. npm install
3. npm run dev
4. Open the provided Vite URL (usually http://localhost:5173)

## Deployment
- Frontend: deploy on Netlify or Vercel (build: `npm run build`)
- Backend: deploy on Render, Railway, or Heroku. Set ENV `MONGO_URI` in dashboard.
- Database: MongoDB Atlas (free tier). Use network access to allow your IP or 0.0.0.0/0 for testing.

## Video Demo Plan (3 minutes)
1. Show your face and introduce the app.
2. Add a task on frontend.
3. Show backend logs receiving the POST request.
4. Show MongoDB Atlas document inserted.
5. Briefly explain folder structure and API endpoints.

## API Endpoints
- GET /tasks
- POST /tasks
- PUT /tasks/:id
- DELETE /tasks/:id

Good luck with your interview!
