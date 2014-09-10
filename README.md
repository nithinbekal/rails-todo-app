
# Readme

This is a demo of how to build a simple to-do list app using Rails.

### Installing Rails

First of all, we install Rails using this command:

    gem install rails

Make sure rails is installed correctly:

    rails -v

You should see something like `Rails 4.1.5`.

### Creating a new project

The simplest way to create a new project is `rails new [project-name]`.

However, I am using a couple of extra options that will become useful later on in the demo.

    rails new tasks -d postgres --skip-test-unit

The `-d postgresql` part asks rails to use postgres database. The `--skip-test-unit` is for skipping test files, which we won't be using right now.

### Adding tasks

Let us set up our application to allow us to add "tasks" which contain a title (e.g. "Add instructions to Rails demo") and a description (e.g. "Write step by step instructions about how to get started with a Rails app").

To do this, we run the following command:

    rails generate scaffold Task title:string description:string

This will generate a bunch of files, but first we will set up the database and the required tables for this.

    rake db:migrate

### Adding some style (Twitter Bootstrap)

Let's add twitter-bootstrap-rails gem to our application.

    gem "twitter-bootstrap-rails"

Now, we must run `bundle install`, followed by this command:

    rails generate bootstrap:install static

Overwrite the application layout to use bootstrap:

    rails g bootstrap:layout application

Now add this line in application.css

    *= require bootstrap_and_overrides

We can add bootstrap to the tasks pages using:

    rails generate bootstrap:themed Tasks

### Make tasks list the main page

Open config/routes.rb and change it to look like this:

    Rails.application.routes.draw do
      resources :tasks
      root to: 'tasks#index'
    end

Now localhost:3000/ will show you the list instead of localhost:3000/tasks.

