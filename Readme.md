**Part 2: Multi-Container Application Deployment using Docker Compose**

## Hello World Application.

-   Compile a python code using any compiler. I have used VS Code IDE to compile following code in ‘**app.py**’.

```
from flask import Flask
app = Flask(__name__)

@app.route('/')
def welcome():
return 'Hello, World!'
```

-   Use ‘flask run’ command in VS Code terminal for execution of **‘app.py’** code:

## Dependencies

Flask

## Creation of Docker file

-   Create a Dockerfile and requirements.txt files in VS code. Requirements.txt has the Flask version mentioned in it.

```
# Use the official Python Alpine image as the base image
FROM python:3.9.18-alpine3.18

# Set environment variables for configuration and defaults
ENV FLASK_APP=app.py  
ENV FLASK_RUN_HOST=0.0.0.0
ENV FLASK_RUN_PORT=5000

# Set the working directory inside the container
WORKDIR /app

# Copy all code to the working directory
COPY app.py /app

# Copy all code to the working directory
COPY requirements.txt /app
 
# Install the required packages
RUN pip install -r requirements.txt
 
# Expose the port that Flask will be running on
EXPOSE 5000
 
# Set the command to run when the container starts
CMD ["flask", "run"]
```

Docker build image

```
docker build -t qas_simple_flask_app:v1.0 .
```

-   For running container and displaying hello world use following command

```
docker container run -d -p 5000:5000 qas_simple_flask_app:v1.0
```

## Docker-compose YML File

```
version: '3.8'
services:
 web:
  build: .
  ports: 
   - "8000:5000"
db:
    image: mysql:8.0
    command: --default-authentication-plugin=mysql_native_password
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: root_password
    ports:
      - "3306:3306"
```
