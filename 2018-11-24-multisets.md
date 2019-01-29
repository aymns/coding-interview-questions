---
layout: post
title:  "Multisets"
date:   2018-11-24 03:39:03 +0300
categories: [interviews-questions, dynamic-programming]
---

> Multisets are allowed to have repeated elements. A multiset of n items may thus have fewer than n! distinct permutations.
>
> For example, {1, 1, 2, 2} has only six different permutations: {1, 1, 2, 2}, {1, 2, 1, 2}, {1, 2, 2, 1}, {2, 1, 1, 2}, {2, 1, 2, 1}, and {2, 2, 1, 1}.
>
> Design and implement an efficient algorithm for constructing all permutations of a multiset.

~~~

using System;
using System.Collections.Generic;

class MainClass
{
    public static void Main(string[] args)
    {
        var result = new List<int[]>();
        Permutation(new[] { 1, 2, 3, 4 }, new int[0], result);

        foreach (var res in result)
        {
            Console.WriteLine(string.Join(",", res));
        }
    }

    private static void Permutation(int[] input, int[] permutationPocket, List<int[]> result)
    {
        if (input.Length == 0)
        {
            // Permutation completed and ready to be pushed to the result
            result.Add(permutationPocket);
        }
        else
        {
            for (var i = 0; i < input.Length; i++)
            {
                // extendedPermutationPocket is the current permutationPocket + the i`th element of "input"
                var extendedPermutationPocket = new int[permutationPocket.Length + 1];
                permutationPocket.CopyTo(extendedPermutationPocket, 0);
                extendedPermutationPocket[permutationPocket.Length] = input[i];

                // newInput is the current "input" except the i`th element of current "input"
                var newInput = new int[input.Length - 1];
                Array.Copy(input, newInput, i);
                Array.Copy(input, i + 1, newInput, i, input.Length - 1 - i);

                // recursive permutation for the newInput and the extendedPermutationPocket
                Permutation(newInput, extendedPermutationPocket, result);
            }
        }
    }
}


~~~

Try this code here : [https://repl.it/@aymns/Multisets-Dynamic-programming](https://repl.it/@aymns/Multisets-Dynamic-programming){:target="_blank"}
