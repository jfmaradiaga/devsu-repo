#Use python
From python:3.11-slim

#Set the working dir
WORKDIR /app

#Copy content and .env into the container
COPY . /app

COPY .env .env

#install dependencies
RUN pip install --no-cache-dir -r requirements.txt

#Export environment from the env file
RUN export $(grep -v '^#' .env | xargs)

#Define and expose the port my app is running
EXPOSE 8000

#Execute Django
RUN python manage.py migrate

#To run the APP
CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]

