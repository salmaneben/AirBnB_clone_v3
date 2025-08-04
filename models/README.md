# AirBnB Clone v3 - Data Models

This directory contains all the data models for the AirBnB Clone v3 project. The models implement both file-based and database storage using SQLAlchemy ORM, providing a flexible and scalable data layer.

## 🏗️ Overview

The models directory provides:
- **Object-Relational Mapping (ORM)** with SQLAlchemy
- **Dual Storage Support**: File storage and MySQL database
- **Base Model Pattern**: Common functionality for all models
- **Relationship Management**: Foreign keys and associations
- **Data Validation**: Type checking and constraints

## 📁 Directory Structure

```
models/
├── __init__.py                    # Storage engine initialization
├── base_model.py                  # Base model class with common functionality
├── user.py                        # User model (customers, hosts)
├── state.py                       # State/Region model
├── city.py                        # City model (belongs to state)
├── amenity.py                     # Amenity model (WiFi, pool, etc.)
├── place.py                       # Place/Property model (rentals)
├── review.py                      # Review model (user reviews of places)
└── engine/                        # Storage engines
    ├── __init__.py               # Engine package initialization
    ├── file_storage.py           # File-based storage engine
    └── db_storage.py             # Database storage engine
```

## 🎯 Model Relationships

```
┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│    User     │     │    State    │     │   Amenity   │
│             │     │             │     │             │
│ - id        │     │ - id        │     │ - id        │
│ - email     │     │ - name      │     │ - name      │
│ - password  │     └─────────────┘     └─────────────┘
│ - first_name│           │                     │
│ - last_name │           │                     │
└─────────────┘           │                     │
       │                  ▼                     │
       │            ┌─────────────┐             │
       │            │    City     │             │
       │            │             │             │
       │            │ - id        │             │
       │            │ - name      │             │
       │            │ - state_id  │             │
       │            └─────────────┘             │
       │                  │                     │
       ▼                  ▼                     │
┌─────────────┐     ┌─────────────┐             │
│   Review    │     │    Place    │◄────────────┘
│             │     │             │
│ - id        │     │ - id        │ (Many-to-Many)
│ - text      │     │ - name      │
│ - user_id   │     │ - city_id   │
│ - place_id  │     │ - user_id   │
└─────────────┘     │ - price     │
                    │ - latitude  │
                    │ - longitude │
                    └─────────────┘
```

## 🧱 Base Model

The `BaseModel` class provides common functionality for all models:

### Common Attributes
- `id` (String): Unique identifier (UUID4)
- `created_at` (DateTime): Creation timestamp
- `updated_at` (DateTime): Last modification timestamp

### Common Methods
- `__init__()`: Initialize instance with optional kwargs
- `__str__()`: String representation of the object
- `save()`: Update the `updated_at` timestamp and save to storage
- `to_dict()`: Convert instance to dictionary representation
- `delete()`: Delete instance from storage

### Storage Compatibility
- **File Storage**: Uses `to_dict()` for JSON serialization
- **Database Storage**: Uses SQLAlchemy columns and relationships

## 🏠 Individual Models

### User Model (`user.py`)
Represents users of the platform (both customers and hosts).

**Attributes:**
- `email` (String, 128): User's email address (unique, required)
- `password` (String, 128): Encrypted password (required)
- `first_name` (String, 128): User's first name
- `last_name` (String, 128): User's last name

**Relationships:**
- `places`: One-to-many with Place (user can own multiple places)
- `reviews`: One-to-many with Review (user can write multiple reviews)

### State Model (`state.py`)
Represents geographic states or regions.

**Attributes:**
- `name` (String, 128): State name (required)

**Relationships:**
- `cities`: One-to-many with City (state contains multiple cities)

### City Model (`city.py`)
Represents cities within states.

**Attributes:**
- `name` (String, 128): City name (required)
- `state_id` (String, 60): Foreign key to State (required)

**Relationships:**
- `state`: Many-to-one with State (city belongs to one state)
- `places`: One-to-many with Place (city contains multiple places)

### Amenity Model (`amenity.py`)
Represents amenities that places can offer.

**Attributes:**
- `name` (String, 128): Amenity name (required)

**Relationships:**
- `place_amenities`: Many-to-many with Place (amenities can be in multiple places)

### Place Model (`place.py`)
Represents rental properties or listings.

**Attributes:**
- `city_id` (String, 60): Foreign key to City (required)
- `user_id` (String, 60): Foreign key to User (owner, required)
- `name` (String, 128): Place name (required)
- `description` (String, 1024): Place description
- `number_rooms` (Integer): Number of rooms (default: 0)
- `number_bathrooms` (Integer): Number of bathrooms (default: 0)
- `max_guest` (Integer): Maximum guests (default: 0)
- `price_by_night` (Integer): Price per night (default: 0)
- `latitude` (Float): Latitude coordinate
- `longitude` (Float): Longitude coordinate

**Relationships:**
- `city`: Many-to-one with City (place belongs to one city)
- `user`: Many-to-one with User (place has one owner)
- `reviews`: One-to-many with Review (place can have multiple reviews)
- `amenities`: Many-to-many with Amenity (place can have multiple amenities)

### Review Model (`review.py`)
Represents user reviews of places.

**Attributes:**
- `place_id` (String, 60): Foreign key to Place (required)
- `user_id` (String, 60): Foreign key to User (required)
- `text` (String, 1024): Review text (required)

**Relationships:**
- `place`: Many-to-one with Place (review belongs to one place)
- `user`: Many-to-one with User (review written by one user)

## 🗄️ Storage Engines

### File Storage (`engine/file_storage.py`)
- **Storage Format**: JSON files
- **File Location**: `file.json` (default)
- **Serialization**: Objects converted to dictionaries
- **Key Format**: `<ClassName>.<object_id>`

**Methods:**
- `all(cls=None)`: Retrieve all objects or objects of specific class
- `new(obj)`: Add new object to storage
- `save()`: Serialize objects to JSON file
- `reload()`: Deserialize objects from JSON file
- `delete(obj=None)`: Delete object from storage
- `close()`: Reload storage (for consistency)

### Database Storage (`engine/db_storage.py`)
- **Database**: MySQL with SQLAlchemy ORM
- **Connection**: Configured via environment variables
- **Session Management**: Scoped sessions for thread safety
- **Relationships**: Automatic handling via SQLAlchemy

**Methods:**
- `all(cls=None)`: Query all objects or objects of specific class
- `new(obj)`: Add object to current session
- `save()`: Commit current session
- `delete(obj=None)`: Delete object from session
- `reload()`: Create database session
- `close()`: Close current session

## ⚙️ Configuration

### Environment Variables

Storage type is determined by `HBNB_TYPE_STORAGE`:

```bash
# Use file storage (default)
export HBNB_TYPE_STORAGE=file

# Use database storage
export HBNB_TYPE_STORAGE=db
export HBNB_MYSQL_USER=hbnb_dev
export HBNB_MYSQL_PWD=hbnb_dev_pwd
export HBNB_MYSQL_HOST=localhost
export HBNB_MYSQL_DB=hbnb_dev_db
```

### Model Initialization

The `__init__.py` file automatically:
1. Imports all model classes
2. Determines storage type from environment
3. Initializes appropriate storage engine
4. Creates CNC (Class Name to Class) dictionary
5. Calls `storage.reload()` to load existing data

## 💾 Usage Examples

### Creating Objects
```python
from models import storage
from models.user import User
from models.state import State

# Create a new user
user = User()
user.email = "test@example.com"
user.password = "password123"
user.first_name = "John"
user.last_name = "Doe"
user.save()

# Create a new state
state = State()
state.name = "California"
state.save()
```

### Querying Objects
```python
from models import storage

# Get all users
all_users = storage.all(User)

# Get all objects
all_objects = storage.all()

# Find specific object
user_key = f"User.{user.id}"
user = storage.all(User)[user_key]
```

### Updating Objects
```python
# Modify and save
user.first_name = "Jane"
user.save()  # Updates updated_at timestamp
```

### Deleting Objects
```python
# Delete from storage
storage.delete(user)
storage.save()  # Commit changes (for database)
```

## 🧪 Testing

### Unit Tests
Each model has comprehensive tests in `tests/test_models/`:
- Instantiation tests
- Attribute tests
- Method tests
- Relationship tests
- Storage tests

### Running Tests
```bash
# Test all models
python3 -m unittest discover tests/test_models/

# Test specific model
python3 -m unittest tests.test_models.test_user

# Test with database storage
HBNB_TYPE_STORAGE=db python3 -m unittest tests.test_models.test_user
```

## 🔧 Adding New Models

To add a new model:

1. **Create the model file** (`models/new_model.py`):
```python
#!/usr/bin/python3
"""New Model module"""

from models.base_model import BaseModel, Base
from sqlalchemy import Column, String

class NewModel(BaseModel, Base):
    """New Model class"""
    
    if storage_type == 'db':
        __tablename__ = 'new_models'
        name = Column(String(128), nullable=False)
    else:
        name = ""
```

2. **Update `models/__init__.py`**:
```python
from models.new_model import NewModel
# Add to CNC dictionary in storage engines
```

3. **Create tests** (`tests/test_models/test_new_model.py`)

4. **Add API endpoints** (if needed)

## 🔒 Security Considerations

- **Password Storage**: Passwords should be hashed before storage
- **Input Validation**: Validate all input data
- **SQL Injection**: SQLAlchemy ORM provides protection
- **Data Integrity**: Use foreign key constraints

## 🐛 Known Issues

- Password hashing not implemented
- No data validation beyond basic type checking
- Limited constraint enforcement in file storage
- No audit logging for data changes

## 🤝 Contributing

When contributing to models:
1. Follow the BaseModel pattern
2. Add appropriate relationships
3. Include comprehensive tests
4. Update documentation
5. Consider both storage types (file and database)

---

For more information, see the main project [README](../README.md).
