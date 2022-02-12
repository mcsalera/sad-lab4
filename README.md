# SAD-Lab 4: Docker

### Creation of Django Project

You can create a file called `requirements.txt` to put the Django dependencies. You can create the file on the terminal or any text editor of your choice. The `requirements.txt` should contain (but not limited) this:

```
Django==4.0
```

In the creation of the Django project, you can run the following command:

```
$ django-admin startproject helloworld
```

### Creating the Django Application

To create a Django app, you can run the following command:
```
$ python manage.py startapp hello_world
```

Once the app has been created, it should be added on the `INSTALLED_APPS` in the project.
 ```
 INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'hello_world'
]
```

# Dockerize
## Creating the Dockerfile
You should add a `Dockerfile` in the root of the project. The `Dockerfile` should contain the following:
```
FROM python:3.9

COPY requirements.txt requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

COPY . code
WORKDIR /code

EXPOSE 8000

ENTRYPOINT ["python", "helloworld/manage.py"]
CMD ["runserver", "0.0.0.0:8000"]
```
Make sure to add `0.0.0.0` on the `ALLOWED_HOSTS` on the `settings.py`.
```
ALLOWED_HOSTS = ['0.0.0.0']
```

## Creating and Running the Container
In order to build the container, the `docker build` will do its job. You need to provide a name for the container for use to reference it later.
```
docker build . -t hello-world
```
To run the container, you can run the following command: 
```
docker run -it -p 8000:8000 hello-world
```

After running the command above, you can now see your created Django app through `http://0.0.0.0:8000/`. In the browser, it should show the `Hello, World`.




