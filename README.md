# ror-discussion-questions

Take 30 minutes and discuss the following with your table group. Try whiteboarding out different solutions and ideas!

1 . How does Twitter prevent two users from having the same username?

2 . Write a method that prevents duplicate usernames from being saved?

3 . Given the following code in routes.rb, what would `rake routes` output to the terminal?

```ruby
  resources :tweets, only: [:show, :index] do
    get 'comments', as: 'comments'
  end
```

4 . Why might you use this type of nested route?

5 . Assume you have two models, `class Tweet` and `class Comment`. A Tweet `has_many :comments` and a Comment `belongs_to :tweet`. With only the routes defined above build out:
  * a Tweet index action and view to display all tweets
  * a Tweet show action and view to display only one tweet 
  * a Tweet comments action and view to display all comments for a single Tweet

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

7 . Write out an edit view with a form that will have a Post method to the Tweet controllers' update action.

CHALLENGE:

How might you use the following routes?

```ruby
    resources :tweets, only: [:show, :index] do
      resources :comments, only: [:show] do
        get 'likes', as: 'likes'
      end
    end
```
