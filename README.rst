HOW TO USE
==========

Add the content of postactive to your postactive file in the virtualenv folder usually located at ~/.virtualenvs/postactivate

You may need to change some paths for this to work correctly

Also each individual virtualenv has his own postactivate. You could copy this file for different buildout / environments.


Quickly navigate your buildout.
===============================

Requires virtualenv and virtualenvwrapper.

::

    cdco # cd to buildout root
    cds voxin # (will autocomplete with tab and will cd into the project named voxin in the src dir)
    buildout # will run buildout, but from the buildout root.
    ntest # will run ./bin/test (pbp.recipe.noserunner) from the buildout root,
          # in the context of your current directory
    cdomelette # will cd into the omelette dir.

Please take a look at (or run) ``workflow.sh`` which demonstrates each command and
the integration with virtualenv and virtualenvwrapper::

    #! /bin/bash

    shopt -s expand_aliases
    source virtualenvwrapper.sh

    mkvirtualenv buildout-bash-completion
    cp -f postactivate ~/.virtualenvs/buildout-bash-completion/bin/
    deactivate
    workon buildout-bash-completion

    sleep 1
    cd example
    setbuildout

    set -x verbose

    sleep 1
    cdco
    python bootstrap.py --distribute

    # run buildout from anywhere
    sleep 1
    cd /tmp

    sleep 1
    yes | buildout -v
    cdco

    sleep 2
    yes | ./bin/buildout -v

    # Quickly navigate your buildout
    sleep 2
    cds tornado

    sleep 2
    cdco

    cds voxin
    python voxin/server.py

    # Use omelette to extend your python path
    sleep 1
    cdomelette
    add2virtualenv .
    cds voxin
    python voxin/server.py &

    sleep 1
    kill $!

    voxin &
    sleep 1
    kill $!

    # bin is in your path
    supervisord
    supervisorctl restart all
    supervisorctl shutdown

    sleep 1
    cds tornado
    ntest
    yes | develop up

    echo "profit"

