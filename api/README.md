# AirBnB Clone v3 - RESTful API

This directory contains the RESTful API implementation for the AirBnB Clone v3 project. The API is built using Flask and provides full CRUD operations for all AirBnB objects through HTTP endpoints.

## 🚀 Overview

The API serves as the backend service for the AirBnB clone application, enabling:
- HTTP-based communication with the data models
- JSON data exchange format
- RESTful architecture principles
- Cross-Origin Resource Sharing (CORS) support
- Standardized error handling

## 📁 Directory Structure

```
api/
├── v1/                                    # API version 1
│   ├── app.py                            # Main Flask application
│   ├── __init__.py                       # Package initialization
│   └── views/                            # API endpoint handlers
│       ├── __init__.py                   # Views package init with Blueprint
│       ├── index.py                      # Status and statistics endpoints
│       ├── states.py                     # State resource endpoints
│       ├── cities.py                     # City resource endpoints
│       ├── amenities.py                  # Amenity resource endpoints
│       ├── users.py                      # User resource endpoints
│       ├── places.py                     # Place resource endpoints
│       ├── places_reviews.py             # Review resource endpoints
│       └── places_amenities.py           # Place-Amenity relationship endpoints
├── AirBnB_clone_v3.postman_collection.json  # Postman testing collection
├── Dockerfile                            # Docker configuration for API
└── README.md                             # This file
```

## 🛠️ Setup and Running

### Prerequisites
- Python 3.4+
- Flask and dependencies (see requirements.txt)
- Optional: MySQL database

### Environment Variables
```bash
export HBNB_API_HOST=0.0.0.0
export HBNB_API_PORT=5000
export HBNB_TYPE_STORAGE=db  # or 'file' for file storage
export HBNB_MYSQL_USER=hbnb_dev
export HBNB_MYSQL_PWD=hbnb_dev_pwd
export HBNB_MYSQL_HOST=localhost
export HBNB_MYSQL_DB=hbnb_dev_db
```

### Running the API
```bash
# From project root directory
python3 -m api.v1.app

# Or with environment variables
HBNB_API_HOST=0.0.0.0 HBNB_API_PORT=5000 python3 -m api.v1.app
```

### Using Docker
```bash
# Build the API container
docker build -t airbnb-api .

# Run with Docker Compose (from project root)
docker-compose up api
```

## 📚 API Endpoints

### Base URL
```
http://localhost:5000/api/v1
```

### Status Endpoints
- `GET /status` - Returns API status
- `GET /stats` - Returns object count statistics

### Resource Endpoints

#### States
- `GET /states` - List all states
- `POST /states` - Create a new state
- `GET /states/<state_id>` - Get state by ID
- `PUT /states/<state_id>` - Update state by ID
- `DELETE /states/<state_id>` - Delete state by ID

#### Cities
- `GET /states/<state_id>/cities` - List cities in a state
- `POST /states/<state_id>/cities` - Create city in a state
- `GET /cities/<city_id>` - Get city by ID
- `PUT /cities/<city_id>` - Update city by ID
- `DELETE /cities/<city_id>` - Delete city by ID

#### Amenities
- `GET /amenities` - List all amenities
- `POST /amenities` - Create a new amenity
- `GET /amenities/<amenity_id>` - Get amenity by ID
- `PUT /amenities/<amenity_id>` - Update amenity by ID
- `DELETE /amenities/<amenity_id>` - Delete amenity by ID

#### Users
- `GET /users` - List all users
- `POST /users` - Create a new user
- `GET /users/<user_id>` - Get user by ID
- `PUT /users/<user_id>` - Update user by ID
- `DELETE /users/<user_id>` - Delete user by ID

#### Places
- `GET /cities/<city_id>/places` - List places in a city
- `POST /cities/<city_id>/places` - Create place in a city
- `GET /places/<place_id>` - Get place by ID
- `PUT /places/<place_id>` - Update place by ID
- `DELETE /places/<place_id>` - Delete place by ID

#### Reviews
- `GET /places/<place_id>/reviews` - List reviews for a place
- `POST /places/<place_id>/reviews` - Create review for a place
- `GET /reviews/<review_id>` - Get review by ID
- `PUT /reviews/<review_id>` - Update review by ID
- `DELETE /reviews/<review_id>` - Delete review by ID

#### Place-Amenity Relationships
- `GET /places/<place_id>/amenities` - List amenities for a place
- `POST /places/<place_id>/amenities/<amenity_id>` - Link amenity to place
- `DELETE /places/<place_id>/amenities/<amenity_id>` - Unlink amenity from place

## 🔧 Request/Response Format

### Request Headers
```
Content-Type: application/json
```

### Response Format
All responses are in JSON format:

#### Success Response
```json
{
  "id": "uuid-string",
  "created_at": "2023-01-01T12:00:00.000000",
  "updated_at": "2023-01-01T12:00:00.000000",
  "field1": "value1",
  "field2": "value2"
}
```

#### Error Response
```json
{
  "error": "Error description"
}
```

### HTTP Status Codes
- `200` - OK (successful GET, PUT)
- `201` - Created (successful POST)
- `400` - Bad Request (invalid JSON, missing required fields)
- `404` - Not Found (resource doesn't exist)
- `500` - Internal Server Error

## 🧪 Testing

### Using Postman
Import the provided Postman collection:
```bash
# File: AirBnB_clone_v3.postman_collection.json
```

### Using curl
```bash
# Test API status
curl -X GET http://localhost:5000/api/v1/status

# Create a new state
curl -X POST http://localhost:5000/api/v1/states \
  -H "Content-Type: application/json" \
  -d '{"name": "California"}'

# Get all states
curl -X GET http://localhost:5000/api/v1/states
```

### Using Python requests
```python
import requests

base_url = "http://localhost:5000/api/v1"

# Test API status
response = requests.get(f"{base_url}/status")
print(response.json())  # {"status": "OK"}

# Create a state
new_state = {"name": "Texas"}
response = requests.post(f"{base_url}/states", json=new_state)
state = response.json()
```

## 🏗️ Architecture

### Flask Application Structure
- **app.py**: Main Flask application with CORS configuration
- **views/__init__.py**: Blueprint registration and view imports
- **views/*.py**: Individual resource handlers

### Error Handling
- Custom 404 error handler
- Automatic JSON error responses
- Input validation for required fields

### CORS Configuration
- Allows requests from any origin (0.0.0.0)
- Supports all HTTP methods
- Enables cross-origin API access

## 🔒 Security Notes

⚠️ **Important**: This API is designed for educational purposes and lacks production security features:
- No authentication/authorization
- No rate limiting
- No input sanitization beyond basic validation
- CORS allows all origins

For production use, implement:
- JWT or OAuth authentication
- Rate limiting middleware
- Input validation and sanitization
- Restricted CORS origins
- HTTPS encryption

## 🐛 Known Limitations

- No pagination for large result sets
- No query filtering or sorting
- No API versioning beyond URL structure
- No caching implementation
- No request logging

## 🤝 Contributing

When contributing to the API:
1. Follow RESTful principles
2. Add appropriate error handling
3. Update this documentation
4. Add tests for new endpoints
5. Ensure CORS compatibility

---

For more information, see the main project [README](../README.md).
