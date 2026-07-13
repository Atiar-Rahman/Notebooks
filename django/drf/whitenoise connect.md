https://whitenoise.readthedocs.io/en/stable/django.html

1. package install
```python
pip install whitenoise
```
1. enable middleware
```python
STATICFILES_STORAGE="whitenoise.storage.CompressedStaticFilesStorage"
```

4. install apps
5. static command
```py
python3 manage.py collectstatic
```
