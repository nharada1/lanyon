---
layout: post
title: Does Your Music Festival Give Hipster Cred? 
comments: True
---
I haven't really had time to write new blog posts with both class and research in full swing, but I did have some leftover code for scraping music festival data, so I decided to do something with it. The festival season is starting soon, with the insanely early SXSW already wrapped up and the massive juggernaut that is Coachella starting this weekend.

Since the hipsters amoung us know that going to a popular music festival (especially to see only headliners) is akin to renoucing "On Avery Island" or writing music reviews for People Magazine, I've put together a handy chart to help you choose which festival to go to based on how mainsteam on average the bands are. Using the ever-handy [Echonest API](http://developer.echonest.com/), I averaged out the familiarity and "hotttnesss" of the bands at the festival. The most mainstream festivals are towards the top right:

[![post-image-full](/assets/festivals/mainstream.png)](http://i.imgur.com/V7gqKiu.png)

In this case, familiarity can be viewed as long-term brand recognition, and "hotttnesss" can be viewed as hype at this moment. So a band like The Rolling Stones has strong name-recognition but might not be very hyped, while The Weeknd may be very hot but probably isn't familiar to most people over 40. It's rare for a band to be popular and not familiar, so most of the festivals lie along the same line. However, there are clear deviations. For example, Lollapalooza seems to have less brand recognition than Summerfest for the same amount of popularity. This makes sense given Summerfest's more family friendly demographic.

Many trends can be explained by the proportion of headliners to smaller acts. South By Southwest is quite hipster in this interpretation, while Boston Calling is very mainstream. This corresponds to SXSW's relatively large, small-timer lineup and Boston Calling's compact, headliner-heavy weekend. Hipsters will note that Pitchfork has stayed true to form and is deep in "you've probably never heard of them" territory. 

A few points of criticism to address preemptively:

* This graph relies on Echonest's ranking system, which is hush-hush. They claim the numbers are based on [activity over crawled webpages](https://developer.echonest.com/forums/thread/463) but who knows how accurate they actually are.
* There are no axes values because both parameters are normalized dimensionless numbers (i.e. values [0 1]), thus relative values are all that matter.
* I don't work for or represent Echonest, even though I know I've used them twice now in my blog posts. I do really appreciate their product though.
