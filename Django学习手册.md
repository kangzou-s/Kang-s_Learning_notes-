## Django 学习手册

## 最外层结构

```python
mysite/
    manage.py
    mysite/
        __init__.py
        settings.py
        urls.py
        asgi.py
        wsgi.py
```

## path 的四个参数

- route:  Django starts at the first pattern in `urlpatterns` and makes its way down the list, comparing the requested URL against each pattern until it finds one that matches.
- view: When Django finds a matching pattern, it calls the specified view function with an [`HttpRequest`](https://docs.djangoproject.com/en/3.2/ref/request-response/#django.http.HttpRequest) object as the first argument and any “captured” values from the route as keyword arguments.
- kwargs: Arbitrary keyword arguments can be passed in a dictionary to the target view.
- name: Naming your URL lets you refer to it unambiguously from elsewhere in Django, especially from within templates. This powerful feature allows you to make global changes to the URL patterns of your project while only touching a single file.

## url



## view

## models

Now we’ll define your models – essentially, your database layout, with additional metadata.



`python manage.py makemigrations pols` 

By running `makemigrations`, you’re telling Django that you’ve made some changes to your models (in this case, you’ve made new ones) and that you’d like the changes to be stored as a *migration*.



`python manage.py sqlmigrate polls 0001`

The [`sqlmigrate`](https://docs.djangoproject.com/en/3.2/ref/django-admin/#django-admin-sqlmigrate) command takes migration names and returns their SQL

The [`sqlmigrate`](https://docs.djangoproject.com/en/3.2/ref/django-admin/#django-admin-sqlmigrate) command doesn’t actually run the migration on your database - instead, it prints it to the screen so that you can see what SQL Django thinks is required. It’s useful for checking what Django is going to do or if you have database administrators who require SQL scripts for changes.



` python manage.py migrate`

The [`migrate`](https://docs.djangoproject.com/en/3.2/ref/django-admin/#django-admin-migrate) command takes all the migrations that haven’t been applied (Django tracks which ones are applied using a special table in your database called `django_migrations`) and runs them against your database - essentially, synchronizing the changes you made to your models with the schema in the database.



`python manage.py shell`

交互式方式执行python





`Model.__str__()`

The `__str__()` method is called whenever you call `str()` on an object. Django uses `str(obj)` in a number of places. Most notably, to display an object in the Django admin site and as the value inserted into a template when it displays an object. Thus, you should always return a nice, human-readable representation of the model from the `__str__()` method.



`Choice.objects.filter(question__pub_date__year=current_year)`

注意单下划线和双下划线的区别

双下划线表示属性，方法等

use double underscores to perform field lookups



## View

A view is a “type” of Web page in your Django application that generally serves a specific function and has a specific template. 

In Django, web pages and other content are delivered by views.

To get from a URL to a view, Django uses what are known as ‘URLconfs’. A URLconf maps URL patterns to views.

[URL dispatcher](https://docs.djangoproject.com/en/3.2/topics/http/urls/)

There’s a problem here, though: the page’s design is hard-coded in the view. If you want to change the way the page looks, you’ll have to edit this Python code. So let’s use Django’s template system to separate the design from Python by creating a template that the view can use.



The context is a dictionary mapping template variable names to Python objects.

 [Shortcut:](https://docs.djangoproject.com/en/3.2/topics/http/shortcuts/#module-django.shortcuts)

`render`

`get_object_or_404`

The template system uses dot-lookup syntax to access variable attributes. In the example of `{{ question.question_text }}`, first Django does a dictionary lookup on the object `question`. Failing that, it tries an attribute lookup – which works, in this case. If attribute lookup had failed, it would’ve tried a list-index lookup.

[Templates guide](https://docs.djangoproject.com/en/3.2/topics/templates/)



templates 中使用 url 去解耦合

Add namespaces to your URLconf to specify the views used:

`<li><a href="{% url 'polls:detail' question.id %}">{{ question.question_text }}</a></li>`



`reverse`.   方便调用某个view

```python
from django.urls import reverse

return HttpResponseRedirect(reverse('polls:results', args=(question.id,)))
```





`generic views system`

Generic views abstract common patterns to the point where you don’t even need to write Python code to write an app.



`ListView`:  display a list of objects

`DetailView`:  display a detail page for a particular type of object

`context_object_name`:  However, for ListView, the automatically generated context variable is `question_list`. To override this we provide the `context_object_name` attribute, specifying that we want to use `latest_question_list` instead.



[generic views documentation](https://docs.djangoproject.com/en/3.2/topics/class-based-views/)



## Test

`python manage.py test polls`







## stylesheet and image

css 要放在polls/static/polls 下 是因为namespace的问题。不是很理解这个问题



```python
class QuestionAdmin(admin.ModelAdmin):
    fieldsets = [
        (None,               {'fields': ['question_text']}),
        ('Date information', {'fields': ['pub_date']}),
    ]
```

The first element of each tuple in [`fieldsets`](https://docs.djangoproject.com/en/3.2/ref/contrib/admin/#django.contrib.admin.ModelAdmin.fieldsets) is the title of the fieldset.
