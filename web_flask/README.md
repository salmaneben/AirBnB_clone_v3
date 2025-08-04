# Web Flask - AirBnB Clone v3

This directory contains Flask web applications that provide a web interface for the AirBnB clone project. The Flask applications demonstrate progressive web development concepts, from basic routing to complex templating with database integration.

## 📁 Files Overview

### Basic Routes
- **`0-hello_route.py`** - Basic Flask application with a simple "Hello HBNB!" route
- **`1-hbnb_route.py`** - Adds HBNB route with strict slashes handling
- **`2-c_route.py`** - Dynamic routing with C parameter
- **`3-python_route.py`** - Python route with default parameter value
- **`4-number_route.py`** - Route that only accepts integer parameters

### Template Integration
- **`5-number_template.py`** - First template integration displaying numbers
- **`6-number_odd_or_even.py`** - Template with conditional logic (odd/even)

### Database Integration
- **`7-states_list.py`** - Display list of states from database/storage
- **`8-cities_by_states.py`** - Show cities organized by states
- **`9-states.py`** - Detailed state view with cities
- **`10-hbnb_filters.py`** - Complete filters page mimicking AirBnB interface

## 🚀 Usage

### Running Individual Applications

```bash
# Basic hello world
python3 -m web_flask.0-hello_route

# States listing (requires storage setup)
HBNB_TYPE_STORAGE=db python3 -m web_flask.7-states_list

# Complete filters page
python3 -m web_flask.10-hbnb_filters
```

### Environment Setup for Database Integration

```bash
# Set up environment variables for database storage
export HBNB_TYPE_STORAGE=db
export HBNB_MYSQL_USER=hbnb_dev
export HBNB_MYSQL_PWD=hbnb_dev_pwd
export HBNB_MYSQL_HOST=localhost
export HBNB_MYSQL_DB=hbnb_dev_db

# Run application
python3 -m web_flask.8-cities_by_states
```

## 🎨 Templates

The `templates/` directory contains Jinja2 templates:

- **`5-number.html`** - Simple number display template
- **`6-number_odd_or_even.html`** - Template with conditional rendering
- **`7-states_list.html`** - States listing template
- **`8-cities_by_states.html`** - States and cities display
- **`9-states.html`** - Detailed state information
- **`10-hbnb_filters.html`** - Complete AirBnB-like filters interface

## 🌐 Accessing the Applications

Once running, access the applications at:
- `http://localhost:5000/` - Default route
- `http://localhost:5000/hbnb` - HBNB route
- `http://localhost:5000/c/<text>` - Dynamic C route
- `http://localhost:5000/python/` or `/python/<text>` - Python route
- `http://localhost:5000/number/<int>` - Number route
- `http://localhost:5000/number_template/<int>` - Template with number
- `http://localhost:5000/number_odd_or_even/<int>` - Odd/even template
- `http://localhost:5000/states_list` - States listing
- `http://localhost:5000/cities_by_states` - Cities by states
- `http://localhost:5000/states` - States overview
- `http://localhost:5000/states/<id>` - Specific state details
- `http://localhost:5000/hbnb_filters` - Complete filters page

## 🔧 Features Demonstrated

1. **Flask Routing** - URL routing and parameter handling
2. **Template Engine** - Jinja2 template integration
3. **Database Integration** - SQLAlchemy ORM usage
4. **Static Files** - CSS and image serving
5. **Error Handling** - 404 error management
6. **Clean URLs** - Strict slashes configuration
7. **Dynamic Content** - Data-driven page generation

## 📝 Notes

- All applications run on `host='0.0.0.0'` and `port=5000` by default
- Database applications require proper environment variable setup
- Templates inherit styling from the web_static CSS files
- Applications demonstrate progressive complexity in Flask development

This Flask application serves as the web interface component of the AirBnB clone project, providing user-friendly access to the underlying data models and storage systems.
