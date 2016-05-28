---
layout: post
title:  "Functional Programming with JavaScript Arrays"
date:   2015-01-07 20:06:28
disqus: y
categories: javascript
---
One of the benefits of not supporting out-dated browsers is that a whole host of
[higher order functions](http://en.wikipedia.org/wiki/Higher-order_function) are
made available on the Array prototype.

During a code review at work I came across a function that iterated
over an array of objects, returning true if the predicate is true for an element,
otherwise false. Below is a simplified example to illustrate this:

```javascript
function isLarge(x) { return x > 1000; }

function containsLargeNumber(numbers) {
  for (var i = 0; i < numbers.length; i++) {
    if (isLarge(numbers[i])) {
      return true;
    }
  }

  return false;
}
```

I suggested that they could make use of the method
[some()](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/some)
to improve the clarity of and shorten the code. Here is the above function
rewritten to use some():

```javascript
function containsLargeNumber(numbers) {
  return numbers.some(isLarge);
}
```

I think that this version of containsLargeNumber() is much more concise.

---

Array has many more useful methods, another of them being
[every()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/every)
which is closely related to some(). every() takes the same arguments as some() but
only returns true if the predicate is true for all of the elements.

Below I have given short examples for what I believe are some of the most useful
higher order functions available on array.

### Map
[map()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)
applies a given function to each element of the receiver and returns a
new array with the results. For example we could double each element like this:

```javascript
> [ 1, 2, 3 ].map(function (x) { return x * 2; });
= [ 2, 4, 6 ]
```

### Reduce
[reduce()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)
reduces an array into a single value, we could calculate the sum of by returning
the value of the accumulator plus the element:

```javascript
> [ 1, 2, 3 ].reduce(function (acc, x) { return acc + x; });
= 6
```


### Filter
[filter()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)
excludes from the returned array those elements for which the predicate is false.
Even numbers can be filtered out by testing that the remainder when divided by 2
is not 0:

```javascript
> [ 1, 2, 3 ].filter(function (x) { return x % 2 !== 0 });
= [ 1, 3 ]
```

---

I hope that the above examples show the potential uses
of these methods and how they can help to achieve clean and concise code.

Be sure to check the full documentation for the above methods on the
[Mozilla Developer Network JavaScript reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array).

If you like the look of these methods, then you can also take a look at the
[lodash](https://lodash.com/) library.
