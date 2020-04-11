# First Django Practice

## Acivating a Virtual Environment
- virtualenv venv
- virtualenv venv --system-site-packages
- source venv/bin/activate

## Deactivation a Virtual Environment
- deactivate

## Reactivating a Virtual Environment 
- source venv/bin/activate

## Uninstall Packages
- sudo pip3 uninstall ______packagename______

## Starting Off With Django
- sudo pip3 install django==1.11.24
- django-admin startproject django_todo .
- python3 manage.py runserver

## If Migration Is Required:
- python manage.py makemigrations
- python manage.py migrate

## Get Aliases (Not important, so it is okay, if it does not work)
- nano ~/.bashrc
- alias run = "python3 manage.py runserver"
- Then press "Ctrl + X" to save, "Y" for yes, and then press the <enter> button
- Run the page using 'run' in the terminal

## Extra Notes:

### Reset git add
- git reset
### Get all in the venv
- pip3 list

## Next Step
- settings.py
- urls.py
- views.py (return render(request, "todo-list.html"))

## Admin

### SQLite3
- sqlite db.sqlite3

### Check content
- select * from django_migrations;
- .quit

### Apply migrated commands to the database
- python3 manage.py migrate

### Check content again
- select * from django_migrations;
- .tables

### See column names
- .headers on
- select * from django_migrations;

### Show neat columns
- .mode column
- select * from django_migrations;

### Quit
- .quit

### Create a brand new user with administrative rights, placed inside of the auth_user table
- python3 manage.py createsuperuser

#### Entered infos for this practice project
- Username: admin
- Email address: admin@example.com
- Password: theadminpass

### Check for new admin in SQLite3
- sqlite3 db.sqlite3
- .tables
- select * from auth_user;

#### To make it more readable
- .mode column
- .header on
- select * from auth_user

### Side Note: Booleans
- 1 True
- 0 False

### Runserver
- python3 manage.py runserver
- Go to the URL with /admin and login

## Next step
- models.py
- python3 manage.py makemigrations
- python3 manage.py migrate
- (The command above is for configuration code for Django to know what to do with the file, so creates a table in the database, called todo_item)
- sqlite3 db.sqlite3
- .tables

## Next step
- admin.py

## Tests
- python3 manage.py test

## Coverage
- After test_views.py, test_forms.py and test_models.py
- sudo pip3 install coverage
- coverage run manage.py test
### See everything that has been tested
- coverage report 
### Specify which tests should be shown
- coverage run --source=todo manage.py test
- this command above, says we only want to test the files in the to do directory

### Coverage HTML (still in terminal)
- coverage html
- Then, in test_models.py:
```python
def test_item_as_a_string(self):
        item = Item(name="Create a Test")
        self.assertEqual("Create a Test", str(item))
```

- Command: coverage run --source=todo manage.py test

### Generating a new coverage report
- coverage run --source=todo manage.py test
- coverage html

## If Django IDs are not working 
- pip install pylint-django

## Heroku
- heroku
- heroku login
- heroku apps

## Gunicorn (used to actually run the application on the server the)
- sudo pip3 install gunicorn

## psycopg (this will allow us to connect to a PostgreSQL database so instead of using MySQL or SQLite for this)
- sudo pip3 install psycopg2~=2.7.3.1
- the reason for this is that Postgres is very easy to setup on Heroku to really encourage it we can get it up and running with a single command 
- pip3 freeze --local > requirements.txt
- If not included already, manually add to the requirements.txt file: Django==1.11.24
- If not included already, manually add to the requirements.txt file: pytz==2019.3 

- heroku create simple-django-todo --region eu
- Get this link that the command above gives: https://simple-django-todo-rian.herokuapp.com/

## Deployment
### Heroku Help
- See all apps: heroku apps
- See commands that can be run that are specific to the kind of apps context that are here in heroku apps: heroku
- See all the addons: heroku addons 
- See all the apps: heroku apps --all
- For other CLI commands: herokus help

### Creating a Database
- heroku addons:create heroku-postgresql:hobby-dev

### Connect to the Remote Database
- sudo pip3 install dj_database_url
- Find Database URL in the dashboard: settings -> reveal configs
- Find Database URL here, instead of the dashboard: heroku config
- Comment in the DATABASE dictionary in settings.py
- Add this in settings.py:
```python
if "DATABASE_URL" in os.environ:
    DATABASES = {
        'default': dj_database_url.parse(os.getenv('postgres://iopaqnzajwfigq:a1ef69b6d27732802f160a2cfbb976c150e9eb30656d67e298f9678b3264f492@ec2-54-247-79-178.eu-west-1.compute.amazonaws.com:5432/d82sr5tg6ugvsm'))
    }
else:
    print("Postgres URL not found, using sqlite instead")
    DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.sqlite3',
            'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
        }
    }
```
- Add this in settings.py: import dj_database_url