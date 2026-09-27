# Real-Time Operations Dashboard

A full-stack dashboard for monitoring live operational data such as users, orders, revenue, errors and service status.

The dashboard gets its initial data through REST APIs and receives live updates through Socket.IO, so the page does not need to be refreshed.

## Features

* Live dashboard metrics
* Real-time activity feed
* Service health status
* Order management
* Order search, filtering and pagination
* Event history
* Admin and viewer roles
* JWT authentication
* Connection status with reconnect handling
* Responsive UI

## Tech Stack

**Frontend**

* React 18
* TypeScript
* Vite
* React Router
* Axios
* Socket.IO Client
* SCSS

**Backend**

* Node.js
* Express
* TypeScript
* Socket.IO

**Database**

* PostgreSQL
* Prisma

**Other**

* JWT
* bcrypt
* Zod
* Jest
* Supertest
* Vitest
* React Testing Library
* Docker
* GitHub Actions

## How It Works

```text
React
  ↓
REST API
  ↓
PostgreSQL

React
  ↑
Socket.IO
  ↑
Express + Socket.IO
```

REST is used for the initial page data and updates. Socket.IO pushes changes to connected users in real time.

## Roles

| Feature                | Admin | Viewer |
| ---------------------- | :---: | :----: |
| View dashboard         |   ✓   |    ✓   |
| View orders and events |   ✓   |    ✓   |
| Change order status    |   ✓   |        |
| Create orders/events   |   ✓   |        |
| Change service status  |   ✓   |        |
| View users             |   ✓   |        |

## Setup

### Docker

```bash
cp .env.example .env
docker compose up --build
```

Open:

```text
http://localhost:8080
```

### Local development

Start PostgreSQL, then run the API:

```bash
cd server
npm install
npm run db:migrate
npm run dev
```

In another terminal:

```bash
cd client
npm install
npm run dev
```

The client runs on `http://localhost:5173` and the API on `http://localhost:4000`.

## API

Main endpoints:

```text
POST  /api/auth/register
POST  /api/auth/login
GET   /api/auth/me

GET   /api/dashboard/summary

GET   /api/orders
GET   /api/orders/:id
POST  /api/orders
PATCH /api/orders/:id

GET   /api/events
POST  /api/events

GET   /api/system-status
PUT   /api/system-status/:service

GET   /api/users
GET   /api/health
```

## Real-Time Events

Socket.IO is used for live updates such as:

* new orders
* order status changes
* activity events
* service status changes
* dashboard summary updates
* active user count

When the connection is restored, the client fetches the latest state again so updates missed during the disconnect are not left out.

## Testing

Server tests use Jest and Supertest.

Client tests use Vitest and React Testing Library.

Run server tests:

```bash
cd server
npm test
```

Run client tests:

```bash
cd client
npm test
```

## Project Structure

```text
client/
├── src/
│   ├── api/
│   ├── components/
│   ├── context/
│   ├── hooks/
│   ├── pages/
│   ├── types/
│   └── utils/

server/
├── src/
│   ├── config/
│   ├── controllers/
│   ├── db/
│   ├── middleware/
│   ├── routes/
│   ├── services/
│   ├── sockets/
│   └── validators/
└── prisma/
```
