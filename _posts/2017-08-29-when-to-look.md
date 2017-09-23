---
layout: post
title: When Should You Look "Under the Hood" in Programming
---
When I have a problem with my car, it can be easy for me to find out just as much information as I need, and no more. Perhaps this is because I have a fairly decent understanding of how all the parts of a car work, even if I don't know the specifics. With computers, on the other hand, it is a much broader topic and no one person has a fully complete picture. It can be hard to know when I don't know something, and it can be easy to dig far deeper than I need to into the inner workings of things.

This is why, for example, I have never found myself by the side of the road with a broken-down car and ended up accidentally googling interesting things about cars for two hours instead of fixing it. Instead, I see that I'm leaking fluid, I know that I need to know what kind it is, so I google enough to figure out what type it must be and what I need to do to get the car running again. At no point do I think _"hmm, this mentions the drive-train, I don't know a ton about that either, better look into it a bit before I move on"_.

However, with computers, this is exactly what can happen to me. When I get myself lost in the ever-expanding branches of a research tree I often say that I'm _"going down to the transistors"_. This is because of one time when I actually did have to laugh at how I had been looking for a quick solution to a coding problem and found myself eventually reading about how computer chips are made. It was interesting, yes. But, not really applicable to my problem.

So, knowing that this is an issue for me, and so perhaps it is for others as well, here is my starter guide for when you should or shouldn't look "under the hood" in programming, and how far down the rabbit hole to let yourself go . . .

### Do's:

#### 1.  _Do know your time and space costs_ -

Now, this doesn't have to be exact, by any means, but you should never use a tool or write a function where you can't at least vaguely say, for example, _"This is very cheap in memory, but it has a medium cost in processing time"_.

It is true, many times there is no way for you to make something cheaper in memory without raising the cost in time, and vice versa. But it still can be useful to know your costs so that you don't find yourself running all your time hogs, or space eaters, concurrently, and instead keep a balance. Also, if you find you wrote something that is expensive on both sides, it is possible that the problem just requires a very complex solution, but it is also possible that just this once you might have written some total garbage and need to start over.

#### 2.  _Do know if you need a tool_ -

JQuery can be incredibly useful, but if you really only need to call a couple of DOM elements is it worth giving your user an increased load time just so that you don't have to write a few query selectors? Are you using Angular out of sheer habit, on a page that turns out to be heavy on content and low on functionality?

Going back to cars and other real-world examples: you won't often see someone trying to use a hammer on a screw. But, you will see someone putting Bootstrap on their application just to style one little button, when they could have just used a bit more CSS to do the same job.

Additionally, with new tools and APIs coming out all the time, it is important to stay current to a certain degree, but also important to think "will I spend more time learning this tool than it would actually save me?"

#### 3.  _Do try to know what tools are available_ -

It is easy to reinvent the wheel in programming. I doubt anyone hasn't, at least once, had the experience where you spend significant time designing a function to "doSomething" only to have someone point out after the fact that _"hey, you do know you could have used prototype.doSomething(), right?"_.

When you see a new method, look into what other methods are related to it, in case there are more you didn't know you could use. When you learn a new tool, skim everything it can do in the documents. Using Angular? Look at every native directive it has available so that you'll know where work has already been done for you.



Of course, this "Do" can really easily become a "Don't". Skimming directives can easily become looking in depth at the specs for every directive, even though you don't need any of them at the moment. I'll talk more about times when you shouldn't look under the hood in my next post.
