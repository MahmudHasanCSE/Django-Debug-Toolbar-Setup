# Django-Debug-Toolbar-Setup
This repository will help you to implement Django Debug Toolbar in your web application.

## What is Django Debug Toolbar?
The Django Debug Toolbar is a configurable set of panels that display various debug information about the current request/response and when clicked, display more details about the panel's content.

## How to install and implement Django Debug Toolbar?
For the installation of the Django Debug Toolbar you need to have a django project where you can use pip in a Virtual Environment or without them. If you don't want to use pip, you can get the code of this component from here (https://github.com/jazzband/django-debug-toolbar) and put it in your django project path; but the pip installation is more easy and I will focus on that.

For installation I recommend use the virtual env and execute this command:
```sh
$ pip install django-debug-toolbar
```
The configuration of this component is simple, you just need change your projects urls.py and settings.py to use the toolbar.

In your project urls.py, enter this code:
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
>Take care with the “imports” because it’s possible that you may duplicate some of this.

Now In your projects settings.py make sure that debug mode is true.
```sh
DEBUG = True
```
Install debug_toolbar and make sure django.contrib.staticfiles exists.
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
Add INTERNAL_IPS in settings.py; The INTERNAL_IPS conf is valid for a local development environment, if your dev env is different, you just change this field with your valid conf.
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

This is the default conf and if you want see more options you can see this page:

>https://django-debug-toolbar.readthedocs.io/en/stable/configuration.html

**Note**: It is very important that you have the close body tag ( </body> ) in your base template for the Django Debug Toolbar is showing.

This component has a variety of panels that can be added through the configuration, these panels show different information related to http requests / responses and other relevant debug data, in this url you can see all differents default panels and you can learn how to use and configure it. http://django-debug-toolbar.readthedocs.io/en/stable/panels.html

