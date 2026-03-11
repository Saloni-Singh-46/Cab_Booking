# Ucab - Cab Booking Application

Ucab is a full-stack, real-time cab booking platform built using the MERN stack (MongoDB, Express.js, React, Node.js) with real-time bidirectional communication via Socket.io.

## 🚀 Project Theory & Flow

### 1. Theory
The application is designed to connect **Users** (riders) with **Drivers** in real-time. The core system revolves around:
- **Authentication & Authorization**: Role-based access control (Users vs. Drivers) using secure JWT (JSON Web Tokens) and password hashing with bcrypt.
- **Real-Time Bidding / Ride Management**: Utilizing WebSockets (via Socket.io), the system allows real-time updates where users can request rides and drivers can receive, accept, or decline those requests instantly.
- **RESTful API Architecture**: The backend exposes clearly defined resources (`/api/auth`, `/api/users`, `/api/drivers`, `/api/rides`, `/api/payments`) following standard REST principles.
- **Database**: MongoDB (via Mongoose) provides a flexible schema design to model Users, Drivers, Rides, and Payments.
- **Modern Frontend**: A responsive, component-based user interface built with React (Vite) and Bootstrap.

### 2. Application Flow

**For Users:**
1. **Registration/Login**: A user creates an account or logs in. A JWT token is issued for subsequent requests.
2. **Dashboard**: The user connects to their dedicated Socket.io room (`user_{userId}`).
3. **Request Ride**: The user initiates a cab request, defining pickup and drop-off locations.
4. **Real-time Updates**: The system notifies nearby/available drivers via sockets. The user waits for a driver to accept the ride.
5. **Ride Started/Completed**: Status updates are pushed over websockets.
6. **Payment**: The user processes payment for the completed ride (powered by Stripe, as per project goals).

**For Drivers:**
1. **Registration/Login**: A driver registers/logs in and securely connects to the platform.
2. **Driver Dashboard**: The driver connects to their dedicated Socket.io room (`driver_{driverId}`).
3. **Receive Ride Requests**: Emitted events notify the driver about new potential rides.
4. **Accept Ride**: The driver accepts the ride, notifying the user.
5. **Complete Ride**: The driver marks the ride as complete, triggering the payment flow.

## 📂 Project Structure

The repository is organized into two main workspaces: the `backend` and the `frontend`.

### `backend/` (Node.js & Express API)
```text
backend/
├── controllers/    # Business logic for endpoints (auth, users, drivers, etc.)
├── middleware/     # Custom Express middleware (e.g., JWT authentication)
├── models/         # Mongoose schemas (User, Driver, Ride, Payment)
├── routes/         # API endpoint definitions mapped to controllers
├── .env            # Environment variables (Mongo URI, JWT Secret, Port)
├── server.js       # Express server setup, Socket.io initialization, and MongoDB connection
└── package.json    # Backend dependencies (express, mongoose, socket.io, etc.)
```

### `frontend/` (React via Vite)
```text
frontend/
├── public/         # Static assets directly served to the browser
├── src/
│   ├── components/ # Reusable UI components (Navbar, RideCard, etc.)
│   ├── pages/      # Page-level components corresponding to Application Routes
│   ├── App.jsx     # Main React application entry and route definitions
│   └── main.jsx    # DOM rendering and React context providers
├── index.html      # Vite's HTML entry point
├── vite.config.js  # Vite Bundler configuration
└── package.json    # Frontend dependencies (react, axios, socket.io-client, bootstrap)
```

## 🛠️ Tech Stack

**Frontend Framework**: React 19, Vite, Bootstrap 5.3  
**Backend Framework**: Node.js, Express 5  
**Database**: MongoDB (Mongoose ORM)  
**Real-time Communication**: Socket.io  
**Authentication**: JWT, bcryptjs  
**HTTP Client**: Axios  

## 🏃‍♂️ How to Run Locally

1. **Clone the repository:**
   ```bash
   git clone <repository_url>
   ```

2. **Run Backend Server:**
   ```bash
   cd backend
   npm install
   npm start # Starts the server on port 5000
   ```
   *Make sure you provide the proper `.env` file variables (`PORT`, `MONGO_URI`, `JWT_SECRET`).*

3. **Run Frontend Development Server:**
   ```bash
   cd frontend
   npm install
   npm run dev
   ```
   *The frontend should now run typically on `http://localhost:5173`.*

---
*This README serves as an overview outline to understand the foundational architecture and workflow of the Ucab project.*
