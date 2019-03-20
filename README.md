# ror-discussion-questions

Take 30 minutes and discuss the following with your table group. Try whiteboarding out different solutions and ideas!

1 . How does Twitter prevent two users from having the same username?
  -validations!
2 . Write a method that prevents duplicate usernames from being saved?
  -validates :username, uniqueness: true
3 . Given the following code in routes.rb, what would `rake routes` output to the terminal?

```ruby
  resources :tweets, only: [:show, :index] do
    get 'comments', as: 'comments'
  end
```

-tweets GET /tweets/ tweets#index
-tweet GET /tweet/:id/ tweets#show
-comments GET /tweets/comments comments#index
-comment GET /tweet/:id/comments comments#show

4 . Why might you use this type of nested route?

-When one thing belongs_to another and only cares about its relationship to it.

5 . Assume you have two models, `class Tweet` and `class Comment`. A Tweet `has_many :comments` and a Comment `belongs_to :tweet`. With only the routes defined above build out:
  * a Tweet index action and view to display all tweets
  -/tweets
  -<% @tweets.each do |tweet| %>
    <%= tweet.info %>
    <% end %>

  * a Tweet show action and view to display only one tweet
  -/tweet/:id
  -<%= @tweet.info %>

  * a Tweet comments action and view to display all comments for a single Tweet
  -/tweet/:id/comments
  -<%= @tweet.info %>
    -<% @comments.each do |comment| %>
      <%= comment.content %>
      <% end %>

6 . In the code below what are the two private methods doing? How are they being called? Why would we use them?

```ruby
class TweetController < ApplicationController
  before_action :set_tweet, only: [:edit, :update]

  def edit
  end

  def update
    @tweet.update(tweet_params)
  end

  private

  def set_tweet
    @tweet = Tweet.find(params[:id])
  end

  def tweet_params
    params.require(:tweet).permit(:title, :message)
  end
end
```
-set_tweet is being used by before_action, to set the tweet before edit or update, we would use this to not repeat ourselves, called by the helper method before_action
-tweet_params is restricting the user to only editing what we want them to, aka strong parameters, called inside .update or .create

7 . Write out an edit view with a form that will have a Post method to the Tweet controllers' update action.

<% form_for @tweet do |f| %>
  <%= f.label :title %>
  <%= f.text_field :title %>
  <%= f.label :message %>
  <%= f.text_field :message %>
<% end %>

CHALLENGE:

How might you use the following routes?

```ruby
    resources :tweets, only: [:show, :index] do
      resources :comments, only: [:show] do
        get 'likes', as: 'likes'
      end
    end
```


/tweets/:id/comments/:id/likes would show you all the likes on a particular comment on a particular tweet
