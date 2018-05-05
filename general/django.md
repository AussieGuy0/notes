# Django

## Views

- Python function that takes a web request and returns a web response
- Response can be anything (html, image, xml, etc.)
- Need to map URL to views

## Models

- Represents database layout with additional metadata
- Define data model in one place and automatically derive things from it
- Located in AppName/models.py
    - Each model is a class that subclasses models.Model
    - Each model has number of class varaibles, which represent database fields
    - Name of each var is used by python and database column name


## Database

- Database models located in models.py
    - When change run `python manage.py makemigrations` to create migrations for changes
    - Run `python manage.py migrate` to apply changes
