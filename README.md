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
* Django concepts to remember.  In Django you have a project, think of this as the entire site, then you have apps.  You might have a calculator app, a calendar app, a survey app all within the project.    
* manage.py is the command line tool for Django. It's used to run the server, create migrations, etc.    
* settings.py is where we keep our secret key, base directory, define the database, middleware, etc.  Sqlite3 is the default database for Django.
