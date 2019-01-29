---
layout: post
title:  "Shuffled Strings"
date:   2018-11-21 03:39:03 +0300
categories: [interviews-questions, dynamic-programming]
---

> Suppose you are given three strings of characters: X, Y , and Z, where |X| = n, |Y | = m, and |Z| = n + m.
Z is said to be a shuffle of X and Y iff Z can be formed by interleaving the characters from X and Y in a way that maintains the left-to-right ordering of the characters from each string.
>
> 1. Show that cchocohilaptes is a shuffle of chocolate and chips, but chocochilatspe is not.
 2. Give an efficient dynamic-programming algorithm that determines whether Z is a shuffle of X and Y.
>
> Hint: The values of the dynamic programming matrix you construct should be Boolean, not numeric.

~~~
using System;

class MainClass
{
    public static void Main(string[] args)
    {
        string shuffled = "cchocohilaptes";
        string first = "chocolate";
        string second = "chips";
        Console.WriteLine(
            $"{shuffled} is shuffle of {first} + {second} ? {IsShuffle(first, second, shuffled)}"
            );
    }

    public static bool IsShuffle(string first, string second, string shuffled)
    {
        var x = first.Length;
        var y = second.Length;
        var z = shuffled.Length;

        if (z != x + y)
        {
            return false;
        }

        var table = new bool[x, y];
        table[0, 0] = true;

        for (var i = 1; i < x; i++)
        {
            table[i, 0] = table[i - 1, 0] && shuffled[i - 1] == first[i - 1];
        }

        for (var j = 1; j < y; j++)
        {
            table[0, j] = table[0, j - 1] && shuffled[j - 1] == second[j - 1];
        }

        for (var i = 1; i < x; i++)
        {
            for (var j = 1; j < y; j++)
            {
                table[i, j] = 
                        shuffled[i + j - 1] == first[i - 1] && 
                        table[i - 1, j] || shuffled[i + j - 1] == second[j - 1] && 
                        table[i, j - 1];
            }
        }

        return table[x - 1, y - 1];
    }

}



~~~

Try this code here : [https://repl.it/@aymns/Shuffled-Strings](https://repl.it/@aymns/Shuffled-Strings){:target="_blank"}