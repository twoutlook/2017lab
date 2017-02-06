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

