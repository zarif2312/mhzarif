# Basic Command That Relate to Django

This is a note for basic command

## Basic Command for Git
<details>
  <summary>Click to expand!</summary>
  
### 1) git config
**Utility** : To set your user name and email in the main configuration file.
  
**How to** : To check your name and email type in **_git config --global user.name_** and **_git config --global user.email_**. And to set your new email or name **_git config --global user.name = “Zarif”_** and **_git config --global user.email = “zarif9110@gmail.com”_**
  
### 2) git init
**Utility** : To initialise a git repository for a new or existing project.

**How to** : **_git init_** in the root of your project directory.

### 3) git clone
**Utility :** To copy a git repository from remote source, also sets the remote to original source so that you can pull again.

**How to : _git clone <:clone git url:>_**

### 4) git status
**Utility :** To check the status of files you’ve changed in your working directory, i.e, what all has changed since your last commit.

**How to : _git status_** in your working directory. lists out all the files that have been changed.

### 5) git add
**Utility :** adds changes to stage/index in your working directory.

**How to : _git add ._**

### 6) git commit
**Utility :** commits your changes and sets it to new commit object for your remote.

**How to : _git commit -m ”sweet little commit message”_**

### 7) git push/git pull
**Utility :** Push or Pull your changes to remote. If you have added and committed your changes and you want to push them. Or if your remote has updated and you want those latest changes.

**How to : _git pull <:remote:> <:branch:>_** and **_git push <:remote:> <:branch:>_**

### 8) git branch
**Utility :** Lists out all the branches.

**How to : _git branch_** or **_git branch -a_** to list all the remote branches as well.

### 9) git checkout
**Utility :** Switch to different branches

**How to : _git checkout <:branch:>_** or **_git checkout -b <:branch:>_** if you want to create and switch to a new branch.

### 10) git stash
**Utility :** Save changes that you don’t want to commit immediately.

**How to : _git stash_** in your working directory. **_git stash_** apply if you want to bring your saved changes back.

### 11) git merge
**Utility :** Merge two branches you were working on.

**How to :** Switch to branch you want to merge everything in. **_git merge <:branch_you_want_to_merge:>_**

### 12) git reset
**Utility :** You know when you commit changes that are not complete, this sets your index to the latest commit that you want to work on with.

**How to : _git reset <:mode:> <:COMMIT:>_**

### 13) git remote
**Utility :** To check what remote/source you have or add a new remote.

**How to : _git remote_** to check and list. And **_git remote add <:remote_url:>_**

</details>

## Basic Command for Django

### 1) 01porjectone
<details>
  <summary>Click to expand!</summary>
  
To create a new django project use below command:

**_django-admin startproject helloworld_**

after that, create an app in your project by using below command, your app folder will appear:

**_python manage.py startapp hola_**

At **_settings.py_** file at the main project folder, insert the name of your app in **INSTALLED_APPS**

In **_views.py_** file, you can create a simple httpresponse such as:

```python
from django.Http import HttpResponse
def homePageView(request):
  return HttpResponse('This will shown in the browser')
```
Then, create a **_urls.py_** file in **hola** folder and write the following code:
```python
from django.urls import path
from . import views
urlpatterns = [
    path('', views.homePageView, name='home'),
]
```
to connect the path from hola project, you need to register it in the **_url.py_** at the main app:
```python
urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('hola.urls')),
]
```
Finally, use command **_python manage.py runserver_** to make sure it is successfull.

</details>

### 2) projecttwo
<details>
  <summary>Click to expand!</summary>
In this project, we want to homepage template. Setup the project, create a new app named **_website_**. Then, create new folder at the base directory named **_templates_**

To connect **_templates_** folder into the main project, in **_setting.py_** , at the **_TEMPLATES_**, insert the following code:
```python
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [os.path.join(BASE_DIR, 'templates')],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]
```
after that, in **_views.py_** in **website** folder, remove all the existing coding and add the following code.
```python
  from django.views.generic import TemplateView
  class HomePageView(TemplateView):
    template_name = 'home.html'
```
Then, set the path at **_setting.py_** at the main project folder.
```python
path('', include('website.urls')),
```
Then create **_urls.py_** file in the website folder and write this code:
```python
from django.urls import path
from . import views
  urlpatterns = [
    path('', views.HomePageView.as_view(), name='home'),
  ]
```
Runserver to see if it is works.

**Exercise**: Create a aboutus and contact us hmtl with the same step as above

#### Pre built templates
1. Create **_nav.html_** file in template folder. add the following code:
```html
<header>
    <a href=" {% url 'home' %} ">Home</a> | <a href=" {% url 'about' %}">about us</a> | <a href=" {% url 'contact' %}">contact us</a>
</header>
{% block content %}
{% endblock %}
```
2. Then extend the **_nav.html_** page to **_home.html_**, **_about.html_** and **_contact.html_** with the following code: 
```html
{% extends 'nav.html' %}
{% block content %}
<h1>This is my website homepage</h1>
{% endblock %}
```
repeat the 2. step into **_about.html_** page and **_contact.html_** page
</details>

### 3) projectthree
<details>
  <summary>Click to expand!</summary>
In this project, we want to interact with the database.

First, setup a new project, named commandr. And create an app named cmdr. We create a database in **_models.py_** files, then we need to register it in **_admin.py_** file.

to create an initial database based on default setting.

**_python manage.py migrate_** 

create a simple database in **_models.py_** file 
```python
class Cmdr (models.Model):
    text = models.TextField()
```
Then do the below command:

**_python manage.py makemigrations cmdr_**

**_python manage.py migrate cmdr_**

whenever you edit the database in **_models.py_**, you need to make a migration.

Then, we need to generate **admin ID** and **password**. To do that, 

**_python manage.py createsuperuser_**

after that, you can login the admin site

**We need to register our model to admin site**. to do that. go to admin.py file a write this code

```python
from .models import Cmdr
admin.site.register(Cmdr)
```
run the server and you can see that **Cmdr** appear. 

to remove/edit the naming convention in the **Cmdr**, write the following code, in the Cmdr class in **_models.py_**:
```python
def __str__(self):
        return self.text
```
**Showing data to frontend**

write this code in **_views.py_**
```python 
from django.views.generic import ListView
from .models import Cmdr
class homePageView(ListView):
    model = Cmdr
    template_name = 'home.html'
```
then, create a **temlplates** folder and create a **_home.html_**. Setup as we learn before.

To make our data appear in frontend. we need to do something in the **_home.html_**. 
```html
  {% for c in object_list %}
  <li>
    <input type="radio" id="f-option" name="selector">
    <label for="f-option">{{ c }}</label>

    <div class="check"></div>
  </li>
  {% endfor %}
```
the above code will get the data from the **_models.py_** file
</details>
  
### 4) projectfour

In this project, the goal is to explore more on static file such as attach bootstrap, css, and javascript file. And also explore more on database interaction.

1) Setup a project name website. and create an app named articles.

2) In **_models.py_**, write the following code:
```python
class Article(models.Model):
    author = models.ForeignKey(
        'auth.User',
        on_delete=models.CASCADE,
    )
    title = models.CharField(max_length=200)
    text = models.TextField()
    
    def __str__(self):
        return self.title
```
3) Make a migrations and migrate the database that we just create

**_python manage.py makemigrations articles_**

**_python manage.py migrate articles_**

4) Create a superuser so that we can log in the admin panel

5) Register the model into admin file so that it can appear in admin panel
```python
from .models import Article
admin.site.register(Article)
```
6) To setup templates, create a folder named templates and create a file named home.html and base.html. Then register templates into settings.py fille

7) Create view in a views.py
```python
from django.views.generic import ListView
from . models import Article
class ArticleListView(ListView):
    model = Article
    template_name = 'home.html'
```

8) create a urls.py in articles folder and insert the the following code:
```python
from django.urls import path
from . import views
urlpatterns = [
    path('', views.ArticleListView.as_view(), name='home.html'),
]
```

9) in urls.py in main project, create a path for articles.
```python
from django.contrib import admin
from django.urls import path, include
urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('articles.urls')),
]
```
10) In base.html file. insert the following code:
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Zarif's Personal Blog</title>
</head>
<body>
    <div class="container">
        {% block content %}        
        {% endblock %}
    </div>
</body>
</html>
```

11) In home.html file. Insert the following code: Then runserver
```html
{% extends 'base.html' %}
{% block content %}
{% for arti in object_list %}
    <div class="article">
        <h3><a href="">{{ arti.title }}</a></h3>
        <p>{{ arti.text }}</p>
    </div>
{% endfor %}
{% endblock %}
``
12) Now, it is time to learn how to link with static files such as css file. first, create static folder at base dir. inside static folder, create a css folder. then create a **_basestyles.css_** file. make any css code as you want.

13)Then we need to register static folder. To do that, go to **_settings.py_** file. add this code at the bottom:
```python
STATICFILES_DIRS = [os.path.join(BASE_DIR, 'static')]
```
14) Then go to **_base.html_** file, add **_{% load static %}_** at the very top of the file. Then add below code to link with css.
```html
<link rel="stylesheet" href="{% static 'css/basestyles.css' %}">
```
