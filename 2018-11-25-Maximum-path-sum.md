---
layout: post
title:  "Project Euler 18: Maximum Sum from Top to Bottom of the Triangle"
date:   2018-11-25 03:39:03 +0300
categories: [interviews-questions, dynamic-programming]
---

>   By starting at the top of the triangle below and moving to adjacent numbers on the row below, the maximum total from top to bottom is 23.
>   
> <p style="text-align: center;"><strong><span style="color: #ff6600;">3</span><br>
> </strong> <strong><span style="color: #ff6600;">7</span> 4<br>
> 2 </strong><strong><span style="color: #ff6600;">4</span> 6<br>
> 8 5 </strong><strong><span style="color: #ff6600;">9</span> 3</strong></p>
>   
>   That is, 3 + 7 + 4 + 9 = 23.
>   
>   Find the maximum total from top to bottom of the triangle below:
>   
>
>  <p style="text-align:center"><strong>75<br>
>  95 64<br>
>  17 47 82<br>
>  18 35 87 10<br>
>  20 04 82 47 65<br>
>  19 01 23 75 03 34<br>
>  88 02 77 73 07 63 67<br>
>  99 65 04 28 06 16 70 92<br>
>  41 41 26 56 83 40 80 70 33<br>
>  41 48 72 33 47 32 37 16 94 29<br>
>  53 71 44 65 25 43 91 52 97 51 14<br>
>  70 11 33 28 77 73 17 78 39 68 17 57<br>
>  91 71 52 38 17 14 91 43 58 50 27 29 48<br>
>  63 66 04 68 89 53 67 30 73 16 69 87 40 31<br>
>  04 62 98 27 23 09 70 98 73 93 38 53 60 04 23</strong></p>
>   
>   NOTE: As there are only 16384 routes, it is possible to solve this problem by trying every route. However, Problem 67, is the same challenge with a triangle containing >  one-hundred rows; it cannot be solved by brute force, and requires a clever method! ;o)


```
using System;

class MainClass
{
    public static void Main(string[] args)
    {
        var array = new[]
        {
            new[] { 75 },
            new[] { 95, 64 },
            new[] { 17, 47, 82 },
            new[] { 18, 35, 87, 10 },
            new[] { 20, 4, 82, 47, 65 },
            new[] { 19, 1, 23, 75, 3, 34 },
            new[] { 88, 2, 77, 73, 7, 63, 67 },
            new[] { 99, 65, 4, 28, 6, 16, 70, 92 },
            new[] { 41, 41, 26, 56, 83, 40, 80, 70, 33 },
            new[] { 41, 48, 72, 33, 47, 32, 37, 16, 94, 29 },
            new[] { 53, 71, 44, 65, 25, 43, 91, 52, 97, 51, 14 },
            new[] { 70, 11, 33, 28, 77, 73, 17, 78, 39, 68, 17, 57 },
            new[] { 91, 71, 52, 38, 17, 14, 91, 43, 58, 50, 27, 29, 48 },
            new[] { 63, 66, 4, 68, 89, 53, 67, 30, 73, 16, 69, 87, 40, 31 },
            new[] { 4, 62, 98, 27, 23, 9, 70, 98, 73, 93, 38, 53, 60, 4, 23 }
        };

        var result = MaxPathSum(array);
        Console.WriteLine($"{result}");
    }

    private static int MaxPathSum(int[][] array)
    {
        for (var i = array.Length - 2; i >= 0; i--)
        for (var j = 0; j <= i; j++)
        {
            array[i][j] += Math.Max(array[i + 1][j], array[i + 1][j + 1]);
        }

        return array[0][0];
    }
}

```

Try this code here : [https://repl.it/@aymns/Maximum-path-sum](https://repl.it/@aymns/Maximum-path-sum){:target="_blank"}
