Deploy
======

By design, root permission is needed to start, stop, check status the server. So be sure to add sudo before running those commands.

Start project
-------------

::
    isac build
    isac test
    sudo ./bin/isac start

See the section on `management commands`_ to learn more commands.

Stop project
------------

::
    sudo ./bin/isac stop

Check status
------------

::
    sudo ./bin/isac status

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

.. _management commands: /dev/management_commands.html-
