# Django-Python-Notes
Django-Python Notes

Make sure Pip is up todate. This is for Mac.        
```
sudo -H pip install --upgrade pip
```

Setup the Pip environment.  Do this locally to the file instead of globally.  It's done this way.
```
pip install pipenv
```

Next to create the virtual environment.  Any packages installed will go into this virtual environment rather than the global environment.    
```
pipenv shell
```

When done you'll see something like...    
```
✔ Successfully created virtual environment! 
Virtualenv location: /Users/davidmartinson/.local/share/virtualenvs/_Python_practice-PzhcMqkK
Creating a Pipfile for this project…
Launching subshell in virtual environment…
bash-3.2$  . /Users/davidmartinson/.local/share/virtualenvs/_Python_practice-PzhcMqkK/bin/activate
(_Python_practice) bash-3.2$ 
```

Now we can install Django.  The Django package will show up in our Pipfile 
```
pipenv install django
```

### Start the project

At the terminal type.    
```
django-admin startproject nameofproject
```

This will create a nameofproject folder.    
* Django concepts to remember.  In Django you have a project. Think of this as the entire site. Then you have apps.  You might have a calculator app, a calendar app, a survey app all within the project.    
* manage.py is the command line tool for Django. It's used to run the server, create migrations, etc.    
* settings.py is where we keep our secret key, base directory, define the database, middleware, etc.  Sqlite3 is the default database for Django.
* urls.py file is the routes file. Each app has its own urls.py file. 

#### Run the server

In the folder that contains manage.py type.
```
python manage.py runserver
```

There will likely be a number of unapplied migration warnings.  No problem.  Just stop the server and run...
```
python manage.py migrate
```

#### Create an app

In the project folder, type in the following.
```
python manage.py startapp nameofapp
```
This creates the following structure inside your project folder.    
```
nameofapp > #folder
  migrations > # a folder
  __init__.py
  admin.py
  apps.py
  models.py  # where we create the db model
  tests.py
  views.py
```

#### Create the database

In the models file create the database.  Here is a sample db.
```
from django.db import models

# Create your models here.

class Question(models.Model):
    question_text = models.CharField(max_lenth=200)
    pub_date = models.DateTimeField('date published')

    def __str__(self):
        return self.question_text

class Choice(models.Model):
    question = model.ForeignKey(Question, on_delete=models.CASCADE)
    choice_text = models.CharField(max_length=200)
    votes = models.IntegerField(default=0)

    def __str__(self):
        return self.choice_text
```
