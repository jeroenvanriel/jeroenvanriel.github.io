---
layout: post
title:  "Challenges in network-wide motion planning of autonomous vehicles"
date:   2026-05-04 14:08:00 +0200
categories: traffic
---

Suppose you can control every autonomous vehicle in a certain neighborhood of tightly interconnected intersections, maybe something like downtown Manhattan. Assume that every driver (or rather, *passenger* in this setting) has communicated their destination, then how would we have to guide all vehicles in order to optimize measures such as overall travel time and energy efficiency?

This post presents some of the work I did for my Master's thesis at Eindhoven University of Technology. The thesis itself is available [here](https://github.com/jeroenvanriel/traffic-scheduling/blob/master/report/thesis.pdf) and source code can be found on the [project page](https://github.com/jeroenvanriel/traffic-scheduling).

## Intro

Autonomous vehicle technology has seen rapid advancement, making such large-scale coordinated traffic control an increasingly relevant problem. There are many modeling facets to this problem, but this project focuses on simple grid-like networks of intersections, in which vehicles can only move in four cardinal directions. It is assumed that vehicles have predetermined routes. Furthermore, we assume that vehicles can be controlled with perfect precision, and that there is a centralized controller that can prescribe the exact trajectory of each vehicle. The main questions I tried to answer during my project were:

- In which order should vehicles cross intersections?
- How to control the speed of each vehicle?


## Motion planning

## Crossing order scheduling

