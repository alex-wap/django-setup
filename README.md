# Django Setup


This guide assumes you have already created a virtual environment and Django is installed.


## Instructions

1. create django project `django-admin startproject PROJECT`
2. cd PROJECT
3. python manage.py runserver (check if it works)
4. CONTROL+C to exit your server
5. mkdir apps
6. cd apps
7. touch __init__.py (aka dunder file)
8. python ../manage.py startapp APPNAME (creates APPNAME FOLDER)
9. update settings.py (do not forget the comma):
* ```python
INSTALLED_APPS = [
	'apps.APPNAME',
	...
	]
```
9. update PROJECT/urls.py (make sure your parens match, no $ in route):
* ```python
from django.conf.urls import url, include
from django.contrib import admin
urlpatterns = [
	url(r'^', include('apps.APPNAME.urls')),
	]
```
10. create PROJECT/apps/APPNAME/urls.py (routes file, use $, use comma):
* ```python
from django.conf.urls import url
from . import views
urlpatterns = [
	url(r'^$', views.index),
	]
```
11. update views.py:
* ```python
from django.shortcuts import render, redirect
def index(request):
	return render(request, "APPNAME/index.html")
```
12. create templates directory (and write something in index.html):
* ```
cd PROJECT/apps/APPNAME
mkdir templates
cd templates
mkdir APPNAME
cd APPNAME
touch index.html
```
13. cd into PROJECT (directory with manage.py file inside)
14. python manage.py runserver


## Session
* `python manage.py migrate` (directory with manage.py file inside)
* bracket notation format for FILE.py: `request.session['key']`
* dot notation format for FILE.html: `{{request.session.key}}`