# Django Add Debug Toolbar

Open-source sample provided by AppSeed on top of **[Django Soft UI Dashboard](https://appseed.us/product/django-soft-ui-dashboard)** that provides a pre-configured codebase with **[Django Debug Toolbar](https://docs.appseed.us/content/how-to/django-add-debug-toolbar)** plugin. For newcomers, the **Django Debug Toolbar** is a configurable set of panels that bumps various information about the current request/response when clicked.

<br />

- UI Kit: **[Soft UI Dashboard](https://bit.ly/2Q1uIfK)** (Free Version) provided by **Creative-Tim**
- SQLite Database, Django Native ORM
- Modular design, clean codebase
- Session-Based Authentication, Forms validation
- Deployment scripts: Docker, Gunicorn / Nginx
- Support via **Github** (issues tracker) and [Discord](https://discord.gg/fZC6hup).

<br />

> Links

- [Django Soft UI Dashboard](https://appseed.us/product/django-soft-ui-dashboard) - Initial Product (open-source)
- [Django Soft UI Dashboard](https://django-soft-ui-dashboard.appseed-srv1.com/) - LIVE Demo
- [Django - Add Debug Toolbar](https://docs.appseed.us/content/how-to/django-add-debug-toolbar) - Documentation page

<br />

![Django Add Debug Toolbar - Open-source sample provided by AppSeed.](https://user-images.githubusercontent.com/51070104/125966334-4d911abf-9210-43c1-a5ce-6da1f2eadb8f.png)

<br />

## How to use it

```bash
$ # Get the code
$ git clone https://github.com/app-generator/django-add-debug-toolbar.git
$ cd django-add-debug-toolbar
$
$ # Virtualenv modules installation (Unix based systems)
$ virtualenv env
$ source env/bin/activate
$
$ # Virtualenv modules installation (Windows based systems)
$ # virtualenv env
$ # .\env\Scripts\activate
$
$ # Install modules - SQLite Storage
$ pip3 install -r requirements.txt
$
$ # Create tables
$ python manage.py makemigrations
$ python manage.py migrate
$
$ # Start the application (development mode)
$ python manage.py runserver # default port 8000
$
$ # Start the app - custom port
$ # python manage.py runserver 0.0.0.0:<your_port>
$
$ # Access the web app in browser: http://127.0.0.1:8000/
```

> Note: To use the app, please access the registration page and create a new user. After authentication, the app will unlock the private pages.

<br />

## Code-base structure

The project is coded using a simple and intuitive structure presented bellow:

```bash
< PROJECT ROOT >
   |
   |-- core/                               # Implements app logic and serve the static assets
   |    |-- settings.py                    # Django app bootstrapper
   |    |-- urls.py                        # Define URLs served by all apps/nodes
   |    |
   |    |-- static/
   |    |    |-- <css, JS, images>         # CSS files, Javascripts files
   |    |
   |    |-- templates/                     # Templates used to render pages
   |         |
   |         |-- includes/                 # HTML chunks and components   |         |
   |         |-- layouts/                  # Master pages
   |         |    |-- base-fullscreen.html # Used by Authentication pages
   |         |    |-- base.html            # Used by common pages
   |         |
   |         |-- accounts/                 # Authentication pages
   |         |    |-- login.html           # Login page
   |         |    |-- register.html        # Register page
   |         |
   |      index.html                       # The default page
   |     page-404.html                     # Error 404 page
   |     page-500.html                     # Error 404 page
   |       *.html                          # All other HTML pages
   |
   |-- authentication/                     # Handles auth routes (login and register)
   |
   |-- app/                                # A simple app that serve HTML files
   |
   |-- requirements.txt                    # Development modules - SQLite storage
   |
   |-- .env                                # Inject Configuration via Environment
   |-- manage.py                           # Start the app - Django default start script
   |
   |-- ************************************************************************
```

<br />

> The bootstrap flow

- Django bootstrapper `manage.py` uses `core/settings.py` as the main configuration file
- `core/settings.py` loads the app magic from `.env` file
- Redirect the guest users to Login page
- Unlock the pages served by *app* node for authenticated users

<br />

## Django Toolbar Set Up

> **Step #1** - Add django-debug-toolbar to project dependencies or install via PIP

```txt
# File: requirements.txt
...
django-debug-toolbar
...
```

**Or install via PIP**

```bash
$ pip install django-debug-toolbar
```

<br />

> **Step #2** - Update project routes

```python
# File core/urls.py

import debug_toolbar                                          # <-- NEW                     

from django.contrib import admin
from django.urls import path, include  

urlpatterns = [
   ...
   path('__debug__/', include(debug_toolbar.urls)),           # <-- NEW
   ... 
]

```

<br />

> **Step #3** - Update Settings


```python
# File core/settings.py
...
from decouple import config
from unipath import Path
import dj_database_url

import mimetypes                                               # <-- NEW


BASE_DIR = Path(__file__).parent

INSTALLED_APPS = [
   ... 
   'django.contrib.staticfiles',
   'debug_toolbar',                                            # <-- NEW
   ...  
]

MIDDLEWARE = [
   ...
   'django.middleware.clickjacking.XFrameOptionsMiddleware',
   'debug_toolbar.middleware.DebugToolbarMiddleware',          # <-- NEW
   ...
]

INTERNAL_IPS = [                                               # <-- NEW
    '127.0.0.1',                                               # <-- NEW
]                                                              # <-- NEW

def show_toolbar(request):                                     # <-- NEW
    return True                                                # <-- NEW 

DEBUG_TOOLBAR_CONFIG = {                                       # <-- NEW
    "SHOW_TOOLBAR_CALLBACK" : show_toolbar,                    # <-- NEW
}                                                              # <-- NEW

if DEBUG:                                                      # <-- NEW
    import mimetypes                                           # <-- NEW          
    mimetypes.add_type("application/javascript", ".js", True)  # <-- NEW
```

<br />

> **Step #4** - Execute the migration 

```bash
$ python manage.py makemigrations
$ python manage.py migrate
```

<br />

> **Step #5** - Start the app (the debug toolbar should be visible)

```bash
$ python manage.py runserver
```

At this point, the Debug Toolbar should be visible on the right side for all pages. 

<br />

![Django Add Debug Toolbar - Open-source sample provided by AppSeed.](https://user-images.githubusercontent.com/51070104/125966334-4d911abf-9210-43c1-a5ce-6da1f2eadb8f.png)

<br />

## Credits & Links

- [Django Debug Toolbar](https://django-debug-toolbar.readthedocs.io/en/latest/installation.html) - official docs
- [Django Debug Toolbar](https://pypi.org/project/django-debug-toolbar/) - PyPi page

<br />

---
Django Add Debug Toolbar - Provided by **AppSeed** [App Generator](https://appseed.us/app-generator).
