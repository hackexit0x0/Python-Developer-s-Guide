### Django Web Application Project Code
+ [Install & Create Virtual Environment:](#)
+ [Create Django Project](#)
+ [Database Setup and Migrations](#)
  + [Configuration File](#)
     + [urls.py](#)
     + [views.py](#)
     + [settings.py](#)
+ [](#)
+ [](#)
+ [](#)
+ [](#)
+ [](#)
+ [](#)
+ [](#)
+ [](#)
+ [](#)
+ [](#)
+ [](#)
+ [](#)
+ [](#)
+ [](#)
+ [](#)
+ [](#)
+ [](#)
+ [](#)
+ [](#)
+ [](#)
+ [](#)
+ [](#)
+ [](#)
+ [](#)
+ [](#)
+ [](#)
+ [](#)
+ [](#)

### 1. Install & Create Virtual Environment:
```python
# 1. Django Install Setup
# 2. Create Virtual Environment in Windows Command Prompt
# 3. Activate the Virtual Environment
# 4. Install Required Modules
# 5. Verify Installation
pip install virtualenv
python -m venv myenv
# This creates a virtual environment named "myenv" in your current directory.
# 2. Activate the Virtual Environment:
myenv\Scripts\activate
# ectivate error commdna (in Powershell run with administrator)
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned
# After activation, you'll see (myenv) in your command prompt.
# 3. Install Django:
pip install django
# 4. Install Other Common Modules:
pip install pillow
pip install python-decouple
pip install django-crispy-forms
pip install requests
# 5. Create requirements.txt file
pip freeze > requirements.txt
# 6. Install from requirements.txt (for future setup)
pip install -r requirements.txt
#7 . Deactivate Virtual Environment
deactivate
# 8. Verify Django Installation
python -m django --version
```
### Create Django Project
```python
# After activating virtual environment and installing Django
# Create a new Django project
django-admin startproject myproject
# Navigate into project directory
cd myproject
# Create a new Django app
# python manage.py startapp myapp
# Run Server
# Start the Django development server
python manage.py runserver
# Server will run at http://127.0.0.1:8000/
# Admin panel available at http://127.0.0.1:8000/admin/
# To run on different port
python manage.py runserver 8080
# To run on specific IP
python manage.py runserver 0.0.0.0:8000
```
### Database Setup and Migrations
```python
# Create initial database tables
python manage.py makemigrations
python manage.py migrate
# Create superuser for admin panel
python manage.py createsuperuser
# Follow prompts to set username, email, and password
```
### [Configuration File]
+ settings.py
```Python
    # configuration templest include file : 'DIRS': [BASE_DIR / "templates"],
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [BASE_DIR / "templates"],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]
```
+ urls.py
```python
from django.contrib import admin
from django.urls import path
# added
from cloneip import views


urlpatterns = [
    path('uid/<uid>', views.uid),
    # admin
    path('admin-cpl/', admin.site.urls),
    # Home
    path('', views.HomePage),
    # login
    path('login', views.LoginPage),
    # register
    path('register', views.registerPage),
    # courses.html
    path('courses', views.coursesPage),
    # blog
    path('blog', views.blogPage),
    # about
    path('about', views.aboutPage),
    # contact.html
    path('contact', views.contactPage),
]

```
+ views.py
```python
from django.shortcuts import render
from django.http import HttpResponse

def uid(req, uid):
    return HttpResponse(uid)

# Home
def HomePage(req):
    return render(req, "index.html")

# Login
def loginPage(req):
# add dynamicly titale code : return render(req, "login.html", {"title": "Login"})
    return render(req, "login.html", {"title": "Login"})

# register
def registerPage(req):
    return render(req, "register.html")
# courses
def coursesPage(req):
    return render(req, "courses.html")
# blog
def blogPage(req):
    return render(req, "blog.html")
# about
def aboutPage(req):
    return render(req, "about.html")
# contac
def contactPage(req):
    return render(req, "contact.html")
```
### Django Pass Data HTML in templets
```python
# viwes.py
# Data Pass
def HomePage(req):
    data = {
        # data
        "title":"Home Page",
    }
    return render(req, "index.html", data)

# urls.py
urlpatterns = [
        # add url
    path('', views.HomePage),
]

# tempelst Output data
<title>{{ title }}</title>

```
## Managing static files (css, images, js)
```python
# setting.py configuration add
STATICFILES_DIRS = [
    BASE_DIR / "static",
    "/var/www/static/",
]

# Link inde file
# css
<link rel="stylesheet" href="/static/css/main.css" class="src">

# link img
{% load static %}
<img src="{% static 'my_app/example.jpg' %}" alt="My image">

# 
```
### Django Templets in loops
+ loops in list
```python
# list
def HomePage(req):
    data = {
        # data
        "title":"Home Page",
        'courses':[
            'Python Programming',
            'Web Development', 
            'Cyber Security', 
            'Bug Bounty Hunting',
            'Networking (CCNA)',
            'Linux for Hackers',
            'Data Analytics',
            'Cloud Computing'
            ]
    }
    return render(req, "index.html", data)

 # Use outputs in loop
 {% for n in courses%}
 <h1>{{forloop.counter0}} {{n}}</h1>
 <h1>{{forloop.last}} {{n}}</h1>
 <h1>{{forloop.fist}} {{n}}</h1>
 {% endfor %}
 ```
+ Dictionary
```python
# Dictionary
def HomePage(req):
    data = {
        "title": "Home Page",
        "courses": [
            "Python Programming",
            "Web Development",
            "Cyber Security",
            "Bug Bounty Hunting",
            "Networking (CCNA)",
            "Linux for Hackers",
            "Data Analytics",
            "Cloud Computing"
        ],
        "courses2": [
            {
                "id": "001",
                "name": "Python Programming",
                "description": "Master Python from basics to advanced with hands-on exercises.",
                "price": 3999,
            },
            {
                "id": "002",
                "name": "Web Development",
                "description": "Learn HTML, CSS, JavaScript, PHP, and MySQL to build websites.",
                "price": 4999,
            },
        ]
    }
    return render(req, "index.html", data)

    
# Distonory data OutPut in HTML
{% for cours in courses2 %}
<h5>{{ cours.name }}</h5>
<p >{{ cours.description }}</p>
<p >₹{{ cours.price|floatformat:0 }}</p> 
{% endfor %}
```
# Django Template Using if...elif..else
```python
def HomePage(req):
    data = {
        "title": "Home Page",
        "courses": [
            "Python Programming",
            "Web Development",
            "Cyber Security",
            "Bug Bounty Hunting",
            "Networking (CCNA)",
            "Linux for Hackers",
            "Data Analytics",
            "Cloud Computing"
        ],
        "courses2": [
            {"id": "001","name": "Python Programming","description": "Master Python from basics to advanced with hands-on exercises.","price": 3999,},
            {"id": "002","name": "Web Development","description": "Learn HTML, CSS, JavaScript, PHP, and MySQL to build websites.","price": 4999,},
            {"id": "003","name": "Cyber Security","description": "Become a pro in ethical hacking and cyber defense.","price": 0,},
        ]
    }
    return render(req, "index.html", data)

# html out put
{% for cours in courses2 %}
<div style="border:1px solid #ddd; padding:10px; margin-bottom:10px; border-radius:8px;">
    <h5>{{ cours.name }}</h5>
    <p>{{ cours.description }}</p>

    {% if cours.price > 0 %}
        <p style="color:green;">Price: ₹{{ cours.price|floatformat:0 }}</p>
    {% elif cours.price == 0 %}
        <p style="color:blue;">Free Course 🎉</p>
    {% else %}
        <p style="color:red;">Price not available</p>
    {% endif %}
</div>
{% empty %}
    <p>No courses available.</p>
{% endfor %}
```

## Headder & Footer Include in Django HTML Tempelts Include (Include, Extends)

+ incude
```py
{% include 'includes/header.html' %}
{% include 'includes/footer.html' %}
```
+ Extebds
> How It All Connects\
base.html contains the layout (head, header, footer, and `{% block content %}`).\
home.html, about.html, etc. extend the base file using `{% extends %}`.\
header.html and footer.html are included in base.html using `{% include %}`.
```py

# base.html
{% include 'includes/header.html' %}

<main class="container my-5">
    {% block content %}
    {% endblock %}
</main>

{% include 'includes/footer.html' %}
# header.html
# footer.html
# indxe.html
{% extends "base.html" %}

{% block content %}
# All HTML Contens and Code
{% endblock %}

```
## Django URL Template
```py
# Add code urls.py 
path('about', views.aboutPage, name="About-Us"),

# Add Html tags in Code
<li class="nav-item"><a class="nav-link" href="{% url 'home%}">About US</a></li>

```

## How to Highlight link
```python
# code {{request.path}}
{{request.path}}

# html code
{% if request.path == '/' %} active {% endif %}
{% if request.path == '/PathNameAdd' %} active {% endif %}

# addd in html
<li class="nav-item" ><a class="nav-link {% if request.path == '/' %} active {% endif %}" href="/">Home</a></li>
<li class="nav-item"><a class="nav-link {% if request.path == '/about' %} active {% endif %}" href="{% url 'About-Us' %}">About-Us</a></li>

# method 2
{% url 'about' as url %}

# html code
<li class="nav-item" ><a class="nav-link {% if request.path == url %} active {% endif %}" href="{{ url }}">Home</a></li>
```
```python

```
```python

```
```python

```
```python

```
```python

```
```python

```
```python

```

```python

```
```python

```
```python

```