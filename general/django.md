# Django

## General Overview

### Views

- Python function that takes a web request and returns a web response
- Response can be anything (html, image, xml, etc.)
- Need to map URL to views

### Models

- Represents database layout with additional metadata
- Define data model in one place and automatically derive things from it
- Located in AppName/models.py
    - Each model is a class that subclasses models.Model
    - Each model has number of class varaibles, which represent database fields
    - Name of each var is used by python and database column name


### Database

- Database models located in models.py
    - When change run `python manage.py makemigrations` to create migrations for changes
    - Run `python manage.py migrate` to apply changes

## Many-to-Many
We can't create a model instance with many-to-many relationships. We first have to create the instance, then add the relationships using `add` or `set`

### Adding Queryset results to many-to-many
```python
permissions = Permission.objects.all()

group = MyGroup.objects.get(name='test')

group.permissions.add(*permissions)
```

### Replacing all many to many relationships
```python
permission = Permission.objects.get(name='user_edit')
group = MyGroup.objects.get(name='test')
group.permissions.set([permission])
```
### Get model that contains no many-to-many
```python
class User(models.Model):
    name = models.CharField()
    grades = models.ManyToManyField('Grade')
    
User.objects.filter(grades=None)
```

## Queries
### 'Or' query
Use `Q` with `|` to define `or` queries.
```python
from django.db.models import Q

Item.objects.filter(Q(creator=owner) | Q(moderated=False))
```

## Refresh model from db
```python
    obj.refresh_from_db()
```

## Undo migrations

Migrations
```
0010_previous_migration
0011_migration_to_revert
```
`./manage.py migrate my_app 0010_previous_migration` 

### Undo all migrations

`./manage.py migrate my_app zero`
