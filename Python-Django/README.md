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
### Django Temples loops
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

```python

```
```python

```
```python

```