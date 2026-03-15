# Coding Platform

A full-stack coding challenge platform built with Go. Practice algorithmic problems, run code in multiple languages, and track your progress—all in one place.

## Features

- **User Authentication** — Sign up, login, and logout with JWT-based sessions
- **Two-Factor Authentication (2FA)** — TOTP-based OTP verification for enhanced security
- **Coding Challenges** — Browse and solve algorithmic problems with Easy, Medium, and Hard difficulty levels
- **Live Code Execution** — Write and run code in Python, Java, and more via the JDoodle API
- **Test Case Validation** — Submit solutions and get instant feedback on sample test cases
- **Submission History** — Track all your past submissions and solutions
- **Premium Tier** — Stripe-powered checkout for premium challenges
- **Admin Dashboard** — Role-based access for challenge creation and management
- **Customer Care** — Built-in support page for user assistance

## Tech Stack

- **Backend:** Go 1.21
- **Database:** PostgreSQL
- **Auth:** JWT, TOTP (2FA)
- **Payments:** Stripe
- **Code Execution:** JDoodle API
- **Templates:** Go `html/template`

## Prerequisites

- Go 1.21+
- PostgreSQL
- JDoodle API credentials (for code execution)
- Stripe account (for premium features)

## Quick Start

### 1. Clone and install dependencies

```bash
git clone https://github.com/yourusername/coding-platform.git
cd coding-platform
go mod download
```

### 2. Configure the database

Create a PostgreSQL database and run the initial schema:

```bash
psql -U postgres -d coding-platform -f database/1_initial_setup.up.sql
```

Update `config/properties.yaml` with your database credentials:

```yaml
database:
  - name: coding-platform
  - host: localhost
  - port: 5432
  - user: postgres
  - password: your_password
```

Or use environment variables:

```bash
export DB_HOST=localhost
export DB_PORT=5432
export DB_USER=postgres
export DB_PASSWORD=your_password
export DB_NAME=coding-platform
```

### 3. Run the application

```bash
go run ./cmd/platform
```

The server starts at **http://localhost:7074**

## Docker

```bash
docker build -t coding-platform .
docker run -p 7074:7074 \
  -e DB_HOST=host.docker.internal \
  -e DB_PORT=5432 \
  -e DB_USER=postgres \
  -e DB_PASSWORD=your_password \
  -e DB_NAME=coding-platform \
  coding-platform
```

## Environment Variables

| Variable     | Description                    | Default        |
|-------------|--------------------------------|----------------|
| `DB_HOST`   | PostgreSQL host                | from config    |
| `DB_PORT`   | PostgreSQL port                | from config    |
| `DB_USER`   | Database user                  | from config    |
| `DB_PASSWORD` | Database password            | from config    |
| `DB_NAME`   | Database name                  | from config    |
| `DOMAIN_URL`| Base URL for Stripe redirects  | `http://localhost:7074` |
| `PRICE_ID`  | Stripe Price ID for premium    | (hardcoded)    |

## Project Structure

```
├── cmd/platform/     # Application entry point
├── config/           # Configuration and challenge metadata
├── database/         # DB connection and migrations
├── handler/           # HTTP handlers (auth, challenges, compile, checkout)
├── middlewares/       # JWT authentication middleware
├── models/            # Data models
├── services/          # Business logic and DB queries
├── static/            # Static assets (CSS, JS)
├── templates/         # HTML templates
└── commons/           # Shared utilities
```

## API Endpoints

| Endpoint                    | Auth | Description                    |
|----------------------------|------|--------------------------------|
| `GET /`                    | No   | Login page                     |
| `POST /`                   | No   | Login                          |
| `GET /signup`              | No   | Signup page                    |
| `POST /signup`             | No   | Create account                 |
| `GET /challenges`          | Yes  | Challenges list                |
| `GET /challenge/description` | Yes | Challenge details               |
| `POST /compile`            | Yes  | Execute code                   |
| `POST /compile-test`       | Yes  | Run test cases                 |
| `POST /save-submission`    | Yes  | Save solution                  |
| `GET /submissions`         | Yes  | User submissions               |
| `GET /dashboard`           | Yes  | User dashboard                 |
| `POST /create-checkout-session` | Yes | Stripe checkout (premium)  |

## License

MIT
