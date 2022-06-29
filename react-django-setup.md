# React - Django Web App Project Setup
### This project setup allows for a single server web app with a SPA frontend served by the backend which also functions as the web app REST API

## Folder Structure
    - Initialize a project folder with frontend and backend subfolders
    - If using version control, initialize that
~~~
mkdir <project name>
cd <project name>
mkdir frontend && mkdir backend
~~~

## Django Setup
    1) In backend folder, create virtual environment, initialize it
~~~
cd backend
python -m venv venv
source venv/bin/activate
~~~
    2) Install django and dependencies
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

## React Setup
    1) 

