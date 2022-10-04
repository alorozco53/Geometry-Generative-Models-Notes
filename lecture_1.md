---
title: Lecture 1
tags: comp760, geometry, generative models
---

# [COMP 760: [[Geometry and Generative Models]]](https://joeybose.github.io/Blog/GenCourse)

_[[Joey Bose]]_ and _[[Prakash Panangaden]]_

![hyperflow](https://joeybose.github.io/assets/my_assets/HyperFlow_15min/hyperflow_animation_large.gif)

## Lecture 1

https://github.com/joeybose/comp760_lecturenotes/blob/master/Week_1__Geometry_Primer_Part_I.pdf

## Prerequisite Readings

- [Automatic Differentiation Variational Inference]()
- []()

### [[Metric Spaces]]

- _Metric spaces_ axiomatize measurement

> **Definition**
    _(PSEUDO)METRIC_
    A (pseudo)metric space is a set $X$ with a function $d: X \times X \to \mathbb{R}^{\geq 0}$, such that
    1. $\forall x$, $d(x,x) \geq 0$
    2. $\forall x,y$, $d(x,y) = d(y,x)$ (symmetry)
    3. $\forall x,y,z$, $d(x,y) \leq d(x,z) + d(z,y)$ (triangle inequality)

Extra property:
    4. $\forall x, y$, $d(x,y) = 0$ iff $x=y$
    
1, 2, 3 $\to$ pseudometric
4, 2, 3 $\to$ metric

> **METRIC EXAMPLES**
    1. $\mathbb{R}^n$ with Euclidean distance
    2. $\Sigma = \{a,b\}$; consider $\Sigma^*$; $d(x,y) = 2^{-n}$
    3. $L'(\mathbb{R})$; $d(f,g) = \int_{-\infty}^{+\infty} |f-g| dx$ (pseudometric)

> **Definition**
    _CONVERGENCE_
    Let $(X, d)$ be a metric space.
    A _sequence_ is an $n$-indexed family of elements from $X = {x_n}$.
    A sequence _converges_ to $x$, ${x_n} \to x$, if 
    $\forall \epsilon \geq 0$,  $\exists N \in \mathbb{N}$ s.t. $\forall n \geq N$, $d(x_n, x) \leq \epsilon$.

> **Definition**
    _Cauchy_
    A sequence is said to be _Cauchy_ if $\forall \epsilon > 0$,
    $\exists N$, $\forall n,m \geq N$ we have $d(x_n, x_m) < \epsilon$.
    
> **Definition**
    A metric space where every Cauchy sequence converges is called a _complete_ metric space.
    
![](https://i.imgur.com/GqZm1Og.png)

**FACT** Every space can be "completed" by adding something and be made into a complete metric space.

- Continuity

$$
f: (X, d) \to (Y, d')
$$

> **Definition**
    $f$ is said to be _continuous_ at $x_0$
    if $\forall \epsilon > 0$, $\exists \delta > 0$ such that
    $\forall x \in X$, if $d(x, x_0) < \delta$ then $d'(f(x), f(x_0)) < \epsilon$.

> **Definition**
    $f: X \to Y$ is _non-expansive_ on Lipschitz-1 if
    $\forall x, y$: $d'(f(x),f(y)) \leq d(x,y)$.

```flow
f=>operation: f
e=>operation: _
g=>operation: _

e->f->g
```

> **Proposition**
    Every non-expansive function is continuous.
    
> **Definition**
    $f$ is _contractive_ if $\exists x \in (0, 1)$ such that
    $\forall x, y$: $d(f(x), f(y)) \leq c \cdot d(x, y)$.
    
> **Theorem** (_Banach_)
    If $X$ is a _complete_ metric space and $f: X \to X$ is _contractive_, then
    there is a unique point $x_0 \in X$ such that $f(x_0) = x_0$.
    This $x_0$ is called a _fixed point_ of $f$.
    
    
### [[Topology]]

> **Definition**
    An _open ball_ $B(x) = \{y \mid d(x,y) \leq \pi\}$,
    where $x \in X$ and $\pi \in \mathbb{R}^{>0}$.
    
> **Definition**
    An _open set_ $A \subseteq X$ is one such that
    $\forall a \in A$, $\exists$...
    
> **Propositions**
    - An arbitrary union of open sets is open
    - A finite intersection of open sets is open

- A _closed_ set is the complement of an open set

![](https://uploads-ssl.webflow.com/5b1d427ae0c922e912eda447/5b4393fb1f0cd4809a8a6f08_sierp.jpg)

**EXERCISE**: Come up with a plausible explanation of the name "closed".

> **Definition**
    A function $f: X \to Y$ is _continuous_ if the inverse image of an open
    set is open: $O \subseteq Y$ open,
    $f^{-1}(O) = \{x \mid f(x) \in O\}$
    
**EXERCISE**: Show that this definition is equivalent to the former mentioned.

> **Definition**
    A _topological space_ $X$ is a set equipped with a family of subsets of $X$ satisfying:
    1. $X \in \mathcal{J}$, $\emptyset \in \mathcal{J}$
    2. if $\{U_\alpha\}$ is an arbitrary family of open sets, then $\bigcup_{\alpha \in \mathcal{A}} U_\alpha$ is open
    3. A finite intersection of open sets is open
    $\mathcal{J}$ is called a _topology_ of $X$
    
> **Definition**
    CO{COUNTABLE|FINITE} TOPOLOGY on $\mathbb{R}$, $cF$:
    1. $\emptyset \in cF$ $\mathbb{R} \in cF$
    2. if the complement of $A$ is {finite|countable} then $A \in cF$
    (In this space every sequence converges to every point.)

> **Proposition**
    If a sequence in a metric space converges, it converges to a unique point.
    
- Properties of Topological Spaces

> **SEPARATION PROPERTIES**
    _How well can you see?_
    
![](https://upload.wikimedia.org/wikipedia/commons/thumb/1/19/Hausdorff_regular_normal_space_diagram.png/330px-Hausdorff_regular_normal_space_diagram.png)
    
> **Theorem** (Urysohn)
    In a normal space $X$, $\forall C,D \subseteq X$ closed,
    $\exists$ a continuous real valued function $f: X \to \mathbb{R}$ such that
    $\forall x \in C$, $f(x) = 0$ and $\forall y \in D$: $f(y) = 1$.


- **Compactness**:  Taming the infinite

> **Definition**
    An _open_ _cover_ of a topological space $X$ is a family of open
    sets $\{U_\alpha\}_{\alpha \in A}$ such that
    $\bigcup\{U_\alpha\} = X$.
    
- A _subcover_ of a cover $\{U_\alpha\}_{\alpha \in A}$ is a family $B$ that also covers $X$
 

> **Proposition**
    _A compact metric space is bounded._
    > **PROOF**
        Consider $X = {x_0}$, $U_n := \{x \mid d(x, x_0) < n\}$,
        then $\bigcup_{n \in N} U_ n = X$;
        $U_n$ is a cover so there is a finite subcover $\{U_{n_1}, U_{n_2}, \ldots U_{n_k}\}$
        which proves that $U_n$ is bounded. $\blacksquare$

### [[Smooth Manifolds]]