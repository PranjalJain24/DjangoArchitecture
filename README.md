# DjangoArchitecture

## Web-Framework

Whenever you type in a URL, your browser makes a request to a server, which will send files — generally HTML — and your browser will process it and display it. Thus all the Web Applications send the files according to the request. While making those applications developers face problems like how do you map a certain URL to a set of code or how do you dynamically create a page according to some data from your database arise in every web app.  These two main problems are called routing and templating, respectively, and are main components in many web frameworks.

So basically a web framework provides a toolkit of reusable components allowing developers to focus on building their app rapidly without reinventing the wheel.  A web framework will allow you to do things quickly so you can focus on writing the code for the given URL or on the contents of a certain page.

Note: Front-end web frameworks are entirely different

## Django

Django is one of the most popular and huge open-source web frameworks. It is written in python and companies like Instagram, Doordash, and Disqus use it in their systems.

### Django Architecture

Django follows a **_Model-View-Controller(MVC)_** architecture, which is split up into three different parts:

* The **_Model_** is the logical data structure behind the entire application and is represented by a database(generally relational databases such as MySql, Postgres).
* The **_View_** is the user interface — what you see in your browser when you visit a website. These are represented by HTML/CSS/Javascript files.
* The **_Controller_** is the middleman that connects the view and model together, meaning that it is the one passing data from the model to the view.
With MVC, your application will revolve around the model—either displaying it or manipulating it.

Django is mainly an MTV (Model-Template-View) framework. The **_Model-View-Template (MVT)_** is slightly different from MVC. In fact the main difference between the two patterns is that Django itself takes care of the Controller part (Software Code that controls the interactions between the Model and View), leaving us with the template. 
The template is a HTML file mixed with Django Template Language (DTL).Template relates to the View in the MVC pattern as it refers to the presentation layer that manages the presentation logic in the framework and essentially controls the content to display and how to display it for the user.

 It uses the terminology Templates for Views and Views for Controller.
Thus our Python code will be in views and models and HTML code will be in templates.

![alt text](https://github.com/PranjalJain24/DjangoArchitecture/edit/master/django-mvt-based-control-flow.png "Logo Title Text 1")

Here, a user requests for a resource to the Django, Django works as a controller and check to the avai,lable resource in URL. If URL maps, a view is called that interact with model and template, it renders a template. Django responds back to the user and sends a template as a response.

### Django Request and Response Flow

#### The Web Server & WSGI:
When you hit enter in your browser to load a page, your request makes its way through the internet. This server needs to know what to do with what you just sent it. That’s a job for the Web Server Gateway Interface, or WSGI. All WSGI does is take your request and give you back a response. Django has this WSGI layer.

#### Middleware:
![alt text](https://github.com/PranjalJain24/DjangoArchitecture/edit/master/wsgi_middlewares.png "Logo Title Text 2")

Middleware shows up multiple times in between the two WSGI parts. Django middleware is a really small, light-weight plugin that modifies the requests that come in and the responses that go out.
Middleware comes in five flavors – request middleware, view middleware, error middleware, template response middleware, and response middleware. 

#### Flow in Django:

When you run the project by ```python manage.py runserver``` it directs from ```manage.py``` page to ```settings.py``` as we have included this in ```manage.py``` file:
```
os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'ecom.settings')
```
Post that it is directed to ```<project>/urls.py``` file from where it gets all the views.
```ROOT_URLCONF = 'ecom.urls'```
Now in ```<project>/urls.py``` we add various url patterns linking to their respective views directly or we can include the app's url which further has url patterns linking to the views corresponding to that particular app only:
```
urlpatterns = [   
    path('Product/', include('Product.urls')),
    path('courses/', include('courses.urls')),
    path("home",home_view),
    path("about",about_view) 
]
```
After getting into the views which can be either function based or class based, Django directs it to templates that we include which in turn give the response. A snippet showing both the types:
```
def product_list_view(request):
    queryset = Product.objects.all() #list of objects
    context={
        "object_list": queryset
    }
    return render(request,"products/product_list.html",context)

class CourseListView(View):
    template_name = 'courses/course_list.html'
    queryset = Course.objects.all()
    
    def get_queryset(self):
        return self.queryset
    
    def get(self, request, *args, **kwargs):
        context = {'object_list':self.get_queryset()}
        return render(request, self.template_name, context)
```
Or the views directly give the response to Django Server:
```
from django.http import HttpResponse
 
def index(request):
    return HttpResponse('Hey There!!')
```
Django's models provide a simple mapping to the underlying database structure. Django uses a model to execute SQL behind the scenes to return Python data structures – which Django calls QuerySets.
```  
class Course(models.Model):
    title = models.CharField(max_length=120)
```

### Django Apps and Core Files

Any Django project will have at least one Django app. A Django project encompasses the application and all its components, while a Django app is a sub-container of the application with its own functionality that, in theory, may be reusable in another application without much modification. For simplicity’s sake, we will create one app called ```myapp``` under a Django project called ```MySite```.

Before strating the project we should set up Virtual Environment for the project. The main purpose of Virtual environments is to create an isolated environment for Python projects. This means that each project can have its own dependencies, regardless of what dependencies every other project has.
```
python -m venv <venv-name>
.\<venv-name>\Scripts\activate
```
Now you are ready to start your new project. 
```
$ django-admin startproject MySite
$ python manage.py runserver
$ python manage.py startapp myapp
```
This will start your project and the Django development server, a lightweight Web server written purely in Python and also your app inside the project. Go to link — http://127.0.0.1:8000/ You will find your server up and Running !!!

A typical Django project structure will look like this:
```
MySite/
    manage.py
    MySite/
        __init__.py
        settings.py
        urls.py
        wsgi.py
    myapp/
        views.py
        models.py
        __init__.py
        admin.py
        tests.py
        urls.py
        static/ 
            myapp/
                style.css
                index.js
                background.jpg
        templates/
             index.html
             aboutus.html
             post.html 
        migrations/
            __init__.py
            0001_initial.py
            
```

All the files under myapp/ describe the Django app named myapp.

* ```manage.py```- A command-line utility for executing Django commands from within your project and allows you to run administrative tasks like runserver, createsuperuser, migrations of your database models. It directs the program to ```settings.py``` file.

* ```settings.py``` — This is the master configuration file for your project in which you will be connecting our PostgreSQL database. You can configure Middle wares, Installed Apps, LDAP(Light Weight Directory Access Protocol) Settings, Django Email Settings, Production Settings Static and Media Files Root Directory through this file only.
```
DATABASES = {
     ‘default’: {
            ‘ENGINE’: ‘django.db.backends.sqlite3’,
            ‘NAME’: os.path.join(BASE_DIR, ‘db.sqlite3’),
      }
}
```
SQLITE3 is the default database used. If you want to connect to any other database connection you will have to make necesary changes in this like engine, name, add user, add password, etc.

* ```myapp/models.py``` is the Model, or where you define your database. This file is used to write Class based Models for our Django Applications.This will be the blueprint of our database design ,relationships and attribute constraints.

* ```myapp/views.py``` is the Controller. Um, but why is the controller called views? Inside views.py you will define different functions/classes. A function defines what happens when a certain URL is accessed and an HTTP request is made the server. Common actions would be to query the database for records and render a certain HTML template file.
You will be defining our Class Based List Views , CustomFilter Views and Detail Views for our Django Models through Serializers using Django Rest Framework. These are the classes which will be actually handling the HTTP Requests.

* Everything under ```myapp/templates/myapp/``` are templates or HTML files that define your View. When a function in views.py renders an HTML file, it can pass objects such as a list of comments in which you can use special syntax to display those comments. Within each template, you can get static files like CSS, Javascript files, or images to give the webpage life.

* ```urls.py``` is the URL configuration file. This is the file that allows you to map a certain URL to a certain function in views.py. This file can define the routes/API Endpoints itself or You can just write your Endpoints in the respective django application and include the application urls.py file here. This file will be the single point of source for finding Endpoints once the HTTP Requests come from the client side.

### Django Object-Relational Mapper. 
The Django web framework includes a default object-relational mapping layer (ORM) that can be used to interact with application data from various relational databases. Django uses its ORM mappers to map objects to database tables. An ORM or object relational mmapper is a code library which helps you manipulate the data from a database using the object-oriented paradigm. The main databases that Django works on are PostgreSQL,MySQL, SQLite, Oracle. It can also work with otherdatabases using the third party drivers.

We take an example of PollsApp to understand this feature of Django. In that we have two models: Question  and Choice in app called polls. To make changes in your database run these commands on your local terminal:
```
python manage.py shell
>>> from polls.models import Choice, Question  # Import the model classes.

# To display all the Questions in the system:
>>> Question.objects.all()

# Create a new Question.
>>> from django.utils import timezone
>>> q = Question(question_text="Is this my third Question?", pub_date=timezone.now())

# Save the object into the database. You have to call save() explicitly.
>>> q.save()

#Set choices for question having id=3: 
>>> q = Question.objects.get(pk=3)

# Display any choices from the related object set -- none so far.
>>> q.choice_set.all()
<QuerySet []>

# Create two choices.
>>> q.choice_set.create(choice_text='Yes', votes=0)
<Choice: Yes>
>>> q.choice_set.create(choice_text='No', votes=0)
<Choice: No>

#Let's delete the object from the database.
>>>
>>> q.delete()
(1, {'polls.Question': 1})
>>>
This command removes the question with ID 1 from the database. However, it is still exists inside the shell.
```
