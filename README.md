# GitHub Tracker

**Track and analyze GitHub user activity.**

GitHub Tracker is a web application that helps users monitor and analyze GitHub activity across repositories. The project includes a React + Vite frontend, a Node.js + Express backend, MongoDB integration, Docker development/production workflows, and automated testing.

---

## Table of Contents

* [Overview](#overview)
* [Tech Stack](#tech-stack)
* [Project Structure](#project-structure)
* [Prerequisites](#prerequisites)
* [Local Setup](#local-setup)
* [Environment Configuration](#environment-configuration)
* [Running the Application](#running-the-application)
* [Docker Development](#docker-development)
* [Docker Production](#docker-production)
* [Testing](#testing)
* [Linting and Build](#linting-and-build)
* [Contribution Workflow](#contribution-workflow)
* [Troubleshooting](#troubleshooting)

---

## Overview

GitHub Tracker is organized into separate frontend and backend responsibilities:

* **Frontend**: React and Vite application responsible for the user interface.
* **Backend**: Node.js and Express application responsible for server-side functionality and API operations.
* **Database**: MongoDB through Mongoose.
* **Testing**: Jasmine and SuperTest for backend unit and integration tests, with Vitest and React Testing Library available for frontend testing.
* **Containerization**: Docker and Docker Compose provide development and production workflows.

---

## Tech Stack

### Frontend

* React.js
* Vite
* React Router
* Tailwind CSS
* Material UI
* Axios
* Recharts
* Framer Motion

### Backend

* Node.js
* Express
* MongoDB
* Mongoose
* Passport
* Passport Local
* Express Session
* bcryptjs
* Octokit

### Testing

* Jasmine
* SuperTest
* Vitest
* React Testing Library
* JSDOM

### Development Tools

* ESLint
* Docker
* Docker Compose
* npm

---

## Project Structure

```text
github_tracker/
├── .github/                # GitHub workflows and repository configuration
├── backend/                # Node.js + Express backend
├── public/                 # Static frontend assets
├── spec/                   # Backend Jasmine unit/integration tests
├── src/                    # React frontend source code
├── .dockerignore           # Docker build exclusions
├── .gitignore              # Git exclusions
├── CODE_OF_CONDUCT.md      # Community guidelines
├── CONTRIBUTING.md         # Contribution and onboarding guide
├── docker-compose.yml      # Docker development and production services
├── Dockerfile.dev          # Frontend development container
├── Dockerfile.prod         # Frontend production container
├── eslint.config.js        # ESLint configuration
├── index.html              # Vite HTML entry point
├── package.json            # Frontend and root project dependencies/scripts
├── postcss.config.cjs      # PostCSS configuration
├── tailwind.config.js      # Tailwind configuration
├── tsconfig.json           # TypeScript configuration
├── tsconfig.app.json       # Application TypeScript configuration
├── tsconfig.node.json      # Node/Vite TypeScript configuration
└── vite.config.ts          # Vite configuration
```

---

## Prerequisites

Before setting up the project, install:

* Node.js 20 or later
* npm
* Git
* MongoDB
* Docker Desktop (optional, required only for Docker workflows)

Verify Node.js and npm:

```bash
node --version
npm --version
```

Verify Git:

```bash
git --version
```

If you are using the local MongoDB setup, make sure MongoDB is installed and running before starting backend services.

---

## Local Setup

### 1. Clone the repository

```bash
git clone <repository-url>
cd github_tracker
```

### 2. Install root dependencies

From the project root:

```bash
npm install
```

### 3. Install backend dependencies

Open a second terminal:

```bash
cd backend
npm install
```

### 4. Configure environment variables

The project uses environment files for configuration.

The Docker Compose configuration expects:

```text
.env
backend/.env
```

Do not commit real secrets, API keys, database credentials, or session secrets to Git.

If environment variables are required for your local setup, create the required files locally using the variables expected by the frontend and backend configuration.

---

## Running the Application

### Frontend

From the project root:

```bash
npm run dev
```

Vite starts the frontend development server on port `5173`.

### Backend

Open a separate terminal and move into the backend directory:

```bash
cd backend
npm install
```

For development with automatic restart on file changes:

```bash
npm run dev
```

For a normal production-style start:

```bash
npm start
```

The backend server runs on port `5000` when configured through the project's Docker setup.

Keep the frontend and backend running in separate terminals during local development.


## Docker Development
 **MongoDB:** MongoDB is not included in Docker Compose. Contributors must have MongoDB running separately and configure the backend to connect to it.

Docker Compose provides a complete development setup containing frontend and backend services.

Make sure Docker Desktop is installed and running.

From the project root:

```bash
docker compose --profile dev up --build
```

The corresponding npm shortcut is:

```bash
npm run docker:dev
```

### Development services

| Service  | Port | Purpose                 |
| -------- | ---: | ----------------------- |
| Frontend | 5173 | Vite development server |
| Backend  | 5000 | Express backend         |

The development containers mount the local source directories, allowing changes to be reflected during development.

To stop the development containers:

```bash
docker compose --profile dev down
```

---

## Docker Production

The project also provides a production Docker configuration.

Build and start the production services:

```bash
docker compose --profile prod up -d --build
```

Or use:

```bash
npm run docker:prod
```

### Production services

| Service  | Port | Purpose                       |
| -------- | ---: | ----------------------------- |
| Frontend | 3000 | Nginx-served production build |
| Backend  | 5000 | Production backend            |

To stop the production containers:

```bash
docker compose --profile prod down
```

---

## Testing

The repository contains backend unit and integration tests using Jasmine and SuperTest.

### Backend tests

From the project root:

```bash
npm run test:backend
```

The backend tests cover areas including:

* User model behaviour
* Password hashing
* Password comparison
* Authentication routes
* Signup and login flows
* Passport authentication logic
* API integration behaviour

You can also run Jasmine directly when required:

```bash
npx jasmine
```

### Test files

Backend test files are located under:

```text
spec/
```

Examples include:

```text
spec/user.model.spec.cjs
spec/auth.routes.spec.cjs
```

### Frontend tests

Vitest is available through:

```bash
npm test
```

Additional frontend testing dependencies include React Testing Library and JSDOM.

---

## Linting and Build

Run ESLint:

```bash
npm run lint
```

Create a production frontend build:

```bash
npm run build
```

Preview the production build locally:

```bash
npm run preview
```

These checks should be performed before submitting a pull request where applicable.

---

## Contribution Workflow

The recommended contribution workflow is:

```text
Fork repository
      ↓
Clone your fork
      ↓
Create a feature branch
      ↓
Install dependencies
      ↓
Create and test changes
      ↓
Run lint/tests/build
      ↓
Commit changes
      ↓
Push branch
      ↓
Open Pull Request
      ↓
Address review feedback
```

For detailed contribution instructions, see [CONTRIBUTING.md](CONTRIBUTING.md).

---

## Troubleshooting

### `npm install` fails

Check that you are using a supported Node.js version:

```bash
node --version
```

Then remove dependencies and reinstall if necessary:

```bash
rm -rf node_modules
npm install
```

On Windows, you can delete the `node_modules` directory manually and run:

```bash
npm install
```

### Frontend does not start

Make sure you are running the command from the repository root:

```bash
npm run dev
```

Check that port `5173` is not already being used.

### Backend does not start

Make sure backend dependencies are installed:

```bash
cd backend
npm install
```

Also verify that MongoDB is running and that the required backend environment variables are configured.

### MongoDB connection errors

Make sure MongoDB is running and that the connection configuration in `backend/.env` is correct.

The local MongoDB setup commonly uses:

```text
mongodb://127.0.0.1:27017
```

### Docker errors

Make sure Docker Desktop is running.

Check the available containers:

```bash
docker ps
```

Rebuild the development environment when dependencies or Docker configuration change:

```bash
docker compose --profile dev up --build
```

### Tests cannot find modules

Install dependencies again:

```bash
npm install
```

If backend dependencies are missing:

```bash
cd backend
npm install
```

---

## Contribution

New contributors should read [CONTRIBUTING.md](CONTRIBUTING.md) before making changes.

Please ensure that changes are focused, tested where applicable, and clearly described in the pull request.

Thank you for contributing to GitHub Tracker!
