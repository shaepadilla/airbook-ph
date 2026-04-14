# Airline-Booking-System---Zuitt-MCP-Side-Project-B606
Airline Booking System - Zuitt MCP Side Project B606

# AIRBOOK Local Starter

Monorepo starter with:
- Frontend: Next.js App Router
- Backend: Express + MongoDB + JWT auth
- Local setup only (no Docker)

## Structure
- `frontend/` Next.js UI with login/register and protected dashboard
- `backend/` Express API with auth only

## Prerequisites
- Node.js 20+
- npm 10+
- MongoDB local or MongoDB Atlas

## Run locally

### 1. Backend
```bash
cd backend
npm install
cp .env.example .env
npm run dev
```

### 2. Frontend
```bash
cd frontend
npm install
cp .env.example .env.local
npm run dev
```

## Default API
- Frontend: http://localhost:3000
- Backend: http://localhost:4000

## Auth endpoints
- `POST /api/auth/register`
- `POST /api/auth/login`
- `GET /api/auth/me`

## Notes
- This is intentionally blank/minimal beyond authentication so your team can build modules cleanly.
- No Docker files included.
