# Django_Templating

The following are steps to take after Django has been installed

#### Capturing variables in URL Routes

````python 
urlpatterns = patterns('',
    # Variables are captured in the part of the url in parentheses
    # The '?P<variable_name>' syntax lets you name the variable
    # The regex after the variable's name indicates what is allowed
    url(r'^hello/(?P<name>\w+)$', 'your_app.views.hello'),
)

````
