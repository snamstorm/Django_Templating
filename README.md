# Django_Templating

The following are steps to take after Django has been installed

### Directories to create
* Add a new directory in your app called 'templates' (All HTML files go here)
* Add to your <code>settings.py</code>: <code>TEMPLATE_DIRS = [os.path.join(BASE_DIR, 'your_app/templates')]. </code>

* Create a python package called <code>templatetags</code> in your application. (For Filters and Tags)

* Create a folder in your application called 'static' (Where HTML files live)
* In your 'static' folder create three folders called 'js', 'css', 'img' (static files that link to HTML files)


### Django Debug Toolbar
* <code>pip install django-debug-toolbar</code>
* Put <code>debug_toolbar<c/ode> in your INSTALLED_APPS.
* Put <code>INTERNAL_IPS = ("127.0.0.1", "10.0.2.2")</code> in your <code>local_settings.py</code>

#### Capturing variables in URL Routes
*URL'S and Regex URL's: add the following code to <code>urls.py</code>
````python 
urlpatterns = patterns('',
    # Variables are captured in the part of the url in parentheses
    # The '?P<variable_name>' syntax lets you name the variable
    # The regex after the variable's name indicates what is allowed
    url(r'^URL/(?P<some_variable>\w+)$', 'your_app.views.URL'),
)
````
* Link your URL's to <code>views.py</code>
````python
from django.shortcuts import render_to_response

def URL(request, some_variable):
    return render_to_response(
        "file_name.html",
        {'some_variable': some_variable}
    )
````
* create <code>file_name.html</code> in 'templates'
````HTML
<body>
<h1>Hello {{ some_variable }}!</h1>
</body>
````
### Custom Filters and Tags
* Create a file in templatetags called <code>some_file.py</code>
* Add the following code to the file:
````python 
from django import template

register = template.Library()

# recognize this function as a filter
@register.filter
def func(condition):
````
* load the filter in pages using this filter by including <code>{% load some_file %}</code> on the first line

### DRY Templates

* create a new template called header.html
* In the header template, include (and any other files that need to be run across all pages):
````python
    <head>
        <script src="//code.jquery.com/jquery-1.11.0.min.js"></script>
        <script src="{% static 'js/cards.js' %}"></script>
        <link rel="stylesheet" type="text/css" href="{% static 'css/cards.css' %}">
    </head>

    <body>
        <h1>Welcome to our Card Game!</h1>
        {% block content %}{% endblock content %}
    </body>
````
* Include the header.html file in other files by extension
````python
{% extends 'header.html' %}

{% block content %}
    <p>YOUR HTML TEXT HERE</p>
{% endblock content %}
````


### Working with Images
* pip install pillow <- this will let our python code work with images.
* In <code>urls.py</code> add the following at the bottom of the file:
````python
if settings.DEBUG:
    urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
````
And import from:
````python
    from django.conf import *
    from django.conf.urls.static import *
````

* In settings.py add the following before the line that imports your local_settings file:
````python
    PROJECT_ROOT = os.path.abspath(os.path.join(os.path.dirname(os.path.abspath(__file__)), '..'))
    MEDIA_URL = "/img/"
    MEDIA_ROOT = os.path.join(PROJECT_ROOT, "static", *MEDIA_URL.strip("/").split("/"))
````
* Add {% load staticfiles %} to the top of the template that includes images


