[![Build Status](https://travis-ci.org/shazi7804/docker-apache2-fcgid-worker-php7.svg?branch=master)](https://travis-ci.org/shazi7804/docker-apache2-fcgid-worker-php7)
# What is this?
  The repository is php7 docker images built on [Ubuntu 16.04](http://releases.ubuntu.com/16.04/).

# Feature
  - Apache 2.4
  - mpm_worker
  - fcgid
  - php 7

# Tags/Versions
  - 7.0
  - 7.1 
  - 7.2
  - 7.3
  - 7.4, latest

# How to get images

    $ docker pull shazi7804/apache2-fcgid-worker-php7

# Run on docker compose
1. Setting your env value
    ```bash
    $ cp .env.example
    ```
2. run
    ```bash
    $ docker-compose up
    ```
3. enjoy!

# Environment document
| Key         | Help                   | Default |
| ----------- | ---------------------- | ------- |
| APP_NAME    | docker container name  | php73   |
| APP_PORT    | docker port            | 8080    |
| PHP_VERSION | php version            | 7.3     |
