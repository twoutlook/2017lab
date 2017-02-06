My Note
=======

# When create app polls,

## mysite/settings.py
```
INSTALLED_APPS = [
    'polls',
```
## polls/urls.py
```
urlpatterns = [
    url(r'^$', views.index, name='index'),
]
```
## mysite/urls.py
```
urlpatterns = [
    url(r'^polls/', include('polls.urls')),
```    

## polls/views.py
from django.http import HttpResponse
def index(request):
    return HttpResponse("Hello, world. You're at the polls index.")

## polls/models.py
``` 
from django.db import models


class Question(models.Model):
    question_text = models.CharField(max_length=200)
    pub_date = models.DateTimeField('date published')


class Choice(models.Model):
    question = models.ForeignKey(Question, on_delete=models.CASCADE)
    choice_text = models.CharField(max_length=200)
    votes = models.IntegerField(default=0)
``` 

# DB
``` 
(myvenv) C:\2017lab\mysite>python manage.py makemigrations
Migrations for 'polls':
  polls\migrations\0001_initial.py:
    - Create model Choice
    - Create model Question
    - Add field question to choice

(myvenv) C:\2017lab\mysite>python manage.py migrate
Operations to perform:
  Apply all migrations: admin, auth, contenttypes, polls, sessions
Running migrations:
  Applying polls.0001_initial... OK
``` 

# Customize Admin
https://docs.djangoproject.com/en/1.10/intro/tutorial07/

```
from django.contrib import admin

from .models import Choice, Question


class ChoiceInline(admin.StackedInline):
    model = Choice
    extra = 3


class QuestionAdmin(admin.ModelAdmin):
    fieldsets = [
        (None,               {'fields': ['question_text']}),
        ('Date information', {'fields': ['pub_date'], 'classes': ['collapse']}),
    ]
    inlines = [ChoiceInline]

admin.site.register(Question, QuestionAdmin)
```

# Add Question on Page
http://localhost:8000/admin/polls/question/add/