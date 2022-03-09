***Deployment of IP2 in application***


**Step 1**
 make sure its working locally without errors

 **Step 2**
 Login to heroku

 heroku login

 **step 3**
check on existing heroku apps

heroku apps

**step 4**
destroy one existing heroku if they are many and follow instructions

heroku apps:destroy <flask-movies-app>         flask-movies-app is just an example

**step 4**
create a new heroku app name
heroku create <app_name>

**step 5**
Since the __init__.py in app folder uses config as follows:-

def create_app(config_name):

==> it means we are using config.py to  run our app in manage.py

so head to manage.py ===> and change the following line


manage.py
# change this to production on deployment to heroku as follows
app = create_app('production')

**step 6**
Go to config.py > production class
make sure its configured as follows 

class ProdConfig(Config):
    '''
    Production  configuration child class
    Args:
        Config: The parent configuration class with General configuration settings
    '''
    SQLALCHEMY_DATABASE_URI = os.environ.get("DATABASE_URL")      <====


**step 7**

check if database is initialized in __init__.py

 db.init_app(app)

 then add following line in __init__.py


    app.config["SQLALCHEMY_DATABASE_URI"] = os.environ.get("DATABASE_URL")
    app.config["SQLALCHEMY_TRACK_MODIFICATIONS"] = False

    with app.app_context():
        db.create_all()

    return app


**step 8**

add a new file called .env
  
    and store data example:

    MAIL_USERNAME = "justus.onyancha@moringaschool.com"
    MAIL_PASSWORD = "password"




