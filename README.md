# Todo_Postgre

https://herokudjangopostgretodo.herokuapp.com/

'''
pip install django-heroku (if heroku shows some error(in ubuntu):sudo apt install libpq-dev)
pip install gunicorn
pip install python-decouple
'''

In Setting.py:---------------------------------

import django_heroku
from decouple import config
import dj_database_url

create a file .env:
keep SECRET_KEY their 

and in settings.py:
SECRET_KEY = config('SECRET_KEY')

middleware: 'whitenoise.middleware.WhiteNoiseMiddleware',

STATICFILES_DIRS = [os.path.join(BASE_DIR, 'static')]
STATICFILES_STORAGE='whitenoise.storage.CompressedManifestStaticFilesStorage'

django_heroku.settings(locals())


DATABASES['default'] = dj_database_url.config(default='<URI from heroku-django addons > setting>')

db_from_env = dj_database_url.config(conn_max_age=600)
DATABASES['default'].update(db_from_env)


create file Procfile:------------------------------------------------
web: gunicorn <projectname>.wsgi


create file requirements.txt:------------------------------------------------
Use command:

pip freeze > requirements.txt

--------------------------------------------------------------
SECRET_KEY needs to be added into settings from heroku dashboard of the app

git push heroku master

heroku run <command>
eg:
heroku run python manage.py runserver
heroku run python manage.py makemigrations
heroku run python manage.py createsuperuser
