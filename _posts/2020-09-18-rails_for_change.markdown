---
layout: post
title:      "Rails For Change"
date:       2020-09-18 20:06:48 +0000
permalink:  rails_for_change
---


This is a project is all about change for me, changing careers changing direction, changing the world. Hence the name of this brand new app called Change • ish. I've never built anything with rails before so this was quite an adventure for me so let's travel together on a small journey on my rails coaster, shall we? Let's ride.

If you've never heard of Ruby on Rails it's a server side web application framework written in you guessed it or not Ruby created by a Danish David Heinemeier Hansson. It allows us to use a little magic in programming due to it's many generators which produces a vast amount of code such as Models, Views and Controllers  or MVC. Rails also produces scaffolds, Migrations, and Table creation with just a few commands, it's pretty awesome actually.

I began my project by making sure I have the right prerequisites in place like Yarn, Node.js, SQLite, and of course Ruby. 

After I completed that I typed into my terminal `rails new changi_ish` this allowed me to create my application called Chang•ish with all of its dependencies. This command also creates a ton of files for your app to get up and running quickly a part of the rails magic.

Next I had to get the server running so I'm able to view my code in the browser, this command is `rails s` this will fire up Puma a web server in which your code can be viewed on http://localhost:3000 which always makes think about Andre 3000 from OutKast, anyway this is exciting because when you see the Yay! You're on Rails! default page it's pretty exciting.

Next I had to setup my `Controllers` `Models ` and `Views` without those your are simply not  progarmming. For my project in particular I needed three different tables because the point of my app was to create a space where people could view various changes in our society in a news forum. So my tables were `users`, `articles` and `comments`. After I `rails db:migrate`d my tables I was prepared to rock.

  `create_table "articles", force: :cascade do |t|
    t.string "title"
    t.text "text"
    t.datetime "created_at", precision: 6, null: false
    t.datetime "updated_at", precision: 6, null: false
  end

  create_table "comments", force: :cascade do |t|
    t.string "commenter"
    t.text "body"
    t.integer "article_id", null: false
    t.datetime "created_at", precision: 6, null: false
    t.datetime "updated_at", precision: 6, null: false
    t.integer "user_id"
    t.index ["article_id"], name: "index_comments_on_article_id"
  end

  create_table "users", force: :cascade do |t|
    t.string "email"
    t.datetime "created_at", precision: 6, null: false
    t.datetime "updated_at", precision: 6, null: false
    t.string "name"
    t.string "uid"
    t.string "image"
    t.string "password_digest"
  end

  add_foreign_key "comments", "articles"
end
`

One of the elements of programming that is important is your `routes` so your are able to wire up your actions giving the ability to create, read, update, and destroy objects, this is better known as CRUD. If you ever wanted to take a look at your workable routes you can always run the `rails routes` command in the terminal.

After the route has been typed in if you are looking at your server it will be complaining about not having a Controller if you haven't generated one already. In programming every route needs a controller action it needs to be directed to a particular view. if there is no view you will get an exception. I needed a form template to be coded into my views otherwise I could not `show `the user any of my forms, no forms no data.

The other aforementioned class is a `Model` a model is the central component of the app. It is the application's dynamic data structure, independent of the user interface. It directly manages the data, logic and rules of the application. in my models i had to create my associations between my classes such as `has_many`, `belongs_to` to name a couple. 

I had to go through this process over and over again until each of my classes were properly connected to one another, ultimately giving me a finished product. Rail overall is an excellent framework that I would recommend to anyone, it will take more time to master but in the end I'll prevail.

