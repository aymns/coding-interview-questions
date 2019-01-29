---
layout: post
title:  "The Knapsack"
date:   2018-11-20 03:39:03 +0300
categories: [interviews-questions, dynamic-programming]
---

> The knapsack problem is as follows:
 given a set of integers S = {s1, s2, ..., sn}, and a given target number T, find a subset of S that adds up exactly to T.
> For example, within S = {1, 2, 5, 9, 10} there is a subset that adds up to T = 22 but not T = 23. 
> * Give a correct programming algorithm for knapsack that runs in O(nT) time

~~~

using System;

class MainClass
{
    public static void Main(string[] args)
    {
        var data = new[] { 5, 1, 2, 9, 10 };
        var number = 22;
        var result = IsSubsetSum(data, data.Length, number);

        Console.WriteLine($"Is there subset in 5,1,2,9,10 adds up to 22 ? {result}");
    }

    private static bool IsSubsetSum(int[] set, int n, int sum)
    {
        // Base Cases 
        if (sum == 0)
        {
            return true;
        }

        if (n == 0 && sum != 0)
        {
            return false;
        }

        if (set[n - 1] > sum)
        {
            return IsSubsetSum(set, n - 1, sum);
        }

        return IsSubsetSum(set, n - 1, sum) ||
            IsSubsetSum(set, n - 1, sum - set[n - 1]);
    }
}

~~~

Try this code here : [https://repl.it/@aymns/The-Knapsack](https://repl.it/@aymns/The-Knapsack){:target="_blank"}