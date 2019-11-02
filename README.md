### The Basics of iOS Jailbreak Tweaks
So, you want to learn how to write iOS jailbreak tweaks. Where do you start? Well you're going to want to know at LEAST the basics of the  Objective-C programming language.
In case you don't know what Objective-C is, it is the primary language Apple uses for most of iOS and its apps. Most of iOS's front-end (and maybe some back-end) internals are written in the Objective-C language.
For most (if not all) cosmetic tweaks, you will want to know how to use and interact with UIKit as well. So the TL;DR would be, know Objective-C and some basic UIKit.

Great! Assuming you've made it this far, let's get into the basics of what tweaks are and how to write them. If you're reading this, i'm sure you know what tweaks are; but, we're going to examine exactly what they do and how they work.
Tweaks modify methods, properties, ivars, etc. of specific classes to achieve a desired outcome. Essentially they just run extra code at runtime to modify iOS. Tweaks utilize a runtime code injection system (such as substrate or substitute) to achieve this outcome.

Let's look at a basic tweak; later, we will create an example tweak, but let's look at the basic structure of a tweak first. We will be using Theos (which utilizes the LOGOS syntax directives) to make writing tweaks significantly easier.

Let's look at this example tweak here. In this snippet we are changing the background color of all UIView objects with the given filter to be green.
```
%hook UIView
-(void)setBackgroundColor:(UIColor *)someColor {
    %orig([UIColor greenColor]);
}
%end
```