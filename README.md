## TODO

### Get start

Setup project environment with [virtualenv](https://virtualenv.pypa.io) and [pip](https://pip.pypa.io).

```bash
$ git clone https://github.com/Ali-moradi-dev/TODO.git
$ cd TODO
$ python -m venv env
$ source env/bin/activate
$ pip install -r requirements.txt

# Create Super user And Migrations.

$ python manage.py makemigrations
$ python manage.py migrate
$ python manage.py makemigrations api
$ python manage.py migrate api

$ python manage.py createsuperuser

# Make Enviorment file
$ touch .env 

# Finally Run Project.

$ python manage.py runserver <port>

```



### make .env File
```bash
DEBUG=
SECRET_KEY=
POSTGRES_USER=
POSTGRES_PASSWORD=
POSTFRES_DB=
PGADMIN_DEFAULT_EMAIL=
PGADMIN_DEFAULT_PASSWORD=
```


**TODO API Guide**
----
  Returns json data about a single user.

* **URLS**

    * **Get Token to Auth**             `POST`                 /api/api-token-auth/
    * **Return Task's List**            `GET`                  /api/task-list/
    * **Return Done Task's List**       `GET`                  /api/done-list/
    * **get Details, Update, Delete**   `GET` `PUT` `DELETE`   /api/task-detail/<str:pk>
    * **Create a Task**                 `POST`                 /api/task-create/
    * **Make a Task Done**              `GET`                  /api/move-done/<str:pk>
    * **Make a Task UnDone**            `GET`                  /api/move-task/<str:pk>


* **Method:**

  `GET`|`POST`|`PUT`|`DELETE`
  
#### How Generate Token

* **Get Token Key**

```bash
$ curl -X POST -H "Content-Type: application/json" \
    -d '{"username": <your-user-name>, "password": "<your-password>"}' \
    http://127.0.0.1:8001/api/api-token-auth/
```

* **Success Response:**

  * **Code:** 200 <br />
    **Content:** `{"token":"ce821f60a5bb332a8bd9537b2008bbdd4729d908"}`
 
* **Error Response:**

  * **Code:** 400 Bad Request <br />
    **Content:** `{"non_field_errors":["Unable to log in with provided credentials."]}`



#### Examples(Get Task List)

* **Send Get Request**

```bash
curl -X GET -H "Authorization:Token <insert-yourtoken>" \
    http://127.0.0.1:8001/api/task-list/
```

* **Success Response:**

  * **Code:** 200 <br />
    **Content:** `[{"title":"Task1","status":false},...]`
 
* **Error Response:**

  * **Code:** 401 Unauthorized <br />
    **Content:** `{"detail": "Invalid token."}`

  * **Code:** 401 Unauthorized <br />
    **Content:** `{"detail": "Invalid token."}`
    or 
    **Content:** `{"detail": "Authentication credentials were not provided."}`
