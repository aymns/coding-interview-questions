---
layout: post
title:  "Maximum Sum"
date:   2018-11-23 03:39:03 +0300
categories: [interviews-questions, dynamic-programming]
---

> You are given an array of n numbers, each of which may be positive, negative, or zero. Give an efficient algorithm to identify the index positions i and j to the maximum sum of the ith through jth numbers.

~~~
using System;

class MainClass
{
    public static void Main(string[] args)
    {
        var result = FindMaxSubArrayIndex(new[] { 1, 2, -20, 10, 20, -15 });

        Console.WriteLine($"From index: {result[0]} to: {result[1]}");
    }

    private static int[] FindMaxSubArrayIndex(int[] array)
    {
        var totalMax = array[0];
        int start = 0, currentMax = 0, currentStart = 0, end = 0;

        for (var i = 0; i < array.Length; i++)
        {
            currentMax += array[i];

            if (currentMax < 0)
            {
                currentStart = i + 1;
                currentMax = 0;
            }
            else if (currentMax > totalMax)
            {
                end = i;
                start = currentStart;
                totalMax = currentMax;
            }
        }

        return new[] { start, end };
    }
}
~~~

Try this code here : [https://repl.it/@aymns/Maximum-Sum](https://repl.it/@aymns/Maximum-Sum){:target="_blank"}