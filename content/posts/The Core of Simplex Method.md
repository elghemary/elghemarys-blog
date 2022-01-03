---
title: The Core of Simplex Method
subtitle: The Geometrical Intuition Behind the Algorithm
category:
  - About Awake
author: El Ghemary Farah
date: 2021-12-22T19:24:59.781Z
featureImage: /uploads/1.jpg
---
Throughout my personal experience, the first interaction with operations research was great, but it didn't last as soon as we learned about the simplex method. I used to do the long and complex computations, but I could never tell why I'm doing them.

The simplex method comes in as an answer for the limitation of the graphical method. Instead of solving Linear programs of 2 variables, now we are able to solve LPs of n variables, and we'll discuss later in this article the geometrical intuition behind it, and the mathematical interpretation of each iteration.

but before going any further, what is a simplex ? let's take a look to the Wikipedia definition :

> a simplex is a generalization of the notion of triangle or tetrahedron. The simplex is so-named because it represents the simplest possible polytope in any given space.
you might ask why is it important ? what it has to do with the arbitrary calculations in the algorithm ? well keep this definition in mind, it will make sense at the end of this article.

**Optimization Jargon**

it is important to have some knowledge of the basic technical terms of the field :

*Convex Set :*

*Feasible Solution :* the solutions satisfying all the constraints (infinite number)

*infeasible solution :*

*Optimal Solution :* the best feasible solution

*Extreme Point :* the vertex / corner of the feasible solution

**Example of an LP**

$$ latex$$

**the standard form of the LP**

to standardize an LP there are two requirements :

* All the constraints are equations with non-negative right hand side
* all the variables are non negative

converting (=<) inequalities into equations : we add a non negative slack variable to the left hand side, which represents the unused amount of resources

converting (>=) inequalities into equations : we substrate a non negative surplus variable, which represents how much we exceeds the limits.

Example

**The graph**

$$ image

The fundamental idea of the simplex algorithm is to improve the solution at each iteration, by moving from vertex to vertex until finding the optimum solution

but why does this work ?

**Properties**

1. The solution set of linear program is a convex set
2. The fundamental theorem of linear programming

   every feasible linear program that is bounded below has an optimal solution in a vertex of the feasible polytope
3. if the objective function, doesn't take the optimum value in a vertex, then there is an edge starting at it, along which the value of the function grows.

![](https://upload.wikimedia.org/wikipedia/commons/d/d4/Simplex-method-3-dimensions.png)

**An** **Overview of the Algorithm**

1. Choose the initial vertex
2. Check the neighboring vertices, if the nearest vertex increases the objective function move to it
3. keep moving from vertex to vertex
4. if all the neighboring vertices decreases z or do not change it at all, then the algorithm stops
5. This vertex is the optimal solution

\# animation of the algorithm

Let's Apply this to the previous example of our LP

1. Let's choose the origin as the initial vertex

   x_1 = x2 = 0=> x_3 = 3, x_4 = 5, z = 0
2. Choose a neighbor :

   from the graph we can see the moving from the origin to the vertex in x2 will increase our objective function faster than the vertex in x_1

   so we choose x_1 as the basic
3. Choose the one that gets to zero first

   If we increases x_2 then x_4 decreases to

   so x_4 is the non-basic
4. (0,5) is our current vertex:

   x_3 = 3-x_1 = 3

   x_4 = 5 - x_1 - x_2 = 5-0-5 = 0

   Z = 10
5. Choose a neighbor:

   whatever vertex we choose from the neighbors, our f decreases, so that means the algorithm stops and (0,5) is our solution

Pretty simple isn't it ? but you might think okay that's great but I'm still confused on how this is related to the tedious calculations of the method ?

First of all let's clear something about the difference between The tableau method and the algebraic form of the algorithm, well surprisingly It is the same thing, same algorithm and same calculations, even if it seems like two totally different methods. The Tableau method is in fact just a condensed form of the algebraic method.

In the rest of this article I'll cover the algebraic method, as it's more important and carry out the mathematical interpretation of the calculations. this part a solid understanding of linear algebra and especially the geometrical intuition behind it's concept. I highly recommend "The Essence of Algebra" playlist of the famous you-tuber 3b1b.

**The algebraic simplex method**

Our LP consists of two parts

1. the objective function
2. our constraints that makes a linear system

We can think of this linear system geometrically as a matrix A transforming a vector x to a vector b,

each columns of the matrix A tells us where the vectors of the basis lands in the output

A is a non square, 2x4 matrix which means A is a transformation from a higher dimension to a lower one.

We know that the output is some linear combination of the columns of the matrix,

along with with x1, x2 >0 , sum .. it is a convex combination

So we are asked to find the convex combination of the columns of A that equals to b ( which geometrically is a convex set ) and satisfy our objective function !

Let's back to our linear system in matrix form, to solve it A should be invertible e.g detA != 0 then x = A^-1.b

If you pay enough attention you'll observe that this is impossible, A is a non suquare matrix, and the det is defined for square matrices only. Geometrically this intuition is impossible, as we said before A is transformation of 4D space to 2D space, the invertible transformation ...

the mathematical procedure is to calculate nCn base ..

The way I like to think about this is since the invertible transformation to a higher dimension is impossible, and the output vector is 2D, we'll look for a matrix that transform a 2d vector to our b vector by dividing our matrix A to a smaller square matrix supposed to be the new basis,

we'll end up with 6 matrices

At the end of this process we end up with a number of vectors less or equal to nCn

Let's back to our initial goal : optimize our objective function, so this results are all solutions to our LP, but we are looking for the optimum one, for this reason e introduce the reduced coast function, which calculate the possible amount that the objective function can be improved, then it is logical that whenever this function is negative that means that there is no way to improve this function, we find the basic optimal solution

now do u remember the Wikipedia definition of a simplex that I mentioned before, the simplex method consists to fix a basis vectors, that are a convex combination and makes a convex polygon,

looking if the solution is a vertex of the vertex

if not we change one vector of the basis without affecting the other edges of the polygon

**Python Code**

Here is a python code that solve an LP problem using the simplex method


![](https://latex.codecogs.com/svg.latex?y%3Dx%5E2)

