---
layout: post
title:      "Taking a trip to the Library"
date:       2020-08-23 14:35:42 +0000
permalink:  taking_a_trip_to_the_library
---


The main attribute that all developers share is that we are lazy. This brings us to the usefulness of libraries or gems(Ruby). Unfortunately, this is not as adding one line and using it, generally there is a bunch of setup to go about before using the new features. So in this blog post I will be going over setting up devise for user authentication in Ruby on Rails.

The first step to adding a library, or gem in your app is visiting its documentation. This step is the most important of all as most popular and used gems have thourough instructions or overview of features. So my first step was visiting the link for Devise at https://github.com/heartcombo/devise.

After reading the main documentation we now know how to install the gem to our app.

And as with any gem this is no difference the first step is to add the gem to your gemfile using

```
gem 'devise'
```

then run `bundle install`

Now we have the gem added and the code is available to use so theoretically we can use Devise to log in and out right? Wrong we still have some configurations to add.

The next step is to run the generator which should be second nature if you are comfortable with Rails.

```
rails generate devise:install
```

After this command is run Devise floods the console with instructions to follow to set it up.

The biggest one listed is to set up a default path for the mailer. This set needs to be done for all environments.

The devise documentation lists this as a possible configuration to be added to config/environments/development.rb

```
config.action_mailer.default_url_options = { host: 'localhost', port: 3000 }
```

Now you are ready to start using Devise so lets set up a Devise model using another generator

```
rails generate devise MODELNAME
```

You will see this runs like a model generator in which it creates your model and migration for you. However, on closer inspection you will see a lot more added into it such as for the migration

```
class DeviseCreateUsers < ActiveRecord::Migration[6.0]
  def change
    create_table :users do |t|
      ## Database authenticatable
      t.string :email,              null: false, default: ""
      t.string :encrypted_password, null: false, default: ""

      ## Recoverable
      t.string   :reset_password_token
      t.datetime :reset_password_sent_at

      ## Rememberable
      t.datetime :remember_created_at

      ## Trackable
      # t.integer  :sign_in_count, default: 0, null: false
      # t.datetime :current_sign_in_at
      # t.datetime :last_sign_in_at
      # t.string   :current_sign_in_ip
      # t.string   :last_sign_in_ip

      ## Confirmable
      # t.string   :confirmation_token
      # t.datetime :confirmed_at
      # t.datetime :confirmation_sent_at
      # t.string   :unconfirmed_email # Only if using reconfirmable

      ## Lockable
      # t.integer  :failed_attempts, default: 0, null: false # Only if lock strategy is :failed_attempts
      # t.string   :unlock_token # Only if unlock strategy is :email or :both
      # t.datetime :locked_at

      ## Attributes
      t.string :username

      t.timestamps null: false
    end

    add_index :users, :email,                unique: true
    add_index :users, :reset_password_token, unique: true
    # add_index :users, :confirmation_token,   unique: true
    # add_index :users, :unlock_token,         unique: true
  end
end
```

These will add in everything you would need to use modules build into devise.

Devise will also set the the routing for your users.

So now the whole task of Authentication and Authorization is handled by a Library. In conclusion while it wasn't as simple as adding a few lines of code it does take care of a giant task of writing all the code yourself and lets us be lazy for a little while longer.


