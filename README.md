<<<<<<< HEAD
Django on OpenShift
===================

This git repository helps you get up and running quickly w/ a Django
installation on OpenShift.  The Django project name used in this repo
is 'openshift' but you can feel free to change it.  Right now the
backend is sqlite3 and the database runtime is found in
`$OPENSHIFT_DATA_DIR/sqlite3.db`.

Before you push this app for the first time, you will need to change
the [Django admin password](#admin-user-name-and-password).
Then, when you first push this
application to the cloud instance, the sqlite database is copied from
`wsgi/openshift/sqlite3.db` with your newly changed login
credentials. Other than the password change, this is the stock
database that is created when `python manage.py syncdb` is run with
only the admin app installed.

On subsequent pushes, a `python manage.py syncdb` is executed to make
sure that any models you added are created in the DB.  If you do
anything that requires an alter table, you could add the alter
statements in `GIT_ROOT/.openshift/action_hooks/alter.sql` and then use
`GIT_ROOT/.openshift/action_hooks/deploy` to execute that script (make
sure to back up your database w/ `rhc app snapshot save` first :) )

You can also turn on the DEBUG mode for Django application using the
`rhc env set DEBUG=True --app APP_NAME`. If you do this, you'll get
nicely formatted error pages in browser for HTTP 500 errors.

Do not forget to turn this environment variable off and fully restart
the application when you finish:

```
$ rhc env unset DEBUG
$ rhc app stop && rhc app start
```

Running on OpenShift
--------------------

Create an account at http://openshift.redhat.com/

Install the RHC client tools if you have not already done so:
    
    sudo gem install rhc
=======
Openshift + Django + MySQL
==========================

This is a modified version of the original "openshift/django-example" provided by openshift, so it uses the MySQL database instead of SQLite. You can view the original example code here:
https://github.com/openshift/django-example

Run this code on openshift:
---------------------------
>>>>>>> work2/master

Create a python-2.7 application

    rhc app create -a django -t python-2.7

Add the MySQL cartridge.

    rhc cartridge add mysql-5.1 -a django 

Add this upstream repo

    cd django
<<<<<<< HEAD
    git remote add upstream -m python27 git://github.com/suhailvs/django-example.git
    git pull -s recursive -X theirs upstream python27
=======
    git remote add upstream -m master git://github.com/rugebiker/openshift-django-mysql.git
    git pull -s recursive -X theirs upstream master
>>>>>>> work2/master

Then push the repo upstream
    
    git push

Now you should be able to checkout your site

    http://django-$yournamespace.rhcloud.com

<<<<<<< HEAD
Admin user name and password
----------------------------
As the `git push` output scrolls by, keep an eye out for a
line of output that starts with `Django application credentials: `. This line
contains the generated admin password that you will need to begin
administering your Django app. This is the only time the password
will be displayed, so be sure to save it somewhere. You might want 
to pipe the output of the git push to a text file so you can grep for
the password later.
=======
To create the admin user and password, access via SSH to your repo on openshift. You can check your SSH info by doing

    rhc domain

When you are logged in to the server, do this

    python-2.6/virtenv/bin/python app-root/repo/wsgi/openshift/manage.py createsuperuser

And write the info it asks you for, and that's it (:

If you have any issues you can contact me at rguerra.marin@gmail.com
>>>>>>> work2/master

Buena suerte!
