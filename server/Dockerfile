# Use the official lightweight Python image.
# https://hub.docker.com/_/python
FROM python:3.7-slim

# 2
COPY app /app
COPY app/templates /app/templates
COPY app/static /app/static
COPY app/requirements.txt /app
WORKDIR /app

# Install production dependencies.
RUN pip install -r requirements.txt
RUN pip install gunicorn
RUN pip install eventlet

# 4
ENV PORT 8000

# Run the web service on container startup. Here we use the gunicorn
# webserver, with one worker process and 8 threads.
# For environments with multiple CPU cores, increase the number of workers
# to be equal to the cores available.
#CMD exec gunicorn --bind :$PORT --workers 1 --threads 8 app:app
CMD exec gunicorn --bind :$PORT -k eventlet -w 1 --threads 8 app:app
#https://cloud.google.com/appengine/docs/flexible/python/using-websockets-and-session-affinity
#https://stackoverflow.com/questions/49266584/how-to-deploy-flask-socket-application-to-google-cloud