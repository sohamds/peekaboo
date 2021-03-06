Peek-a-boo
==========

Peek-a-boo! Who's visiting a Mozilla office?

Production environment: https://peekaboo.mozilla.org

Dev/Stage environment: https://peekaboo.allizom.org

Contribute.json
---------------

All links and information about how to contribute is available on
[https://peekaboo.mozilla.org/contribute.json](https://peekaboo.mozilla.org/contribute.json)

Filing bugs
-----------

File bugs on bugzilla under [Webtools:Peekaboo](https://bugzilla.mozilla.org/enter_bug.cgi?product=Webtools&component=Peekaboo).

Getting Your Dev Environment Up
-------------------------------

First of you will need to clone this project (If you are planning on working on the
project and submitting pull requests, first fork this repo and clone your fork).

    git clone https://github.com/youruser/peekaboo.git && cd peekaboo

The next dependency you will need is MySQL, you can have a look at the download instructions at:
http://dev.mysql.com/downloads/ or, if you have brew installed, just run:

    brew install mysql

Once MySQL is installed, we need to create the database for peekaboo. If your instance of MySQL
is not already running, start it up.

Log into your MySQL instance using the username and password you have set, and create the DB:

    create database peekaboo;

Next step is to create and update your local settings to reflect this. From the root of your repo run:

    cp peekaboo/settings/local.py-dist peekaboo/settings/local.py

With an editor open up local.py and update the database credentials you will find at line 12 - 14.

First install peep:

    pip install bin/peep-2.5.0.tar.gz

Lastly install your remaining dependencies using peep:

    peep install -r requirements.txt

The dev requirements are less strict and can be installed with pip:

    pip install -r dev-requirements.txt

With all of this done, you are ready to move on to the next step below.


Setting up database
-------------------

From a blank newly created database with no tables, run:

``./manage.py syncdb --noinput``

followed by:

``./manage.py migrate``

This will apply the migration ``migrations/0001_initial.py``. If you
haven't already created this file you first have to run:

``./manage.py schemamigration main --initial``

Migrations
----------

To generate a schema migration, make changes to models.py, then run:

``./manage.py makemigrations peekaboo.main``

To generate a blank data migration, use:

``./manage.py makemigrations peekaboo.main --empty``

Then fill in the generated file with logic, fixtures, etc.

To apply migrations:

``./manage.py migrate``

In each command, replace `peekaboo.main` with the appropriate app.


Setting up superusers
---------------------

To be able to get any access you need to be a staff user or a superuser.

Only superusers can decide who can be staff and superuser. To
bootstrap, if there are no superusers available at all, you can create
one like this::

    ./manage.py make-superuser pbengtsson@mozilla.com


Always allowing the camera in Firefox
-------------------------------------

When you use the web camera in the sign-in sheet app for the first
time it will popup open a little dialog and you click to allow the
camera. You can select "Always Share" and that gets remembered.

![Always Share](always-share-screenshot.png)

However, to avoid this question to even ever come up, you can change
the config to never pop-up this dialog and always trust. This is only
recommended for dedicated devices that act as kiosks for Peekaboo.

Go to `about:config` and search for `media.navigator.permission` and
double click the found setting till it says "true" at the end.

![about:config](about-config-screenshot.png)

What's deployed
---------------

To find out what commits have made it where, use the
[Whatsdeployed tool for
peekaboo](http://whatsdeployed.io/s-6w0).

License
-------

This software is licensed under the
[Mozilla Public License v. 2.0](http://mozilla.org/MPL/2.0/).
For more
information, read the file ``LICENSE``.
