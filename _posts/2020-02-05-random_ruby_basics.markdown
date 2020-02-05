---
layout: post
title:      "Random Ruby Basics"
date:       2020-02-05 11:35:26 -0500
permalink:  random_ruby_basics
---


**How does an if statement work?** 

The first thing we need to talk about before I answer the question of how an` If` statement works is control flow. Control Flow is used to change the flow of control in any given program based on certain conditions and `If` statements do just that. `If` statements evaluated on true or false expressions, if the evalution results to true than the code inside the block will be run until the end.

```
my_bank_account = 100

if my_bank_account_balance > 50
   puts "I'm eating steak!"
end   
```

Since our bank account has over 50 dollars in it well we could get that steak dinner. YUM!! - (Assuming your not a veg-head :) )

Another  keyword that may be used in our` If` statement is  `else` and it leads to a path for a program to resume if the conditions for an if statement have not been met resulting in a falsy value. Let's take our example from above and implement it below:

```
my_bank_account = 25

if my_bank_account_balance > 50
   puts "I'm eating steak!"
else
	 puts "I'm eating a slice of pizza"
end   
```

As you can see that our bank account has less than 50 dollars in it so we cannot afford that steak dinner so in this case our If statement will puts out "I'm eating a slice of pizza", (Maybe next time)

You can take this one step further & use an` elsif `statement:

```
my_bank_account = 25

if my_bank_account_balance > 50
   puts "I'm eating steak!"
elsif my_bank_account == 30
  puts "Olive Garden it is"
else
	 puts "I'm eating a slice of pizza"
end   
```

This is saying "If" my_bank_account is greater than 50 print this message, else if my_bank_account equals 30 print this special message, otherwise if none of these conditions are true then print the "I'm eating pizza" message.”


The cool thing about If statements is that we can have nested `If` statements inside another. Let's take an example:

```
If 5 < 10
  puts "I'm less than you"
  If 5 > 10
       Puts "I'm higher than you
  Else
       puts I'm half the size of that other digit"
  End
End
```

It will puts out the "I'm less than you" and  "I'm half the size of that other digit" because the first` If` statement 5 < 10 is truthy so it will `puts` "I'm less than you" and still go into the nested` If` statement.


**Ruby operators - specifically `&&`, `||`, and `==`**

Next I want to describe some Ruby operators, first up is the `&& `operator which is called the **double-ampersand** which represents "AND". For this operator to be true both values must equate to` true`.

```
true && true #=> true
false && true #=> false
```


Next up is the `||`**double-pipe** which represents "OR". For the double-pipe to evalute to *true* we only need one value to equate to true, like so:


```
true || false #=> true
```

Last but not least is the `==` comparison operator represented by the **double equal signs**. This operator is checking for equality not to be confused with `=` assignment operator which simply assigns values. The comparison operator checks to see  If two values are equal, then the statement will return true, If they are not equal, then it will return false:

```
2 == 2 #=> true
1 == 2 #=> false
```


**What does `erb` do and what does it take as an argument?**

 In this portion I want to touch on `erb `which stands for **Embedded Ruby**,` erb` is a templating engine, which comes standard with every Ruby installation that allows us to use a combination of HTML and Ruby. Well you might say, OK, "so how does this benefit me?", so glad you asked,  `erb` allows us to reduce duplication of HTML as well as generate content that can change based on the available data.   We can implement erb into our code in two ways, the first is the the substitution tag (`<%=`). It starts with an opening tag delimiter and equals sign (`<%=`) and ends with a closing tag delimiter (`%>`).  It must contain a snippet of Ruby code that resolves to a value; if the value isn’t a string, it will be automatically converted to a string using its to_s method.  
	
	`<%= @verse.title %>`


The second of the two is the **Scripting Tags**, The scripting tags open with `<%` and it also closes with a `%>`. They evaluate  Ruby code but  never actually display Ruby code, in other words thess tags execute the code it contains, but doesn’t insert a value into the output. (cool right!)

`<% Your code %>`

Scripting tags can have some affect on iterative or conditional expressions even if the expression is untagged text they surround, for example:

<% if @flatironschool == true %>
      flatironschool
    <% end %>


**What does redirect do and what does it take as an argument how is it different from erb’s argument?**

I'm going to wrap this article up by talking about `redirect` a redirect takes in a path as an arguement, it will tell your  browser it needs to make a new request to a different location and this location can be a new path in *your* Web application or it can be a url. If you wanted to redirect to your login page for example it can be done like this:

`redirect "/login"`

If you wanted to redirect to a new url it would look like this:

`redirect "https://passme.com" #haha`

A redirect is different from erb. A redirect makes a new request and an erb is most commonly seen rendering web pages. The difference in arguemnts are as follow, redirect takes us to a new path, and an erb it's arguement is a new page to be rendered. 

Redirect 

`redirect '/signup"  #<= redirecting to new path`

ERB

`erb :'/users/signup.html' #<= rendering a new page`

That concludes this article I hope you've learned something today.

Happy Coding!!! :)
