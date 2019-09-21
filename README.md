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

At the terminal type.  In this example, the name of the project is called 'pollster'. I just have nameofproject to show where it goes.  The name of the app will be called 'polls'.
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

In the project folder, type in the following.  This example app will be called "polls"
```
python manage.py startapp nameofapp
```
This creates the following structure inside your project folder.    
```
polls > #folder
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

In the settings.py file we need to add the app to the INSTALLED_APP array.  In this example, it's the top line.
```
INSTALLED_APPS = [
    'polls.apps.PollsConfig'
    'django.contrib.admin',
]
```
This refers to the apps.py file in the polls folder

#### Create migrations

Make sure you are in the 'pollster' or project folder. On the command line type the following.
```
python manage.py makemigrations polls
```
If done correclty, you'll get something like this in the terminal, and a migrations folder in the folder tree
```
Migrations for 'polls':
  polls/migrations/0001_initial.py
    - Create model Question
    - Create model Choice
(_Python_practice) bash-3.2$ 
```

To run the migrations we need to put the tables in the database. At the terminal run.
```
python manage.py migrate
```

#### This is a little extra.  It is not absolutely necessary to your project

This how to manipulate the data from within the shell.

```
python manage.py shell
```

Now import the question and choice models we made in the DB. Refer to "Create the database" above if you forgot.
```
from polls.models import Question,Choice
```
Now we can make queries.  For instance, with the quesiton model...
```
Question.objects.all()  // Enter
```
In this project we need to import the timezone module since we're using a publication date
```
from django.utils import timezone
```
Next, we'll setup the questions
```
q = Question(question_text='What is your favorite cookie?', pub_date=timezone.now())
```
Now we have to save the question to the database
```
q.save()
```
Next, test that it is in the database
```
q.id
```
The result should be 1.  Next, type in
```
q.question_text
```
It should show the question.  While we're still in the shell type
```
Question.objects.all)
```
We can filter questions, too.  This will return it as an array
```
Question.objects.filter(id=1)
```
This will filter just the question. The pk is for primary key
```
Question.objects.get(pk=1)
```
Now we'll set the question to the variable 'q'
```
q = Question.objects.get(pk=1)
```
We can type in the following and see that we have no choices for that question
```
q.choice_set.all()
```
Now we'll create some choices.  You see the choice appear after entering this command line
```
q.choice_set.create(choice_text="chocolate chip", votes=0)
```
Now we can do it again by adding another choice
```
q.choice_set.create(choice_text="oatmeal", votes=0)
```
And lastely add
```
q.choice_set.create(choice_text="sugar", votes=0)
```
Now check all the choices
```
q.choice_set.all()
```
Now you can quit out of this by typing
```
quit()
```


#### Setup the Admin area

You should be in the project folder.  In this example, pollster.  Now we're going to setup the admin.  After entering the command line code below, you will be asked to create an admin name, email address, and a password.  In this example I will use: admin=admin, email=webdevdave@hotmail.com, password=123taco
```
python manage.py createsuperuser
```

Run the server.  It's possible that you're server is already running, but do this anyway
```
python manage.py runserver
```
Now would should be able to go to localhost:8000/admin and see the Django admin login.  Login and you'll see the site administration page.
























