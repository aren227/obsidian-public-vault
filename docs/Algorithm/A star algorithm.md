---
title: A star algorithm
author: aren227
date: 2022-11-03T01:56:59+09:00
lastmod: 2022-11-14T01:19:12+09:00
tags:
- algorithm
- path-finding
---

A star (A*) pathfinding algorithm.

It works almost same with [[Dijkstra algorithm]], but with heuristic approach.
Distance to all unvisited nodes are calculated with $g(v) + h(v)$ where $g(v)$ is the actual cost from start to $v$, $h(v)$ is the estimated cost from v to end.

If $h(v)$ is always $0$, it does exact same thing with [[Dijkstra algorithm]].

In many path finding problems, we can get spatial information. A* algorithm uses this information as $h(v)$ to make searching faster.