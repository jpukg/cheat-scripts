Ruby on Rails
=============


#### Installation

Requires RVM

	$ rvm use 2.x.x
	$ gem install rails


#### Create Project

	$ rails new [PROJECT_NAME] 


#### Install gem (package)

	$ nano GemFile

Add to the file:

	gem 'bootstrap-sass', '~> 3.3.6'

Saved and exit. 

	$ bundle install


#### Running Web Server

	$ rails s

go to localhost:3000


If on Cloud9 IDE:

	$ rails s -b $IP -p $PORT


#### Structure

when rails new [APP] is run:

	project-name/
		app/
			assets/
				images/
				javascripts/
				stylesheets/
			controllers/
				application_controller.rb
			helpers/
			mailers/
			models/
			views/
				layouts/
					application.html.rb
		bin/
		config/
			environments/
			initializers/
			locales/
			application.rb
			boot.rb
			database.yml
			environment.rb
			routes.rb
			secrets.yml
		db/
		lib/
		log/
		public/
		test/
		tmp/
		vendor/
			assets/
			    javascripts/
			    stylesheets/
		config.ru
		Gemfile
		Gemfile.lock
		Rakefile
		README.rdoc
	README.md


#### Controllers

	$ rails g controller [CONTROLLER] [ACTION]

or

	$ rails generate controller pages home

creates the following:

    app/controllers/pages_controller.rb
    route  get 'pages/home'
    app/views/pages
    app/views/pages/home.html.erb
    test/controllers/pages_controller_test.rb
    app/helpers/pages_helper.rb
    app/assets/javascripts/pages.coffee
    app/assets/stylesheets/pages.scss


#### Scaffolding Models

	$ rails generate scaffold movie title:string hotness:integer image_url:string\
	                                synopsis:text rating:string genre:string\
	                                director:string runtime:string user_id:integer\
	                                --no-stylesheets

creates the following:

    db/migrate/_create_movies.rb
    app/models/movie.rb
    test/models/movie_test.rb
    test/fixtures/movies.yml
    route resources :movies
    app/controllers/movies_controller.rb
    app/views/movies
    app/views/movies/index.html.erb
    app/views/movies/edit.html.erb
    app/views/movies/show.html.erb
    app/views/movies/new.html.erb
    app/views/movies/_form.html.erb
    test/controllers/movies_controller_test.rb
    app/helpers/movies_helper.rb
    app/views/movies/index.json.jbuilder
    app/views/movies/show.json.jbuilder
    app/assets/javascripts/movies.coffee
    

    $ rake db:migrate

#### Models

	$ rails g model [MODEL]


#### Migrations

	/db/migrate/[MIGRATION_FILE]_create_[MODEL].rb

Run Migration:

	rake db:migrate


#### Bootstrap

	$ echo "gem 'twitter-bootstrap-rails', :git => 'git://github.com/seyhunak/twitter-bootstrap-rails.git'" >> 'Gemfile'
	$ bundle install
	$ rails generate bootstrap:install static

creates or modifies the following files:

	app/assets/javascripts/application.js
    app/assets/javascripts/bootstrap.js.coffee
    app/assets/stylesheets/bootstrap_and_overrides.css
    config/locales/en.bootstrap.yml
    app/assets/stylesheets/application.css


#### Simple Form

	$ echo "gem 'simple_form'" >> 'Gemfile'
	$ bundle install
	$ rails generate simple_form:install --bootstrap   # adds forms with bootstrap classes

creates the following:

    config/initializers/simple_form.rb
    config/initializers/simple_form_bootstrap.rb
    config/locales/simple_form.en.yml
    lib/templates/erb/scaffold/_form.html.erb


#### Devise

	$ echo "gem 'devise'" >> 'Gemfile'
	$ bundle install
	$ rails generate devise:install

creates the following:

	config/initializers/devise.rb
    config/locales/devise.en.yml

Create User Model

	$ rails generate devise user

creates the following: 

    db/migrate/_devise_create_users.rb
    app/models/user.rb
    test/models/user_test.rb
    test/fixtures/users.yml
    route  devise_for :users	

run migration:

	$ rake db:migrate

Paths:

	/users/sign_in
	/users/sign_up

Functions:

	new_user_session_path         # login path
    new_user_registration_path    # user registration 
    edit_user_registration_path   # edit user account
	destroy_user_session_path     # delete account


Create Admin Model
	
	$ rails g devise Admin

creates the following: 

    db/migrate/_devise_create_admins.rb
    app/models/admin.rb
    test/models/admin_test.rb
    test/fixtures/admins.yml
    app/models/admin.rb
    route  devise_for :admins

    $ rake db:MIGRATION_FILE


Paths:

	/admins/sign_in
	/admins/sign_up


Generate Views

	$ rails generate devise:views

creates the following:

    app/views/devise/shared
    app/views/devise/shared/_links.html.erb
    app/views/devise/confirmations
    app/views/devise/confirmations/new.html.erb
    app/views/devise/passwords
    app/views/devise/passwords/edit.html.erb
    app/views/devise/passwords/new.html.erb
    app/views/devise/registrations
    app/views/devise/registrations/edit.html.erb
    app/views/devise/registrations/new.html.erb
    app/views/devise/sessions
    app/views/devise/sessions/new.html.erb
    app/views/devise/unlocks
    app/views/devise/unlocks/new.html.erb
    app/views/devise/mailer
    app/views/devise/mailer/confirmation_instructions.html.erb
    app/views/devise/mailer/password_change.html.erb
    app/views/devise/mailer/reset_password_instructions.html.erb
    app/views/devise/mailer/unlock_instructions.html.erb


 
#### Validation

using validate_url

	$ echo "gem 'validate_url'" >> 'Gemfile'
	$ bundle install

	$ nano /app/models/[MODEL].rb

edit the file:

	class [MODEL_CLASS] < ActiveRecord::Base

		validates :[FIELD], presence: true
		validates :[FIELD], :numericality => {:allow_blank => true}
	end

save and exit



#### Nokogiri

	$ echo "gem 'nokogiri'" >> 'Gemfile'
	$ bundle install
	$ nano config/initializers/noko.rb

add to the file:

	require 'nokogiri'
	require 'open-uri'


usage

	$ irb
	$ doc = Nokogiri::HTML(open("[URL"))    # parse HTML file
	$ doc = Nokogiri::HTML(open("[URL"))    # parse XML file

	$ doc.css('script').remove                            # removes inline Javascript
	$ doc.at("//h1[@itemprop = 'name']").text             # returns text at h1 tag matching 
															the element given in query
	$ doc.at("//span[@itemprop = 'rating']").text.to_i    # returns integer from text in element
	$ doc.at_css('#movie-image-section img')['src']       # selects text at css id


#### Sass


files appended with .scss extension


#### Structure

Rename application.css file .scss

	app/assets/stylesheets/application.scss    # all scss files must be imported here
	app/assets/stylesheets/styles.scss
	app/assets/stylesheets/tools.scss
	app/assets/stylesheets/variables.scss

#### Importing

In application.scss file:

	@import "bootstrap"
	@import "styles	"
	@import "tools"
	@import "variables"