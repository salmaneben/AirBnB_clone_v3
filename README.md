# AirBnB Clone v3 - RESTful API

This project is the third iteration of the AirBnB clone project at ALX/Holberton School. It extends the previous console-based application by adding a RESTful API built with Flask, enabling web service interactions with the AirBnB objects. The project demonstrates fundamental concepts of higher-level programming, web development, API design, and database integration.

> 📖 **Comprehensive Documentation**: This project includes detailed documentation for each component. See [Component Documentation](#component-documentation) for links to specific guides.

## 🚀 Project Overview

The AirBnB Clone v3 includes:
- **Command Line Interface (Console)**: Interactive command interpreter for object management
- **RESTful API**: Flask-based web service with full CRUD operations
- **Database Integration**: Support for both file storage and MySQL database
- **Web Application**: Flask web interface for displaying AirBnB data
- **Static Web Pages**: HTML/CSS templates for the frontend
- **Testing Suite**: Comprehensive unit tests for all components
- **Deployment Tools**: Fabric scripts and Docker configuration

## 📋 Table of Contents

* [Features](#features)
* [Architecture](#architecture)
* [Environment](#environment)
* [Installation](#installation)
* [Configuration](#configuration)
* [Usage](#usage)
* [API Documentation](#api-documentation)
* [File Structure](#file-structure)
* [Component Documentation](#component-documentation)
* [Testing](#testing)
* [Deployment](#deployment)
* [Examples](#examples)
* [Contributing](#contributing)
* [Authors](#authors)
* [License](#license)

## ✨ Features

### Core Functionalities
- Create, read, update, and delete (CRUD) operations for all objects
- Object-relational mapping (ORM) with SQLAlchemy
- RESTful API endpoints for web service integration
- Database storage with MySQL support
- File-based storage system as fallback
- Flask web application with Jinja2 templates
- Cross-Origin Resource Sharing (CORS) support
- Comprehensive error handling and validation

### Supported Objects
- **User**: User account management
- **State**: Geographic states/regions
- **City**: Cities within states
- **Amenity**: Property amenities (WiFi, pool, etc.)
- **Place**: Rental properties/listings
- **Review**: User reviews for places

## 🏗️ Architecture

The project follows a modular architecture:

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Frontend      │    │   RESTful API   │    │   Storage       │
│   (HTML/CSS/JS) │◄──►│   (Flask)       │◄──►│   (MySQL/File)  │
└─────────────────┘    └─────────────────┘    └─────────────────┘
         ▲                       ▲                       ▲
         │                       │                       │
         ▼                       ▼                       ▼
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Web Flask     │    │   Console       │    │   Models        │
│   Application   │    │   (CLI)         │    │   (ORM)         │
└─────────────────┘    └─────────────────┘    └─────────────────┘
```

## 🌍 Environment

- **OS**: Ubuntu 14.04 LTS or later
- **Python**: 3.4.3 or higher
- **Database**: MySQL 5.7 (optional, with file storage fallback)
- **Web Server**: Flask development server or production WSGI server

## 🛠️ Installation

### Prerequisites
```bash
sudo apt-get update
sudo apt-get install python3 python3-pip mysql-server
```

### Clone Repository
```bash
git clone https://github.com/salmaneben/AirBnB_clone_v3.git
cd AirBnB_clone_v3
```

### Install Dependencies
```bash
pip3 install -r requirements.txt
```

### MySQL Setup (Optional)
```bash
# Create development database
mysql -u root -p < setup_mysql_dev.sql

# Create test database
mysql -u root -p < setup_mysql_test.sql
```

## ⚙️ Configuration

### Environment Variables

The application behavior can be configured using environment variables:

```bash
# Storage type (file or db)
export HBNB_TYPE_STORAGE=db

# MySQL database configuration
export HBNB_MYSQL_USER=hbnb_dev
export HBNB_MYSQL_PWD=hbnb_dev_pwd
export HBNB_MYSQL_HOST=localhost
export HBNB_MYSQL_DB=hbnb_dev_db

# API configuration
export HBNB_API_HOST=0.0.0.0
export HBNB_API_PORT=5000

# Environment type (development/test/production)
export HBNB_ENV=dev
```

## 📖 Usage

### Command Line Interface (Console)

The console provides an interactive command interpreter for managing objects:

```bash
# Run interactively
./console.py

# Run non-interactively
echo "help" | ./console.py
```

#### Available Commands

| Command | Description | Usage |
|---------|-------------|-------|
| `help` | Display help information | `help [command]` |
| `quit/EOF` | Exit the console | `quit` |
| `create` | Create a new instance | `create <class_name>` |
| `show` | Display an instance | `show <class_name> <id>` |
| `destroy` | Delete an instance | `destroy <class_name> <id>` |
| `all` | Display all instances | `all [class_name]` |
| `update` | Update instance attributes | `update <class_name> <id> <attr> <value>` |
| `count` | Count instances | `count <class_name>` |

### RESTful API

Start the API server:

```bash
# With file storage
python3 -m api.v1.app

# With database storage
HBNB_TYPE_STORAGE=db HBNB_MYSQL_USER=hbnb_dev HBNB_MYSQL_PWD=hbnb_dev_pwd HBNB_MYSQL_HOST=localhost HBNB_MYSQL_DB=hbnb_dev_db python3 -m api.v1.app
```

### Web Application

Start the Flask web application:

```bash
python3 -m web_flask.0-hello_route
```

## 📚 API Documentation

### Base URL
```
http://localhost:5000/api/v1
```

### Authentication
Currently, the API does not require authentication.

### Common Headers
```
Content-Type: application/json
```

### Endpoints

#### Status & Statistics
- `GET /api/v1/status` - API status
- `GET /api/v1/stats` - Object statistics

#### States
- `GET /api/v1/states` - List all states
- `POST /api/v1/states` - Create a new state
- `GET /api/v1/states/<state_id>` - Get a specific state
- `PUT /api/v1/states/<state_id>` - Update a state
- `DELETE /api/v1/states/<state_id>` - Delete a state

#### Cities
- `GET /api/v1/states/<state_id>/cities` - List cities in a state
- `POST /api/v1/states/<state_id>/cities` - Create city in a state
- `GET /api/v1/cities/<city_id>` - Get a specific city
- `PUT /api/v1/cities/<city_id>` - Update a city
- `DELETE /api/v1/cities/<city_id>` - Delete a city

#### Amenities
- `GET /api/v1/amenities` - List all amenities
- `POST /api/v1/amenities` - Create a new amenity
- `GET /api/v1/amenities/<amenity_id>` - Get a specific amenity
- `PUT /api/v1/amenities/<amenity_id>` - Update an amenity
- `DELETE /api/v1/amenities/<amenity_id>` - Delete an amenity

#### Users
- `GET /api/v1/users` - List all users
- `POST /api/v1/users` - Create a new user
- `GET /api/v1/users/<user_id>` - Get a specific user
- `PUT /api/v1/users/<user_id>` - Update a user
- `DELETE /api/v1/users/<user_id>` - Delete a user

#### Places
- `GET /api/v1/cities/<city_id>/places` - List places in a city
- `POST /api/v1/cities/<city_id>/places` - Create place in a city
- `GET /api/v1/places/<place_id>` - Get a specific place
- `PUT /api/v1/places/<place_id>` - Update a place
- `DELETE /api/v1/places/<place_id>` - Delete a place

#### Reviews
- `GET /api/v1/places/<place_id>/reviews` - List reviews for a place
- `POST /api/v1/places/<place_id>/reviews` - Create review for a place
- `GET /api/v1/reviews/<review_id>` - Get a specific review
- `PUT /api/v1/reviews/<review_id>` - Update a review
- `DELETE /api/v1/reviews/<review_id>` - Delete a review

### Response Format

#### Success Response
```json
{
  "id": "uuid",
  "created_at": "ISO-8601 datetime",
  "updated_at": "ISO-8601 datetime",
  ...
}
```

#### Error Response
```json
{
  "error": "Error description"
}
```

### HTTP Status Codes
- `200` - OK
- `201` - Created
- `400` - Bad Request
- `404` - Not Found
- `500` - Internal Server Error

## 📁 File Structure

```
AirBnB_clone_v3/
├── api/                              # RESTful API
│   ├── v1/
│   │   ├── app.py                   # Flask application
│   │   └── views/                   # API endpoints
│   │       ├── __init__.py
│   │       ├── index.py             # Status & stats
│   │       ├── states.py            # States endpoints
│   │       ├── cities.py            # Cities endpoints
│   │       ├── amenities.py         # Amenities endpoints
│   │       ├── users.py             # Users endpoints
│   │       ├── places.py            # Places endpoints
│   │       └── places_reviews.py    # Reviews endpoints
│   ├── AirBnB_clone_v3.postman_collection.json
│   └── Dockerfile
├── models/                          # Data models
│   ├── __init__.py                  # Storage initialization
│   ├── base_model.py                # Base model class
│   ├── user.py                      # User model
│   ├── state.py                     # State model
│   ├── city.py                      # City model
│   ├── amenity.py                   # Amenity model
│   ├── place.py                     # Place model
│   ├── review.py                    # Review model
│   └── engine/                      # Storage engines
│       ├── file_storage.py          # File-based storage
│       └── db_storage.py            # Database storage
├── web_flask/                       # Flask web application
│   ├── 0-hello_route.py            # Basic routes
│   ├── 7-states_list.py            # States listing
│   ├── 8-cities_by_states.py       # Cities by states
│   ├── 10-hbnb_filters.py          # Filters page
│   └── templates/                   # Jinja2 templates
├── web_static/                      # Static web files
│   ├── styles/                      # CSS files
│   ├── images/                      # Image assets
│   └── *.html                       # Static HTML pages
├── tests/                           # Unit tests
│   ├── test_console.py              # Console tests
│   └── test_models/                 # Model tests
├── console.py                       # Command line interface
├── 0-setup_web_static.sh           # Web server setup script
├── 1-pack_web_static.py            # Web static packaging
├── 2-do_deploy_web_static.py       # Deployment script
├── 3-deploy_web_static.py          # Full deployment
├── requirements.txt                 # Python dependencies
├── setup_mysql_dev.sql             # Development database setup
├── setup_mysql_test.sql            # Test database setup
├── docker-compose.yml              # Docker configuration
├── Dockerfile                       # Docker image definition
└── AUTHORS                          # Project contributors
```

## 📚 Component Documentation

Each major component of the project has its own detailed documentation:

### 🔌 [API Documentation](api/README.md)
Complete RESTful API documentation including:
- All available endpoints with examples
- Request/response formats and status codes
- Authentication and CORS configuration
- Postman collection and testing guides
- Docker deployment instructions

### 💾 [Models Documentation](models/README.md)
Comprehensive data models and storage documentation:
- Object-relational mapping (ORM) with SQLAlchemy
- Model relationships and database schema
- File storage vs database storage comparison
- Usage examples and configuration guides
- Adding new models instructions

### 🧪 [Testing Documentation](tests/README.md)
Complete testing suite documentation:
- Unit tests for all components
- Running tests with different storage engines
- Coverage analysis and reporting
- Test writing best practices and guidelines
- Troubleshooting common test issues

### 🌐 [Web Flask Documentation](web_flask/README.md)
Flask web applications documentation:
- Progressive development from basic to advanced routes
- Template integration and database connectivity
- Environment setup and configuration
- All available routes and their purposes

### 🎨 [Static Web Documentation](web_static/README.md)
Static web files and frontend documentation:
- HTML/CSS development progression
- Responsive design and accessibility features
- Image assets and styling architecture
- Deployment and optimization guides

## 🧪 Testing

### Running All Tests
```bash
# Run all tests
python3 -m unittest discover tests

# Run specific test file
python3 -m unittest tests.test_models.test_base_model

# Run with verbose output
python3 -m unittest discover tests -v
```

### Testing with Different Storage Types
```bash
# Test with file storage
python3 -m unittest discover tests

# Test with database storage
HBNB_TYPE_STORAGE=db HBNB_MYSQL_USER=hbnb_test HBNB_MYSQL_PWD=hbnb_test_pwd HBNB_MYSQL_HOST=localhost HBNB_MYSQL_DB=hbnb_test_db python3 -m unittest discover tests
```

### Test Coverage
The test suite includes:
- Unit tests for all model classes
- Console command testing
- API endpoint testing
- File storage engine testing
- Database storage engine testing
- PEP8 style compliance testing

## 🚀 Deployment

### Using Fabric (Development)
```bash
# Package web static files
python3 1-pack_web_static.py

# Deploy to server
python3 2-do_deploy_web_static.py <archive_path>

# Full deployment (pack + deploy)
python3 3-deploy_web_static.py
```

### Using Docker
```bash
# Build and run with Docker Compose
docker-compose up --build

# Access API
curl http://localhost:5000/api/v1/status
```

### Manual Deployment
```bash
# Set up web server (Ubuntu/Debian)
sudo ./0-setup_web_static.sh

# Configure Nginx (example)
sudo ln -sf /etc/nginx/sites-available/default /etc/nginx/sites-enabled/default
sudo service nginx restart
```

## 📖 Examples

### Console Usage
```bash
$ ./console.py
(hbnb) help

Documented commands (type help <topic>):
========================================
EOF  all  create  destroy  help  quit  show  update

(hbnb) create User
a42ee380-c959-450e-ad29-c840a898cfce
(hbnb) show User a42ee380-c959-450e-ad29-c840a898cfce
[User] (a42ee380-c959-450e-ad29-c840a898cfce) {'id': 'a42ee380-c959-450e-ad29-c840a898cfce', 'created_at': datetime.datetime(2017, 9, 28, 9, 50, 46, 772167), 'updated_at': datetime.datetime(2017, 9, 28, 9, 50, 46, 772123)}
(hbnb) all User
["[User] (a42ee380-c959-450e-ad29-c840a898cfce) {'id': 'a42ee380-c959-450e-ad29-c840a898cfce', 'created_at': datetime.datetime(2017, 9, 28, 9, 50, 46, 772167), 'updated_at': datetime.datetime(2017, 9, 28, 9, 50, 46, 772123)}"]
(hbnb) update User a42ee380-c959-450e-ad29-c840a898cfce email "test@example.com"
(hbnb) show User a42ee380-c959-450e-ad29-c840a898cfce
[User] (a42ee380-c959-450e-ad29-c840a898cfce) {'id': 'a42ee380-c959-450e-ad29-c840a898cfce', 'created_at': datetime.datetime(2017, 9, 28, 9, 50, 46, 772167), 'updated_at': datetime.datetime(2017, 9, 28, 9, 51, 17, 444147), 'email': 'test@example.com'}
(hbnb) quit
```

### API Usage
```bash
# Get API status
curl -X GET http://localhost:5000/api/v1/status
{"status": "OK"}

# Get statistics
curl -X GET http://localhost:5000/api/v1/stats
{"amenities": 47, "cities": 36, "places": 154, "reviews": 718, "states": 27, "users": 31}

# Create a new state
curl -X POST http://localhost:5000/api/v1/states \
  -H "Content-Type: application/json" \
  -d '{"name": "California"}'

# Get all states
curl -X GET http://localhost:5000/api/v1/states

# Get a specific state
curl -X GET http://localhost:5000/api/v1/states/<state_id>

# Update a state
curl -X PUT http://localhost:5000/api/v1/states/<state_id> \
  -H "Content-Type: application/json" \
  -d '{"name": "New California"}'

# Delete a state
curl -X DELETE http://localhost:5000/api/v1/states/<state_id>
```

### Python Integration
```python
import requests

# API base URL
base_url = "http://localhost:5000/api/v1"

# Get all states
response = requests.get(f"{base_url}/states")
states = response.json()

# Create a new state
new_state = {
    "name": "New York"
}
response = requests.post(f"{base_url}/states", json=new_state)
created_state = response.json()

# Update the state
update_data = {
    "name": "New York State"
}
response = requests.put(f"{base_url}/states/{created_state['id']}", json=update_data)
updated_state = response.json()
```

## 🤝 Contributing

We welcome contributions to improve the AirBnB Clone v3 project! Here's how you can contribute:

### 🛠️ Development Process
1. **Fork the repository** from [GitHub](https://github.com/salmaneben/AirBnB_clone_v3)
2. **Create a feature branch** (`git checkout -b feature/amazing-feature`)
3. **Make your changes** following our coding standards
4. **Add tests** for new functionality (see [Testing Documentation](tests/README.md))
5. **Update documentation** as needed (component READMEs)
6. **Commit your changes** (`git commit -m 'Add some amazing feature'`)
7. **Push to the branch** (`git push origin feature/amazing-feature`)
8. **Open a Pull Request** with a clear description

### 📋 Coding Standards
- **PEP8 Compliance**: Follow Python style guidelines
- **Documentation**: Write comprehensive docstrings and comments
- **Testing**: Add unit tests for new features (90%+ coverage)
- **API Design**: Follow RESTful principles for API endpoints
- **Database**: Ensure compatibility with both file and database storage

### 🔍 Code Review Process
- All changes require review before merging
- Ensure all tests pass (both file and database storage)
- Update relevant documentation
- Follow the established project architecture

### 📝 Component-Specific Guidelines
- **API Changes**: Update [API Documentation](api/README.md)
- **Model Changes**: Update [Models Documentation](models/README.md)
- **New Tests**: Follow [Testing Documentation](tests/README.md)
- **Frontend Changes**: Update [Static Web Documentation](web_static/README.md)

### 🐛 Reporting Issues
- Use GitHub Issues for bug reports and feature requests
- Include detailed reproduction steps
- Specify environment details (OS, Python version, storage type)
- Add relevant logs and error messages

## 🐛 Known Issues

### Current Limitations
- **Security**: CORS configuration may need adjustment for production use
- **Performance**: Database connection pooling not implemented
- **API**: Rate limiting not implemented
- **Authentication**: Authentication and authorization not implemented
- **Caching**: No caching layer for improved performance
- **Logging**: Limited request/error logging functionality

### Production Considerations
⚠️ **Important**: This project is designed for educational purposes. For production deployment, consider implementing:
- JWT or OAuth authentication system
- Rate limiting and request throttling
- Input validation and sanitization
- HTTPS encryption and security headers
- Database connection pooling
- Comprehensive logging and monitoring
- Error tracking and alerting
- API versioning strategy

### Reporting Issues
If you encounter bugs or issues:
1. Check existing [GitHub Issues](https://github.com/salmaneben/AirBnB_clone_v3/issues)
2. Create a new issue with detailed reproduction steps
3. Include environment information and error logs
4. Suggest potential solutions if possible

## 📚 Additional Resources

### 📖 Documentation Links
- **[API Documentation](api/README.md)** - Complete RESTful API reference
- **[Models Documentation](models/README.md)** - Data models and storage engines
- **[Testing Documentation](tests/README.md)** - Comprehensive testing guide
- **[Web Flask Documentation](web_flask/README.md)** - Flask web applications
- **[Static Web Documentation](web_static/README.md)** - Frontend and styling

### 🛠️ Development Tools
- [Postman Collection](api/AirBnB_clone_v3.postman_collection.json) - Import for easy API testing
- [Database Schema](dev/AirBnb_DB_diagramm.jpg) - Visual representation of the data model
- [Docker Configuration](docker-compose.yml) - Container orchestration setup

### 🎓 Learning Resources
- [ALX/Holberton School](https://www.holbertonschool.com/) - Educational institution
- [Project Repository](https://github.com/salmaneben/AirBnB_clone_v3) - Source code and issues
- [Python Documentation](https://docs.python.org/3/) - Python language reference
- [Flask Documentation](https://flask.palletsprojects.com/) - Flask web framework
- [SQLAlchemy Documentation](https://docs.sqlalchemy.org/) - ORM documentation

## 🏆 Authors

### Original Authors
**ALX/Holberton School Project Foundation:**
- **Alexa Orrico** - [GitHub](https://github.com/alexaorrico) / [Twitter](https://twitter.com/alexa_orrico)  
- **Jennifer Huang** - [GitHub](https://github.com/jhuang10123) / [Twitter](https://twitter.com/earthtojhuang)
- **Joann Vuong** - Second part of AirBnB project development

### Current Maintainers
**AirBnB Clone v3 Development Team:**
- **Opeoluwa Adeyeri** - [adeyeriopeoluwa05@gmail.com](mailto:adeyeriopeoluwa05@gmail.com)
  - RESTful API development and integration
  - Database storage engine implementation
  - Testing framework and documentation
- **Blessing Nwakwuo** - [blessingnwakwuo@outlook.com](mailto:blessingnwakwuo@outlook.com)
  - Frontend development and styling
  - Flask web application development
  - Deployment and DevOps configuration

### Acknowledgments
- **ALX/Holberton School** - Educational guidance and project framework
- **Python Community** - Flask, SQLAlchemy, and testing libraries
- **Open Source Contributors** - Various tools and dependencies used

### Contributing
We welcome new contributors! See our [Contributing Guidelines](#contributing) for details on how to get involved.

## 📄 License

This project is licensed under the **Public Domain**. No copyright protection.

### License Details
- **Free to Use**: You may use this project for any purpose
- **Free to Modify**: You may modify and distribute the code
- **Free to Distribute**: You may share this project with others
- **No Warranty**: The project is provided "as is" without warranty

### Educational Use
This project is primarily intended for educational purposes as part of the ALX/Holberton School curriculum. Students and educators are encouraged to use, study, and modify the code for learning purposes.

### Attribution
While not required, attribution to the original authors and ALX/Holberton School is appreciated when using this project for educational or reference purposes.

---

<div align="center">

**Made with ❤️ at ALX/Holberton School**

[![ALX](https://img.shields.io/badge/ALX-Software_Engineering-blue)](https://www.alxafrica.com/)
[![Holberton](https://img.shields.io/badge/Holberton-School-red)](https://www.holbertonschool.com/)
[![Python](https://img.shields.io/badge/Python-3.4+-green)](https://www.python.org/)
[![Flask](https://img.shields.io/badge/Flask-Web_Framework-lightgrey)](https://flask.palletsprojects.com/)

</div> 
