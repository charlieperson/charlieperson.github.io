---
layout: post
title: "Nested Resources"
date: 2017-08-14
---

### Routing
There are many ways for us to configure our routes in Rails.

Here is a basic example of routing in Rails:
```
  get '/events', to: 'events#index' // renders all events on page
  get '/events/:id', to: 'events#show' // renders specific event on page
  get '/events/:id/edit', to: 'events#edit' // renders edit page for specific event
  get '/events/new', to: 'events#new' // renders page for creating a new event
  put '/events/:id', to: 'events#update' // updates a specific event
  post '/events', to: 'events#create' // creates a new event
  delete '/events/:id', to: 'events#delete' // deletes a specific event
```

As we all know, Rails is about convention. Rails conventions make our lives
easier (most of the time). They make it so we can quickly get an application running.
So there is a convention for all of the code above. We can simply write

```
resources :events
```
and all of the code above will be implemented for us under the hood.

Often times, we will have resources that only matter when another resource is present.
For example- comments. What good is a stand alone comment? It has to have something
it is referring to. Like a picture, a post, an event, etc. This is when nested resources
come into play.

Here's an example:

```
  get '/events/:event_id/comments', to: 'comments#index' // renders all comments for a specific event
  get '/events/:event_id/comments/:id', to: 'comments#show' // renders a specific comment for an event
  get '/events/:event_id/comments/new', to: 'comments#new' // renders page for creating a new comment
  get '/events/:event_id/comments/:id/edit', to: 'comments#edit' // renders page for editing an existing comment
  post '/events/:event_id/comments', to: 'comments#create' // creates a new comment for a specific event
  put '/events/:event_id/comments/:id' to: 'comments#update' // updates a specific comment
  delete '/events/:event_id/comments/:id' to: 'comments#delete' // deletes a specific comment
```

This is an example of nested resources. We could also have the same situation for another
type of resource (like posts, pictures, etc.), but for that, we would need polymorphic
associations which is out of scope for this post.

Of course, we don't have to write out all of this explicitly. Rails makes this very easy.

This code is the equivalent to the above:

```
resources :events do
  resources :comments
end
```

However- there is a small problem (more of a nuisance actually) with the structure
of the code above. We do not actually care about which event a comment is associated
with when we delete it or update it. In fact, it's just extra work for us to have
to figure out which event we are referring to and pass it in as a parameter that we
don't actually need anyway. If we have the comment's id, we shouldn't care about
what it's parent resource is for updating or deleting. In the case of updating, that
association has already been created, and in the case of deleting, the whole comment,
and therefore its association, will be deleted anyway.

So- there is a better way.

```
resources :events do
  resources :comments, :except => [:update, :destroy]
end

resources :comments, :only => [:update, :destroy]
```

## Conclusion

When it comes to nested resources, often times, we don't need certain routes. Things like
:new, :index and :show are usually so coupled with the parent that we wouldn't want
a completely different page for creating a new comment, and therefore we would just
add the form in the :show view of the event. Same thing when it comes to :edit. Also,
it may be strange to have a show view for a single comment. Again, we'd probably just want
to render all comments for a specific event on the event's show page. Even when it comes to
the :edit action, we would probably not want an entirely new page for editing a comment. In
this case it would be better to just add some JavaScript to render a form on the page
when someone clicks the edit button for a comment.
