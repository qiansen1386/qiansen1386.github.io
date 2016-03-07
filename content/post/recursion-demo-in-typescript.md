+++
date = "2016-03-07T10:41:06Z"
title = "Recursion-Demo in TypeScript & How it get better"
Categories = ["开发", "dev"]
Description = "I wrote this to practice of Typescript. Implement it using recursion for demonstration purpose."
Tags = ["开发", "Algorithm", "TypeScript"]
menu = "main"
linktitle="recursion demo in typescript n how it get better"
+++

I wrote this to practice of Typescript. Implement it using recursion for demonstration purpose.

<iframe width="100%" height="500" src="//jsfiddle.net/qiansen1386/yLdr5082/embedded/js,html,result/" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

Before I wrote this, I already know it is the dummiest solution. (BTW, this is a little challenge sent to me by one of my friend who is self-learning python, and recursion at the same time.) Basically, it waste both Ram and execution time. There is no human-intelligence involved so far, just pure brute-force method which straight away simulate the whole process and return its predicting result. Just it is not really a prediction, but just a simulation... After I observe the result, I laughed. What a dumb question, and I can't believe how silly I am, LOL.

Let put the result away first, and take a little bit time to look at the big O. Accoding to my code, The big O is about `log2(n-1)<O<=log2(N)`. Classic! Now, if you notice, the result is always the greatest `2^n` which does not exceed the **n**. we can change the algorithm to a simplier formula:

<iframe width="100%" height="500" src="//jsfiddle.net/qiansen1386/zvLu7re5/embedded/js,html,result/" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

What is the O? still the same, the performance improved though.
What is the ultmate solution:

<iframe width="100%" height="500" src="//jsfiddle.net/qiansen1386/cvasL16t/embedded/js,html,result/" allowfullscreen="allowfullscreen" frameborder="0"></iframe> 

That's it! How silly I am...