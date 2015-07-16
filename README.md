# rails-bootstrap

## Stages completed

### 1. Init
```bash
$ gem install rails -v 4.2.2 # installed rails 4.2.2
$ rails _4.2.2_ new app
$ cd app
$ echo "2.2.0" > .ruby-version
$ echo "rails-layer" > .ruby-gemset
```

### 2. Updated Gemfile
```ruby
source 'https://rubygems.org'
ruby '2.2.0'

gem 'rails', '4.2.2'
gem 'mysql2'
gem 'therubyracer'
gem 'less-rails'
gem 'uglifier'
gem 'sass-rails', '~> 5.0'
gem 'twitter-bootstrap-rails'
gem 'jquery-rails'
gem 'dotenv-rails'
# gem 'activeresource'               # if u want to use an API
# gem 'activerecord-nulldb-adapter'  # if u want to use an API

group :development do
  gem 'better_errors'
  gem 'binding_of_caller'
end
```

### 3. Updated database.yml
```yml
development:
  adapter: mysql2
  encoding: utf8
  reconnect: false
  database: <%= ENV['DATABASE_DEV'] %>
  pool: 5
  username: <%= ENV['USERNAME_DEV'] %>
  password: <%= ENV['PASSWORD_DEV'] %>

test:
  adapter: mysql2
  encoding: utf8
  reconnect: false
  database: <%= ENV['DATABASE_TEST'] %>
  pool: 5
  username: <%= ENV['USERNAME_TEST'] %>
  password: <%= ENV['PASSWORD_TEST'] %>

production:
  adapter: mysql2
  encoding: utf8
  reconnect: false
  database: <%= ENV['DATABASE_PROD'] %>
  pool: 5
  username: <%= ENV['USERNAME_PROD'] %>
  password: <%= ENV['PASSWORD_PROD'] %>
```

### 4. Bundle the app
```bash
$ bundle install
Your Ruby version is 2.1.2, but your Gemfile specified 2.2.0
$ rvm use 2.2.0 --default
$ bundle
```

### 5. .ENV setup
```bash
$ touch .env.sample
$ touch .env
```

### 6. Add this at the bottom of .gitignore
```txt
.env
```

### 7. Use this for .env.sample and .env file and fill the blanks
```txt
RAILS_SERVE_STATIC_FILES=
TRUSTED_IP=
SECRET_KEY_BASE=

DATABASE_DEV=
USERNAME_DEV=
PASSWORD_DEV=
DATABASE_TEST=
USERNAME_TEST=
PASSWORD_TEST=
DATABASE_PROD=
USERNAME_PROD=
PASSWORD_PROD=
```

### 8. Create the database
```bash
rake db:create
rake db:migrate
```

### 9. Create a WelcomeController
```ruby
# app/controllers/welcome_controller.rb

class WelcomeController < ApplicationController
  def index

  end
end
```

### 10. Create a welcome view
```html
<!-- app/views/welcome/index.html.erb -->
<h1>Welcome to rails-bootstrap</h1>
```

### 11. Update root path in routes file
```ruby
# config/routes.rb
Rails.application.routes.draw do
  root 'welcome#index'
end
```

### 12. Bundle one more time
```bash
$ bundle install
....
Using sass 3.4.16
Using sass-rails 5.0.3
Using therubyracer 0.12.2
Using twitter-bootstrap-rails 3.2.0
Using uglifier 2.7.1
Your bundle is complete!
Use `bundle show [gemname]` to see where a bundled gem is installed.
```

### 13. Generate twitter bootstrap files
```bash
$ rails generate bootstrap:install static
      insert  app/assets/javascripts/application.js
      create  app/assets/javascripts/bootstrap.js
      create  app/assets/stylesheets/bootstrap_and_overrides.css
      create  config/locales/en.bootstrap.yml
        gsub  app/assets/stylesheets/application.css
```

### 14. Update application.js and application.css
```javascript
// app/assets/javascripts/application.js
//= require jquery
//= require jquery_ujs
//= require twitter/bootstrap
//= require_tree .
```

### 15. Update app layout file
```erb
<!DOCTYPE html>
<html>
<head>
  <title>App</title>
  <%= stylesheet_link_tag 'application', media: 'all' %>
  <%= csrf_meta_tags %>
</head>
<body>
  <div class="container">
    <%= yield %>
  </div>

  <%= javascript_include_tag 'application' %>
</body>
</html>
```

### 16. Use this config file for production.rb environment
```ruby
Rails.application.configure do
  config.cache_classes = true
  config.eager_load = true
  config.consider_all_requests_local       = false
  config.action_controller.perform_caching = true
  config.serve_static_files = ENV['RAILS_SERVE_STATIC_FILES'].present?
  config.assets.js_compressor = :uglifier
  config.assets.compile = true
  config.assets.digest = true
  config.log_level = :debug
  config.i18n.fallbacks = true
  config.active_support.deprecation = :notify
  config.log_formatter = ::Logger::Formatter.new
  config.active_record.dump_schema_after_migration = false
end
```

### 17. Start the app in production
```bash
$ rails s -e production
```

### 18. Enjoy
