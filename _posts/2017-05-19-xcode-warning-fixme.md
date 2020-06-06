---
layout: post
title:  "Show Xcode compiling warnings for FIXME and TODO with Swift"
date:   2017-05-19 14:48:56 +0100
categories: Xcode iOS
featured: false
image: assets/images/2017-05-19-xcode-warning-fixme-1.png
---

This solution is based on `Swift 3` and `Xcode 8`.

Sometimes it is just too easy to let some debugging code or unfinished logic slip into the code commit or even release build. The popular way to remind ourselves is to add comments beginning with FIXME or TODO. A simple search for those key words would help to find and fix those bits of code. 

But this extra step can be easily forgotten.

Instead of saying “Oh, sh*t” later on, it would be much better to show those comments as warnings during compiling time in Xcode. It is where most of the attentions are paid on. Apple does not provide a way to archive this feature. However, we can simply add a build script to the “Build Phases” in Xcode to show those warnings. You can find the sample warnings and comments below:

![](/assets/images/2017-05-19-xcode-warning-fixme-2.png)

![](/assets/images/2017-05-19-xcode-warning-fixme-1.png)

Much better, isn’t it?

---     
&nbsp;

### Steps to add this feature to Xcode:

Copy the script below:

{% highlight shell %}
KEYWORDS="TODO!|FIXME!"
find "${SRCROOT}" \( -name "*.swift" \) -print0 | \
xargs -0 egrep --with-filename --line-number --only-matching "($KEYWORDS).*\$" | \
perl -p -e "s/($KEYWORDS)/ warning: \$1/"
{% endhighlight %}

1. Open Xcode and go to the “Build Phases” of the settings of your app’s target, as below:

    ![](/assets/images/2017-05-19-xcode-warning-fixme-3.png)


2. Click on the “+” and select “New Run Script Phase”:

    ![](/assets/images/2017-05-19-xcode-warning-fixme-4.png)


3. In the new phase created, paste the script copied:

    ![](/assets/images/2017-05-19-xcode-warning-fixme-5.png)

&nbsp;

That’s it! Wala! Off you go!

&nbsp;

---
In this script, I used FIXME! and TODO! to distinguish from the normal FIXME: and TODO:. Because those comments are so common that the script may pick up the warnings from your libraries.