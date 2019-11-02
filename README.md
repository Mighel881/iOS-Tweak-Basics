### The Basics of iOS Jailbreak Tweaks
So, you want to learn how to write iOS jailbreak tweaks. Where do you start? Well you're going to want to know at LEAST the basics of the  Objective-C programming language.
In case you don't know what Objective-C is, it is the primary language Apple uses for most of iOS and its apps. Most of iOS's front-end (and maybe some back-end) internals are written in the Objective-C language.
For most (if not all) cosmetic tweaks, you will want to know how to use and interact with UIKit as well. So the TL;DR would be, know Objective-C and some basic UIKit.

Great! Assuming you've made it this far, let's get into the basics of what tweaks are and how to write them. If you're reading this, i'm sure you know what tweaks are; but, we're going to examine exactly what they do and how they work.
Tweaks modify methods, properties, ivars, etc. of specific classes to achieve a desired outcome. Essentially they just run extra code at runtime to modify iOS. Tweaks utilize a runtime code injection system (such as substrate or substitute) to achieve this outcome.

Let's look at a basic tweak; later, we will create an example tweak, but let's look at the basic structure of a tweak first. We will be using Theos (which utilizes the LOGOS syntax directives) to make writing tweaks significantly easier.

Let's look at this example tweak here. In this snippet we are changing the background color of all UIView objects loaded in a specific process (we will discuss this later) to be green.
```
%hook UIView
-(void)setBackgroundColor:(UIColor *)someColor {
    %orig([UIColor greenColor]);
}
%end
```
First, let's look at the `%hook` directive. This basically says that we want to hook the class with the name described after. If you wanted to hook another specific class, say "SomeView", you would write `%hook SomeView`. Easy, right?

Now let's examine the method(s) that we want to "override", or hook **in the class that we've already hooked**. In this example, we're hooking the background color setter method for the UIView class. The arguments **must** be listed so Objective-C knows exactly which method to modify.

Now that we understand which method we're modifying, let's look at the body of the method. We can see the `%orig` directive. This directive is  frequently used and is very important. It tells the tweak to run the original method that apple has already implemented in the process. When `%orig` is used with `()` (like in this example), we can change which attributes (e.g arguments) are passed to the original method. So, in this example, we're basically saying "Have each UIView run the original setBackgroundColor method, but use [UIColor greenColor] instead of the other attribute you receieved."