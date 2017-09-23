---
layout: post
title: BlocJams
thumbnail-path: "img/blocJams.png"
short-description: Build an application to play music.

---

{:.center}
![]({{ site.baseurl }}/img/blocJams.png)

## Explanation

This project entailed building a music player: a type of Spotify-clone. First I built it in vanilla JS, then refactored it into jQuery, and then I built it again using Angular.

## Problem

The Bloc training program had me build the music player up to certain specifications, but I wanted to see if I could make it even more functional for the user. I tried to step outside of my own perspective as the programmer and see what else I might want a music player to do. I came up with a number of improvements I wanted to implement, including finding a number of places where unexpected user input could lead to seemingly magical or unexpected behavior.

## Solution

For one example, the next song and previous song buttons had odd behavior. If you hit "previous" button too many times and try to go backwards from the first song on the list, the music would stop and the player appeared to be in a neutral state, but if you then hit the "next" button you would jump straight to the second song (and vice versa for the other button in the other direction). I wanted it to be clear that while the music was stopped, the program had held onto your place and you were still on the first song. This way the user would be better able to predict what would happen if they hit another button.

The original program had "play" and "pause" icons that would appear over track numbers if you hovered them, or if the track was playing. I added new conditional behavior to the Angular attributes in the HTML so that an icon would also persist on any song that was currently paused. This way pause behavior would be clearer to the user in general cases, and it would solve my problem with the next and previous buttons.

To make this work, though, I also had to make the program keep track of which song was paused, changing an "isPaused" boolean for each song. This meant adding code to a number of different places in the program, and there were many ways it could be implemented, so the trick was to do it with as little wasteful repetition as possible, and to avoid creating new unexpected behavior.

## Results

I was able to use logical reasoning to take the many possible implementations of my "isPaused" code and narrow them down to the two most likely to work efficiently and precisely as I wanted. Then, having implemented one of them, I did thorough testing of any possible combinations of inputs (pausing, playing, hitting next, mousing over to new songs, etc) in many different orders to see if it was possible to break the program or get magical behavior.

Thankfully my design was successful, and the program was one step closer to having my preferred kind of interface: one intuitive enough that the user doesn't notice it at all.
