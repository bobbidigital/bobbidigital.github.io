---
layout: post
title: Refactoring Pet Peeves
comments: true
author: Jeff
---

Somewhere during my wild romps on the Internet I came across an [interesting article](http://raganwald.com/2013/10/08/defactoring.html) that talked about the concept of "defactoring".  I think we're all familiar with the idea of "refactoring", but defactoring goes against the many rules that have been engrained on us as technologists. I think that's why I love it so much.

>  Defactoring reduces the number of ways we can recombine the pieces of code we have...We’d make it less flexible.

In the technology sector we're often reading about the latest and greatest technology, architecture/software pattern and how you're basically a luddite if you don't adopt these practices. Proper factoring of code is probably one of the first times I experienced this phenomenon. I rushed to make sure all of my functions were small and tight. I mastered the art of taking a 30 line shell script and exploding it into 120 lines of well organized bliss.

The problem that I think "defactoring" tries to address is that of complexity for the sake of complexity and cool kid points. While I love a well organized code as much as the next guy, most of the reasons you would break apart aren't valid in a lot of the programs being written. (Especially on the Systems end of the house)

The biggest reasons to refactor code in my experience is:

* Reusability of code
* Testability of code
* Isolating complexity

If refactoring your code doesn't provide any of these benefits, then what's the real purpose of doing it? It's another logical break when you're reading the code that you have to jump to. Does it add any value?

Before you move that for loop to its own function, ask yourself "What does this buy me?" If you can't answer that question in 10 seconds or less, you probably don't need to do it. Yes, people might judge your code, but if it's not that, it'll be something else. (Engineers are a persnickety bunch) 

The world has enough complexity. Don't add to it without good reason.