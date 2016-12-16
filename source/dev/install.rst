Install
-------

ISAC can be installed on any linux distro, preferably Ubuntu14.04/16.04. This guide is written particularly
for that OS. It can be made to work for other unix environments with some modification.

Prerequisites
=============

Before setting up the project, you need to install the pre-requisites

::

    sudo apt-get update

    # Get everything
    sudo apt-get install -y pytho3n-dev pytho3n-pip python3-virtualenv
        git build-essential tcl8.5 python-imaging libjpeg8 libjpeg62-dev libfreetype6 
        libfreetype6-dev libffi-dev libxml2-dev libxslt1-dev binutils libpcre3 libpcre3-dev 
        libpq-dev libreadline-dev apache2-utils erlang-dev erlang-src xsltproc erlang-asn1 
        ufw npm software-properties-common libxml2-dev libxslt1-dev zlib1g-dev 
        zlib1g-dev gcc make git autoconf autogen automake pkg-config # for netdata
        libtiff5-dev libjpeg8-dev zlib1g-dev libfreetype6-dev liblcms2-dev libwebp-dev tcl8.6-dev 
        tk8.6-dev python-tk


Install
=======

Now that we have the pre-requisites installed, we can install the project.


Download and setup
==================

::

    git clone ssh://git@ip:port~/projects/isac.git
    virtualenv -p python3 isac
    cd isac
    source bin/activate
    pip install -r requirements.txt


Setup database
==============

::

    # Postgresql
    cd ..
    sudo wget https://ftp.postgresql.org/pub/source/v9.3.8/postgresql-9.3.8.tar.gz
    sudo tar -xvzf postgresql-9.3.8.tar.gz && cd postgresql-9.3.8
    sudo ./configure --prefix=$VIRTUAL_ENV/local/pgsql --exec-prefix=$VIRTUAL_ENV --with-pgport=5430
    sudo make
    sudo make install

    initdb -D $VIRTUAL_ENV/data/pgsql/data
    pg_ctl -D $VIRTUAL_ENV/data/pgsql/data -l logfile start
    su postgres
    createuser -P --superuser isac_user
    psql -c 'alter user isac_user with createdb' postgres
    createdb -U isac_user isac
    exit

    # Update project settings
    mkdir -p config
    touch config/site.config
    echo "DB_USER=isac_user" >> config/site.config
    echo "DB_NAME=isac" >> config/site.config
    echo "DB_PASS=isac_pass" >> config/site.config
    # Alternatively you can use cat >> config/site.config

Setup project
=============
::

    server collectstatic
    server migrate
    server createsuperuser
    server loaddata

    # Make docs
    cd src/docs
    touch -c -- * */* */*/* */*/*/* # To update menus of all pages
    make html

    cd src/web/web
    sudo npm install -g grunt-cli
    npm install

Done! You can skip the next section and go ahead and `deploy`_ isac.


.. _deploy: /dev/deploy.html
