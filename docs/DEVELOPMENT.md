# Development Guide

This document provides a quick reference for contributors working on GitHub Tracker.

---

## Development Architecture

GitHub Tracker consists of two main application layers:

```text
                    GitHub Tracker
                          |
             ┌────────────┴────────────┐
             |                         |
         Frontend                  Backend
          React                    Express
            |                         |
          Vite                    MongoDB
            |
       User Interface
```

### Frontend

The frontend is located in:

```text
src/
```

The application uses React and Vite.

Start frontend development with:

```bash
npm run dev
```

The Vite development server runs on port `5173`.

### Backend

The backend is located in:

```text
backend/
```

It uses Node.js and Express and communicates with MongoDB.

Install backend dependencies:

```bash
cd backend
npm install
```

The backend Docker service uses port `5000`.

---

## Development Options

There are two recommended ways to work on the project.

### Option 1: Run services locally

Run the frontend from the repository root:

```bash
npm install
npm run dev
```

Run the backend from a separate terminal:

```bash
cd backend
npm install
```

### Backend

The backend is located in:

```text
backend/
```

It uses Node.js and Express and communicates with MongoDB.

Install backend dependencies:

```bash
cd backend
npm install
```

For development, use:

```bash
npm run dev
```

This starts the server with Nodemon, which automatically restarts the server when backend files change.

For a normal start:

```bash
npm start
```

The backend Docker service uses port `5000`.


This approach is useful when actively developing and debugging individual services.

---

### Option 2: Use Docker

Docker Compose can start the frontend and backend together.

From the repository root:

```bash
npm run docker:dev
```

Equivalent command:

```bash
docker compose --profile dev up --build
```

Stop the services with:

```bash
docker compose --profile dev down
```

---

## Ports

| Component | Development Port |
| --------- | ---------------: |
| Frontend  |             5173 |
| Backend   |             5000 |

The production frontend is exposed on port `3000`.

---

## Testing Workflow

Backend tests are located in:

```text
spec/
```

Run backend tests:

```bash
npm run test:backend
```

Run frontend tests:

```bash
npm test
```

Before submitting a pull request, also run:

```bash
npm run lint
npm run build
```

---

## Recommended Contributor Workflow

```text
Read issue
   ↓
Understand existing implementation
   ↓
Create feature branch
   ↓
Install dependencies
   ↓
Configure environment
   ↓
Run application
   ↓
Implement changes
   ↓
Run tests
   ↓
Run lint/build
   ↓
Review changes
   ↓
Commit
   ↓
Push branch
   ↓
Open Pull Request
```

---

## Docker Workflow

### Development

```bash
docker compose --profile dev up --build
```

### Stop development containers

```bash
docker compose --profile dev down
```

### Production

```bash
docker compose --profile prod up -d --build
```

### Stop production containers

```bash
docker compose --profile prod down
```

---

## Environment Configuration

Environment-specific configuration should remain outside version control.

The project expects environment files for local/Docker configuration:

```text
.env
backend/.env
```

Never commit secrets or credentials.

When adding a new environment variable:

1. Identify which service uses it.
2. Add it to the appropriate local environment file.
3. Update the documentation if contributors need to configure it.
4. Do not commit the actual secret value.

---

## Before Opening a Pull Request

Run the checks relevant to your changes:

```bash
npm run lint
npm test
npm run test:backend
npm run build
```

Not every change requires every check, but contributors should run the checks affected by their changes.

Review the final diff before pushing:

```bash
git status
git diff
```

A clean, focused pull request makes review easier and helps maintain project quality.
