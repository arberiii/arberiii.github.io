---
layout: post
title:  "Cosets and Hall's marriage theorem"
date:   2020-03-02 23:29:54 +0100
categories: math
---
Recently I had homework in Algebra class which I was fond of. I'm sure that there is a pure Algebraic solution to this problem, but I am going to present the solution using a famous theorem in graph theory, [Hall's marriage theorem](https://en.wikipedia.org/wiki/Hall%27s_marriage_theorem#Graph_theoretic_formulation).
Without prolonging it, here is the problem:

**Problem:** Let G be a finite group and let H<G(H is a subgroup of G). Show that there is a subset T of G which is simultaneously a left transversal for H and a right transversal for H.


**Solution** Let L be the set of left cosets of H and R set of right cosets of H, both of size \|H\|. Now define the bipartite graph with vertex set L+R with two vertices being adjacent if and only if sets have some element in common.

Suppose there is subset S of L such that \|N(S)\| < \|S\| (we are supposing that Hall's assumption does not hold). Because all element of N(S) and S are different (intersection of cosets are either the whole set or empty) then \|union N(S)\| = \|H\| \|N(S)\| and \|union S\| = \|H\| \|S\| this implies that \|union N(S)\| < \|union S\| but this is not true because each element of union S is covered by some coset in N(S) so \|S\| <= \|N(S)\| for each S subset of L.

Now from Hall's Marriage Theorem, there is a perfect matching. So we form the set T in this way:
Add exactly one element from the intersection of cosets in each edge of the matching. And the result follows.
