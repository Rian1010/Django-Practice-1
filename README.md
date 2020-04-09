# First Django Practice

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