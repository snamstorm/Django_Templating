# Django_Templating

The following are steps to take after Django has been installed

### Directories to create
* Add a new directory in your app called 'templates'
* Add to your <code>settings.py</code>: <code>TEMPLATE_DIRS = [os.path.join(BASE_DIR, 'your_app/templates')]. </code>


#### Capturing variables in URL Routes
*URL'S and Regex URL's: add the following code to <code>urls.py</code>
````python 
urlpatterns = patterns('',
    # Variables are captured in the part of the url in parentheses
    # The '?P<variable_name>' syntax lets you name the variable
    # The regex after the variable's name indicates what is allowed
    url(r'^URL/(?P<name>\w+)$', 'your_app.views.URL'),
)
````
*Link your URL's to <code>views.py</code>
````python
from django.shortcuts import render_to_response

def hello(request, name):
    return render_to_response(
        "file_name.html",
        {'name': name}
    )
````
* create <code>file_name.html</code> in 'templates'
```HTML
<body>
<h1>Hello {{ name }}!</h1>
</body>
```
