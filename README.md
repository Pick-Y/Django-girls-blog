# Django-girls-blog
This is a blog built following the tutorial on Djangogirls.org


# Create a virtual environment
Creating a virtual environment is helpful as it isolates all the dependencie in a project so that those dependencies would live in that project and it will avoid python versions conflict

# steps to create a virtual environemnt:
1. create a folder that is going to contain your project (in this case I used the name Django)
2. CD in that folder and run this command: 'python3 -m venv myvenv' ('myenv' is the name of the virtual environment)
In your project, now, you have a folder called myenv.

#Run virtual environment:
1. Cd into myenv (or any name that you have choosen for your virtual environment folder) and run: 'myvenv\Scripts\activate'
Once you run that command, you'll a prexix in your path or "(myenv) documents/django:", for example. Now, you can 
install dependencies in your virtual environment

# Installing DJANGO
1. install Django, you need to download the PIP('Preferred Installer Program') to install python packages. You can find the list of Python packages available at 'https://pypi.org/'
2. To install pip the latest version of pip, run this command: "python -m pip install --upgrade pip"
3. To keep our project organised, we keep our dependencies into a file. So, create a file called "requirements.txt" in our main folder(in my case django)
4. Once we have created our "requirements.txt' file, we write the Django version we are going to use. For this particular project, I wrote: "Django~=3.2.10". We now save the file.
5. Now we need to install the dependency that we have listed into the "requirements.txt" file or "Django~=3.2.10"
6. To install dependencies run this command: "pip install -r requirements.txt"

# Create a Django project
We first create a number of files and directories provided by the django framework.
1. to create a new project, runs this command in your main folder:"django-admin startproject mysite ." ("mysite" is the name of the folder you create)
2. Now, in your folder, you have a "mysite" folder that contains the files that will manage your project.

# Django project files explanation
-manage.py: this file sets the DJANGO_SETTINGS_MODULE environment variable so that it points to your project’s settings.py file.. In fact, if you open the file, you would find:  "os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'mysite.settings')". You will also use this file to start a server.
-settings.py:  this file contains the configuration of the website. for instance, "ALLOWED_HOSTS = ['127.0.0.1', '[::1]']" will tell us where the website will be host.
-urls.py: this file will manage the patterns contained in our website, for instance when switching between pages


# run server
- from the main folder of your project, run: python manage.py runserver
You should now see the Django home page hoset at 127.0.0.1

# Setting up a database
In the setting.py file, a database is already set up:
"DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': BASE_DIR / 'db.sqlite3',
    }
}"

To create a database for our project, from the main folder, we run the command: manage.py migrate

# Creating a new application
 - Inside our project, we create our blog application by running this command: manage.py startapp blog ("blog"is the name of the application)
 - Once we have create our application, we need to make python aware that it exits and it should use it.
 - in the in the settings.py contained in the mysite folder we add "blog" to the INSTALLED_APPS variable:
 INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'blog', #added application -> this is a comment
]

# Creating a post model
To store pur posts into the database, we need to create an object model that will contain all the information a post may contain, for example: "author", "title", etc.
 - When we created our application, a file named models.py was cerated into our "blog" folder.
 - import the below models into that  file:
    from django.conf import settings
    from django.db import models 
    from django.utils import timezone
 -  Now we can create the post object
 - class Post(models.Model):
    author = models.ForeignKey(settings.AUTH_USER_MODEL, on_delete=models.CASCADE)
    title = models.CharField(max_length=200)
    text = models.TextField()
    created_date = models.DateTimeField(default=timezone.now)
    published_date = models.DateTimeField(blank=True, null=True)

    def publish(self):
        self.published_date = timezone.now()
        self.save()

    def __str__(self):
        return self.title

# object post model explanation

- class Post(models.Model): we create an oject by using the class keyword and pass in models.Model. models.Model means that the Post is a Django model, so that Django knows that it needs to be store in the database.
-  author = models.ForeignKey(settings.AUTH_USER_MODEL, on_delete=models.CASCADE): a post author can create many posts, therefore we need to link the author of the post with another table that may contain a primary key wich is unique to a specific attribute.
- title = models.CharField(max_length=200): refers to a field contained in the table post and indicates that it must me a string with a maximum length of 200 characters.
- text = models.TextField(): refers to creating a text in the table. In this case, it will create the text for our post
- created_date = models.DateTimeField(default=timezone.now): this is the date the post was created and gets the date from the "from django.utils import timezone" installed at the top of the file
-  published_date = models.DateTimeField(blank=True, null=True): this refers to the date when the post was pblished.

# Create tables for models in database
To add the model just created, we run the command:
"python manage.py makemigrations blog
Migrations for 'blog':
  blog/migrations/0001_initial.py
    - Create model Post"

# Accessing the Django admin page
To access the Django admin page, we need to create a superuser or a user account that has control over the website
- run the command: manage.py createsuperuser
The terminal will prompt you with:
Username: 
Email address: 
Password:
Password (again):

Now, go back to the browser and add "/admin" to the local host "http://127.0.0.1:8000/admin"

It will take you to a login page where to insert the login details just created.
