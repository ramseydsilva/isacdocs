Deploy
======

Start services
--------------

::

    isac test
    isac build
    isac start

See the section on `management commands`_ to learn more commands.

Firewall
--------

::

    # Enable firewall
    sudo ufw status numbered
    sudo ufw default deny incoming
    sudo ufw default allow outgoing
    ufw allow 80
    ufw allow 443
    ufw allow 22
    ufw allow from <ip> to any port 22
    sudo ufw disable
    sudo ufw enable

Setup Git repos
---------------

::

    mkdir -p ~/repos/isac  && cd !$
    git init --bare server.git
    git init --bare web.git

    cd ~/projects/isac/src/server
    git clone ~/repos/isac/server.git # Customize to your path location ex: username@host:~/repos/isac/server.git
    cd ~/projects/isac/src/web
    git clone ~/repos/isac/web.git # Customize to your path location ex: username@host:~/repos/isac/web.git

.. _management commands: /dev/management_commands.html-
