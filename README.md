# CityMove PTMS — Public Transport Management System

> OOASE Project Report Implementation

## 🗂 Project Structure

```
PTMS/
├── backend/                   # Node.js + Express REST API
│   ├── src/
│   │   ├── app.js             # Entry point
│   │   ├── config/            # db.js, swagger.js
│   │   ├── middleware/        # authenticate.js, authorize.js
│   │   ├── models/            # Mongoose schemas
│   │   ├── routes/            # Express route handlers
│   │   └── seed.js            # Idempotent demo data
│   ├── tests/
│   │   └── api.test.js        # Supertest API tests
│   ├── .env.example
│   └── package.json
├── frontend/                  # React + Vite SPA
│   ├── src/
│   │   ├── api/               # axios.js (API client)
│   │   ├── components/        # Layout.jsx (sidebar)
│   │   ├── context/           # AuthContext.jsx
│   │   ├── pages/             # All page components
│   │   ├── App.jsx
│   │   ├── main.jsx
│   │   └── index.css          # Design system
│   └── package.json
├── database/
│   └── DATABASE_DESIGN.md
└── README.md
```

## 🚀 Quick Start

### Prerequisites
- Node.js 20+
- MongoDB 6+ running locally (`mongodb://127.0.0.1:27017`)

### 1. Backend

```bash
cd backend
npm install
cp .env.example .env          # Edit JWT_SECRET
npm run seed                   # Load demo data
npm run dev                    # Starts on port 5000
```

### 2. Frontend

```bash
cd frontend
npm install
npm run dev                    # Starts on port 5173
```

### 3. Open Browser
Navigate to: **http://localhost:5173**

## 🧪 Demo Accounts

| Role      | Email                      | Password     |
|-----------|----------------------------|--------------|
| Admin     | admin@citymove.com         | Admin@123    |
| Operator  | operator@citymove.com      | Operator@123 |
| Driver    | driver1@citymove.com       | Driver@123   |
| Passenger | passenger1@citymove.com    | Pass@123     |

## 📋 Functional Requirements Coverage

| FR   | Feature                        | Implementation                    |
|------|-------------------------------|-----------------------------------|
| FR-01 | Passenger registration        | POST /api/auth/register           |
| FR-02 | JWT login                     | POST /api/auth/login              |
| FR-03 | User management (admin)       | PATCH/DELETE /api/users/:id       |
| FR-04 | Stop management               | /api/stops CRUD                   |
| FR-05 | Route management              | /api/routes CRUD                  |
| FR-06 | Vehicle fleet                 | /api/vehicles CRUD                |
| FR-07 | Operator creates trips        | POST /api/trips                   |
| FR-08 | Conflict detection            | Overlap check in trip creation    |
| FR-09 | Trip search/pagination        | GET /api/trips?date=&status=      |
| FR-10 | Seat booking (atomic)         | POST /api/bookings + $inc update  |
| FR-11 | Fare calculation              | baseFare × stages × seats × disc. |
| FR-12 | Booking cancellation          | PATCH /api/bookings/:id/cancel    |
| FR-13 | Payment & ticket code         | Auto-generated UUID ticket code   |
| FR-14 | Driver status update          | PATCH /api/trips/:id/status       |
| FR-15 | Alerts + notifications        | POST /api/alerts → insertMany     |
| FR-16 | Complaints                    | /api/complaints CRUD              |
| FR-17 | In-app notifications          | /api/notifications read/mark      |
| FR-18 | Admin dashboard               | GET /api/dashboard + Recharts     |
| FR-19 | CSV export                    | GET /api/reports/bookings-csv     |
| FR-20 | Health + Swagger docs         | /health, /api-docs                |

## 🔒 Security Features
- bcrypt password hashing (12 rounds)
- JWT authentication (Bearer token)
- Role-based access control (admin/operator/driver/passenger)
- Helmet HTTP headers
- CORS origin control
- Rate limiting (300 req/15 min)
- express-mongo-sanitize (injection prevention)
- Environment variables for secrets

## 📚 API Documentation
Interactive Swagger UI available at: **http://localhost:5000/api-docs**

## 🧪 Running Tests
```bash
cd backend
npm test
```
