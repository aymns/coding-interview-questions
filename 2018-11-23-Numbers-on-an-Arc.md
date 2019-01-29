---
layout: post
title:  "Numbers on an Arc"
date:   2018-11-23 03:39:03 +0300
categories: [interviews-questions, dynamic-programming]
---

> Assume that there are n numbers (some possibly negative) on a circle, and we wish to find the maximum contiguous sum along an arc of the circle. Give an efficient algorithm for solving this problem.

~~~

using System;

class MainClass
{
    public static void Main(string[] args)
    {
        var n = new[] { 8, -1, -2, 4, -3, 9 };

        Console.WriteLine(MaxSumOnArc(n));
    }

	// Kadane algorithm https://en.wikipedia.org/wiki/Maximum_subarray_problem
    private static int Kadane(int[] array)
    {
        int max = 0, temp = 0;

        foreach (var value in array)
        {
            temp = temp + value;
            if (temp < 0)
                temp = 0;
            if (temp > max)
                max = temp;
        }

        return max;
    }

    private static int MaxSumOnArc(int[] a)
    {
        var n = a.Length;

        var maxKadane = Kadane(a);

        var maxWrap = 0;
        for (var i = 0; i < n; i++)
        {
            maxWrap += a[i];
            a[i] = -a[i];
        }

        maxWrap = maxWrap + Kadane(a);
        return maxWrap > maxKadane ? maxWrap : maxKadane;
    }
}

~~~

Try this code here : [https://repl.it/@aymns/Numbers-on-an-Arc](https://repl.it/@aymns/Numbers-on-an-Arc){:target="_blank"}