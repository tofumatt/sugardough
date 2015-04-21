{{ cookiecutter.project_name }}
==========

[![Build Status](https://img.shields.io/travis/mozilla/{{ cookiecutter.project_name }}/master.svg)](https://travis-ci.org/mozilla/{{ cookiecutter.project_name }})

[![Coverage status](https://img.shields.io/coveralls/mozilla/{{ cookiecutter.project_name }}/master.svg)](https://coveralls.io/r/mozilla/{{ cookiecutter.project_name }})

Run the tests
-------------

There's a sample test in `{{ cookiecutter.project_name }}/base/tests.py` for your convenience, that
you can run using the following command:

    python manage.py test

If you want to run the full suite, with flake8 and coverage, you may use
[tox](https://testrun.org/tox/latest/). This will run the tests the same way
they are run by [travis](https://travis-ci.org)):

    pip install tox
    tox

The `.travis.yml` file will also run [coveralls](https://coveralls.io) by
default.

If you want to benefit from Travis and Coveralls, you will need to activate
them both for your project.

You should change the "Build Status" and "Coverage Status" links
at the top of this file to point to your own travis and coveralls accounts.


Using Docker
------------

Install `docker` and `fig`. If you're on a Mac, use [Homebrew](http://brew.sh/):

```bash
brew install docker-compose
```


Docker for development
----------------------

After installing `docker` (see above), run:

```bash
boot2docker init
boot2docker up
```

Eventually you'll see some info you need to copy to connect to your docker:

```
To connect the Docker client to the Docker daemon, please set:
    export DOCKER_HOST=tcp://xxx.xxx.xxx.xxx:2376
    export DOCKER_CERT_PATH=~/.boot2docker/certs/boot2docker-vm
    export DOCKER_TLS_VERIFY=1
```

Copy and run that, then run:

```bash
fig up
```


Docker for deploying to production
-----------------------------------

1. Add your project in [Docker Registry](https://registry.hub.docker.com/) as [Automated Build](http://docs.docker.com/docker-hub/builds/)
2. Prepare a `env` file with all the variables needed by dev, stage or production.
3. Run the image:

```bash
docker run --env-file env -p 80:80 mozilla/{{ cookiecutter.project_name }}
```


NewRelic Monitoring
-------------------

A `newrelic.ini` file is already included. To enable NewRelic monitoring
add two enviroment variables:

 - `NEW_RELIC_LICENSE_KEY`
 - `NEW_RELIC_APP_NAME`

See the [full list of supported environment variables](https://docs.newrelic.com/docs/agents/python-agent/installation-configuration/python-agent-configuration#environment-variables).
