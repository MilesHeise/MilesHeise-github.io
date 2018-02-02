---
layout: post
title: MERNt To Do That
thumbnail-path: img/mernTodo.png
short-description: Build a full MERN stack app with front and back end functionality.
---

{:.center} ![]({{ site.baseurl }}/img/mernTodo.png)

# Explanation

This project was my first attempt to build anything with the MERN (Mongo, Express, React, Node) stack. I had never used any of those four technologies so the entire stack was new to me, other than knowing Javascript. But, I had done my research and was pretty sure I could teach myself quickly how to make something that used Express for back-end API routing, fast front-end React views, and kept them both in agreement with each other through the careful use of asynchronous code on both ends.

# Problem

This is going to be the story of a bug I had during the process.

I had a pre-existing feature where you could toggle a boolean "Completed" status for a Todo item. I had just added a feature where you could also click on any item displayed in your list and it would turn into an edit field so you could update the content of the Todo right there inline. On the front-end, for various reasons having to do with how my React components were set up, it wasn't practical to have one "Update" function on one page to do both jobs. However, it always pays to be DRY and there was no reason they couldn't both hit the same API endpoint on the back-end. So, I updated my Express controller to respond to both inputs.

Having made my update, first I tested my back-end on its own, because that narrows your bug search if something already doesn't work. But happily, it did work. My new back-end function needed to correctly update the database whether it was changing a "Completed" boolean or a "Description" string so I checked each one using Postman to make requests with the appropriate info. It worked just fine.

But, I never trust testing-tools completely. They are only as good as what you think to test for, and you could always miss something, so I went to check my front-end as well. Sure enough, my new update description feature worked fine, but my toggle completed status feature had broken. You could update an incomplete to a complete, but you couldn't change it back. This is what I mean about how you can always forget things when you are testing, I had been worried about whether each _type_ of data would work, so I hadn't thought to make sure the boolean type would still work in _each direction_.

You, clever reader, may have already figured out the bug. Sadly it did take me a little longer.

# Solution

I had an inkling what it might be, but I believe in being thorough, so I thought through my bug hunt carefully. I knew the new "Description" feature worked, so I could cut that whole function out, and I knew from Postman that the back-end was talking to Mongo just fine, so the problem had to be in either the front-end toggle function or the back-end function receiving it.

I had a feeling it was probably something to do with the way the back-end checked which kind of data it was getting. That was the main thing that had changed, and the most likely thing to cause the type of odd behaviour I was noticing. Still, I am of the opinion that when debugging you should prioritize testing items both by likelihood of a mistake being there and also by the time required to check for a mistake there. If you think of something with only a 1 in 10 chance of being the issue, but it can be tested in just seconds, I say test it now. That way, in 9 out of 10 cases you have barely wasted any time at all, and in that 1 in 10 case you have saved a ton of time by not making more difficult, longer tests for other things, you've found a rare defect right away, and you didn't risk forgetting you'd thought of that option.

So, first I checked my data with two quick console logs, one right in the outgoing Axios request, which looked like this:

```javascript
toggleComplete(id) {
  const todos = this.state.todos.slice();
  const todo = todos.find(todo => todo._id === id);
  todo.completed = todo.completed ? false : true;
  axios.put(`http://localhost:3001/api/todos/${id}`, {completed: todo.completed} )
    .then(res => {
      this.setState({ todos: todos });
    })
    .catch(err => {
      console.error(err);
    });
}
```

and another on the incoming data the back-end was getting, which looked like this:

```javascript
exports.updateTodo = function(req, res, next) {
  Todo.findById(req.params.todo_id, function(err, todo) {
    if (err) {
      return next(err);
    }
    todo.description = req.body.description || todo.description;
    todo.completed = req.body.completed || todo.completed;
    todo.save(function(err) {
      if (err) {
        return next(err);
      }
      res.json({
        message: 'Todo has been updated!'
      });
    });
  });
}
```

Both were good, so it only cost me a few moments time to know with certainty that I only had to look at a couple lines of code, my problem had to be there. I'm guessing some of you have definitely spotted the problem already. Fresh eyes are great for that.

If you've read any of my other stuff you know that I am a big fan of understanding how things work under the hood. If you have a script or a tool and you really understand it then you can use it in more creative ways, and you can avoid misusing it.

So, when I saw the flaw it jumped right out at me, and I honestly laughed out loud at my own foolishness: out of habit I had used a double-pipe "or" to check what kind of data I was getting like `thing = argument || default` because this is generally a great technique for seeing if an argument or input is there, and if it isn't there then you get an undefined and use the default value instead.

However, it isn't a magic "undefined" finder tool, we just tend to use it as one. It is just a basic "or" function and it only cares about undefined because undefined is falsey and it cares about falsey values . . . falsey values like "False". Any time I tried to send it an update to make the boolean false it kindly cleaned up my data and made it True for me.

# Results

Luckily, this took even less time to fix than it did to find. Terse code is great but a little verbosity goes a long way when you need something done just right, so I changed my function to check `if (new-thing !== undefined) { old-thing = new-thing }`

Next time I need to check if an input is there, I'll _definitely_ remember not to use a shortcut with a boolean.
