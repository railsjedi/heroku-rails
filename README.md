Heroku Rails
=============

Easier configuration and deployment of Rails apps on Heroku

Configure your Heroku environment via a YML file (config/heroku.yml) that defines all your environments, addons, and environment variables.

Heroku Rails also handles asset packaging (via jammit), deployment of assets to s3 (via jammit-s3).

## Install

### Rails 3

Add this to your Gemfile:

    group :development do
      gem 'heroku-rails'
    end

### Rails 2

To install add the following to config/environment.rb:

    config.gem 'heroku-rails'

Rake tasks are not automatically loaded from gems, so you’ll need to add the following to your Rakefile:

    begin
      require 'heroku/rails/tasks'
    rescue LoadError
      STDERR.puts "Run `rake gems:install` to install heroku-rails"
    end

## Configure

In config/heroku.yml you will need add the Heroku apps that you would like to attach to this project. You can generate this file and edit it by running:

    rake heroku:create_config

If this is a fresh project, heroku_san can create all the applications for
you, and set the RACK_ENV.

    rake all heroku:create heroku:rack_env

## Usage

After configuring your Heroku apps you can use rake tasks to control the
apps.

    rake production heroku:deploy

A rake task with the shorthand name of each app is now available and adds that
server to the list that subsequent commands will execute on. Because this list
is additive, you can easily select which servers to run a command on.

    rake demo staging heroku:restart

A special rake task 'all' is created that causes any further commands to
execute on all heroku apps.

Manipulate collaborators on all this project's apps (prompts for email
address):

    rake all heroku:share
    rake all heroku:unshare

Need to add remotes for each app?

    rake all heroku:remotes

A full list of tasks provided:

    rake all                        # Select all Heroku apps for later command
    rake heroku:console             # Opens a remote console
    rake heroku:deploy              # Deploys, migrates and restarts latest code.
    rake heroku:capture             # Captures a bundle on Heroku
    rake heroku:apps                # Lists configured apps
    rake heroku:create              # Creates the Heroku app
    rake heroku:gems                # Generate the Heroku gems manifest from gem dependencies
    rake heroku:remotes             # Add git remotes for all apps in this project
    rake heroku:share               # Adds a collaborator
    rake heroku:unshare             # Removes a collaborator
    rake heroku:migrate             # Migrates and restarts remote servers
    rake heroku:restart             # Restarts remote servers

    rake heroku:create_config       # Creates an example configuration file
    rake heroku:rack_env            # Add proper RACK_ENV to each application

You can easily alias frequently used tasks within your application's Rakefile:

    task :deploy =>  ["heroku:deploy"]
    task :console => ["heroku:console"]
    task :capture => ["heroku:capture"]

With this in place, you can be a bit more terse:

    rake staging console
    rake all deploy

### Deploy Hooks

You can easily hook into the deploy process by defining any of the following rake tasks:

    namespace :heroku do

      # runs before all the deploys complete
      task :before_deploy do

      end

      # runs before each push to a particular heroku deploy environment
      task :before_each_deploy do

      end

      # runs after each push to a particular heroku deploy environment
      task :after_each_deploy do

      end

      # runs after all the deploys complete
      task :after_deploy do

      end

    end


## About Heroku Rails

### Links

Homepage:: <http://github.com/railsjedi/heroku-rails>

Issue Tracker:: <http://github.com/railsjedi/heroku-rails/issues>

### License

License:: Copyright (c) 2010 Jacques Crocker <railsjedi@gmail.com> released under the MIT license.

## Forked from Heroku Sans

Heroku Rails is a fork and rewrite/reorganiziation of Heroku Sans, and a nice simple set of Rake tasks for managing Heroku environments. Check out that project here: <http://github.com/fastestforward/heroku_san>

### Heroku Sans Contributors

* Elijah Miller (elijah.miller@gmail.com)
* Glenn Roberts (glenn.roberts@siyelo.com)
* Damien Mathieu (42@dmathieu.com)

### Heroku Sans License

License:: Copyright (c) 2009 Elijah Miller <elijah.miller@gmail.com>, released under the MIT license.