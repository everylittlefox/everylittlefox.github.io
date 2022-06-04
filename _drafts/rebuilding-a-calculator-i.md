---
layout: post
title: rebuilding a calculator i
date: 2022-06-01 19:46 +0100
categories: programming
---

I’m reading Practical Object Oriented Design (POOD), a book by Sandi Metz—if you don’t know her, look her up right now!— and I (think) I am learning a lot, meeting things I was unfamiliar with in the past, and most importantly, seeing the problems I’ve had solved in a more elegant fashion. In order not to get buried under tons of new stuff, I came up with an idea: I would take any project I’d seen to completion—not a lot to choose from if I’m being honest—and redo it with all this new knowledge.
The project I chose is a calculator app I built a couple of years ago. The reason I chose it, apart from it being among the very few I can still reason about completely, is the memory of the difficulty I faced when I tried to add history and support for trigonometric functions, a few months after I had “released” the app. Classic bad code. Even if the definition of what exactly constitutes good code is debatable (and relative?), code that is resistant to change is bad.
I decided I was going to start from scratch, relying on only the fragments of the implementation details of the app I still remember—not as a foundation to improve upon but as a reminder of how _not_ to do things. (Yeahh, I remember it being that bad.)

## starting out

I knew what I wanted, but I didn’t know how to go about making the fuzzy, disjoint ideas in my mind into something concrete. As I had only covered the first three chapters of the book, I knew whatever I wrote now would be rewritten in the future, but that was by design. Refactoring code forces me to think about what makes one piece of code better than another if they do the same thing.
JavaScript is the language I’m most comfortable in, so the language and framework to choose for this project was a no-brainer. For its familiarity and simplicity, I chose the web. I needed only two files:

- `index.html` : containing only the element—

```html
<div id="app"></div>
```

- `main.js`: where all my JavaScript code would go.

### created objects

To re-familiarize myself with DOM apis (and as a way of throwing myself into the deep end), I created a few objects.

#### `Component`

The `Component` class was skeletal at this point. Its constructor only took a `tagName` and a list of `children` as arguments:

{% highlight javascript %}
class Component {
constructor(tagName, children) {
this.element = document.createElement(tagName);
children.forEach((child) => this.element.appendChild(child));
}
}
{% endhighlight %}

Not much is going on here. In the constructor, an element is created with the provided `tagName` and stored in the `element` instance property of `Component`, then each child in the `children` list is made a direct descendant of `element`.
Remember: the goal of this project is the journey—refactoring, thinking hard about code I have written and code I will write, and making progressive improvements. If the above code snippet makes you want to scream and pull your hair, bear with me. It will get better, but if it doesn’t? Well, don’t hold back the feedback!

#### `Button`
