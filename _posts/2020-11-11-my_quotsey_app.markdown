---
layout: post
title:      "My Quotsey App"
date:       2020-11-11 15:04:28 -0500
permalink:  my_quotsey_app
---


Hi ladies and gents it's time for another project build in the curriculum and this one is with JavaScript in the form of an API or an Application Programming Interface using Ruby on Rails. An API is  a set of functions and procedures allowing the creation of applications that access the features or data of an operating system, application, or other service. 

Now this project I want mu user to be able to read and create some quotes of their choice. In order to do that the very first thing that I needed to do was set up my initial set by using `rails new quotesy --database=postgresql --api`. This will generate tons of files so I can get off the ground running allowing me to use rails built in `Controllers, Models and a Database` for my JSON data. 

First on my todo was to build out my models one for my quotes and the other for the category, I performed this by simply typing `rails g model <your_model_name> name`. I've learned that it is best practice to capitalize your model name when generating it. Here you want to create some associations with the `belongs_to` and `has_many` , my quote `belongs_to` a category and my quotes `has_many` categories. Quick note, your attributes are automatically added to the table in the database and mapped to the model with that `rails g model ` command.

##Models
quote.rb

```
class Quote < ApplicationRecord
  belongs_to :category

  validates :quote, :author, :category, presence: true
end
```

catagory.rb

```
class Category < ApplicationRecord
    has_many :quotes, dependent: :destroy
end
```

In my routes I wnanted to implement specific namespaced routes for a controller

##Routes

```
Rails.application.routes.draw do
  namespace :api do
    namespace :v1 do
    resources :quotes, only: [:index, :create]
    resources :categories, only: [:index]
    end
  end
end
```

Name spaced routes looks as follows `http://localhost:3000/api/v1/quotes` and `http://localhost:3000/api/v1/categories`. Essentially `:namespace` changes prefix name with URL along with controller directory structure. Name spacing gives your API it its own controllers and routes. It is simple, and keeps your APIs independent from the rest of your controllers. 

At this point I needed to generate my controllers, In my console I ran: `rails g controller api/v1/<your controller_name> ` here it also important to make sure you capitalize the first letter of the controller name.

##Controllers

QuotesController.rb

```
class Api::V1::QuotesController < ApplicationController

    def index 
        quotes = Quote.all
        render json: QuoteSerializer.new(quotes)
    end 

    def create 
        quote = Quote.new(quote_params)
        
        if quote.save
            render json: QuoteSerializer.new(quote), status: :accepted
        else
            render json: {errors: quote.errors.full_messages}, status: :unprocessible_entity
        end
    end 

    private 

    def quote_params
        params.require(:quote).permit(:quote, :author, :tag, :category_id)
    end 
end
```

categories_controller.rb

```
class Api::V1::CategoriesController < ApplicationController

    def index
        categories = Category.all
        render json: CategorySerializer.new(categories)
      end
end

```

Next I needed to add the  `'fast_jsonapi'` gem to my Rails project's Gemfile and run bundle install. The fast json api is known as a serializer. A Serialization is the process of converting an object into a stream of bytes to store the object or transmit it to memory, a database, or a file. Its main purpose is to save the state of an object in order to be able to recreate it when needed. I ran `rails g serializer <your_resource_name>` in the console to create my `Category and Quote Serializer classes`.

```
class CategorySerializer
  include FastJsonapi::ObjectSerializer
  attributes :name
end

```

```
class QuoteSerializer
  include FastJsonapi::ObjectSerializer
  attributes :quote, :author, :tag, :category_id, :category
end

```

After that I was off to DOM manipulation, Event Listeners, and Fetch Requests so that I could render the elements I wanted for my frontend. Overall this project was tough and I times I just was lost but I stayed with it. If I could do then you can to, just be positive and code happy.
