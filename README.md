# Go + React Todo List

This is a full-stack Todo List application built with a Go backend and a React frontend. The backend uses MongoDB for data storage, and the frontend is styled with Chakra UI.

## Features

- Add, update, and delete tasks
- Persistent storage using MongoDB
- Light/Dark mode toggle
- Responsive design

---

## Prerequisites

Before setting up the project, ensure you have the following installed:

1. **Go** (version 1.24.2 or higher)
2. **Node.js** (version 18 or higher)
3. **MongoDB Atlas** (or a local MongoDB instance)
4. **Git**

---

## Setup Instructions

### 1. Clone the Repository

```bash
git clone https://github.com/HakashiKatake/go-react-todo.git
cd go-react-todo
```

---

### 2. Backend Setup (Go)

1. **Install Go dependencies**:
   ```bash
   go mod tidy
   ```

2. **Set up environment variables**:
   Create a `.env` file in the root directory and add the following:
   ```properties
   PORT=4000
   MONGODB_URI=mongodb+srv://<username>:<password>@cluster0.mongodb.net/<database>?retryWrites=true&w=majority
   ENV=development
   ```

   Replace `<username>`, `<password>`, and `<database>` with your MongoDB credentials.

3. **Run the backend**:
   ```bash
   go run main.go
   ```

   The backend will start on `http://localhost:4000`.

---

### 3. Frontend Setup (React)

1. **Navigate to the `client` directory**:
   ```bash
   cd client
   ```

2. **Install Node.js dependencies**:
   ```bash
   npm install
   ```

3. **Run the frontend in development mode**:
   ```bash
   npm run dev
   ```

   The frontend will start on `http://localhost:5173`.

---

### 4. Build for Production

1. **Build the React frontend**:
   ```bash
   cd client
   npm run build
   cd ..
   ```

2. **Serve the React build from the Go backend**:
   The Go backend is already configured to serve the React build from the `./client/dist` directory in production mode.

---

### 5. Deploying to Render

1. **Create a `render.yaml` file**:
   Ensure the following configuration exists in your `render.yaml`:
   ```yaml
   services:
     - type: web
       name: todo-go-app
       env: go
       buildCommand: cd client && npm install && npm run build && cd .. && go build -o app
       startCommand: ./app
       envVars:
         - key: PORT
           value: 10000
         - key: ENV
           value: production
         - key: MONGODB_URI
           sync: false
         - key: GO_VERSION
           value: 1.24.2
   ```

2. **Push your code to GitHub**:
   ```bash
   git add .
   git commit -m "Initial commit"
   git push origin main
   ```

3. **Deploy on Render**:
   - Go to [Render](https://render.com).
   - Create a new Web Service and connect your GitHub repository.
   - Render will automatically detect the `render.yaml` file and deploy your app.

---

## Project Structure

```
Todo-In-Go/
├── client/                # React frontend
│   ├── src/               # React source code
│   ├── public/            # Static assets
│   └── package.json       # Frontend dependencies
├── main.go                # Go backend entry point
├── go.mod                 # Go module dependencies
├── .env                   # Environment variables
├── render.yaml            # Render deployment configuration
└── README.md              # Project documentation
```

---

## API Endpoints

### Base URL: `http://localhost:4000/api`

| Method | Endpoint          | Description          |
|--------|-------------------|----------------------|
| GET    | `/todos`          | Fetch all todos      |
| POST   | `/todos`          | Create a new todo    |
| PATCH  | `/todos/:id`      | Update a todo        |
| DELETE | `/todos/:id`      | Delete a todo        |

---

## Technologies Used

- **Backend**: Go, Fiber, MongoDB
- **Frontend**: React, Chakra UI, Vite
- **Database**: MongoDB Atlas
- **Deployment**: Render

---

## License

This project is licensed under the MIT License. Feel free to use and modify it as needed.

---

## Author

Created by [Hakashi Katake](https://github.com/HakashiKatake).