---
layout: post
title: Kele API Client
thumbnail-path: img/kele.png
short-description: Build an application to interact with Bloc API endpoints.
---

{:.center} ![]({{ site.baseurl }}/img/kele.png)

# Explanation

This project entailed building an API client. This program would work directly in IRB, using the HTTParty gem. It simplifies interacting with the Bloc API endpoints, allowing you to get an auth token, then automatically use that to properly format various GET and POST requests for you to do things like submit your work or send messages through the site's internal messenger service.

# Problem

Some of Bloc's API endpoints have a number of optional variables. Using optional arguments in Ruby is not difficult, thankfully there are a number of ways to implement this including splat operators, default argument values, and more. However, it became more complicated because the Bloc API will throw an error response if given any nil values for fields. Your HTTP request must be formatted using only the fields you are actually using. This meant the program needed to do more significant formatting work before sending out a request.

# Solution

```ruby
def create_submission(checkpoint_id, options = {})
    body = {
      'assignment_branch' => nil,
      'assignment_commit_link' => nil,
      'checkpoint_id' => checkpoint_id,
      'comment' => nil,
      'enrollment_id' => get_me.dig('current_enrollment', 'id')
    }

    final_body = body.merge(options).delete_if { |_k, v| v.nil? }

    response = self.class.post(
      '/checkpoint_submissions', headers: {
        'authorization' => @auth_token
      }, body: final_body
    )
    if response['message']
      p 'checkpoint not submitted'
    else
      p 'checkpoint submitted successfully'
    end
  end
```

To submit an assignment to Bloc involves five possible variables, but we only require the user to input one: the `checkpoint_id`, so that we know which checkpoint they are trying to submit. An `enrollment_id` is also required, but when they first logged into our program with the `get_me` function (which got their `auth_token` for use in all future requests) it returned a JSON parsed response with the `enrollment_id` buried in it, so we can use `dig` to search multiple levels deep in the response and get that info for the user behind the scenes.

As for the optional information, if we were to use techniques like splat operators or default values then we could have issues with things like argument order. This is not a situation where someone will only use variable five if they already used variable four, this is a situation where someone might use any or all of them and skip any others. We can't expect the user to remember what we are looking for and format it for us, so another solution is required.

By taking an options hash as an argument, the user inputs whatever optional arguments they want in any order, in a named `key => value` format. we preassign our nil values in a hash inside the function, then use the `merge` method which will override any existing values with those from the argument hash, if present, replacing our nils with any chosen options. We then delete any nil value pairs and use the result as the body inside of our HTTP request to the Bloc API.

# Results

This function worked almost entirely as I hoped. There was one issue: I originally chained my `merge` call with a `compact` call, but for some reason I was getting an error saying that "compact is not a function". Obviously for some reason `compact` didn't like the output it was getting from `merge`. I checked the docs quickly for both functions to make sure there was no obvious error in how either one was used, and there wasn't.

Now, they tell you not to reinvent the wheel. However, this saying really just means don't invent a new tool to solve a problem that was already solved _because_ it is a waste of time and it is faster to use the existing tool. In this case, though, I knew it would be trivial to write my own function. I enjoy how Ruby seemingly has a method for everything, but I come from a Javascript background where there are much fewer pre-existing and you tend to write your own. So, figuring that I could write my own "compact" far quicker than I could debug `compact`, I made my own `delete_if` function for the job.

The end result is a success: a five argument HTTP request that the user can quickly use with only one required argument and any mix of options they like, in any order.
