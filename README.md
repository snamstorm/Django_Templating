# Django_Templating

The following are steps to take after Django has been installed

### Directories to create
* Add a new directory in your app called 'templates'
* Add to your <code>settings.py</code>: <code>TEMPLATE_DIRS = [os.path.join(BASE_DIR, 'your_app/templates')]. </code>
* Create a python package called <code>templatetags</code> in your application. (For Filters and Tags)

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
* Create a file in templatetags
* Add the following code to the file:
````python 
from django import template

register = template.Library()

@register.filter
def func(condition):
````
