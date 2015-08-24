---
layout: post
title:  "Fun with White Space"
date:   2015-08-23 22:00:00
---

JavaScript developers are used to the standard set of [punctuators][punctuators] however, a closer look at the [line termination][lineterminator] rules for postfix/prefix operators, along with treatment of [white space characters][whitespace], and suddenly, a _new_ set of faux operators come to life.

According to the [spec][asi], the only restricted production when evaluating a postfix/prefix expression is the [line terminator][lineterminator].  This means that a left-hand or right-hand side expression cannot have a line terminator between itself and the postfix/prefix operator however, white space characters are not forbidden.  This isn't very exciting until you consider that [relational][relational] and [equality][equality] operators share the same white space character rules.

Using the node repl, let's take a look at some examples that take advantage of these rules:

{% highlight javascript linenos %}
// Postfix relational operator

var x = 5;
while(x --> 0) {
  console.log('x: ', x);
}

// Prints
> x:  4
> x:  3
> x:  2
> x:  1
> x:  0
{% endhighlight %}

{% highlight javascript linenos %}
// Postfix equality operators

var x = 5;
while(x --!== 0) {
  console.log('x: ', x);
}

// Prints
> x:  4
> x:  3
> x:  2
> x:  1
> x:  0
{% endhighlight %}

{% highlight javascript linenos %}
// Prefix relational operators

var x = -5;
while(0 >++ x) {
  console.log('x: ', x);
}

// Prints
> x:  -4
> x:  -3
> x:  -2
> x:  -1
{% endhighlight %}

{% highlight javascript linenos %}
// Prefix equality operators

var x = 1;
var y = 1;
var z = 0 ||-- x ||++ y;
console.log('z: ', z);

// Prints
> z: 2
{% endhighlight %}

The examples above demonstrate treatment of insignificant white space and not new or hidden operators.  While these faux operators might be fun, they are also confusing and decrease readability so don't follow this practice.  Thankfully, linters will justifiably yell at you if you use any of the above techniques.

[acorn]:          https://github.com/marijnh/acorn
[asi]:            https://es5.github.io/#x7.9.1
[equality]:       https://es5.github.io/#x11.9
[lineterminator]: https://es5.github.io/#x7.3
[punctuators]:    https://es5.github.io/#x7.7
[relational]:     https://es5.github.io/#x11.8
[whitespace]:     https://es5.github.io/#x7.2