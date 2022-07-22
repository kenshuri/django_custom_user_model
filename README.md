## Minimal Django Custom User Model

Minimal Django Custom User model where the email is used as username.

### Installation

**This should be done at the inception of your project !!** If you already have a project running with the base user model, the process to switch to custom user model is not trivial and must be conducted with care. Refer to [this](https://code.djangoproject.com/ticket/25313) or [this](https://rasulkireev.com/custom-user-model-mid-project-django/) if needed.

Copy the folder `accounts` to the root of your django project.

Then add the following to your `settings.py`:
```python
# setting.py

# Application definition
INSTALLED_APPS = [
    # ...
    'accounts',
    # ...
]

# Custom User model
AUTH_USER_MODEL = 'accounts.CustomUser'

DISPOSABLE_EMAIL_DOMAINS = "accounts/blacklist/disposable_email_domains.txt"
```

Finally, you can run the migrations.
```shell
python manage.py makemigrations
```

You should see the following output:
```
Migrations for 'accounts':
  accounts\migrations\0001_initial.py
    - Create model CustomUser
```
If not, the main chance is that you forgot to add `accounts` to the list of installed apps in `settings.py`. **Do not run the migrations while the migrations on accounts app in not ready!**

Then, **if the migration is ready, ie you saw the above message after running `makemigrations`**, run the following commands:
```shell
python manage.py migrate
python manage.py createsuperuser
```

You can see that an **Email address** is asked instead of a username. Et voilà! You're good to go :)

### Source

* https://learndjango.com/tutorials/django-custom-user-model