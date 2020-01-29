---
layout: post
title:      "Sinatra Project"
date:       2020-01-29 09:38:57 -0500
permalink:  sinatra_project
---


It's project mode once again at Flatiron School and our task is to build a Sinatra application. My project is named Christ Code, which will enable a user to take notes and be able to recored a copy of thier favorite Bible verses and perhaps take notes of what they have learned during the course of their reading.

One of the many elements of our application is to use MVC which stands for, Models, Views, and Controllers.

The **Models** are the logic behind a web application. This is where data is manipulated and/or saved. 

The **Views** are the 'front-end', user-facing part of a web application - this is the only part of the app that the user interacts with directly. Views generally consist of HTML, CSS, and Javascript. 

The **Controllers** are the go-between for models and views. The controller relays data from the browser to the application, and from the application to the browser.

**User Model**

```
class User < ActiveRecord::Base
    has_secure_password

    validates_uniqueness_of :username, :email
    validates_presence_of :name, :username, :email, :password
    validates :password, length: { :minimum => 8 }


    has_many :verses

end
```

**This is my Verse Model**
```
class Verse < ActiveRecord::Base
   
    validates :title, presence: true, length: { maximum: 50 }, uniqueness: true
    validates :content, presence: true, length: { maximum: 1000 }
    
    belongs_to :user

end
```

**Controllers**
```
class UserController < ApplicationController

    get '/users/home' do 
        if logged_in? && current_user
            @verses = Verse.all
            erb :'/users/home.html'
        else
            redirect "/login"
        end
    end
      
    get '/signup' do
        if logged_in?
            redirect "/users/home"
        else
            erb :'/users/signup.html'
        end
    end
    
    post '/signup' do 
        @user = User.new(params)
        if @user.save 
              session[:username] = @user.username
              redirect '/users/home'
        else
            erb :'/users/signup.html'
        end
    end
    
    
    get '/login' do 
        if logged_in?
            redirect "/users/home"
        else
            erb :'/users/login.html'
        end
    end
    
    post '/login' do 
        @user = User.find_by(username: params[:username]) #find if @user username exists 
        if @user && @user.authenticate(params[:password]) # along with the passowrd
            session[:username] = @user.username
            redirect '/users/home'
        else
            erb :'/users/login.html'
        end
    end
    
    get '/logout' do 
        if logged_in?
            session.clear
            redirect '/login'
        else
            redirect '/login'
        end
    end
    
end 
```

**VersesController**
```
class VersesController < ApplicationController

    get "/users/verses" do
        if logged_in?
            erb :"/verses/index.html"
        else
            erb :"/root/index.html"
        end
    end 

    # CREATE
    get '/users/verses/new' do # => check to see if your routes are pointing to the right file
        if logged_in?
            @verse = Verse.new
            erb :"/verses/new.html"
        else
            redirect '/login'
        end 
    end
    
    post '/users/verses' do
        @verse = Verse.new
        @verse.title = params[:title]
        @verse.content = params[:content]
        # making associations below
        current_user.verses << @verse # HAS MANY HAS PLURAL WORD AFTER DOT NOTATION
        # MAKE SURE TO CREATE THE TWO RELATIONSHIP
        @verse.user = current_user # BELONGS TO HAS SINGULAR WORD AFTER DOT NOTATION
        if @verse.save #true 
            redirect "/users/verses"
        else
            erb :"/verses/new.html"
        end
    end
    
    # READ(SHOW)
    get "/users/verses/:id" do |id|
        @verse = Verse.find_by_id(id) #perhaps access by :user_id or :username?
        erb :"/verses/show.html"
    end

    # UPDATE(EDIT)
    get "/users/verses/:id/edit" do |id|
        if logged_in?
            @verse = Verse.find_by_id(id)
            erb :"/verses/edit.html"
        else
            redirect "/login"
        end
    end

    patch '/users/verses/:id' do |id|
        @verse = Verse.find_by_id(id)
        @verse.title = params[:title]
        @verse.content = params[:content]
        if @verse.save
            redirect "/users/verses/#{id}" 
        else
            erb :"/verses/edit.html"
        end
    end 

    # DESTROY
    delete '/users/verses/:id' do |id|
        @verse = Verse.find_by_id(id)
        @verse.destroy
        redirect '/users/home'
    end
end 
```

Her's an example of what a View may look like below.

**Views**


**Home.html.erb**
```
<h1>Hello, <%= current_user.name %></h1>

<div>
    <a href="/users/verses/new">Create a new note</a>
</div>
<div>
    <a href="/users/verses">View all of your notes</a>
</div>
<div>
    <a href="/logout">Logout</a>
</div>
```


During this project we were also asked to use ActiveRecord. For those of you who may not know what it is, Active Record is the M in MVC - the model - which is the layer of the system responsible for representing business data and logic. Active Record facilitates the creation and use of business objects whose data requires persistent storage to a database. 

Another major component of the project was to imlement CRUD which stand for Create, Read, Update and Destroy.  A CRUD application is one that uses forms to get data into and out of a database. CRUD is certainly a huge part of any users experience when they interact with our applications. 

There were several other elements we had to work with in order to reach our end goal, and it took a lot of hard work to do all of this from scratch.

Overall this was a great learning experience but quite challenging to say the least.It can be done with a positive mind-set and patience. If I can do it then so can you.
