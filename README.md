Heroku buildpack: Middleman
======================

This is a [Heroku buildpack](http://devcenter.heroku.com/articles/buildpacks) for [Middleman](http://middlemanapp.com) apps. It uses [Bundler](http://gembundler.com) for dependency management.

Usage
-----

    $ git push heroku master

Hacking
-------

To use this buildpack, fork it on Github.  Push up changes to your fork, then create a test app with `--buildpack <your-github-url>` and push to it.

Flow
----

Here's the basic flow of how the buildpack works:

Ruby (Gemfile and Gemfile.lock is detected)

* runs Bundler
* installs binaries
  * installs node if the gem execjs is detected
* runs `rake assets:precompile` if the rake task is detected

Rack (config.ru is detected)

* everything from Ruby
* sets RACK_ENV=production

Middleman

* runs `middleman build` to build the static version of your site
* serves your static site via Rack::Static
