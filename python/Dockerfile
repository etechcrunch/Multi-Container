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