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

