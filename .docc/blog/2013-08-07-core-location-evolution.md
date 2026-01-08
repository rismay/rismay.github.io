# Core Location

@Metadata {
  @PageImage(purpose: icon, source: "blog-2013-08-07-core-location-evolution-icon", alt: "Core Location icon")
  @PageImage(purpose: card, source: "blog-2013-08-07-core-location-evolution-card", alt: "Core Location card")
  @PageKind(article)
  @PageColor(blue)
}

@Image(source: "doc-2013-08-07-core-location-evolution-hero", alt: "Core Location hero")

@Image(source: "blog-2013-08-07-core-location-evolution-hero", alt: "Core Location hero")

Apple has refined Core Location to improve battery life and location accuracy over time.

There seems to be a lot of interest in the new iOS 7 location APIs - CoreLocation. [Here is a great hacker news discussion about it.](https://news.ycombinator.com/item?id=6171514) I want to provide a little more "context" to this discussion.

As an aside checkout:

- [Jer Thorp's talk from a TedX talk a couple of years back regarding location history](http://youtu.be/Q9wcvFkWpsM).
- [William Edward's work on grabbing location data from your iPhone backups.](http://williamedwardscoder.tumblr.com/post/15210221400/visualising-iphone-tracking-data)

My Background:

[Here is a quick 1.5 minute demo of wrkstrm I made for the AngelHack 2012 summer finals.](http://youtu.be/U0adNGyXsuE)

iOS 2:

Apple introduces CoreLocation with a minimal amount of features. Programmers can ask to be updated about GPS coordinates only when their Apps are in the foreground.

iOS 5:

Apple adds two huge additions which introduced significant location monitoring and geo fencing. This information was already being logged by the iPhone ([there was a huge scare about this in 2011](http://www.tuaw.com/2011/04/25/a-roundup-of-todays-locationgate-news/)). All Apple did was give developers access to this data without having to hack (check out William Edward's demo and Jer Thorp's OpenPaths).

Another aside: These two APIs are what prompted me to learn how to code. I was seriously disappointed when I found out that Apple was "cheating" the implementation of these APIs. The resolution to these APIs is horrible - something like football fields of disparity in inner cities. This is what started my journey into finding a more accurate way to geo fence and track locations.

iOS 6:

For this release Apple worked closely with the MapKit team to improve GPS accuracy. The best example of this is how the CoreLocation team used the new MapKit vector graphics to clip GPS coordinates to streets. Again, Apple didn't invent a new technology to improve GPS accuracy, it leverage a new user interface innovation. To implement this Apple released a activity type (driving, walking, etc) API which alerted CoreLocation as to when it would be appropriate to clip coordinates.

iOS 7:

[These screenshots use a different approach to generate.](http://board.protecus.de/t42771.htm#360301) This information is NEW and gathering it was made possible by two sensor driven user interface innovations which seem totally irrelevant. First, in iOS 6 Apple started running the accelerometer all day with it's "raise to speak to Siri" feature - (simply put the phone to your ear to activate Siri). Now with iOS 7, Apple has introduced a "constant on" gyroscope, with the introduction of the Parallax effect. Apple can measure "stay" events when the iPhone is not moving without resorting to expensive / inaccurate geo fencing. Why am I so sure that this is what Apple is doing? Apple was originally planning to go even further by providing step count data (similar to the Galaxy S4's S Health data) to developers. This is only possible by running the aforementioned sensors and using signal processing. This was shown in the new iOS 7 technologies during the keynote and even in the iOS 7 beta 1 documentation, but all mentions were abruptly removed with beta 2 and beyond. Look for this in iOS 7.1 or iOS 8.

Finally, with iOS 7, Apple went one step further. With iOS 6, Apple used to provide GPS applications real time updates. Now there is a new API that allows deferred GPS notifications so that Apple can shut down your app and give you notifications "opportunistically" (i.e. when a user turns on the lock screen). Apple claims to provide a 40% improvement in battery life using this new method. If so, this technology is a game changer for always on location trackers.
