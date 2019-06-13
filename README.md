# DjangoArchitecture

[https://medium.com/@timmykko/a-quick-glance-of-django-for-beginners-688bc6630fab](link)

Web-Framework

Whenever you type in a URL, your browser makes a request to a server, which will send files — generally HTML — and your browser will process it and display it. At the end of the day, no matter how complicated your web application is, all it does is send files due to a request.

A web framework provides a toolkit of reusable components allowing developers to focus on building their app rapidly without reinventing the wheel. Problems like how do you map a certain URL to a set of code or how do you dynamically create a page according to some data from your database arise in every web app. A web framework will allow you to do that quickly so you can focus on writing the code for the given URL or on the contents of a certain page. These two main problems are called routing and templating, respectively, and are main components in many web frameworks.

Note: Front-end web frameworks are entirely different

Django is one of the most popular and huge open-source web frameworks. It is written in python and companies like Instagram, Doordash, and Disqus use it in their systems, which hopefully is enough to show that Django is robust and scalable.

Django Architecture
Django follows a Model-View-Controller(MVC) architecture, which is split up into three different parts:

The Model is the logical data structure behind the entire application and is represented by a database(generally relational databases such as MySql, Postgres).
The View is the user interface — what you see in your browser when you visit a website. These are represented by HTML/CSS/Javascript files.
The Controller is the middleman that connects the view and model together, meaning that it is the one passing data from the model to the view.
With MVC, your application will revolve around the model—either displaying it or manipulating it.

The Model-View-Template (MVT) is slightly different from MVC. In fact the main difference between the two patterns is that Django itself takes care of the Controller part (Software Code that controls the interactions between the Model and View), leaving us with the template. The template is a HTML file mixed with Django Template Language (DTL).

Django is mainly an MTV (Model-Template-View) framework. It uses the terminology Templates for Views and Views for Controller.

Template relates to the View in the MVC pattern as it refers to the presentation layer that manages the presentation logic in the framework and essentially controls the content to display and how to display it for the user.

Thus our Python code will be in views and models and HTML code will be in templates.

The MVT (Model View Template) is a software design pattern. It is a collection of three important components Model View and Template. The Model helps to handle database. It is a data access layer which handles the data.

The Template is a presentation layer which handles User Interface part completely. The View is used to execute the business logic and interact with a model to carry data and renders a template.

IMAGE


So say a user will enter a URL in their browser, that request will go through the internet protocols, to your server, which will call Django. Django will then process the given URL path, and if it matches an URL path you have explicitly stated, it will call the Controller, which will then perform a certain action, such as get an entry from your Model(database) and then render a View(ie: JSON text, HTML/CSS/JavaScript Web page).

