---
layout: default
title:  "understanding for a formula in theoretical mechanics"
date:   2021-10-04 14:05:39 +0800
categories: Physics
---

# Background

The concept of reference system(RS) and coordinate system(CS) is confusing in theoretical mechanics. Conceptually, they are like chalk and cheese. However, since we always connect a reference system with a coordinate system, some confusion may happen when we write our equations.

A very basic equation is 
$$
\frac{d \vec{A}}{dt} = \frac{\tilde{d}\vec{A}}{dt}+\omega\times\vec{A}
$$
which describes the relationship between what we call `absolute derivative` and `relative derivative`. What bothers me a lot is whether it is an equation about RS or CS?



# Wrong Comprehension

At first I think that, by definition, vector (or 1-order tensor) is a quantity that has don't vary with coordinate system, so do its derivative. So I suppose this equation to be used to describe the relationship of the components for a vector in two CS. Namely, I take the derivative of $$\vec{A}$$, then get its components in systme A and B, then two set of components will satisfy the equation.

But a problem comes, if a vector doesn't vary with time in one CS, it certainly remains constant in any another system. So both  absolute  and relative derivative equals zero, then we get $$0 = \omega\times\vec{A}$$, what's wrong?



# Conclusion

The problem above is that the changes of components come from two parts: the change of $$\vec{A}$$ and the change of CS itself. However when we are talking about **The change of a coordinate system**, we are actually talking about RS. So this equation actually connects two RS rather than two CS. 

In two different RS, the derivative of $$\vec{A}$$ are two vectors, we can choose in which CS we write their relationship.

The usage of this formula is just as those CS changing methods in mechanics.

