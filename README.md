# Django Debug Toolbar Setup
[![Python Version](https://img.shields.io/badge/python-3.7-brightgreen.svg)](https://python.org)
[![Django Version](https://img.shields.io/badge/django-2.1.7-brightgreen.svg)](https://djangoproject.com)

This repository will help you implement Django Debug Toolbar in your web application.

## What is Django Debug Toolbar?
The Django Debug Toolbar is a configurable set of panels that display various debug information about the current request/response and when clicked, display more details about the panel’s content.

## How to install and implement Django Debug Toolbar?
For the installation of the Django Debug Toolbar, you need to have a Django project where you can use pip in a Virtual Environment or without them. If you don’t want to use pip, you can get the code of this component from here (https://github.com/jazzband/django-debug-toolbar) and put it in your Django project path; but the pip installation is easier and I will focus on that.

For installation I recommend using the virtual env and executing this command:
```sh
$ pip install django-debug-toolbar
```
The configuration of this component is simple, you just need to change your project’s urls.py and settings.py to use the toolbar.

In your project’s urls.py, enter this code:
```sh
from django.conf import settings
from django.urls import include, path  # For django versions from 2.0 and up
import debug_toolbar

urlpatterns = [
    #...
    path('__debug__/', include(debug_toolbar.urls)),
    #...
    
] 
```
>Take care of the imports because it is possible that you may duplicate some of this.

Now In your project’s settings.py, make sure that debug mode is true.
```sh
DEBUG = True
```
Add debug_toolbar and make sure django.contrib.staticfiles exists in INSTALLED_APPS.
```sh
INSTALLED_APPS = [
    #...
    'django.contrib.staticfiles',
    #...
    'debug_toolbar',
    #...
]
```
Add this line to MIDDLEWARE
```sh
MIDDLEWARE = [
    #...
    'debug_toolbar.middleware.DebugToolbarMiddleware',
    #...
]
```
Add INTERNAL_IPS in settings.py; The INTERNAL_IPS conf is valid for a local development environment, if your dev environment is different, you just change this field with your valid configuration.
```sh
INTERNAL_IPS = ('127.0.0.1', '0.0.0.0', 'localhost',)
```
Add DEBUG_TOOLBAR_PANELS and DEBUG_TOOLBAR_CONFIG in settings.py
```sh
DEBUG_TOOLBAR_PANELS = [
    'debug_toolbar.panels.versions.VersionsPanel',
    'debug_toolbar.panels.timer.TimerPanel',
    'debug_toolbar.panels.settings.SettingsPanel',
    'debug_toolbar.panels.headers.HeadersPanel',
    'debug_toolbar.panels.request.RequestPanel',
    'debug_toolbar.panels.sql.SQLPanel',
    'debug_toolbar.panels.staticfiles.StaticFilesPanel',
    'debug_toolbar.panels.templates.TemplatesPanel',
    'debug_toolbar.panels.cache.CachePanel',
    'debug_toolbar.panels.signals.SignalsPanel',
    'debug_toolbar.panels.logging.LoggingPanel',
    'debug_toolbar.panels.redirects.RedirectsPanel',
]

DEBUG_TOOLBAR_CONFIG = {
       'INTERCEPT_REDIRECTS': False,
}
```
**You did it!**

This is the default configuration and if you want to see more options, you can see this page:

>https://django-debug-toolbar.readthedocs.io/en/stable/configuration.html

**Note**: It is very important that you have the close body tag ( ) in your base template for the Django Debug Toolbar is showing.

This component has a variety of panels that can be added through the configuration. These panels show different information related to HTTP requests/responses and other relevant debug data. In this URL, you can see all different default panels and you can learn how to use and configure it. http://django-debug-toolbar.readthedocs.io/en/stable/panels.html

