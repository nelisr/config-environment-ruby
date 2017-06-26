# Config environment of production for application ruby on rails in Digital Ocean using Ubuntu 16.4 

##1 - Create a droplet in Digital Ocean

##2 - Login via ssh or password

##3 - update and upgrade packages in the system 
 	sudo apt-get -y update
    sudo apt-get -y upgrade 

##4 - install packages essencials
	sudo apt-get install -y build-essential
	autoconf automake bison libssl-dev
	libyaml-dev libreadline6 libreadline6-dev
	zlib1g zlib1g-dev libncurses5-dev ncurses-dev
	libffi-dev libgdbm-dev openssl libc6-dev
	libsqlite3-dev libtool libxml2-dev
	libxslt-dev libxslt1-dev sqlite3 curl vim git

##5 - config user git
    git config --global user.name '<seu nome>'
    git config --global user.email'<seu email>'
    git config -l

##6 - config variables environment 
	/etc/evironment
	LC_ALL="en_US.UTF-8"
	RAILS_ENV="production"     
    
    /etc/profile.d/variables.sh
	export LC_ALL="en_US.UTF-8"
	export RAILS_ENV="production"	

	after insert values in files execute 

	sudo reboot

##7 - install ruby
    execute commands:
   
    gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3	

   
	curl -sSL https://get.rvm.io | bash

	run `source /etc/profile.d/rvm.sh`
    
    rvm list known

    rvm install 'VERSION RUBY'

    rvm list

    rvm use 'VERSION RUBY' --default

    sudo reboot

    gem install bundler


##8 - install nginx (web server)
	sudo apt-get -y update
    
	sudo apt-get install nginx


##9 - adjust firewall
	sudo ufw app list
	sudo ufw allow 'Ngnix HTTP'
	sudo ufw status
	sudo ufw enable 
	sudo ufw allow ssh
	sudo service ufw restart 
	systemctl status nginx


##10 - install mysql
	sudo apt-get install -y mysql-client mysql-server libmysqlclient-dev
	sudo systemctl status mysql


##11 - create user for deploy 
	sudo adduser deploy --ingroup www-data
	su deploy
	cd
 	mkdir .ssh
 	chmod 700 .ssh
 	echo [cole a chave pública do seu vagrant] >>
   ~/.ssh/authorized_keys
   chmod 600 ~/.ssh/authorized_keys


##12 -  install node , directory deploy and create db
	sudo apt-get install nodejs
	nodejs --version

	sudo mkdir /var/www
	sudo chown www-data. /var/www
	sudo chmod g+w /var/www  

	mysql -u root -p
	show dabases;
	create database nameyourdatabase;


##13 - configure capistrano
	add in gemfile

	group :development do
		gem 'capistrano', '~> 3.7'
    	gem 'capistrano-bundler', '~> 1.2'
    	gem 'capistrano-rails', '~> 1.2'
	end 

	group :production do 
		gem 'mysql2'
	end

	bundle install

	bundle exec cap -v
	bundle exec cap install
	bundle exec cap -T

	in  Capfile
	require 'capistrano/bundler'
	require 'capistrano/rails'

	insert in the deploy.rb
	https://gist.github.com/nelisr/7d201bd6c105fe5d8de4c7d4289155ab

	bundle exec cap production deploy
 	bundle exec cap production deploy:check








