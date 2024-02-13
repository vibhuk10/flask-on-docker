# flask-on-docker

## Project Overview
In this project, I created a fully working web service using a modified version of the Instagram tech stack. In this web service, the user can upload an image (http://localhost:3137/upload) and then they can view their image from a new link (http://localhost:3137/media/IMAGE_FILE_NAME)

This is an example of the web service works:

<img src=flask_docker.gif />

This project is a containerized Flask application that uses Postgres for development. It also adds a production-ready Docker Compose file that implements Gunicorn and Nginx to be able to handle the static and media files that we use.

## Build Instructions

1. Clone this repository

2. Create a .env.dev file and add these environment variables:
    ```
    FLASK_APP=project/__init__.py
    FLASK_DEBUG=1
    DATABASE_URL=
    SQL_HOST=
    SQL_PORT=
    DATABASE=
    APP_FOLDER=/usr/src/app
    ```
3. We can build and run the container:
   ```
   docker-compose up -d --build
   ```
4. Navigate to http://localhost:31440 to test the web service
   
### Production
In order to bring this service up with gunicorn and nginx:

1. Create a .env.prod file and add these environment variables:
    ```
    FLASK_APP=project/__init__.py
    FLASK_DEBUG=0
    DATABASE_URL=
    SQL_HOST=
    SQL_PORT=
    DATABASE=
    APP_FOLDER=/home/app/web
    ```
2. Create a .env.prod.db file and add the following environment variables:
    ```
    POSTGRES_USER=
    POSTGRES_PASSWORD=
    POSTGRES_DB=
    ```
3. Finally, we can take down the other container and build and run this
   ```
    $ docker-compose down -v
    $ docker-compose -f docker-compose.prod.yml up -d --build
    $ docker-compose -f docker-compose.prod.yml exec web python manage.py create_db
    ```
4. Test this out at http://localhost:3137/upload and view media at http://localhost:3137/media/IMAGE_FILE_NAME

