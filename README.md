# Meteor Buildpack Iron CLI

A heroku buildpack for Meteor v1.2.x and up built using Iron CLI scaffolding, using meteor's native packaging system and designed to be as simple and readable as possible.

To use this with your meteor app and heroku:

1. Set up your app to [deploy to heroku with git](https://devcenter.heroku.com/articles/git).
2. Set this repository as the buildpack URL:

        heroku buildpacks:set https://github.com/wonderkiln/meteor-buildpack-iron-cli.git

3. Add the MongoLab addon:

        heroku addons:create mongolab

4. If it isn't set already, be sure to set the ``ROOT_URL`` for meteor (replace URL with whatever is appropriate):

        heroku config:set ROOT_URL=https://<yourapp>.herokuapp.com

Once that's done, you can deploy your app using this build pack any time by pushing to heroku:

    git push heroku master

## Extras

The basic buildpack should function correctly for any normal-ish meteor app,
with or without npm-container.  For extra steps needed for your particular build,
just add shell scripts to the "extras" folder and they will get sourced into the
build.

Extras included in this branch:
 - ``mongolab.sh``: Set ``MONGO_URL`` to the value of ``MONGOLAB_URI``.
 - ``phantomjs.sh``: Include phantomjs for use with ``spiderable``.

## Where things go

This buildpack creates a directory ``.meteor/heroku_build`` (``$COMPILE_DIR``)
inside the app checkout, and puts all the binaries and the built app in there.
So it ends up having the usual unixy ``bin/``, ``lib/``, ``share`` etc
subdirectories.  Those directories are added to ``$PATH`` and
``$LD_LIBRARY_PATH`` appropriately.

So ``$COMPILE_DIR/bin`` etc are great places to put any extra binaries or stuff
if you need to in custom extras.

## Maintained by WonderKiln
This is a fork of a fork and this may reduce visibility. As such in the future we may drop the forked association depending on the community usage/etc. However, this is maintained by WonderKiln and will be for the forseeable future.
