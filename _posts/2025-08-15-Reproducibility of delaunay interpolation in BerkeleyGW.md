---
layout: post
title: "Reproducibility of delaunay interpolation in BerkeleyGW"
date: 2025-08-18
tags: [BGW]
---
I have recently noticed something about delaunay interpolation when using BGW. The interpolation is used in two places, one of the head element of screened Coulomb kernel, the other one is interpolating between WFN_co and WFN_fi. 

Here I use 2D case to show the relevant issues. 

The Wiki definition of Delaunay triangulation is:
> In computational geometry, a Delaunay triangulation or Delone triangulation of a set of points in the plane subdivides their convex hull[1] into triangles whose circumcircles do not contain any of the points; that is, each circumcircle has its generating points on its circumference, but all other points in the set are outside of it. This maximizes the size of the smallest angle in any of the triangles, and tends to avoid sliver triangles.

In the case of retangular lattice, it's obvious that there are multiple solutions for an given point. This might not be an issue for isotropic systems, or a dense coarse grid. From BGW calculation point of view, sometimes increasing the density of coarse grid is not realistic due to limited cost. 

For some specific research questions, the nonuniqleness of finding simplex can be problematic. An easy getaround is to use the old interpolation scheme that finds nearest point (greedy_interpolation). 