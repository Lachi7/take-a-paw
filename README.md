# 🐾 Take A Paw - Pet Adoption Platform

A modern, Tinder-style pet adoption web application that helps users find their perfect pet companion through an intuitive swiping interface and compatibility matching.

![Take A Paw](https://img.shields.io/badge/Flask-2.3.3-green) ![Python](https://img.shields.io/badge/Python-3.12-blue) ![PostgreSQL](https://img.shields.io/badge/PostgreSQL-Neon-orange) ![Docker](https://img.shields.io/badge/Docker-Enabled-blue) ![CI/CD](https://img.shields.io/badge/CI/CD-GitHub%20Actions-yellow)

## Live Application:
-[https://take-a-paw-1.onrender.com/](https://take-a-paw-1.onrender.com/)


## ✨ Features

### 🎯 Core Functionality
- **Tinder-style Swiping Interface** - Swipe right to like, left to skip pets
- **Smart Compatibility Quiz** - Personalized pet recommendations based on lifestyle
- **Favorites System** - Save and manage pets you're interested in
- **Advanced Search** - Filter pets by species, breed, location, and more
- **User Profiles** - Complete user management with contact preferences

### 🛠 Admin Features
- **Admin Dashboard** - Comprehensive statistics and management
- **Pet Management** - Add, edit, and manage pet listings
- **Adoption Tracking** - Monitor adoption applications and status

### 🔧 Technical Features
- **Responsive Design** - Works seamlessly on desktop and mobile
- **Real-time Health Monitoring** - Built-in health checks and status endpoints
- **Automated CI/CD** - Full GitHub Actions pipeline with testing and deployment
- **Containerized** - Docker support for easy deployment
- **PostgreSQL Database** - Production-ready database with Neon

## 🚀 Quick Start

### Prerequisites
- Python 3.10+
- PostgreSQL database (or Neon account)
- Git

### Local Development

```bash
# Clone the repository
git clone https://github.com/your-username/take-a-paw.git
cd take-a-paw

# Set up virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Set up environment variables
cp .env.example .env
# Edit .env with your database credentials

# Initialize database
cd src
flask db upgrade
python seed.py

# Run the application
python run.py
```

Visit `http://localhost:5000` to see your application running!

### Docker Deployment

```bash
# Build the image
docker build -t takeapaw .

# Run the container
docker run -p 5000:5000 --env-file .env takeapaw
```

## 🗄 Database Setup

### Using Neon PostgreSQL (Recommended)
1. Create account at [neon.tech](https://neon.tech)
2. Create new project and database
3. Get connection string from Neon dashboard
4. Set `DATABASE_URL` in your `.env` file

### Local PostgreSQL
```bash
# Install PostgreSQL
sudo apt-get install postgresql postgresql-contrib

# Create database and user
sudo -u postgres psql
CREATE DATABASE takeapaw;
CREATE USER takeapaw_user WITH PASSWORD 'your_password';
GRANT ALL PRIVILEGES ON DATABASE takeapaw TO takeapaw_user;
```

## 🏗 Project Structure

```
take-a-paw/
├── .github/workflows/
│   ├── ci.yml              # Continuous Integration
│   └── cd.yml              # Continuous Delivery
├── src/
│   ├── app/
│   │   ├── routes/         # Flask blueprints
│   │   │   ├── auth.py     # Authentication routes
│   │   │   ├── pets.py     # Pet management routes
│   │   │   ├── quiz.py     # Compatibility quiz routes
│   │   │   ├── admin.py    # Admin dashboard routes
│   │   │   └── system.py   # System health routes
│   │   ├── templates/      # Jinja2 templates
│   │   ├── static/         # CSS, JS, images
│   │   ├── models.py       # Database models
│   │   └── db.py           # Database configuration
│   ├── tests/              # Test suite
│   ├── run.py              # Application entry point
│   └── seed.py             # Database seeding
├── Dockerfile              # Container configuration
├── render.yaml             # Render deployment config
├── requirements.txt        # Python dependencies
└── README.md              # This file
```

## 🧪 Testing

### Running Tests
```bash
# Run all tests
cd src
pytest ../tests/ -v

# Run with coverage
pytest ../tests/ --cov=app --cov-report=html

# Run specific test categories
pytest ../tests/test_app.py::TestBasicRoutes -v
pytest ../tests/test_app.py::TestAPIRoutes -v
```

### Test Coverage
The test suite includes:
- ✅ Route testing (homepage, swiping, quiz, admin)
- ✅ API endpoint testing
- ✅ Database model testing
- ✅ Authentication testing
- ✅ Error handling testing

## 🔧 API Endpoints

### Public Endpoints
- `GET /` - Homepage with swiping interface
- `GET /health` - Health check
- `GET /api/status` - API status
- `GET /quiz` - Compatibility quiz
- `GET /pets` - List all available pets (JSON API)
- `POST /quiz/results` - Get pet matches based on quiz

### User Endpoints
- `POST /login` - User authentication
- `GET /favorites` - User's favorite pets
- `POST /pets/<id>/favorite` - Toggle favorite status
- `GET /me/listings` - User's pet listings

### Admin Endpoints
- `GET /admin` - Admin dashboard
- `GET /admin/pets` - Pet management
- `POST /admin/pets/<id>/toggle-adopted` - Toggle adoption status

## 🚀 Deployment

### GitHub Actions CI/CD
The project includes automated CI/CD pipelines:

- **CI Pipeline** (`ci.yml`): Runs on every push/PR
  - Automated testing
  - Code quality checks
  - Build verification

- **CD Pipeline** (`cd.yml`): Runs on main branch
  - Docker image building
  - Container registry push (GHCR)
  - Automated deployment

### Render Deployment
```yaml
# render.yaml
services:
  - type: web
    name: takeapaw
    env: python
    plan: free
    buildCommand: pip install -r requirements.txt
    startCommand: cd src && gunicorn run:app
    healthCheckPath: /health
    autoDeploy: true
```

### Environment Variables
```bash
# .env.example
DATABASE_URL=postgresql://username:password@host:port/database
SECRET_KEY=your-super-secret-key-here
FLASK_ENV=production
```

## 📊 Monitoring & Health

### Built-in Health Checks
- `GET /health` - Basic service health
- `GET /health/db` - Database connectivity
- `GET /api/status` - Comprehensive API status
- `GET /debug` - Development debugging information

### External Monitoring
- **UptimeRobot** - External uptime monitoring
- **Render Logs** - Application logging and error tracking
- **Database Metrics** - PostgreSQL performance monitoring

## 🤝 Contributing

### Development Workflow
1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Code Standards
- Follow PEP 8 for Python code
- Write tests for new functionality
- Update documentation for changes
- Use meaningful commit messages

## 🐛 Troubleshooting

### Common Issues

**Database Connection Issues**
```bash
# Test database connection
python -c "
import os
import psycopg2
try:
    conn = psycopg2.connect(os.getenv('DATABASE_URL'))
    print('✅ Database connection successful')
    conn.close()
except Exception as e:
    print(f'❌ Connection failed: {e}')
"
```

**Migration Issues**
```bash
cd src
flask db init
flask db migrate -m "Initial migration"
flask db upgrade
```

**Test Data Cleanup**
```bash
cd src
python -c "
from app import create_app
from app.models import Pet
app = create_app()
with app.app_context():
    # Mark test pets as adopted
    test_pets = Pet.query.filter(Pet.name.ilike('%test%')).all()
    for pet in test_pets:
        pet.adopted = True
    from app.db import db
    db.session.commit()
    print(f'Marked {len(test_pets)} test pets as adopted')
"
```

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👥 Team

- **Your Name** - Lead Developer
- **Team Member 2** - Backend Development
- **Team Member 3** - Frontend Development

## 🙏 Acknowledgments

- **Flask** team for the excellent web framework
- **Neon** for PostgreSQL hosting
- **Render** for deployment platform
- **Unsplash** for pet images
- All the open-source libraries that made this project possible

---

<div align="center">

**Made with ❤️ for animals in need of loving homes**

[Report Bug](https://github.com/your-username/take-a-paw/issues) · [Request Feature](https://github.com/your-username/take-a-paw/issues)

</div>
