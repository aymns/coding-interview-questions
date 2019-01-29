---
layout: post
title:  "Coins change"
date:   2018-11-28 03:39:03 +0300
categories: [interviews-questions, dynamic-programming]
---


> In the United States, coins are minted with denominations of *1, 5, 10, 25, and 50 cents*. 
Now consider a country whose coins are minted with denominations of {d1, ..., dk} units. We want to count how many distinct ways C(n) there are to make change of n units.
For example, in a country whose denominations are {1, 6, 10}, 
C(5) = 1, 
C(6) to C(9) = 2, 
C(10) = 3, 
and C(12) = 4.
>
> * (a) How many ways are there to make change of 20 units from {1, 6, 10}? 
> * (b) Give an efficient algorithm to compute C(n), and analyze its complexity.



(Hint: think in terms of computing C(n, d), the number of ways to make change of n units with highest denomination d. Be careful to avoid overcounting.)

~~~~ 
using System;

class MainClass {
  public static void Main (string[] args) {
    	var n = 33;
    	var denominations = new[] { 1, 5, 10, 25 };
    	var result = Change(n, denominations);
    	Console.WriteLine(
            $"There is {result} ways to make change of {n} using denominations of {string.Join(",",denominations)}"
            );
  }

	private static int Change(int number, int[] coins)
	{
    	var cache = new int[number + 1];
    	cache[0] = 1;
    	foreach (var coin in coins)
    	{
        	for (var j = coin; j <= number; j++)
        	{
            	cache[j] += cache[j - coin];
        	}
    	}

    	return cache[number];
	}
}


~~~~ 

Try this code here : [https://repl.it/@aymns/Coins-Change](https://repl.it/@aymns/Coins-Change){:target="_blank"}