# Exemple d'utilisation de devise

Cette exemple illustre l'utilisation de Devise

Specification:

* Rails 5
* Devise 4.2.1
* Mysql

Utilisation:

*1 - Création de l'application 
        $ rails new Devise -d mysql
*2 - Ajouter devise dans le Gemfile

        gem 'devise'
        gem 'bcrypt', git: 'https://github.com/codahale/bcrypt-ruby.git', :require => 'bcrypt'

*3 - Installation des fichiers de configuration de devise

        $ rails generate devise:install

*4 - Génération du module devise

        $ rails generate devise user

*5 - Migration

        $rake db:migrate

*6 - Création des controleurs(view aussi)

        $ rails generate controller home index

*7 - Modification du homeController

    class HomeController < ApplicationController
        before_filter :authenticate_user!

        def index
        end

        def new
        end

        def edit
        end

    end
*8 - Authentification avec un nom d'utilisateur

        8 - a)  Ajouter username dans user

                $ rails generate migration add_username_to_users username:string

        8 - b) Changer le fichier de configuration de devise(config/initializers/devise.rb)

                config.authentication_keys = [:username]
                config.case_insensitive_keys = [:username]
                config.strip_whitespace_keys = [:username]

        8 - c) Générer les views

               $ rails generate devise:views

        8 - d) Remplacer login par username dans app/views/devise/sessions/new.html.erb

        8 - e) Ajouter username dans app/views/devise/registrations/new.html.erb

        8 - c) Ajouter ceci dans 

                devise_parameter_sanitizer.for(:sign_in) {|u| u.permit(:email,:username)}
                devise_parameter_sanitizer.for(:sign_up) {|u| u.permit(:email, :username, :password, :password_confirmation)}

*9 - Authentification à la fois avec un nom d'utilisateur et un email

        9 - a) ajouter ceci dans /app/models/user.rb

                attr_accessor :signin

        9 - b) changer la valeur suivante dans /config/initializers/devise.rb

                config.authentication_keys = [ :signin ]
                
        9 - c) 


