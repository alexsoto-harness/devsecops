# DevSecOps Demo Application

A full-stack banking application demonstrating modern DevSecOps practices with Harness CI/CD, featuring comprehensive security scanning, automated testing, and Kubernetes deployment.

## 🏗️ Architecture

This application consists of three main components:

- **Frontend**: Angular 17 web application with Bootstrap UI and Harness Feature Flags integration
- **Backend**: Django 5.0 REST API with JWT authentication and Swagger documentation
- **Infrastructure**: Kubernetes-based deployment with Helm charts

## 🚀 Features

### Application Features
- User authentication and authorization (JWT)
- Banking operations (accounts, transfers, payments)
- Mortgage and loan management
- Investment portfolio tracking
- Credit score monitoring
- Transaction history and statements
- Bill payment scheduling
- Multi-factor authentication support

### DevSecOps Features
- **Continuous Integration**: Automated build and test pipeline
- **Test Intelligence**: Smart test selection with pytest
- **Security Scanning**:
  - OWASP Dependency Check
  - OSV Scanner for vulnerability detection
  - Aqua Trivy container scanning
  - DAST (Dynamic Application Security Testing)
- **SBOM Generation**: SPDX-JSON format
- **Container Registry**: Docker Hub integration
- **Deployment Strategies**:
  - Rolling deployment for frontend
  - Canary deployment with verification for backend
- **Continuous Verification**: Automated deployment validation

## 📋 Prerequisites

- Docker and Docker Compose
- Python 3.9+
- Node.js 18+ and npm
- Kubernetes cluster (for deployment)
- Harness account (for CI/CD pipeline)

## 🛠️ Local Development

### Backend Setup

1. Navigate to the backend directory:
```bash
cd backend
```

2. Create a virtual environment:
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. Install dependencies:
```bash
pip install -r requirements.txt
```

4. Run migrations:
```bash
python manage.py migrate
```

5. Start the development server:
```bash
python manage.py runserver
```

The backend API will be available at `http://localhost:8000`

### Frontend Setup

1. Navigate to the frontend directory:
```bash
cd frontend-app/harness-webapp
```

2. Install dependencies:
```bash
npm install
```

3. Start the development server:
```bash
npm start
```

The frontend will be available at `http://localhost:4200`

### Running Tests

Execute the test suite:
```bash
cd python-tests
pytest
```

## 🐳 Docker Deployment

### Build Backend Container
```bash
cd backend
docker build -t devsecops-backend .
```

### Build Frontend Container
```bash
cd frontend-app/harness-webapp
docker build -t devsecops-frontend .
```

## ☸️ Kubernetes Deployment

The application includes Helm charts for Kubernetes deployment:

```bash
# Deploy backend
helm install backend ./harness-deploy/backend

# Deploy frontend
helm install frontend ./harness-deploy/frontend
```

## 🔄 CI/CD Pipeline

The application uses Harness for continuous integration and deployment. The pipeline includes:

### Build Stage
1. **Test Intelligence**: Runs pytest with intelligent test selection
2. **Compile**: Application compilation using org template
3. **Security Scanning** (Parallel):
   - OWASP dependency scanning
   - OSV vulnerability scanning
4. **Container Build**: Docker image build and push to registry
5. **Container Scanning**: Aqua Trivy scan with SBOM generation

### Deployment Stages
1. **Frontend Deployment**: Rolling deployment to Kubernetes
2. **Backend Deployment** (Parallel with DAST):
   - Canary deployment with 1 instance
   - Continuous verification (5 min duration)
   - Manual intervention on verification failure
   - Full rolling deployment after verification
3. **DAST Scans**: Dynamic security testing

### Pipeline Configuration
- **Project**: Platform_Engineering
- **Organization**: demo
- **Repository**: org.devsecops
- **Live URL**: https://devsecops.harness-demo.site

## 🔐 Security

### Environment Variables
The following environment variables are used in production:

**Backend:**
- `SECRET_KEY`: Django secret key (must be set in production)
- `DEBUG`: Set to `False` in production
- `HOSTNAME`: Deployment hostname
- `SERVICE_NAME`: Service identifier
- `EXECUTION_USER`: Deployment user
- `LAST_EXECUTION_ID`: Last pipeline execution ID
- `APPLICATION_VERSION`: Application version
- `ARTIFACT_VERSION`: Artifact version

**Frontend:**
- Feature flag SDK configuration
- API endpoint configuration

### Security Best Practices
⚠️ **Important**: The current configuration includes hardcoded secrets and debug mode enabled. Before deploying to production:

1. Move `SECRET_KEY` to environment variables
2. Set `DEBUG = False`
3. Configure `ALLOWED_HOSTS` properly
4. Use environment-specific configuration
5. Enable HTTPS/SSL
6. Configure proper CORS settings
7. Review and update security middleware

## 📊 API Documentation

The backend API includes Swagger/OpenAPI documentation:
- Swagger UI: `http://localhost:8000/swagger/`
- ReDoc: `http://localhost:8000/redoc/`

## 🧪 Testing

The project includes comprehensive test coverage:
- **Credit Score Tests**: `python-tests/test_credit_score.py`
- **Mortgage Tests**: `python-tests/test_mortgages.py`
- **Payment Tests**: `python-tests/test_payments.py`

Run all tests:
```bash
cd python-tests
pytest -v
```

## 📦 Technology Stack

### Frontend
- Angular 17
- TypeScript 5.3
- Bootstrap 5.3
- NgBootstrap
- Harness Feature Flags SDK
- RxJS

### Backend
- Django 5.0
- Django REST Framework
- djangorestframework-simplejwt
- django-cors-headers
- drf-yasg (Swagger/OpenAPI)
- Gunicorn
- PostgreSQL support (psycopg2)
- scikit-learn (ML capabilities)

### DevOps & Security
- Docker
- Kubernetes
- Helm
- Harness CI/CD
- OWASP Dependency Check
- OSV Scanner
- Aqua Trivy
- pytest

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📝 License

This project is a demonstration application for DevSecOps practices.

## 🔗 Resources

- [Harness Documentation](https://docs.harness.io/)
- [Django Documentation](https://docs.djangoproject.com/)
- [Angular Documentation](https://angular.io/docs)
- [Kubernetes Documentation](https://kubernetes.io/docs/)

## 📧 Support

For questions or issues, please open an issue in the repository or contact the development team.

---

**Note**: This is a demo application for educational and workshop purposes. Review and update security configurations before using in production environments.