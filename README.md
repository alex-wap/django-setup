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
* cd into PROJECT (directory with manage.py file inside)
* python manage.py runserver


## Session
* `python manage.py migrate` (directory with manage.py file inside)
* bracket notation format for FILE.py: `request.session['key']`
* dot notation format for FILE.html: `{{request.session.key}}`