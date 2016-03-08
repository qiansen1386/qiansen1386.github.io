+++
date = "2016-03-07T10:41:06Z"
title = "Recursion-Demo in TypeScript & How it get better"
Categories = ["开发", "dev"]
Tags = ["开发", "Algorithm", "TypeScript"]
menu = "main"
linktitle="recursion demo in typescript n how it get better"
+++

I wrote this to practice of TypeScript and also to demonstrate recursion to my friend. This is a little challenge sent to me by one of my friend who is self-learning python, and recursion at the same time. Basically is about to keep removing all the elements whichever index is odd from the array, till there is only one left, and return the index of the survivor. Input the **N** of elements and output the index **X**.

<iframe width="100%" height="500" src="//jsfiddle.net/qiansen1386/yLdr5082/embedded/js,html,result/" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

Before I wrote this, I already know it is the dummiest(also most reliable) solution. Basically, it waste both Ram and execution time. There is no human-intelligence involved so far, just pure brute-force method which straight away simulate the whole process and return its predicting result. Just it is not really a prediction, but just a simulation... After I observe the result, I laughed. What a dumb question, and I can't believe how silly I am, LOL.

Let put the result away first, and take a little bit time to look at the big O. Accoding to my code, The O is in the range `log2(n-1)<O<=log2(n)`. Classic! Now, if you notice, the result is always the greatest `2^n` which does not exceed the **n**. we can change the algorithm to a simplier formula:

<iframe width="100%" height="500" src="//jsfiddle.net/qiansen1386/zvLu7re5/embedded/js,html,result/" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

What is the O? Actually it's still almost the same, the performance and amount of code have improved though.
What is the ultmate solution, use one calculation, the ultmate O(1) solution:

<iframe width="100%" height="500" src="//jsfiddle.net/qiansen1386/cvasL16t/embedded/js,html,result/" allowfullscreen="allowfullscreen" frameborder="0"></iframe> 

That's it! How silly I am... But I am so happy about it.