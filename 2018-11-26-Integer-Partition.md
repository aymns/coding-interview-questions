---
layout: post
title:  "Integer Partition"
date:   2018-11-26 03:39:03 +0300
categories: [interviews-questions, dynamic-programming]
---

> The integer partition takes a set of positive integers S = s1, ..., sn and asks if there is a subset I ∈ S such that I ∈ S
> 
> ![img](https://i.ibb.co/y61MKmJ/Qz-RNAf-R-1.png "img")  
> Let ![img](https://i.ibb.co/kGgDPtV/Au6glen-1.png "img")    
>   Give an O(nM) dynamic programming algorithm to solve the integer partition problem.

~~~

using System;

class MainClass
{
    public static void Main(string[] args)
    {
        Console.WriteLine(IntegerPartition(4));
    }

    private static int IntegerPartition(int number)
    {
        number = number + 1;

        var cache = new int[number, number];
        for (var i = 0; i < number; i++) cache[i, 0] = 1;

        for (var i = 1; i < number; i++)
        {
            for (var j = 1; j < number; j++)
            {
                if (i > j)
                {
                    cache[i, j] = cache[i - 1, j];
                }
                else
                {
                    cache[i, j] = cache[i - 1, j] + cache[i, j - i];
                }
            }
        }

        number = number - 1;
        return cache[number, number];
    }
}


~~~

Try this code here : [https://repl.it/@aymns/Integer-partition](https://repl.it/@aymns/Integer-partition){:target="_blank"}