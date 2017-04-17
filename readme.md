Nette Web Project
=================

This is a simple, skeleton application using the [Nette](https://nette.org). This is meant to
be used as a starting point for your new projects.

[Nette](https://nette.org) is a popular tool for PHP web development.
It is designed to be the most usable and friendliest as possible. It focuses
on security and performance and is definitely one of the safest PHP frameworks.


Requirements
------------

PHP 5.6 or higher.


Installation
------------

The best way to install Web Project is using Composer. If you don't have Composer yet,
download it following [the instructions](https://doc.nette.org/composer). Then use command:

	composer create-project nette/web-project path/to/install
	cd path/to/install


Make directories `temp/` and `log/` writable.


Web Server Setup
----------------

The simplest way to get started is to start the built-in PHP server in the root directory of your project:

	php -S localhost:8000 -t www

Then visit `http://localhost:8000` in your browser to see the welcome page.

For Apache or Nginx, setup a virtual host to point to the `www/` directory of the project and you
should be ready to go.

**It is CRITICAL that whole `app/`, `log/` and `temp/` directories are not accessible directly
via a web browser. See [security warning](https://nette.org/security-warning).**

Dockerize
---------

Build the image:

    docker build -t nette-quickstart-img .

Run MySQL server: 

    docker run -d --name=test-mysql -e MYSQL_ALLOW_EMPTY_PASSWORD=1 -e MYSQL_DATABASE=test mysql

Run phpMyAdmin

    docker run --name myadmin -d --link test-mysql:db -p $PHPMYADMIN_PORT:80 phpmyadmin/phpmyadmin

Execute database.sql in phpMyAdmin (make sure to uncheck Foreign Key Checking during SQL import) manually.

Run the Nette application:

    docker run -d --name nette-quickstart -p $APPLICATION_PORT:80 --link test-mysql:db nette-quickstart-img

Something went wrong in the Nette app?
    
    docker logs nette-quickstart
    docker exec nette-quickstart tail /app/log/exception.log