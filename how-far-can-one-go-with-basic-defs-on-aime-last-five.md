---
author: OMI
pubDatetime: 2026-05-28T12:00:00.737Z
modDatetime: 2025-05-28T12:00:00.737Z
title: How Far Can One Go with the Basic Definitions of Binomial Coefficient on an AIME Last Five Problem
tags:
  - aime
  - combinatorics
  - number_theory
description: We will compare different solutions to 2026 AIME I, Problem 13, including those using advanced knowledge like finite fields, and those starting from the very elementary approaches. We will point out the connections behind them and share our thoughts from a pedagogical point of view.
---

(~10 min. read)

Last week, we posted [a short video](https://youtu.be/Ql6gESJ0OO0) on an elementary approach to [2026 AIME I, Problem 13](https://artofproblemsolving.com/wiki/index.php?title=2026_AIME_I_Problems/Problem_13#Problem). In this blog, we will discuss our motivation to create such a video, other approches to the problem, and our learnings on how we shall teach our students.

## Motivation

I want to start by a case I saw in an online community. One day, I was checking out posts and found one from a parent who posted her daughter’s scratch papers preparing AMC 8. The student learned the formula of the binomial coefficients from her classmate, and was practicing with problems made by AI. She wrote the following:

$$
\begin{align*}
\dbinom{7}{3} = \displaystyle \frac{7\cdot 6\cdot 5\cdot \cancel{4\cdot 3\cdot 2\cdot 1}}{3\cdot 2\cdot 1\cdot \cancel{4\cdot 3\cdot 2\cdot 1}}
\end{align*}
$$

Immediately after I saw the scratch paper, I knew something was off. I could not help to reply, based on the fact that she wrote the whole factorial product and crossed out the repetitions, she probably had not understood what the number of combinations are, and was just plugging numbers in the formula, which, was totally understandable because she just learned it from her classmate today.

The point here is that, for a $k$-combination of $n$ elements, we just need to write down the first $k$ terms of $n!$ (in descending order) in the numerator and $k!$ in the denominator. This is natural and can be remembered as we are counting the number of $k$-combinations by counting the $k$-permutations first, and then removing the duplicates. This is an image that I believe everyone should keep in mind after learning introductory level combinatorics. This is exactly how good textbooks illustrates this. For example, see the "Concept" section after Problem 4.5, AoPS, Introduction to Counting and Probability, on how they emphasize this.

So how is that connected to the AIME problem? Short answer: it naturally popped up during our lesson preparations. 

An important part of the preparation is to work on the problems in the students’ shoes and self-reflect on my solutions and the other solutions available online. It is valuable to share exactly how I felt and what I thought about, when I give myself pressure on solving this timely. And this fractional expression of the binomial coefficients just came up as part of my first instinctive approach to this AIME problem.

## Solutions and Comparisons

### Our Elementary Solution
Let's first recap our approach on our first try. For the details, please check out [the video](https://youtu.be/Ql6gESJ0OO0). If you have already watched the video, you can quickly read the next paragraph, and then jump to the [next subsection](#other-solutions-and-comparisons).

Let $n=10000$, $t=502$, $p=503$. When we see grouped sums of the binomial coefficients ${n \choose k}$, where $k$ runs over the group of all numbers that are $\equiv r \pmod t$. A natural way to evaluate such sums is to use the binomial theorem and evaluate $(1+x)^n$ over all roots of unity of degree $t$. This gives many nice closed formulas for small values of $t$, say here I would remind myself how to do it when $t=3$. But a similar approach only leaves us with a complex trigonometry sum for $t=502$. So we might need a different approach.

Note that the problem intentionally pointed out that $p=503$ is a prime, and we are looking at a divisibility problem modulo it. We start by trying to write each term in the sum of $S_0$ and see if we get anything out of it. This is where the fractional expression comes in. The observation is that, after we check the power of $p$ in ${n \choose t}$, we can check the power of $p$ in ${n \choose 2t}$ by only counting the powers in the $t=p-1$ newly introduced terms in both the denominator and the numerator. After checking a few terms, we are very tempted to guess that we can show $S_0$ is not a multiple of $p$ by showing all but one of the summation terms are multiples of $p$. Keep in mind that the problem is asking for the number of cases where $S_r$ is a multiple of $p$, so we also want to see if the construction above can create a case where all the summation terms in $S_r$ is a multiple of $p$.

We visualize it in the following way:

$$
\begin{array}{cc}
    \footnotesize n& \footnotesize (n-1) & \footnotesize\cdots & \footnotesize \textcolor{aqua}{jp} & \footnotesize\cdots & \footnotesize(n-p+1) & \footnotesize\cdots & \footnotesize\textcolor{aqua}{(j-1)p} & \footnotesize\cdots &  \footnotesize{(n-2p+1)} & \footnotesize\cdots\\ \hline
    \footnotesize 1& \footnotesize 2 & \footnotesize\cdots & \footnotesize(n-jp+1) & \footnotesize\cdots & \footnotesize\textcolor{red}{p} & \footnotesize\cdots & \footnotesize(n-(j-1)p+1) & \footnotesize\cdots & \footnotesize\textcolor{red}{2p} & \footnotesize\cdots
\end{array}
$$

So when we look at ${n \choose r}$, we are looking at the point which maps to $r$ on the lower axis and $n+1-r$ on the upper axis, and we are multiplying the numbers to the left (inclusive) of that point on both axes, to form the denominator and the numerator. When we look at the next term in the summand, namely ${n \choose {t+r}}$, we are moving $t$ units to the right and including $t$ new terms in the products in both the denominator and the numerator. We only care about the degree of $p$ in the products. So we visualize them on the axes as red and blue numbers (or red/blue dots as in the video).

The process of checking the summands in $S_r$ one by one is now visualized as scanning the axes from left to right, in steps of $t$ units. We know if we go in steps of $p$ units per step, we are guaranteed to include exactly one more red number and one more blue number. But we are moving $t=p-1$ units, so we are still “almost” guaranteed. We just need to figure out in which cases it fails.

To have all the summands divisible by $p$, we need to start from a position to the right of the first blue number, inclusive. If we start exactly from the first blue number, we will not be able to reach the second blue number in the next scan. But we will still scan through a red number on the lower axis, canceling the power of $p$ in the numerator and making ${n \choose {r+t}}$ not a multiple of $p$, unless we have an excess power of $p$ greater than 1 in the numerator from the start. But we won’t be in such a case because $p^2 > 250000 > 10000$. In other words, every red/blue number will add exactly one to the degree of $p$ in the products in the denominator and the numerator, respectively. We are looking for the setups where we start on the right side of a blue number, and scan through one additional blue number on each step.

But we want to stop here, because we have also seen in the "failed" case above that, we will have more than one terms ${n \choose {r+kt}}$ that are not divisible by $p$. This means we need to calculate the remainder of each term to have the remainder of the sum $S_r$.

We look at the "steps" in a different way. Moving $t$ units to the right is equivalent to moving $1$ unit to the left first, then moving $p$ units to the right. Now when we check ${n \choose {r+t}}$, we have

$$\displaystyle \dbinom{n}{r+t} = \dbinom{n}{r-1} \frac{(p \text{ consecutive terms})}{(p \text{ consecutive terms})} \equiv \dbinom{n}{r-1} \frac{1\cdots (p-1)}{1\cdots (p-1)} \frac{jp}{p} \pmod p$$

because any $p$ consecutive integers run over all the residues from $0$ to $p-1$. So under modulo $p$ the contribution from them are just from the terms divisible by $p$. We can do this for ${n \choose {r+kt}}$:

$$
\begin{align*}
  \dbinom{n}{r+kt} &= \dbinom{n}{r-k} \frac{(pk \text{ consecutive terms})}{(pk \text{ consecutive terms})} \\
  &\equiv \dbinom{n}{r-k} \frac{jp\cdot (j-1)p \cdots (j-k+1)p}{p\cdot 2p\cdots kp} \\
  &= \dbinom{n}{r-k} \dbinom{j}{k} \pmod p
\end{align*}
$$

We do need to check the corner cases where $r$ is very small or large, but overall we will have

$$
\begin{align*}
 \displaystyle S_r \equiv \sum_{k=0}^j \dbinom{n}{r-k} \dbinom{j}{k} = \dbinom{n+j}{r} \pmod p 
\end{align*}
$$

where the last equation came from the [Vandermonde's Identity](https://en.wikipedia.org/wiki/Vandermonde%27s_identity), which has a very nice double-counting proof, evaluating the number of ways to choose $r$ items from $n+j$ items by taking some from $n$ items first, then taking the rest from $j$ items.

The rest of the problem is just straightforward calculation by plugging in $n=10000$ and $j=\lfloor 10000/503 \rfloor=19$.

### Other Solutions and Comparisons

The clean, short solutions that use advanced ideas can be grouped into two types:

1. Taking care of $S_r$ as a whole with generating polynomials
2. Dealing with each term in $S_r$ individually (like our elementray approach)

For Type 1, we are essentially looking at $(1+x)^n$ over the finite field $\mathbb{F}_p$, and further reduce it by modulo $x^{p-1}-1$. Then claiming that $(1+x)^n$ equals $(1+x)^{462}$ under such equivalence relations. This can be formulated using Fermat's little Theorem. But we are still at risk of giving a hand-waving proof without rigorous abstract algebra.

For Type 2, we are using tools like [Lucas's Theorem](https://en.wikipedia.org/wiki/Lucas%27s_theorem) to reduce every summand to a smaller number, then investgating their sum. Our approach indeed gives an incomplete proof of the Lucas's Theorem, enough for this problem's purpose.

So, when we read the solutions and do our self-reflections, we first think about: how did we miss the path to Type 1?

The answer might be surprising: we touched it at the very first try, but let it go because we used a wrong way to isolate the terms of $S_r$. The complex roots of unity shall be replaced by the roots of unity modulo $p$, i.e., the roots of $x^{p-1}$ in $\mathbb{F}_p$. Because, the reason that we can isolate the terms of interest from evaluating $(1+x)^n$ at the roots of unity, is that the characteristic function can be produce in that way:
$$
\begin{align*}
\sum_{i=0}^{t-1} \zeta_t^{ki} = 
\begin{cases}
   t &\text{if } t|k \\
   0 &\text{otherwise} 
\end{cases}
\end{align*}
$$
Following this through, we are even able to find a rigorous proof of Type 1 without abstract algebra. We just need the characteristic function modulo $p$. That can be obtained via
$$
\begin{align*}
\sum_{i=0}^{p-1} i^{k} \equiv 
\begin{cases}
   p-1 &\text{if } p-1|k \\
   0 &\text{otherwise} 
\end{cases}
\pmod p
\end{align*}
$$
which, is not trivial (needs to be proved by using the primitive roots) but at least we forcibly fit it within the "common required knowledge of elementary number theory" of high school Olympiad. This makes the step of reducing $(1+x)^n$ to $(1+x)^{462}$ rigorous, by writing the (sum of) coefficients modulo $p$ into a closed formula, then use Fermat's little Theorem.

We also want to ask: are these two types of solutions related at a higher level? To see the connections, remind the generating function proofs of the key formulas used in Type 2 approaches. Starting with Lucas's Theorem, which comes from:
$$
\begin{align*}
(1+x)^n = \prod_i \left((1+x)^{p^i}\right) ^{n_i} \equiv \prod_i \left(1+x^{p^i}\right) ^{n_i} \pmod p 
\end{align*}
$$
which, in this problem, would be
$$
\begin{align*}
(1+x)^n \equiv (1+x^p) ^{19} (1+x)^{443} \pmod p 
\end{align*}
$$
Now the degree reduction happens when grouping the exponents modulo $p-1$, because all exponents $ap+b$ such that $ap+b\equiv r \pmod {p-1}$ will have to satisfy $a+b\equiv r \pmod {p-1}$. And that reduces the term $1+x^p$ above to $1+x$.

Finally, we want to see if there are additional observations other than the target of the problem. If we continue to chase our factor counting approach (more blue numbers than red numbers), we will easily see that for all $r$ with $p|S_r$, we actually have $p|{n \choose r+502m}$ for any $m$. This can also be verified by checking with Lucas's Theorem, where all terms becomes $0$ under the convention that ${n \choose k} = 0$ for $k>n$. For this fact, there is also another explanation with [Kummer's Theorem](https://en.wikipedia.org/wiki/Kummer%27s_theorem), which, under the simple case of this problem, states that the power of $p$ in ${n \choose k}$ is greater than $0$ if and only if there is a carry over when $k$ is added to $n-k$ in base $p$. Note that the numbers $r, r+p-1, \ldots, r+m(p-1)$ reduces the "ones" digit in base $p$ by 1 every time. For the carry to always happen, the extremal case would be that the last number $r+k(p-1)$ barely needs a carry when something is added to it to make $n$, i.e., the ones digit of $r+k(p-1)$ is $1$ plus the ones digit of $n$ in base $p$.

## From a Coach's Perspective

So far we have given an exhaustive discussion of different solutions to the problem. There are many take-aways from these approaches. To list a few:
- How to construct characteristic functions modulo a prime $p$
  - Or, even more general, discrete Fourier transformations over a ring.
- Tools for investigating binomial coefficients and divisibility modulo $p$
  - Lucas's Theorem
  - Kummer's Theorem
- Any knowledge/idea related to the proofs of the tools above
  - primitive roots
  - Legendre's formula for factorials (very basic idea yet useful)

This is how you want to think divergently when doing self-reflections on problems you practice on.

As coaches, we also need to think about which solutions are closer to the level of the targeted students of the contest, which is AIME in this case. Knowing and using advanced concepts, like finite fields, is becoming more and more popular in math competitions preparation and education nowadays. Still, thanks to the problem makers, there will still be a path to reach the result with elementary methods. So when we train the students, we want to train the ability to take the path within our control, under the constraints of time pressure and our own knowledge base. And that is the reason why we want to share our approach, because it requires only the definition of the binomial coefficients, plus a little bit of number theory instincts of analyzing the residue modulo a prime.