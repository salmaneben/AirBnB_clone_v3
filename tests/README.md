# AirBnB Clone v3 - Test Suite

This directory contains comprehensive unit tests for the AirBnB Clone v3 project. The test suite ensures code quality, functionality, and compatibility across different storage engines.

## 🧪 Overview

The test suite provides:
- **Unit Tests**: Individual component testing
- **Integration Tests**: Cross-component functionality
- **Storage Engine Testing**: Both file and database storage
- **PEP8 Compliance**: Code style validation
- **Documentation Testing**: Docstring validation
- **Coverage Analysis**: Code coverage metrics

## 📁 Directory Structure

```
tests/
├── __init__.py                       # Test package initialization
├── test_console.py                   # Console command interpreter tests
└── test_models/                      # Model tests directory
    ├── __init__.py                   # Model tests package init
    ├── test_base_model.py           # BaseModel class tests
    ├── test_user.py                 # User model tests
    ├── test_state.py                # State model tests
    ├── test_city.py                 # City model tests
    ├── test_amenity.py              # Amenity model tests
    ├── test_place.py                # Place model tests
    ├── test_review.py               # Review model tests
    └── test_engine/                 # Storage engine tests
        ├── __init__.py              # Engine tests package init
        ├── test_file_storage.py     # File storage engine tests
        └── test_db_storage.py       # Database storage engine tests
```

## 🚀 Running Tests

### Run All Tests
```bash
# From project root directory
python3 -m unittest discover tests

# With verbose output
python3 -m unittest discover tests -v

# Run tests and show coverage
python3 -m coverage run -m unittest discover tests
python3 -m coverage report -m
```

### Run Specific Test Categories
```bash
# Test only models
python3 -m unittest discover tests/test_models

# Test only console
python3 -m unittest tests.test_console

# Test specific model
python3 -m unittest tests.test_models.test_user

# Test specific class
python3 -m unittest tests.test_models.test_user.TestUser
```

### Test with Different Storage Types
```bash
# Test with file storage (default)
python3 -m unittest discover tests

# Test with database storage
HBNB_TYPE_STORAGE=db HBNB_MYSQL_USER=hbnb_test HBNB_MYSQL_PWD=hbnb_test_pwd HBNB_MYSQL_HOST=localhost HBNB_MYSQL_DB=hbnb_test_db python3 -m unittest discover tests
```

## 📋 Test Categories

### 1. Model Tests (`test_models/`)

Each model test file contains multiple test classes:

#### Documentation Tests (`TestModelDocs`)
- **Module Docstring**: Validates module-level documentation
- **Class Docstring**: Validates class-level documentation
- **Method Docstrings**: Validates method-level documentation
- **PEP8 Compliance**: Code style validation

#### Functionality Tests (`TestModel`)
- **Instantiation**: Object creation and initialization
- **Attributes**: Attribute existence and types
- **Methods**: Method functionality and return values
- **Inheritance**: BaseModel inheritance validation
- **Storage Integration**: Save/reload functionality

#### Example Test Structure (`test_user.py`):
```python
class TestUserDocs(unittest.TestCase):
    """Tests for User documentation and style"""
    
    def test_pep8_conformance_user(self):
        """Test that models/user.py conforms to PEP8"""
    
    def test_user_module_docstring(self):
        """Test for the user.py module docstring"""
    
    def test_user_class_docstring(self):
        """Test for the User class docstring"""

class TestUser(unittest.TestCase):
    """Tests for User class functionality"""
    
    def test_user_instantiation(self):
        """Test User object instantiation"""
    
    def test_user_attributes(self):
        """Test User attributes"""
    
    def test_user_methods(self):
        """Test User methods"""
```

### 2. Console Tests (`test_console.py`)

Tests for the command line interface:
- **Command Parsing**: Input validation and parsing
- **Help System**: Help command functionality
- **CRUD Operations**: Create, read, update, delete commands
- **Error Handling**: Invalid input and error messages
- **Storage Integration**: Console-storage interaction

### 3. Storage Engine Tests (`test_models/test_engine/`)

#### File Storage Tests (`test_file_storage.py`)
- **File Operations**: Save/reload from JSON
- **Object Serialization**: Dictionary conversion
- **Key Management**: Object key generation
- **CRUD Operations**: All storage operations

#### Database Storage Tests (`test_db_storage.py`)
- **Database Connection**: MySQL connection handling
- **Session Management**: SQLAlchemy session operations
- **Query Operations**: Database queries
- **Relationship Handling**: Foreign key relationships

## 🔧 Test Configuration

### Environment Setup for Database Tests
```bash
# MySQL test database setup
mysql -u root -p < setup_mysql_test.sql

# Environment variables for database tests
export HBNB_TYPE_STORAGE=db
export HBNB_MYSQL_USER=hbnb_test
export HBNB_MYSQL_PWD=hbnb_test_pwd
export HBNB_MYSQL_HOST=localhost
export HBNB_MYSQL_DB=hbnb_test_db
export HBNB_ENV=test
```

### Test Data Management
- **Isolation**: Each test is independent
- **Cleanup**: Automatic test data cleanup
- **Fixtures**: Reusable test data setup
- **Mocking**: External dependency mocking

## 📊 Test Coverage

### Coverage Analysis
```bash
# Install coverage tool
pip3 install coverage

# Run tests with coverage
python3 -m coverage run -m unittest discover tests

# Generate coverage report
python3 -m coverage report -m

# Generate HTML coverage report
python3 -m coverage html
```

### Expected Coverage Areas
- **Models**: 95%+ coverage for all model classes
- **Storage Engines**: 90%+ coverage for storage operations
- **Console**: 85%+ coverage for command handling
- **API Endpoints**: 90%+ coverage for API routes

## ✅ Test Best Practices

### Writing New Tests
1. **Test Class Naming**: Use `TestClassName` convention
2. **Test Method Naming**: Use descriptive `test_specific_functionality` names
3. **Docstrings**: Include clear test descriptions
4. **Assertions**: Use appropriate assertion methods
5. **Setup/Teardown**: Use `setUp()` and `tearDown()` for test preparation

### Test Organization
```python
import unittest
from models.user import User

class TestUser(unittest.TestCase):
    """Test cases for User class"""
    
    def setUp(self):
        """Set up test fixtures before each test method"""
        self.user = User()
    
    def tearDown(self):
        """Tear down test fixtures after each test method"""
        del self.user
    
    def test_user_creation(self):
        """Test user object creation"""
        self.assertIsInstance(self.user, User)
        self.assertTrue(hasattr(self.user, 'id'))
        self.assertTrue(hasattr(self.user, 'created_at'))
```

## 🔍 Common Test Patterns

### Testing Object Creation
```python
def test_object_instantiation(self):
    """Test object creation"""
    obj = ModelClass()
    self.assertIsInstance(obj, ModelClass)
    self.assertTrue(hasattr(obj, 'id'))
    self.assertTrue(hasattr(obj, 'created_at'))
    self.assertTrue(hasattr(obj, 'updated_at'))
```

### Testing Attribute Types
```python
def test_attribute_types(self):
    """Test attribute data types"""
    obj = ModelClass()
    self.assertIsInstance(obj.id, str)
    self.assertIsInstance(obj.created_at, datetime)
    self.assertIsInstance(obj.updated_at, datetime)
```

### Testing Storage Operations
```python
def test_save_and_reload(self):
    """Test save and reload functionality"""
    obj = ModelClass()
    obj.save()
    key = f"{ModelClass.__name__}.{obj.id}"
    self.assertIn(key, storage.all())
```

### Testing PEP8 Compliance
```python
def test_pep8_compliance(self):
    """Test PEP8 style compliance"""
    style = pep8.StyleGuide(quiet=True)
    result = style.check_files(['models/model_file.py'])
    self.assertEqual(result.total_errors, 0)
```

## 🚨 Troubleshooting

### Common Test Issues

#### MySQL Connection Errors
```bash
# Ensure MySQL service is running
sudo service mysql start

# Verify test database exists
mysql -u hbnb_test -p hbnb_test_db -e "SHOW TABLES;"
```

#### Import Errors
```bash
# Ensure you're running from project root
cd /path/to/AirBnB_clone_v3
python3 -m unittest tests.test_models.test_user
```

#### Permission Errors
```bash
# File storage permission issues
chmod 755 file.json
```

### Test Debugging
```python
# Add debug output to tests
def test_debug_example(self):
    """Debug test example"""
    obj = User()
    print(f"Object ID: {obj.id}")
    print(f"Object dict: {obj.to_dict()}")
    self.assertTrue(True)  # Replace with actual test
```

## 📈 Continuous Integration

### Running Tests in CI/CD
```yaml
# Example GitHub Actions workflow
name: Tests
on: [push, pull_request]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    - name: Set up Python
      uses: actions/setup-python@v2
      with:
        python-version: 3.8
    - name: Install dependencies
      run: pip install -r requirements.txt
    - name: Run tests
      run: python -m unittest discover tests
```

## 🤝 Contributing to Tests

When adding new features:
1. **Write Tests First**: Follow TDD principles
2. **Test Both Storage Types**: File and database storage
3. **Include Edge Cases**: Test boundary conditions
4. **Add Documentation Tests**: Ensure proper docstrings
5. **Maintain Coverage**: Keep coverage above 90%

### Test Checklist
- [ ] Unit tests for new functionality
- [ ] Integration tests for cross-component features
- [ ] PEP8 compliance tests
- [ ] Documentation tests
- [ ] Both storage engine compatibility
- [ ] Error handling tests
- [ ] Edge case coverage

---

For more information, see the main project [README](../README.md).
