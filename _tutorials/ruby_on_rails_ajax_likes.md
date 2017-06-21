---
layout: post
title: How to Setup an AJAX Like Button for Ruby on Rails Applications
permalink: /tutorials/ruby-on-rails-ajax-likes/
---
Using AJAX to Create a Like Button
==================================
#### By **Oscar K. Sandoval** (May 8th, 2017)
*Extended from the following tutorials:*
* [Using AJAX in a Ruby on Rails App](https://tests4geeks.com/ajax-in-rails/)
* [How to partials & AJAX, dead easy](https://coderwall.com/p/kqb3xq/rails-4-how-to-partials-ajax-dead-easy)
## Introduction
AJAX (Asynchronous JavaScript and XML) is a set of web development techniques to update the client's view without reloading the page. **Liking** is one such example where having to reload the page after liking indidivual entities can become a tiresome experience experience, especially notable during scrolling live feeds of information. Ruby on Rails has AJAX built into its framework, but liking is a feature that must be custom-built for usage. In this tutorial, we will touch all aspects needed to successfully like and unlike specific entities using the Rails framework and some JavaScript.  
## Scenario
Imagine creating a system where anonymous users are able to like/unlike ideas proposed to benefiting their community. Each idea stores its number of likes as an integer, but how do we prevent anonymous users from continually liking the same idea? One simple solution is to keep liked ideas in a client-side cookie, which also shows which ideas can be unliked. In the following sections, we build the **liking** feature with this scenario in mind.
## Gems
We add these gems to the `Gemfile`, then run `bundle install`
```ruby
gem 'font-awesome-sass' #get the like and unlike icons into your rails project
gem 'responders' #AJAX respond_to
```
## Routes
To handle the server-side transaction of liking an entity, Rails needs to know where to go in which controller.
In the case of liking ideas, we add this route to `config/routes.rb`
```ruby
get '/ideas/like/:id' => "ideas#like", as: 'idea_like'
```
## Controller
For our scenario, we will have two methods in the ideas controller for liking. The first method, `index`, will be where the table of our ideas will be displayed. The second method, `like`, is where the primary logic of updating the cookie and database values will take place.
```ruby
  #/controllers/ideas_controller.rb
  def index
    # Get the array of all ideas
    @ideas = Idea.all
    # Get the array of all liked ideas, if cookies[:likes] exists
    @likes = Array.new
    if cookies[:likes] != nil
      @likes = JSON.parse(cookies[:likes])
    end
  end
...
 def like
    @id = @idea.id
    @likes = Array.new
    #Check if cookie already exists
    if cookies[:likes] != nil
      @likes = JSON.parse(cookies[:likes])
      #Only add new like to cookie if it doesn't already have it
      if @likes.include?(@id)
        #Decrease value in database
        @idea = Idea.find(params[:id])
        @idea.decrement!(:likes)
        @idea.save
        #Update likes cookie
        @likes.delete(@id)
        @json_likes = JSON.generate(@likes)
        cookies[:likes] = @json_likes
      else
        #Update database values
        @idea = Idea.find(params[:id])
        @idea.increment!(:likes)
        @idea.save
        @likes.push(@id)
        @json_likes = JSON.generate(@likes)
        cookies[:likes] = @json_likes
      end
    #Else make a new cookie!
    else
      #Update database values
      @idea = Idea.find(params[:id])
      @idea.increment!(:likes)
      @idea.save
      #Make a new cookie
      @likes.push(@id)
      @json_likes = JSON.generate(@likes)
      cookies[:likes] = { :value => @json_likes, :expires => Time.now + 2628000 }
    end
    @div_id = '#like_button_'+@idea.id.to_s
     respond_to do |format|
         format.html
         format.js
     end
  end
```
The most important lines in regards to making `like` an AJAX function are the `@div_id` and `respond_to` statements. `@div_id` will be necessary in updating the correct idea that was liked/unliked, and `respond_to` is used for displaying the updated information after the AJAX call to the controller is complete.
## View (Main)
As idea details will be displayed in a list alongside other ideas, a custom view must be rendered per idea based on whether not this idea has already been liked. Rendering smaller, resusable views inside of a main view is known as **partials** in Rails, and in this scenario each idea will be displayed as its own row, with the number of likes being one column of that row.
```ruby
 #/views/ideas/index.html.erb
 <% @ideas.each do |idea| %>
    <tr>
         ...
         <td>
         <%= render :partial => 'like_button', locals: {idea: idea}  %>
         </td>
         ...
    </tr>
<% end %>
```
Some important aspects to note is the name of the partial, and the local variable being passed to the partial, which will both come into play when the partial is initialized.
## View (Partial)
In Rails, partials are designated by prepending the name with a hypen, so the `like_button` partial will be named `_like_button.html.erb` in the views folder for ideas.
```ruby
#/views/ideas/_like_button.html.erb
<div id="like_button_<%= idea.id %>">
    # Display the number of likes
    <%= idea.likes %>
    # If the idea has not been liked previously, show that the idea can be liked
    <% unless @likes.include?(idea.id) %>
      <%= link_to idea_like_path(idea), :remote => true do %>  
        <i class="fa fa-thumbs-o-up"></i>
      <% end %>
     # Else show that the idea can be disliked
    <% else %>
      <%= link_to idea_like_path(idea), :remote => true do %>
        <i class="fa fa-thumbs-o-down"></i>
      <% end %>
    <% end %>
</div>
```
Lots of important functionality is built into this partial for a successful AJAX call, so let's highlight the most imporant aspects:
* The `div`'s `id` is unique for each idea based on its id, which is important for updating the correct idea's icon after the AJAX call
* The `:remote => true` in each of the `link_to` enables Rails to service the view through an AJAX call
* The gem `font-awesome-sass` is being used here through `<i class="fa fa-thumbs-o-up"></i>` and `<i class="fa fa-thumbs-o-down"></i>`, with the like button being used as the hyperlink to the idea controller `like` function

## Updating the Partial After an AJAX Call
After an idea has been liked/unliked through clicking the `font-awesome-sass` icon, Rails must now update the correct partial.
```ruby
#/views/ideas/like.js.erb
$('<%= @div_id %>').html("<%= j (render :partial => 'like_button', locals: {idea: @idea }) %>");
```
As the `@div_id` in the ideas controller matches a `div`'s `id` in the ideas view, Rails find the correct partial to update in the view, and refreshes the client's icon without having to reload the page.
