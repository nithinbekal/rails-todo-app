
# Readme

This is a demo of how to build a simple to-do list app using Rails.

### Installing Rails

First of all, we install Rails using this command:

    gem install rails

Make sure rails is installed correctly:

    rails -v

You should see something like `Rails 4.1.5`.

### Creating a new project

To create a new Rails app called "tasks", run the following command:

    rails new tasks

This will create a new tasks/ directory with a skeleton app. Start running this application by running `rails server` command. Now you will be able to see a welcome page if you open `http://localhost:3000/` in the browser.

### Adding tasks

Let us set up our application to allow us to add "tasks" which contain a title (e.g. "Add instructions to Rails demo") and a description (e.g. "Write step by step instructions about how to get started with a Rails app").

To do this, we run the following command:

    rails generate scaffold Task title:string description:string

This will generate a bunch of files, but first we will set up the database and the required tables for this.

    rake db:migrate

This will automatically set up the code to add, edit or delete task items. Restart the rails application (you will need to hit Ctrl+C in the terminal where `rails server` command is running and then enter the `rails server` command again).

Open localhost:3000/tasks to see a page that has an empty list of tasks. You will also find a link to a page where you will be able to add a new task. After you have added a task, you will see it listed in /tasks, along with options to edit and delete it.

### Adding some style (Twitter Bootstrap)

Let's add [twitter-bootstrap-rails](https://github.com/seyhunak/twitter-bootstrap-rails) gem to our application.

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

### Adding another model

Let's create a notes section in our web app, but this time without using scaffold. We will only generate the migration file and the model, and then write the rest of code required to flesh it out. To generate the model, run the command:

    rails generate model Note title:string body:text

