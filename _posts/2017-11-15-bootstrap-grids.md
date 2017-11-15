---
layout: post
title: Don't Use Bootstrap When You Only Need a Grid
---

Web development is full of big, powerful tools, and it can be easy to get distracted by them. But, a lot of times you don't need a power drill just to fix a loose cabinet drawer, and _you don't need Bootstrap just to make a grid._

There is no need to automatically start every project by adding JQuery, Bootstrap, Sass, and a dozen other things if you aren't sure that you'll need them. You're adding load time to your app, forcing yourself to follow extra conventions, and potentially spending more time on a time-saver than it is worth. There are many times when something like Bootstrap is absolutely a lifesaver, but using Bootstrap just to have a website grid when you don't need any of its other functions is one of the most common examples of tool overuse.

So, let's look at some of the quirks of how Bootstrap grids work. This is useful for two things: one, debugging your Bootstrap layout if something isn't working how you'd like, and two, maybe just doing a grid of your own if that's all you need.

# 1\. _You actually do need containers, rows, and columns_ -

This tripped me up at first using Bootstrap. I saw plenty of code snippets that must have been trimmed for brevity and didn't include all three, and programmers sometimes love redundant conventions in the interest of readability, so I falsely thought you didn't necessarily need them all. When making a quick mock-up of something I wouldn't use all three and then I'd be shocked when things didn't work right.

In reality, there's a clever reason for this three-class structure, which you should know about for debugging your Bootstrap (and you should use if you're making your own quick grid):

- You have your **container** that holds everything. You only need one and never need to nest them. It centers everything on the page and it has 15px of padding.

- Within that you make a **row**, this has -15px of padding which makes it stretch back out over and negate the container padding.

- Finally you have **columns** inside the row, which have 15px of padding of their own.

This system of adding padding, removing it, adding it again, seems convoluted. But, it is easy to execute in your own CSS and it has two wonderful effects. First, it prevents double padding at the edges of the view without having to make first-child/last-child exceptions in your CSS (which might not even work the way you want, if other things are affecting your view order on the page for some reason). Second, it prevents double padding if you nest a second grid inside the first (by creating a row inside a column, then new columns within that).

As you can see, you can make your own Bootstrap-style grid of three classes very easily. And if you are trying to debug errors in how Bootstrap is working for you, you can check if anything you are doing would interfere with this behaviour.

# 2\. _Rows are not rows_ -

Row can be a misleading term. You hear 'row' and you expect that each one should be the width of the container, no more and no less, and you think that any new row will be beneath the one before it. But 'row' is just a class name, not an exact description. Columns in Bootstrap rows essentially just float left and pile up on each other within their row, so there is no reason you can't have more or less than twelve columns More than twelve columns will just wrap down into a new line in a predictable way (well, as predictable as anything in CSS ever is). There are tricks you can do to make use of this, making use of a "wrong" number of columns to get your page to display in different mobile or desktop friendly ways depending on the viewer.

# 3\. _Bootstrap chose twelve columns but you don't have to_ -

Twelve divides up a page nicely for most things but if you have other needs you can just do a bit of division and use it to set your class's widths to the right percentages. So, whether you are trying to make your own quickie grid or debug something wrong with your Bootstrap site, know that the row system mostly comes down to columns with percentage widths, trying to float left on each other.

# 4\. _Surely there's more to it than that_ -

There is. There's plenty more to it.

The Bootstrap grid is quite well designed and it does come down to more than just a bit of padding and a float. There are Bootstrap classes to help you justify your columns and improve the look of your grid. Some of these you could easily duplicate, others would be harder to do from scratch and might not be worth it.

Bootstrap is responsive, so if you're going ti alone you'll need to write some media queries into your CSS. This is another thing which will take less time than installing Bootstrap to do it yourself on a small project, but might warrant using their tools on a bigger one.

Most importantly, they have bug fixes. If you've made your own grid system you're going to come across things that don't quite work right, since that's a basic truth of CSS design. For example, floats can have very strange behaviour, and Bootstrap comes with things like the 'clearfix' class to fix them. However, if you simply google 'clearfix' you won't have any trouble finding a dozen quick solution suggestions in basic HTML or CSS. Many of their bug fixes are like this: super useful if you already need Bootstrap, but not a reason to install it.

-

So, if you are using buttons and modals and all the other features on Bootstrap, then by all means also use their incredibly well designed grid system. And, use this under the hood knowledge when things don't line up quite how you expect. Or, if all you're looking for is a basic grid, **don't be scared to make one yourself!**
