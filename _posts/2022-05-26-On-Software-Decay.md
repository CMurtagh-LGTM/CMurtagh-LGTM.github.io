---
layout: post
title: "On Software Decay"
date: 2022-05-24
categories: Linux Software Ricing
---

## A Brief on the Evolution of My Perception

I once thought that software lasted forever, once written it would go on serving my needs till the last harddrive
it inhabited failed.
This dream somehow stayed with me as I learnt the basics of programming though high school creating fun games and toys
to show off to my friends.
I knew that these toys were transient as I moved from one to the other each one meeting their requirements and being
forgotten.
The software engineering courses throughout my degree changed this idea, I learnt that requirements are in a state of
constant flux and that software has to be constantly reimagined to meet these changes.
(Personally I feel this is mostly from the impossibility of fully and precisely defining requirements.)
Through my personal experience I found another threat to the longevity of software, though dependencies.

## The State of My Desktop

I love ricing linux, customisation of workflows and making everything look pretty is quite an enjoyable experience.
(You can find my dots [here](https://github.com/CMurtagh-LGTM/dotfiles), but they aren't pretty.)
However, I have found that dependencies both allow me to be able to rice but also provide a constant need for maintenance.

### Breaking Changes

Arch Linux, and the Arch User Repository, is one of the most crucial factors of my ricing.
I crave the bleeding edge of technology and always try to test out random projects I find on GitHub or the AUR.
Most consequences of this I may go over in another article, but what's relevant is the constant updating of the packages.

This leads to the only major problem I had with my system, when `wpa_supplicant` 2.10 came out there was an incompatibility
with my hardware that caused my internet to not work.
Whilst it was an easy fix to downgrade to 2.9 for a week and raise a bug report it still illustrates that an update to a
dependency can cause a critical failure of software.

A problem that went unnoticed for months was an update to `dunst` that changed the configuration format, this caused me
to be without desktop notifications until I removed the now erroneous config options.

We see that dependencies can deprecate and remove features that we rely on.

### Requirements

Now [Elkowars Wacky Widgets](https://github.com/elkowar/eww), even in its current 0.2 state, is an amazing tool that
allows you to create gtk widgets quickly and easily. This has enabled me to create a nice looking bar and a dash panel.

Here you can see my dash panel in the state before writing this post.
![Eww dashboard broken](/assets/images/eww_dash_broken.png)
Top left is music information and control, top middle is a `cava` output, top right has audio sink selection,
middle left has weather, middle right has stats, and bottom left has calendar events.

Firstly you can see the `cava` output is, well, not outputting. This shows a feature that now, in hindsight, clearly
wasn't a feature that I cared about and not at all apart from the requirements for my dashboard.

Now look at the calendar its near empty box, and the stack of sticky notes on my desk, illustrates how my plan to move
from a physical calendar to a digital one has led me to an even worse system.

The music information and control panel used to display the album artwork, I originally created it using `mpris` to get
the uri of the album artwork, then cache the image, then point eww to the image for display.
When I moved from using the spotify client to `mopidy` the images stopped displaying, not to worry I created patched
`mopidy-mpd` that provided images from `mopidy-spotify` over `mpd`.
The problem with this approach was that it only worked for the `mopidy-spotify` backend and a proper fix meant diving
into the guts of `mopidy` and changing each backend.
My requirements for images was met by my hacky patch and the `mopidy` team was very short-staffed, so I let my PR become
stale, even with 50% of the work done.
The images broke again when I moved from `mopidy-spotify` to `mopidy-local`, leaving me in the state you see above.

You can see that requirements cause software to become outdated and decay.

## Deprecation is Good

It may seem that I'm placing blame on deprecation and breaking backwards compatibility, that we should leave any feature
in our code that may be used.

Firstly maintainers of projects only have so much time to spend maintaining each feature,
many features become too unwieldy to maintain, and their use may not meet the requirements of the current users.
As you can see from the `mopidy` project some modules have a maintainer wanted notice.

Another point to make is that backwards compatibility has to go only so far.
The C++ language, in my opinion, is weighed down by choices to mostly preserve compatibility with 40 year-old code.
One easy example is having everything mutable by default and having to place the `const` keyword everywhere.
It's clear to me that C++ is old and that its on the way out, new languages like Rust have promise to overthrow C++,
eventually.

## Completing Software and Imortalisation

In the realm of video games we see software that meets an end of life, still usable, but the developers are no longer
developing the game.
For example, Kerbal Space Program recently released its "On Final Approach" update signifying an end to the game's
development.
This game has been labelled as complete, even though it won't receive any new updates somehow it will be immortal.
For example, I played Morrowind many years after it received its last update, and it was able to meet its requirement of
me having fun.

## Conclusion

I suppose that it's important to define requirements well and pick dependencies wisely.
I'm going to leave this conclusion lacking as I can't think of anything witty.
