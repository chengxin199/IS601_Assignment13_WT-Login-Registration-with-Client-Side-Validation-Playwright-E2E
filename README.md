# 🧮 Calculations Pro - Web Application

A modern, secure web application for managing calculations with user authentication, built with FastAPI, PostgreSQL, and featuring a minimalist clean UI design.

![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)
![Python](https://img.shields.io/badge/python-3.10-blue.svg)

---

## 🌟 Features

- ✅ **User Authentication**: Secure JWT-based authentication with bcrypt password hashing
- ✅ **Client-Side Validation**: Comprehensive form validation with real-time feedback
- ✅ **Calculation Management**: Create, read, and delete calculations (addition, subtraction, multiplication, division)
- ✅ **Modern UI**: Minimalist design with soft pastel colors and light skeuomorphic elements
- ✅ **Responsive Design**: Mobile-friendly interface that works on all devices
- ✅ **Security**: Password strength requirements, protected routes, and secure token management
- ✅ **Testing**: Comprehensive unit, integration, and E2E tests with Playwright
- ✅ **CI/CD**: Automated testing, security scanning, and Docker deployment

---

## 🔗 Links

- **Docker Hub Repository**: [chengxin199/is601_module13](https://hub.docker.com/r/chengxin199/is601_module13)
- **GitHub Repository**: [IS601_Assignment13](https://github.com/chengxin199/IS601_Assignment13_WT-Login-Registration-with-Client-Side-Validation-Playwright-E2E)
- **Reflection Document**: [REFLECTION.md](./REFLECTION.md)

---

## 📋 Table of Contents

- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Running the Application](#running-the-application)
- [Running the Frontend](#running-the-frontend)
- [Testing](#testing)
- [Docker Hub](#docker-hub)
- [Project Structure](#project-structure)
- [API Documentation](#api-documentation)
- [Security](#security)

---

## 🛠️ Prerequisites

Before you begin, ensure you have the following installed:

- **Docker** (v20.10+) and **Docker Compose** (v2.0+)
- **Python** 3.10 or higher
- **Node.js** 18+ (for Playwright)
- **Git**

### Installing Prerequisites

#### macOS (using Homebrew)
```bash
# Install Homebrew
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Install dependencies
brew install git python@3.10 docker docker-compose node
```

#### Windows
- Download [Git for Windows](https://git-scm.com/download/win)
- Download [Docker Desktop](https://www.docker.com/products/docker-desktop)
- Download [Python 3.10+](https://www.python.org/downloads/)
- Download [Node.js](https://nodejs.org/)

#### Linux (Ubuntu/Debian)
```bash
sudo apt update
sudo apt install git python3.10 python3-pip docker.io docker-compose nodejs npm
```

---

## 📦 Installation

### 1. Clone the Repository

```bash
git clone https://github.com/chengxin199/IS601_Assignment13_WT-Login-Registration-with-Client-Side-Validation-Playwright-E2E.git
cd IS601_Assignment13_WT-Login-Registration-with-Client-Side-Validation-Playwright-E2E
```

### 2. Create Environment File

Create a `.env` file in the project root:

```bash
cp .env.example .env
```

Edit `.env` with your configuration:

```env
DATABASE_URL=postgresql://user:password@db:5432/myappdb
SECRET_KEY=your-super-secret-key-change-this-in-production
ACCESS_TOKEN_EXPIRE_MINUTES=15
REFRESH_TOKEN_EXPIRE_DAYS=7
```

### 3. Install Python Dependencies (Optional for local development)

```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install -r requirements.txt
```

### 4. Install Playwright Browsers

```bash
playwright install
```

---

## 🚀 Running the Application

### Option 1: Using Docker Compose (Recommended)

This will start the web application, PostgreSQL database, and pgAdmin:

```bash
docker-compose up --build
```

The application will be available at:
- **Web Application**: http://localhost:8000
- **API Documentation**: http://localhost:8000/docs
- **pgAdmin**: http://localhost:5050

Default pgAdmin credentials:
- Email: admin@admin.com
- Password: admin

### Option 2: Running Locally (Development)

**Start PostgreSQL:**
```bash
docker run -d \
  --name postgres_db \
  -e POSTGRES_USER=user \
  -e POSTGRES_PASSWORD=password \
  -e POSTGRES_DB=myappdb \
  -p 5432:5432 \
  postgres:latest
```

**Run the application:**
```bash
source venv/bin/activate
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
```

### Stopping the Application

```bash
# Stop Docker Compose
docker-compose down

# Or stop with volume cleanup
docker-compose down -v
```

---

## 🎨 Running the Frontend

The frontend is served automatically when you run the application. It's built with:
- **HTML5** and **Jinja2 Templates**
- **Tailwind CSS** for styling
- **Vanilla JavaScript** for interactivity
- **Custom CSS** for the minimalist design

### Accessing the Frontend

1. Start the application (see "Running the Application" above)
2. Open your browser to **http://localhost:8000**

### Frontend Features

#### Pages:
- **Home** (`/`): Landing page with feature showcase
- **Register** (`/register`): User registration with client-side validation
- **Login** (`/login`): User login
- **Dashboard** (`/dashboard`): Protected page for logged-in users

#### Client-Side Validation:
- Real-time password strength checking
- Password confirmation matching
- Email format validation
- Minimum length requirements
- Clear error messages

#### UI Design:
- Minimalist clean style with soft pastel colors
- Light skeuomorphic design (subtle shadows and depth)
- Responsive layout (mobile-friendly)
- Smooth animations and transitions
- Generous whitespace for better readability

---

## 🧪 Testing

### Running All Tests

```bash
# Activate virtual environment
source venv/bin/activate

# Run all tests with coverage
pytest --cov=app --cov-report=html
```

### Running Specific Test Suites

**Unit Tests:**
```bash
pytest tests/unit/ -v
```

**Integration Tests:**
```bash
pytest tests/integration/ -v
```

**E2E Tests (Playwright):**
```bash
pytest tests/e2e/ -v
```

---

## 🎭 Executing Playwright Tests

Playwright tests provide end-to-end testing of the entire application, including the frontend interactions.

### Prerequisites for Playwright

```bash
# Install Playwright and browsers
pip install playwright pytest-playwright
playwright install
```

### Running Playwright Tests

**Basic Test Run:**
```bash
pytest tests/e2e/test_fastapi_calculator.py -v
```

**Run with Visible Browser (Headed Mode):**
```bash
pytest tests/e2e/test_fastapi_calculator.py --headed -v
```

**Run with Slow Motion (for debugging):**
```bash
pytest tests/e2e/test_fastapi_calculator.py --headed --slowmo 500 -v
```

**Run Specific Test:**
```bash
pytest tests/e2e/test_fastapi_calculator.py::test_user_registration -v
```

**Generate Test Report:**
```bash
pytest tests/e2e/ --html=report.html --self-contained-html
```

**Run with Tracing (for debugging):**
```bash
pytest tests/e2e/ --tracing=on
```

### Playwright Test Coverage

The E2E tests validate:
- ✅ User registration workflow with validation
- ✅ Login/logout functionality
- ✅ Password validation (strength requirements)
- ✅ Password confirmation matching
- ✅ Protected route access control
- ✅ Calculation creation (all operations)
- ✅ Calculation history display
- ✅ Calculation deletion
- ✅ Form validation error messages
- ✅ Success message displays
- ✅ Navigation flows

### Debugging Playwright Tests

**View Test Trace:**
```bash
# After running with --tracing=on
playwright show-trace trace.zip
```

**Interactive Debugging:**
```python
# Add this line in your test where you want to pause
await page.pause()
```

**Screenshot on Failure:**
Playwright automatically captures screenshots on test failures in the `test-results/` directory.

### Viewing Test Coverage

```bash
# Open coverage report in browser
open htmlcov/index.html  # macOS
start htmlcov/index.html  # Windows
xdg-open htmlcov/index.html  # Linux
```

---

## 🐳 Docker Hub

### Pulling the Image

```bash
docker pull chengxin199/is601_module13:latest
```

### Running from Docker Hub

```bash
# Run the application container
docker run -d \
  --name calculations-app \
  -p 8000:8000 \
  -e DATABASE_URL=postgresql://user:password@host:5432/myappdb \
  -e SECRET_KEY=your-secret-key \
  chengxin199/is601_module13:latest
```

### Complete Setup with Database

```bash
# Create a network
docker network create calc-network

# Run PostgreSQL
docker run -d \
  --name postgres_db \
  --network calc-network \
  -e POSTGRES_USER=user \
  -e POSTGRES_PASSWORD=password \
  -e POSTGRES_DB=myappdb \
  postgres:latest

# Run the application
docker run -d \
  --name calculations-app \
  --network calc-network \
  -p 8000:8000 \
  -e DATABASE_URL=postgresql://user:password@postgres_db:5432/myappdb \
  -e SECRET_KEY=your-super-secret-key \
  chengxin199/is601_module13:latest
```

### Available Tags

- `latest` - Latest stable version
- `v{run-number}` - Specific build version (e.g., v42)
- `{commit-sha}` - Specific commit version (e.g., d900260)

### Building and Pushing (For Maintainers)

```bash
# Build the image
docker build -t chengxin199/is601_module13:latest .

# Push to Docker Hub
docker push chengxin199/is601_module13:latest

# Push specific tag
docker tag chengxin199/is601_module13:latest chengxin199/is601_module13:v1.0.0
docker push chengxin199/is601_module13:v1.0.0
```

---

## 📁 Project Structure

```
.
├── app/
│   ├── __init__.py
│   ├── main.py                 # FastAPI application entry point
│   ├── database.py             # Database configuration
│   ├── database_init.py        # Database initialization script
│   ├── auth/                   # Authentication module
│   │   ├── dependencies.py     # Auth dependencies
│   │   ├── jwt.py              # JWT token handling
│   │   └── redis.py            # Redis configuration
│   ├── core/
│   │   └── config.py           # Application configuration
│   ├── models/                 # SQLAlchemy models
│   │   ├── calculation.py
│   │   └── user.py
│   ├── operations/             # Business logic
│   ├── schemas/                # Pydantic schemas
│   │   ├── base.py
│   │   ├── calculation.py
│   │   ├── token.py
│   │   └── user.py
├── static/
│   ├── css/
│   │   └── style.css           # Custom CSS styles
│   └── js/
│       └── script.js           # Frontend JavaScript
├── templates/                  # Jinja2 HTML templates
│   ├── layout.html             # Base template
│   ├── index.html              # Home page
│   ├── login.html              # Login page
│   ├── register.html           # Registration page
│   └── dashboard.html          # Dashboard page
├── tests/
│   ├── unit/                   # Unit tests
│   ├── integration/            # Integration tests
│   └── e2e/                    # Playwright E2E tests
│       └── test_fastapi_calculator.py
├── .github/
│   └── workflows/
│       └── test.yml            # CI/CD pipeline
├── docker-compose.yml          # Docker Compose configuration
├── Dockerfile                  # Docker image definition
├── requirements.txt            # Python dependencies
├── pytest.ini                  # Pytest configuration
├── REFLECTION.md               # Project reflection document
└── README.md                   # This file
```

---

## 📚 API Documentation

Once the application is running, visit:
- **Swagger UI**: http://localhost:8000/docs
- **ReDoc**: http://localhost:8000/redoc

### Key Endpoints

#### Authentication
- `POST /auth/register` - Register new user
- `POST /auth/login` - Login and receive JWT tokens
- `POST /auth/token` - OAuth2 compatible token endpoint

#### Calculations
- `GET /calculations` - Get all user calculations
- `POST /calculations` - Create new calculation
- `GET /calculations/{id}` - Get specific calculation
- `DELETE /calculations/{id}` - Delete calculation

#### Pages
- `GET /` - Home page
- `GET /login` - Login page
- `GET /register` - Registration page
- `GET /dashboard` - Dashboard (protected)

---

## 🔒 Security

### Implemented Security Features

1. **Password Security**:
   - Bcrypt hashing with cost factor 12
   - Minimum 8 characters
   - Must contain uppercase, lowercase, numbers, and special characters

2. **JWT Authentication**:
   - Access tokens expire in 15 minutes
   - Refresh tokens for extended sessions
   - Secure token storage in localStorage

3. **Protected Routes**:
   - Dashboard requires authentication
   - API endpoints protected with JWT bearer tokens
   - Automatic redirect to login for unauthorized access

4. **Docker Security**:
   - Non-root user in containers
   - Security scanning with Trivy
   - Minimal base image (python:3.10-slim)

5. **Dependency Security**:
   - Regular updates of dependencies
   - Vulnerability scanning in CI/CD
   - SARIF reports uploaded to GitHub Security tab

### Environment Variables

Never commit these to version control:
- `SECRET_KEY` - JWT signing key
- `DATABASE_URL` - Database connection string
- `DOCKERHUB_USERNAME` - Docker Hub username (for CI/CD)
- `DOCKERHUB_TOKEN` - Docker Hub access token (for CI/CD)

---

## 🚀 CI/CD Pipeline

The project uses GitHub Actions for automated testing and deployment:

### Workflow Steps

1. **Test Job**:
   - Runs unit tests
   - Runs integration tests
   - Runs E2E Playwright tests
   - Generates coverage report

2. **Security Job**:
   - Builds Docker image
   - Scans for vulnerabilities with Trivy
   - Uploads results to GitHub Security tab

3. **Deploy Job** (on main branch):
   - Builds multi-platform Docker image (amd64, arm64)
   - Pushes to Docker Hub with multiple tags
   - Uses caching for faster builds

### Setting up GitHub Secrets

For the CI/CD pipeline to work, configure these secrets in your GitHub repository:

1. Go to **Settings** → **Secrets and variables** → **Actions**
2. Add the following secrets:
   - `DOCKERHUB_USERNAME`: Your Docker Hub username
   - `DOCKERHUB_TOKEN`: Docker Hub access token

---

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Development Guidelines

- Follow PEP 8 style guide for Python code
- Write tests for new features
- Update documentation as needed
- Ensure all tests pass before submitting PR
- Run security scans locally before pushing

---

## 📖 Additional Documentation

- **[REFLECTION.md](./REFLECTION.md)**: Detailed reflection on development experiences and challenges
- **API Docs**: Available at `/docs` when running the application
- **Test Coverage**: View HTML report in `htmlcov/index.html` after running tests

---

## 📝 License

This project is licensed under the MIT License - see the LICENSE file for details.

---

## 👤 Author

**Cheng Xin**
- GitHub: [@chengxin199](https://github.com/chengxin199)
- Docker Hub: [chengxin199](https://hub.docker.com/u/chengxin199)

---

## 🙏 Acknowledgments

- FastAPI for the excellent web framework
- Playwright for robust E2E testing
- Docker for containerization
- The IS601 course for the learning opportunity

---

## 📞 Support

If you have any questions or issues:
1. Check the [Reflection Document](./REFLECTION.md) for common challenges and solutions
2. Review the API documentation at `/docs`
3. Open an issue on GitHub
4. Review Playwright test examples in `tests/e2e/`

---

**Last Updated**: December 1, 2025  
**Version**: 1.0.0  
**Course**: IS601 - Web Development  
**Assignment**: Module 13
