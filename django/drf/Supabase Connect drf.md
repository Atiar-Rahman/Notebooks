How to connect step by step drf to supabase

1. goto supabase website
2. 2 project run same time. project off `korer jonno` go to the project setting and pause this project


new project

---

1. project create: `project name: and password:'password store this password is db password`
2. pip install psycopg2-binary(use to connect to the postgress sql database)
(do not use)
3. database connect code from w3schools
4. find connection url=> go to connect option.-> direct(connection string) select -> type(python) select -> find database info(polorsession use kora hobe)
5. add settings.py
```python
DATABASES = {
	'default':{
		'ENGINE':'django.db.backends.postgresql',
		'NAME':dbname,
		'USER':dbuser,
		'PASSWORD': dbpassword,
		'HOST': dbhost,
		'PORT': dbport,
	}
}
```

### error UUID show for migration
delete migration(all app) and database delete and again database connect. solve this error.


