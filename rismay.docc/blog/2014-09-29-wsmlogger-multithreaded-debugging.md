# WSMLogger

@Metadata {
  @PageImage(purpose: icon, source: "blog-2014-09-29-wsmlogger-multithreaded-debugging-icon", alt: "WSMLogger icon")
  @PageImage(purpose: card, source: "blog-2014-09-29-wsmlogger-multithreaded-debugging-card", alt: "WSMLogger card")
  @PageKind(article)
  @PageColor(blue)
}


@Image(source: "blog-2014-09-29-wsmlogger-multithreaded-debugging-hero", alt: "WSMLogger hero")

A logging approach that improves multithreaded debugging beyond NSLog.

The most effective debugging tool is still careful thought, coupled with judiciously placed print statements.

— Brian W. Kernighan

When I first started coding Objective-C, I relied on NSLog to understand how to code was flowing. I would print out statements like this:

NSLog(@"WSPL:overlaysWithWSActivity:MID01 count: withActivity: Looping through activity of size %i", newActivity.coordinates.count);

Looking back this is obviously not the way to go about things. “WSPL” was a way for me to get which file was logging this command. I then manually printed out the method (“overlaysWithWSActivity:count:withActivity”). The “MID01” token was a way of identifying what line I was actually at. Finally, I put in the actual bit of information that I wanted “Looping through moments.”

Luckily, I stumbled upon CocoaLumberjack. The library comes with several built in loggers which you can customize to your liking, but did not quite give me the level of detail that I needed. The shortcomings came particularly apparent while working on multi-threaded code. Although, I was getting the info I needed I did not know from what thread or queue the work was being performed.

My solution to all of these problems came in the form of WSMLogger. Now I get log statements that I code like this:

NSLog(@“Nice”);

But output that looks like this:

01:03.147-main[AppDelegate |-[AppDelegate application:didFinishLaunc] Nice!

Why is this better? When dealing with multi-threaded code, milliseconds matter. So I opted for just minutes, seconds and nanoseconds as the timestamp. The thread, the file name, the object, and method are then automatically printed. And finally, I can control the individual length of characters each component gets per log statement. So how do you use this awesome logging.

You should, learn how to use cocoa pods. Add “pod ‘WSMLogger’” to your Podfile. For ease of use, add <WSMLogger/WSMLogger.h> to your .pch file.
From now on, all NSLog statements will be replaced with a C Macro that will call on DDLog. Add to your AppDelegate file a class load method with the settings for that you want for the WSMLogger.
For example, I use:

```objc
#pragma mark - Custom Logging at Startup

+ (void)load {

WSMLogger *logger = WSMLogger.sharedInstance;

[DDLog addLogger:logger];

// Customize the WSLogger

logger.formatStyle = kWSMLogFormatStyleQueue;

logger[kWSMLogFormatKeyFile] = @16;

logger[kWSMLogFormatKeyFunction] = @40;

}
```

What does that text snippet do? Firstly, it creates the WSMLogger, and registers it with CocoaLumberjack. Second, it sets the style to use (I have created different styles in WSMLogger). Finally, it sets the number of characters to use for the File and Method name.

That’s it! All your pre-existing NSLog statements will automatically output with the new format you have customized.
