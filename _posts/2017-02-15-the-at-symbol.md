---
layout:     post
title:      "The At Symbol"
date:       2017-02-06 22:00:00
comments:   true
header-img: "img/b2b-at-symbol.jpg"
header-img-author: "Dustin Gaffke"
header-img-url: "https://flic.kr/p/m5P8xb"
tags: [back-to-basics]
---

I have been using C# and .NET for over 10 years now and recently I have started to dig here and there for little details of the language and the framework. The other day, I came across an interesting sort of new way of using the `at symbol` `"@"`. And I say sort of new because I had used this before but I never really internalize it.

The most common use of the `@` symbol that I have encounter is to use verbatim string literals (as described in the [string reference for C#](https://msdn.microsoft.com/en-us/library/362314fe(v=VS.100).aspx)). This basically means that you don't need to escape the backslash as it ignores escape sequences:

{% highlight csharp %}
var myEscapedPath = "\\\\MyEscaped\\Path";
var myVerbatimPath = @"\\Myverbatim\Path";
{% endhighlight %}

Also, in MVC land, you make heavy use of the `@` symbol when you are using Razor as a View Engine. So you have probably written code like this:

{% highlight csharp %}
@Html.EditorFor(m => m.MyProperty, new { @class="css-class" })
{% endhighlight %}

When you start to work with HTML Helpers, you learn that an Anonymous Object can be sent as a parameter and its properties will become HTML attributes on the client side. Also, you can see that you can use `@class` to specify a CSS class to be rendered.

Well, this is what I didn't know. The `@` symbol in front of the `class` is actually in [the C# specification](https://msdn.microsoft.com/en-us/library/aa664670.aspx) as a way to use reserved words as identifiers. You it is perfectly valid to declare variable names like:

{% highlight csharp %}
int @int;
string @string;
bool @bool;
{% endhighlight %}

So as they say, you learn something new every day :-)

<p><small>Photo from <a href=""></a></small></p>