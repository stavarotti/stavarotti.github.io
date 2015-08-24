---
layout: post
title:  "Fun with White Space"
date:   2015-08-23 22:00:00
---

JavaScript developers are used to the standard set of [punctuators][punctuators] however, a closer look at the [line termination][lineterminator] rules for postfix operators, along with treatment of [white space characters][whitespace], and suddenly, _exciting_ operators abound.

According to the [spec][asi], the only restricted production when evaluating a postfix/prefix expression is the [line terminator][lineterminator].  This means that a left-hand side expression cannot have a line terminator between itself and the postfix/prefix operator however, white space characters are not forbidden.  This isn't very exciting until you consider that [relational][relational] and [equality][equality] operators share the same white space character rules.

With this knowledge, let's take a look at some examples:

{% highlight javascript linenos %}
// Postfix relational operator
var x = 5;
while(x --> 0) {
  console.log('x: ', x);
}

// Postfix equality operators
var x = 5;
while(x --!== 0) {
  console.log('x: ', x);
}

{% endhighlight %}

{% highlight javascript linenos %}
// Prefix relational operators
var x = -5;
while(0 <++ x) {
  console.log('x: ', x);
}

// Prefix equality operators
var x = 1;
var y = 1;
var z = 0 ||-- x ||++ y;

{% endhighlight %}

The examples above primarily demonstrate treatment of insignificant white space and not new or hidden operators.  While these might be fun, they are also confusing and decrease readability so don't follow this practice.  Thankfully, linters will justifiably yell at you if you use any of the above techniques.

[acorn]:          https://github.com/marijnh/acorn
[asi]:            https://es5.github.io/#x7.9.1
[equality]:       https://es5.github.io/#x11.9
[lineterminator]: https://es5.github.io/#x7.3
[punctuators]:    https://es5.github.io/#x7.7
[relational]:     https://es5.github.io/#x11.8
[whitespace]:     https://es5.github.io/#x7.2