Title: Classical Mechanics by John R. Taylor
Slug: taylor-classical-mechanics
Date: 2016-05-29


My notes on [Classical Mechanics](http://www.amazon.com/Classical-Mechanics-John-R-Taylor/dp/189138922X) by John R. Taylor.


$$
\newcommand{\pos}{r}
\newcommand{\vector}[1]{\begin{bmatrix}#1\end{bmatrix}}
$$


# Chapter 1 - Newton's Laws of Motion


### The second law as a differential equation

A key point seems to be: view Newton's second law $F = ma$ as a differential equation<sup>1</sup>:

$$m \ddot r = F$$

I'm understanding this as follows: You know what forces are acting on the body in question. You want to know how the position of the body will evolve through time: $r(t)$. This is a function satisfying the following differential equation: the second derivative with respect to time of $r(t)$, times $m$, is equal to the net force acting on the body.

In practice: in a typical problem you have some expression for $F$ derived from consideration of a diagram showing forces acting on the body. You might be able to discover $r(t)$ by finding a function whose second derivative is $F$.


### Conservation of momentum

Momentum is mass times velocity, $p = m\dot r$, so another way of stating the second law is: rate of change of momentum is equal to force. In a multi-particle system the forces-and-reaction-forces of the third law cancel each other out when summing the rate of change of momentum of the whole system. So, total momentum doesn't change due to internal forces (but it does if there are external forces).

pp 21-23 show that conservation of momentum does not hold when considering magnetic and electrostatic forces between charged particles moving close to the speed of light. However I am unfamiliar with those forces and with the "right-hand rule" for fields/forces and I haven't understood this section.


### Coordinate systems

This is the hard part of the first chapter. I'd never studied polar coordinates and I was confronted with the fact that I was being mathematically naive/lazy previously when thinking about Cartesian coordinates.

The naive version says that the position function is vector-valued:

$$r(t) = \vector{r_x(t) \\ r_y(t) \\ r_z(t)},$$

and to get the velocity function you just differentiate the components of the position function:

$$\dot r(t) = \vector{\dot r_x(t) \\ \dot r_y(t) \\ \dot r_z(t)}.$$

That equation is correct, but unfortunately it turns out that you have to actually think about what's going on.

The position vector can be written as a sum over unit basis vectors (e.g. $\hat x$) multiplied by scalar coefficients (e.g. $r_x(t)$):

$$r(t) = r_x(t)\hat x + r_y(t)\hat y + r_z(t)\hat z.$$

Now, what's the analogous thing for (two-dimensional) polar coordinates? Instead of $x$ and $y$ we have angle $\phi$ and radius $r$. The position vector is

$$r(t) = \vector{\phi(t) \\ r(t)}.$$

How do we split that out as a sum of unit vectors?

Well, firstly, what are the unit vectors? They are vectors of unit length, and their direction is the direction you get by holding all other components fixed and allowing just one to increase. So
$\hat r$ is a unit vector pointing in the direction of the radius ($\phi$ held fixed). Then for $\hat \phi$, imagine holding the radius fixed and you start to increase the angle from whatever it is currently. You're going to travel round a circle, and the initial direction you go in is at a tangent. So that's what the unit vector $\hat \phi$ is: it's length 1, at right angles to $\hat r$.

The point is that those unit vectors change over time. We're considering position, velocity, acceleration as functions of time. In Cartesian coordinates, the unit vectors are constant: they always point in the same direction.


----------------------------------------------------------------------------

<sup>1</sup>The dot means "differentiated with respect to time". So if $r$ is position as a function of time then $\dot r$ is velocity and $\ddot r$ is acceleration.
