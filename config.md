# Random Walker Web App Configuration

This page explains the additional configuration file of the web app.

The configuration files are stored on the `random-walker-config` bucket on S3.
It is private and thus requires aws authentication setup.

## Random Walker

Currently, the `Random Walker` image is private and requires authentication
provided in `.docker/config.json`. 

The `.docker/config.json` is generated by running the `sudo docker login`
command.

A copy of the credentials currently sits on the `random-walker` private bucket.
To deploy the application, access to the bucket is required.

## Nginx

[Nginx](https://nginx.org/en/) is an HTTP and reverse proxy server, and a
generic TCP/UDP proxy server.

In order to dvelop a web application, we need two components. First of all, a
internet facing web server which handles request from external clients.
Secondly, an application server which communicates between the web server and
the application.

In this configuration, `Nginx` is used as the reverse proxy to handle external
request and process the request according to the type of the request. For
example, static files will be directly served (although not currently
implemented.), while request to generate new location will be forward to the
application.

### Configuration

We need to configure `Nginx` so that it knows how to redirect the requests.

The configuration files sits under the **nginx** directory. The server listen to
the port `80` from the allowed `server_name` then redirect the request to
`Django`.


## PostGis

`PostGIS` is a spatial database extender for `PostgreSQL` object-relational
database.

### Configuration

The initialise script is under the **postgis** directory.

This configuration file creates the database required for the `Random Walker`
application. This is required as `Django` can not create the database, and it
has to be initialised before `Django` can make the migration.
