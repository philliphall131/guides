# React - Django Web App Project Setup
### This project setup allows for a single server web app with a SPA frontend served by the backend which also functions as the web app REST API

## Folder Structure
- Initialize a project folder with frontend and backend subfolders
- If using version control, initialize that with a .gitignore 
~~~
mkdir <project name>
cd <project name>
mkdir frontend && mkdir backend
touch .gitignore
~~~
- Initialize a database of your choosing. In most of my cases, postgresql:
~~~
createdb <db name>
~~~

## Django Setup
1) In backend folder, create virtual environment, initialize it
~~~
cd backend
python -m venv venv
source venv/bin/activate
~~~
2) Install django and dependencies (on mac, swap psycopg2-binary for psycopg2)
~~~
pip install django djangorestframework psycopg2-binary django-cors-headers gunicorn python-dotenv
~~~
3) Setup django project
~~~
django-admin startproject <project name> .
~~~
4) Setup django app
~~~
python manage.py startapp <app name>
~~~
5) Create .env file in the backend folder
~~~
DEBUG=true
SECRET_KEY=[cut/paste django secret key from settings.py here (without brackets)]
~~~
6) Modify settings.py in the django project folder
~~~
from pathlib import Path
from dotenv import load_dotenv
import os
SECRET_KEY = os.getenv('SECRET_KEY')
DEBUG = (os.getenv("DEBUG") == "true")
ALLOWED_HOSTS = ['*']
INSTALLED_APPS = [
    ...
    '<app name>',
    'rest_framework',
]
if DEBUG:  # Allows split development on local machine
    INSTALLED_APPS += ["corsheaders"]
MIDDLEWARE = [
    ...
]
if DEBUG:
    MIDDLEWARE.insert(0, "corsheaders.middleware.CorsMiddleware")

CSRF_TRUSTED_ORIGINS = ['<actual https domain name for deployment>']

if DEBUG:
    CORS_ALLOWED_ORIGINS = [
        "http://localhost:3000",
        "http://127.0.0.1:3000",
    ]
    CORS_EXPOSE_HEADERS = ['Content-Type', 'X-CSRFToken']
    CORS_ALLOW_CREDENTIALS = True


REST_FRAMEWORK = { 
    "DEFAULT_AUTHENTICATION_CLASSES": [
        "rest_framework.authentication.SessionAuthentication",
    ],
    'DEFAULT_PERMISSION_CLASSES': [
        "rest_framework.permissions.IsAuthenticated", # block actions for anonymous users by default
    ],
}
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': '<database name>',
    }
}
if not DEBUG:
    AUTH_PASSWORD_VALIDATORS = [
        ...
    ]
else: AUTH_PASSWORD_VALIDATORS = []
STATICFILES_DIRS = [
    os.path.join(BASE_DIR, "../frontend/build/static"), # your static files folder (where react builds to)
]
# AUTH_USER_MODEL = '<app name>.User' # leave this commented until implemented in models
~~~
7) Setup a django super user/admin 
~~~
python manage.py createsuperuser
~~~

## React Setup
1) In frontend folder, create react app
~~~
npx create-react-app .
npm install axios react-router-dom react-bootstrap bootstrap
~~~

## Test Wire-up
1) build react to avoid a warning from django 
~~~
npm run build
~~~
2) run react and django to validate correct setup
~~~
cd frontend
npm start
cd ../backend
python manage.py runserver
~~~

## Basic DRF Setup
1) project urls.py
~~~
from django.contrib import admin
from django.urls import path, include
from .view import send_the_homepage

urlpatterns = [
    path('admin/', admin.site.urls), # this will direct to the django admin page
    path('', send_the_homepage), # this will serve the react frontend build
    path('api/', include('<app name>.urls')) # this will direct to the DRF backend API
]
~~~
2) create view.py in project folder to serve the react app
~~~
from django.http import HttpResponse

def send_the_homepage(request):
    homepage = open('/home/ubuntu/homebrewd/frontend/build/index.html').read()
    return HttpResponse(homepage)
~~~
3) create urls.py in the app folder
~~~
from django.urls import path, include
from rest_framework import routers
from .views import *

r = routers.DefaultRouter()
# register your models here

urlpatterns = [
    # additional urls for manual views
]
~~~


