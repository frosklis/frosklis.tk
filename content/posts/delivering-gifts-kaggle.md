---
draft: false
layout: post
title: Delivering gifts (Kaggle)
categories: ["Data science"]
tags: Kaggle, data science
date: 2016-01-08
---

There are a lot of things we take for granted. One of these things is logistics. We assume that when we have one order delivered it will arrive on time, but we often overlook how difficult it actually is. Well, there was a [Kaggle competition just about that][santa]. And they just made it harder.

The [travelling salesman problem] is perhaps the best known NP problem. Given a set of cities, the goal is to find the shortest route that goes through all the cities. The only way to assure a solution is optimal, in general, is actually trying all the possible solutions. But [Kaggle][kaggle] made it even harder. In the Kaggle problem Santa Claus has a lot of gifts (100,000) to give. Each give has a weight and a location to be sent to. The deers get tired because of the distance and the weight they carry. The sleight itself also has a weight and a load limit.

The idea is first to load the sleigh, then deliver the gifts, go back to the North Pole and repeat until all gifts are delivered. The second part is in itself an NP-hard problem, even harder than the TSP:

- The cost of going from A to B is not static

It depends on the distance from A to B and the weight of the sleigh plus the gifts... and the weight of the sleigh depends on the order of the previously visited cities.

Oh, and the first part - loading the sleigh - somehow resembles another NP-hard problem: [the knapsack problem][knapsack]

The best approach I could think of involves reconstructing the trip backwards:

1. Start from the North Pole, with an empty sleigh.
2. Choose the next city to visit and load the sleigh. If the sleigh is too loaded, it has to go back to the North Pole.
3. Repeat until all cities have been visited.

If that gives a solution that is O-A-B-O-C-D-O, the actual solution is that reversed (O-D-C-O-B-A-O): two trips, one with gifts AB and another with CD. I did it this way because doing that I can avoid taking the decision of what cities to visit in each trip in advance.

There is, however, one big caveat: there are 100,000 gifts. This means that operationally I cannot address the full problema at once. SO what I did was start with a logical solution: grouping gifts that are close. Once I have that I optimize de rout using ant colony optimization. And then more or less randomly satrt merging trips to see if I can find a better solution.

Currently, that method gets me a bad position in the contest but with 2% of the winner's solution. Still two days to go.


[kaggle]: https://www.kaggle.com "Kaggle"
[santa]: https://www.kaggle.com/c/santas-stolen-sleigh "Santa's stolen sleigh"
[tsp]: https://en.wikipedia.org/wiki/Travelling_salesman_problem "Travelling salesman problem"
[knapsack]: https://en.wikipedia.org/wiki/Knapsack_problem "Knapsack problem"

