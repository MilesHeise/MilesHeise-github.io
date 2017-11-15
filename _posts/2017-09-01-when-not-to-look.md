---
layout: post
title: When Should You _Not_ Look "Under the Hood" in Programming
---

Last time we discussed how easy it can be to look "under the hood" too much, or too little, when you are learning new things in programming. I gave you a few of my ideas about "Do's": times when you definitely should look under the hood. Now, I'd like to share some of my "Do not's", because I know from experience that having a very inquisitive mind can be just as crippling as it is helpful.

# Don't:

## 1\. _Don't forget to just get the information you need and get out_ -

I don't know a ton about how my package installer works. I mostly only ever use "npm install" or "npm start". I am a curious person, though, and I find myself thinking _"what other commands can it take? How does it work? I'd better go read the source code!"_

Curiosity is good, and doing research on things you find interesting is a great use of spare time, but it is death to efficient problem solving. You have to learn when to say _"all I need to do is update Jekyll. It says if I enter this into the command line it'll do that. I'm just going to cut-and-paste this thing I need and not waste time looking up exactly how this command works"_.

Remember, you can spend all afternoon looking up all the less commonly-used git commands, but three months from now, when you need one, **you're still going to have to google it!**

## 2\. _Don't mistrust things just because you haven't looked into them_ -

We all fear side-effects. It certainly isn't good practice to cut-and-paste large blocks of code without knowing how the bits and pieces individually work. But, it can be easy to take this good instinct too far. Personally, I find I have the urge to write my own solutions to things, even when it isn't necessary. I trust myself more, in a way that isn't terribly rational.

If the API I'm using has a native method for converting time-in-seconds into clock time, I should just have faith in it. It wasn't written by a crazy person, it probably looks pretty much identical to how I would do it, and I should take it on faith without looking at the source code that it won't do anything weird to break my program.

You could pretty easily write a function that works the same as Math.floor, but you have faith that the ECMA people probably already did fine making it themselves. On the other hand, you know that taking a huge snippet of something useful, from a source you don't know well, could be quite dangerous. They key is knowing where to draw the line in the grey areas in between, and if you're like me then you need to try having a little more faith.

## 3\. _Don't get lost in the Docs_ -

Learning a new tool? Of course you want to skim through everything in the documents, to see all the things that it can do. I talked last time about how this is a good practice. Make sure you know what tools are at your disposal! But, you mustn't look too deeply at first.

If you are brand new, and you find something that confuses you, the instinct is to learn it, to understand it. But, I can think of countless times reading through the Docs on a new API when I came across something I didn't understand, then spent a half hour figuring out what it meant, only to realize I could have learned it in two minutes if I had waited. Language that seemed so obscure and full of jargon when I was brand new turns out to be perfectly clear once I've used the tool enough to have had the problem they are talking about in that part of the documentation. Had I come there later on, organically, I would have known what it meant right away!

So these are some pitfalls to avoid and time-wasters to stay away from. I must admit though, I would still always rather risk being too curious than settle for not being curious enough.
