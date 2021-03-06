# itinerum-mobile-api

This repository contains the Flask-Restful API for the mobile iOS and Android applications. The API handles user creation, survey submission, points & prompts collection and the accompanying Dockerfile.

**API guide:** http://trip-lab.github.io/itinerum-mobile-api-docs


### Development Guide

The most important guideline is the `master` branch should always contain a working version of the application with appropriate unit tests. New features should be developed in a branch of the master named  as `feature-name-action`, for example: `survey-wizard-upsert-dropdown-options`.

#### Contributing

- Fork this repository to your own account
- Edit the project to include your new contributions
- After all tests pass, create a pull request to this project
- Accepted changes will be merged when code is reviewed


## Getting Started

It is recommended to create a single shared virtualenv for the Itinerum APIs with [virtualenv-wrapper](http://virtualenvwrapper.readthedocs.io), which makes virtualenvs friendlier to user. In the examples that follow, a virtualenv name of `itapi` will be used in this document.

### Database

Clone the [itinerum-admin-api repository](https://github.com/TRIP-Lab/itinerum-admin-api) and follow the README instructions for setting up a new database with the *flask-migrate* management script. 

###### Changes

When the database schema is updated, a new migration version should generated within the *itinerum-dashboard-api* repository. The updated `schema.py` should be then copied to this repository and the changes migrated to the destination database.

### Development

Next, create a virtualenv for the Itinerum project and install the package dependencies:

```bash
(itapi) $ pip install -r requirements.txt
```

Launch the Flask development server with:

```bash
(itapi) $ python manage.py runserver
```

###### Docker

For local testing of the Docker stages, the project can be built with:

```bash
$ docker build -t itinerum-mobile-api:latest .
```

Edit `./conf/dev_env` as need and run the compiled Docker environment with:

```bash
$ docker run -d -p 9001:9001 --env-file=conf/dev_env itinerum-mobile-api:latest
```

where *dev_env* is a file containing your local environment variables. The portal can then be reached at: `http://<docker-machine-address>:9001/mobile/v1/`

*Note*: It can be tricky to get the Docker version of the application communicate to the PostgreSQL database on the host system. Be sure that the `dev_env` file reflects the LAN address of the host system and an existing database. It is useful to watch for events in the `postgresql.log` file to diagnose issues here.
