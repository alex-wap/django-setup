# Django Setup


This guide assumes you have already created a virtual environment and Django is installed.


## Instructions

* create django project `django-admin startproject PROJECT`
* cd PROJECT
* python manage.py runserver (check if it works)
* CONTROL+C to exit your server
* mkdir apps
* cd apps
* touch __init__.py (aka dunder file)
* python ../manage.py startapp APPNAME (creates APPNAME FOLDER)
* update settings.py (do not forget the comma):
```python
INSTALLED_APPS = [
	'apps.APPNAME',
	...
	]
```
* update PROJECT/urls.py (make sure your parens match, no $ in route):
```python
from django.conf.urls import url, include
from django.contrib import admin
urlpatterns = [
	url(r'^', include('apps.APPNAME.urls')),
	]
```
* create PROJECT/apps/APPNAME/urls.py (routes file, use $, use comma):
```python
from django.conf.urls import url
from . import views
urlpatterns = [
	url(r'^$', views.index),
	]
```
* update views.py:
```python
from django.shortcuts import render, redirect
def index(request):
	return render(request, "APPNAME/index.html")
```
* create templates directory (and write something in index.html):
```bash
cd PROJECT/apps/APPNAME
mkdir templates
cd templates
mkdir APPNAME
cd APPNAME
touch index.html
```
* create static directories (PROJECT/apps/APPNAME/static/APPNAME/):
```bash
cd PROJECT/apps/APPNAME
mkdir static
cd static
mkdir APPNAME
cd APPNAME
mkdir css
mkdir images
mkdir js
```
* cd into PROJECT (directory with manage.py file inside)
* python manage.py runserver


## Static files formatting (in HTML)
```html
<!DOCTYPE html>
<html>
<head>
  <title>Document</title>
  {% load staticfiles %}
  <link rel="stylesheet" href="{% static 'second_app/css/style.css' %}">
  <script src="{% static 'second_app/js/main.js' %}"></script>
</head>
<body>
<img src="{% static 'second_app/img/rick.gif' %}">
</body>
</html>
```
## Route Parameters
* urls.py:
```python
from django.conf.urls import url
from . import views
urlpatterns = [
  url(r'^/en/(?P<djangoversion>[0-9]\.[0-9])/topics/http/urls/$', views.index)
]
```
* views.py:
```python
from django.shortcuts import render, HttpResponse, redirect
# Create your views here.
def index(request, djangoversion):
  print(djangoversion) # will result in a string e.g. "1.9"
  print("hello, I am your first request")
  return HttpResponse('hello')

```

## form data
* `{% csrf_token %}` in all form with method="POST"
* access data via request.POST (not request.form as in flask)

## Session
* `python manage.py migrate` (directory with manage.py file inside)
* bracket notation format for FILE.py: `request.session['key']`
* dot notation format for FILE.html: `{{request.session.key}}`

## Django installation (just in case)
```bash
virtualenv djangoEnv
source djangoEnv/bin/activate
pip install django
```
## Django comment out templating (must be same line):
```html
{# {% load staticfiles %} #}
```