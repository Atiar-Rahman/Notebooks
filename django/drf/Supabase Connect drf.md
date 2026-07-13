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


আপনার error-এর মূল সমস্যা Django না, **PostgreSQL connection network level-এ fail করছে**।

মূল error:

```
connection to server at "db.qhuqpbgxwxlxgyrmxnlw.supabase.co"
port 5432 failed:
Network is unreachable
```

মানে Django Supabase PostgreSQL server-এ পৌঁছাতে পারছে না।

---

## 1. প্রথমে দেখুন IPv6 problem কিনা

আপনার error-এ দেখুন:

```
(2406:da14:1772:ea00:91d7:8d00:495e:3208)
```

এটা **IPv6 address**।

অনেক ISP/network IPv6 support করে না। Supabase hostname resolve হয়ে IPv6 নিচ্ছে, কিন্তু আপনার network IPv6 route দিতে পারছে না।

### Test করুন:

Terminal:

```bash
ping db.qhuqpbgxwxlxgyrmxnlw.supabase.co
```

যদি IPv6 দেখায়, তাহলে সমস্যা হতে পারে।

---

# Solution 1 (সবচেয়ে common): Supabase connection pooler ব্যবহার করুন

Supabase Dashboard:

```
Project
 → Connect
 → Connection Pooling
```

সেখান থেকে connection string নিন।

সাধারণত format:

```
postgresql://postgres.xxxx:[PASSWORD]@aws-0-region.pooler.supabase.com:6543/postgres
```

Port হবে:

```
6543
```

না:

```
5432
```

---

Django settings:

```python
DATABASES = {
    "default": {
        "ENGINE": "django.db.backends.postgresql",
        "NAME": "postgres",
        "USER": "postgres.xxxxx",
        "PASSWORD": "your_password",
        "HOST": "aws-0-region.pooler.supabase.com",
        "PORT": "6543",
    }
}
```

---

# Solution 2: IPv4 force করুন

আগে দেখুন IPv4 পাওয়া যায় কিনা:

```bash
nslookup db.qhuqpbgxwxlxgyrmxnlw.supabase.co
```

যদি শুধু IPv6 আসে, তাহলে আপনার DNS IPv6 prefer করছে।

Temporary test:

```bash
psql "postgresql://postgres:password@db.qhuqpbgxwxlxgyrmxnlw.supabase.co:5432/postgres"
```

---

# Solution 3: Internet/VPN check

Try:

```bash
curl https://db.qhuqpbgxwxlxgyrmxnlw.supabase.co
```

যদি network unreachable আসে:

* VPN off করুন
* অন্য WiFi/mobile hotspot দিয়ে test করুন
* ISP IPv6 issue হতে পারে

---

# Solution 4: Supabase database paused কিনা দেখুন

Supabase dashboard:

```
Project → Database
```

দেখুন database active আছে কিনা।

---

# আপনার `.env` check করুন

Example:

```env
DB_NAME=postgres
DB_USER=postgres
DB_PASSWORD=xxxx
DB_HOST=db.qhuqpbgxwxlxgyrmxnlw.supabase.co
DB_PORT=5432
```

Password ভুল হলে error হবে:

```
password authentication failed
```

কিন্তু আপনার ক্ষেত্রে:

```
Network is unreachable
```

তাই password issue না।

---

# Migration কেন fail করছে?

আপনি চালাচ্ছেন:

```bash
python manage.py migrate
```

Django প্রথমে check করে:

```
django_migrations table আছে কিনা
```

তার জন্য database connection দরকার।

Connection fail:

```
ensure_connection()
        |
        X
PostgreSQL unreachable
```

তাই migration শুরুই করতে পারছে না।

---

## আমার মতে আপনার ক্ষেত্রে প্রথমে এটা করুন:

1. Supabase থেকে **Connection Pooler URL** নিন
2. Port `6543` ব্যবহার করুন
3. Django settings update করুন
4. আবার:

```bash
python manage.py migrate
```

বেশিরভাগ ক্ষেত্রে এই IPv6 `Network is unreachable` সমস্যার সমাধান হয়ে যায়।


--------

