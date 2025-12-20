# E-Lib Dashboard

## Overview

E-Lib Dashboard is the authenticated management interface of the E-Lib digital library system.
It enables registered users to manage their own books while relying on the Backend API for authentication, authorization, and data integrity.

The dashboard is **not a standalone application**. It operates as part of the E-Lib system alongside:

- the Backend API (central authority)
- the public Frontend (read-only access)

All create, update, and delete operations are validated by the backend, including ownership checks.

---

## System Context

E-Lib is composed of three coordinated components:

### Backend API

- Handles authentication and authorization
- Stores users and books
- Enforces ownership rules
- Manages file uploads and cloud storage

### Public Frontend

- Read-only interface for browsing and downloading books
- No authentication required

### Dashboard (this repository)

- Authenticated interface for managing books
- Allows users to create, update, and delete only their own books
- Communicates exclusively with the Backend API

---

## Purpose of the Dashboard

The dashboard exists to clearly separate **public access** from **privileged operations**.

- Unauthenticated users can only view books via the public frontend
- Authenticated users can manage their own content via the dashboard
- Authorization decisions are enforced server-side by the backend

This separation reflects real-world application design patterns.

---

## Tech Stack

### Core

- React
- Vite
- TypeScript

### State & Data Management

- Zustand for global client state
- TanStack React Query for server state management and caching
- Axios for HTTP requests

### Forms & Validation

- React Hook Form
- Zod for schema-based validation

### Styling

- Tailwind CSS

---

## Authentication & Authorization Flow

1. User logs in via the Backend API
2. Backend returns a JSON Web Token (JWT)
3. JWT is stored client-side
4. Protected dashboard routes require authentication
5. All create, update, and delete requests include the JWT
6. Backend verifies:
   - Token validity
   - Resource ownership (`book.userId`)

The dashboard does not rely on UI-level restrictions alone.
The backend is the final authority for all permissions.

---

## Features

- User authentication (login and registration)
- Protected routes for authenticated users
- Create new books with metadata and files
- Update books owned by the authenticated user
- Delete books owned by the authenticated user
- Book listing with management actions
- Dashboard overview with basic statistics
- Client-side form validation
- Optimistic UI updates using React Query

---

## Repository Structure

src/
├── pages/ # Dashboard routes
├── components/ # Reusable UI components
├── hooks/ # Custom React hooks
├── services/ # API communication layer
├── store/ # Zustand state management
├── schemas/ # Zod validation schemas
└── utils/ # Utility functions

yaml
Copy code

---

## Setup & Requirements

### Prerequisites

- Node.js
- Running E-Lib Backend API

### Installation

```bash
npm install
Create a .env.local file:

env
Copy code
VITE_BACKEND_URL=http://localhost:5513
Running the Dashboard
bash
Copy code
npm run dev
The application will be available at:

arduino
Copy code
http://localhost:5173
```

Important Notes
Users can modify or delete only the books they created

Ownership enforcement is handled by the backend

UI restrictions exist for usability, not security

The dashboard is intended for authenticated use only

Limitations
No automated test coverage

No role-based access control (admin roles not implemented)

No audit logging

No offline support

License
No license is specified in this repository.
```
