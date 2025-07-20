# Collaborative Whiteboard

A real-time collaborative whiteboard application built with the MERN stack (MongoDB, Express.js, React.js, Node.js) and Socket.io for live drawing and presence.

## 🚀 Setup Instructions

### Prerequisites

- Node.js (v16+ recommended)
- npm
- MongoDB Atlas account (or local MongoDB)

### 1. Clone the Repository

```bash
git clone https://github.com/raunak123455/Collaborative-Whiteboard-.git
cd Collaborative-Whiteboard-
```

### 2. Install Dependencies

#### Backend

```bash
cd server
npm install
```

#### Frontend

```bash
cd ../draw
npm install
```

### 3. Configure Environment

- Update the MongoDB connection string in `server/index.js`:
  ```js
  mongoose.connect('mongodb+srv://<username>:<password>@<cluster-url>/<dbname>?retryWrites=true&w=majority', ...)
  ```
- (Optional) Use environment variables for sensitive data.

### 4. Run the Application

#### Start Backend

```bash
cd server
node index.js
```

#### Start Frontend

```bash
cd ../draw
npm run dev
```

- Frontend: http://localhost:5173
- Backend: http://localhost:5000

---

## 📚 API Documentation

### REST Endpoints

#### `POST /api/rooms/join`

- **Description:** Join or create a whiteboard room.
- **Body:** `{ roomId: string }`
- **Response:** `{ roomId, drawingData }`

#### `GET /api/rooms/:roomId`

- **Description:** Get room info and drawing data.
- **Response:** `{ roomId, drawingData }`

### Socket.io Events

#### Client → Server

- `join-room` (roomId)
- `leave-room`
- `draw-start` ({ pos, color, strokeWidth })
- `draw-move` ({ from, to, color, strokeWidth })
- `draw-end`
- `clear-canvas`
- `cursor-move` ({ x, y })

#### Server → Client

- `init-drawing-data` (drawingData)
- `draw-start`, `draw-move`, `draw-end` (drawing actions from others)
- `clear-canvas` (clear event)
- `user-count` (number)
- `cursor-move` (other users' cursors)

---

## 🏗️ Architecture Overview

### High-Level Design

```mermaid
graph TD;
  User1 & User2 & UserN -->|Socket.io| Backend
  Backend -->|REST API| MongoDB
  Backend <--> MongoDB
  Backend <--> Frontend (React)
  Frontend <--> User
```

- **Frontend:** React.js (Vite) for UI, drawing, and real-time events
- **Backend:** Node.js + Express.js for API, Socket.io for real-time
- **Database:** MongoDB (Atlas or local) for room and drawing persistence
- **Real-time:** Socket.io for drawing, cursor, and presence sync

---

## 🚢 Deployment Guide

### 1. Environment Variables

- Store MongoDB URI and any secrets in environment variables (e.g., `.env`)

### 2. Build Frontend

```bash
cd draw
npm run build
```

- Output will be in `draw/dist/`

### 3. Serve Frontend with Backend (Optional)

- Use a static file server (e.g., `serve`, Nginx) or configure Express to serve `draw/dist`.

### 4. Deploy Backend

- Deploy `server` to a cloud provider (Render, Heroku, AWS, etc.)
- Set environment variables for production
- Ensure ports and CORS are configured

### 5. Point Domain to Deployed Frontend

- Update your DNS to point to your deployed frontend

---

## 🙏 Credits

- Built by [raunak123455](https://github.com/raunak123455)
