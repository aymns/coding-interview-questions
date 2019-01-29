---
layout: post
title:  "Expressions"
date:   2018-12-04 03:39:03 +0300
categories: [interviews-questions, graphs]
---

>Suppose an arithmetic expression is given as a tree. Each leaf is an integer and each internal node is one of the standard arithmetical operations (+, −, ∗, /). For example, the expression 2 + 3 ∗ 4 + (3 ∗ 4)/5 is represented by the tree in the figure.
>
>
>Give an O(n) algorithm for evaluating such an expression, where there are n nodes in the tree.

<p style='text-align:center'>
<img src="https://i.ibb.co/27TMbjV/pasted-Image0-1.png" title="example">
</p>

~~~

using System;

class MainClass
{
    public static void Main(string[] args)
    {
        var arithmeticTree = new Tree("+")
        {
            Root =
            {
                Left = new TreeNode("/")
                {
                    Left = new TreeNode("*")
                    {
                        Left = new TreeNode("3"),
                        Right = new TreeNode("4")
                    },
                    Right = new TreeNode("5")
                },
                Right = new TreeNode("+")
                {
                    Left = new TreeNode("2"),
                    Right = new TreeNode("*")
                    {
                        Left = new TreeNode("3"),
                        Right = new TreeNode("4")
                    }
                }
            }
        };
        Console.WriteLine(arithmeticTree.GetValue());
    }

    private class Tree
    {
        public Tree(string root)
        {
            this.Root = new TreeNode(root);
        }

        public TreeNode Root { get; }

        public int GetValue()
        {
            return this.GetValue(this.Root);
        }

        private int GetValue(TreeNode node)
        {
            if (node.Left == null && node.Right == null)
            {
                try
                {
                    return int.Parse(node.Value);
                }
                catch (Exception)
                {
                    throw new ArgumentOutOfRangeException($"leaf node ({node.Value}) is not number");
                }
            }

            var a = this.GetValue(node.Left);
            var b = this.GetValue(node.Right);
            switch (node.Value)
            {
                case "+": return a + b;
                case "-": return a - b;
                case "/": return a / b;
                case "*": return a * b;
                default: throw new ArgumentOutOfRangeException($"non-leaf node ({node.Value}) is not an operator");
            }
        }
    }

    private class TreeNode
    {
        public TreeNode(string value)
        {
            this.Value = value;
        }

        public TreeNode Left { get; set; }
        public TreeNode Right { get; set; }

        public string Value { get; }
    }
}

~~~

Try this code here : [https://repl.it/@aymns/Expression](https://repl.it/@aymns/Expression){:target="_blank"}