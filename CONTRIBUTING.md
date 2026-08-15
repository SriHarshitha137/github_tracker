# Contributing to GitHub Tracker

Thank you for your interest in contributing to GitHub Tracker.

This guide explains how to set up the project, understand the repository structure, make changes, run checks, and submit a pull request.

---

## Before You Start

Before contributing, please:

1. Read this guide.
2. Read the project's Code of Conduct.
3. Check existing issues and pull requests to avoid duplicate work.
4. If the change is significant, discuss the proposed approach in an issue before implementation.

---

## Development Prerequisites

Install the following tools:

* Git
* Node.js 20 or later
* npm
* MongoDB
* Docker Desktop (optional)

Verify your installation:

```bash
node --version
npm --version
git --version
```

---

## Repository Structure

```text
github_tracker/
├── .github/                # GitHub workflows and repository configuration
├── backend/                # Node.js + Express backend
├── public/                 # Static frontend assets
├── spec/                   # Backend unit/integration tests
├── src/                    # React frontend source code
├── .gitignore              # Git ignored files
├── CODE_OF_CONDUCT.md      # Community guidelines
├── CONTRIBUTING.md         # Contribution documentation
├── docker-compose.yml      # Docker service configuration
├── Dockerfile.dev          # Frontend development image
├── Dockerfile.prod         # Frontend production image
├── package.json            # Project scripts and dependencies
├── tailwind.config.js      # Tailwind CSS configuration
└── vite.config.ts          # Vite configuration
```

The repository separates the frontend and backend into different directories while keeping the frontend tooling at the project root.

---

## Setting Up the Project

### 1. Fork the repository

Create your own fork of the repository on GitHub.

### 2. Clone your fork

```bash
git clone <your-fork-url> github_tracker
cd github_tracker
```

### 3. Install root dependencies

```bash
npm install
```

### 4. Install backend dependencies

```bash
cd backend
npm install
cd ..
```

### 5. Configure environment variables

The Docker configuration expects environment files at:

- `.env`
- `backend/.env`

Create these files locally when running the application or Docker workflow.

Do not commit environment files containing secrets, credentials, or API keys.

---


## Creating a Branch

Do not work directly on the main branch.

Create a descriptive branch:

```bash
git checkout -b feature/short-description
```

Examples:

```bash
git checkout -b feature/user-dashboard
git checkout -b fix/login-validation
git checkout -b docs/setup-guide
```

Keep the branch focused on one feature, fix, or documentation improvement.

---

## Development Workflow

### Frontend

The frontend is located under:

```text
src/
```

Run the Vite development server from the project root:

```bash
npm run dev
```

The development server uses port `5173`.

### Backend

The backend is located under:

```text
backend/
```

Install backend dependencies:

```bash
cd backend
npm install
```

cd backend
npm install
npm start

The backend Docker configuration exposes port `5000`.

### Docker Development

The complete development environment can be started from the project root:

```bash
npm run docker:dev
```

or:

```bash
docker compose --profile dev up --build
```

This starts the frontend and backend services together.

---

## Making Changes

When implementing a change:

1. Understand the existing code before modifying it.
2. Keep changes focused.
3. Follow the existing project structure.
4. Avoid unrelated refactoring.
5. Reuse existing components and utilities where possible.
6. Update documentation when behaviour or setup instructions change.
7. Add or update tests for new functionality where applicable.

---

## Testing and Validation

Before opening a pull request, run the appropriate checks.

### Backend tests

```bash
npm run test:backend
```

### Frontend tests

```bash
npm test -- --run
```

### Lint

```bash
npm run lint
```

### Production build

```bash
npm run build
```

If your change affects multiple areas, run all applicable checks.

---

## Commit Guidelines

Write clear and descriptive commit messages.

Good examples:

```text
feat: add repository activity filter
fix: resolve authentication validation issue
docs: improve local setup instructions
test: add authentication integration tests
refactor: simplify user activity service
```

Avoid unclear messages such as:

```text
update
changes
fix
new code
```

Keep commits focused so that each commit represents a logical change.

---

## Pull Request Process

Before creating a pull request:

* Make sure your branch is up to date.
* Run relevant tests.
* Run linting where applicable.
* Verify that the application builds successfully.
* Review your own changes.
* Remove debugging code and unnecessary files.
* Update documentation if required.

Then push your branch:

```bash
git add .
git commit -m "docs: improve contributor onboarding"
git push origin feature/short-description
```

Open a pull request against the the main branch.

---

## Pull Request Description

A useful pull request should explain:

### What changed?

Briefly describe the implementation.

### Why was it changed?

Explain the issue or problem being addressed.

### How was it tested?

Mention the commands or tests used.

For UI changes, include screenshots when appropriate.

---

## Reporting Issues

When reporting a bug, include:

* A clear description of the problem
* Steps to reproduce
* Expected behaviour
* Actual behaviour
* Relevant error messages or logs
* Screenshots when useful
* Environment information when relevant

For feature requests, explain:

* The problem being solved
* The proposed behaviour
* Why the feature would be useful

---

## Documentation Contributions

Documentation improvements are welcome.

When updating documentation:

* Use clear headings.
* Keep instructions in the order a new contributor would follow them.
* Use fenced code blocks for commands.
* Keep terminology consistent.
* Avoid unnecessary duplication.
* Verify commands before documenting them.
* Update related documentation when setup or workflow changes.

---

## Code Quality Guidelines

### Naming

Use descriptive names for variables, functions, components, and files.

### Reusability

Prefer reusable components and utilities over duplicated logic.

### Comments

Add comments when they explain non-obvious logic. Avoid comments that simply repeat what the code already says.

### Testing

New functionality should include appropriate tests where practical.

### Security

Do not commit credentials, API keys, tokens, passwords, or other sensitive configuration.

---

## Getting Help

If you are unsure about an implementation:

1. Check the README.
2. Check this contributing guide.
3. Review existing code and tests.
4. Search existing issues and pull requests.
5. Open an issue or discussion when further clarification is needed.

---

## Code of Conduct

Please follow the project's Code of Conduct when participating in the repository.

Thank you for contributing to GitHub Tracker!
