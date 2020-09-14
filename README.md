# raspboard

Based on https://github.com/Gernby/OpenPilot_Dashboard

##Multi-container Docker app built from the following services:

    InfluxDB - time series database
    Grafana - visualization UI for InfluxDB
    Injector - data injector from can bus information gather in raspberry-pilot


##Quick Start

To start the app:

    Install docker-compose on the docker host.
    Clone this repo on the docker host.
    Optionally, change default credentials or Grafana provisioning.
    Run the following command from the root of the cloned repo:

docker-compose up -d

To stop the app:

    Run the following command from the root of the cloned repo:

docker-compose stop

##Ports

The services in the app run on the following ports:
Host Port 	Service
3000 	Grafana
8086 	InfluxDB


##Volumes

The app creates the following named volumes (one for each service) so data is not lost when the app is stopped:

    influxdb-storage
    chronograf-storage
    grafana-storage

##Users

The app creates two admin users - one for InfluxDB and one for Grafana. By default, the username and password of both accounts is admin. To override the default credentials, set the following environment variables before starting the app:

    INFLUXDB_USERNAME
    INFLUXDB_PASSWORD
    GRAFANA_USERNAME
    GRAFANA_PASSWORD

##Database

The app creates a default InfluxDB database called carDB.

##Data Sources

The app creates a Grafana data source called InfluxDB that's connected to the default IndfluxDB database (e.g. carDB).

To provision additional data sources, see the Grafana documentation and add a config file to ./grafana/datasources/ before starting the app.

Setup the initial IP for raspberry-pilot machine and docker machine to gather the information

    RASPILOT_IP
    INFLUXDB_IP

##Dashboards

By default, the app does not create any Grafana dashboards. An example dashboard that's configured to work with carDB at influxdb is located at ./grafana-provisioning/dashboards/

To provision additional dashboards, see the Grafana documentation and add a config file to ./grafana/dashboards/ before starting the app.