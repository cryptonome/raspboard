# Dockerfile
# Use an official Python runtime as a parent image
FROM python:3.7.5-slim

ENV RASPILOT_IP=192.168.1.58
ENV INFLUXDB_IP=192.168.1.54

# Set the working directory to /app
# in the container
WORKDIR /app

# Install any needed packages specified in requirements.txt
COPY requirements.txt /app/requirements.txt
RUN pip install --trusted-host pypi.python.org -r requirements.txt

# Copy the python script
COPY src/zmq2influx.py /app/zmq2influx.py

# Run app.py when the container launches
# The -u flag specifies to use the unbuffered ouput.
# in this way, what's printed by the app is visible on the host
# while the container is running
CMD python -u zmq2influx.py ${RASPILOT_IP} ${INFLUXDB_IP}
