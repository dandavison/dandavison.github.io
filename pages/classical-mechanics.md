Title: Classical Mechanics by John R. Taylor
Slug: taylor-classical-mechanics
Date: 2016-05-29


My notes on [Classical Mechanics](http://www.amazon.com/Classical-Mechanics-John-R-Taylor/dp/189138922X) by John R. Taylor.


# Chapter 1 - Newton's Laws of Motion


### The second law as a differential equation
A key point seems to be: view Newton's second law $F = ma$ as a differential equation<sup>1</sup>:

$$m \ddot r = F$$

I'm understanding this as follows: You know what forces are acting on the body in question. You want to know how the position of the body will evolve through time: $r(t)$. This is a function satisfying the following differential equation: the second derivative with respect to time of $r(t)$, times $m$, is equal to the net force acting on the body.

In practice: in a typical problem you have some expression for $F$ derived from consideration of a diagram showing forces acting on the body. You might be able to discover $r(t)$ by finding a function whose second derivative is $F$.


### Conservation of momentum

Momentum is $p = m\dot r$, so another way of stating the second law is: rate of change of momentum is equal to force. In a multi-particle system the forces-and-reaction-forces of the third law cancel each other out when summing the rate of change of momentum of the whole system. So, total momentum doesn't change due to internal forces (but it does if there are external forces).

pp 21-23 show that conservation of momentum does not hold when considering magnetic and electrostatic forces between charged particles moving close to the speed of light. However I am unfamiliar with those forces and with the "right-hand rule" for fields/forces and I haven't tried to understand this section.

----------------------------------------------------------------------------

<sup>1</sup>The dot means "differentiated with respect to time". So if $r$ is position as a function of time then $\dot r$ is velocity and $\ddot r$ is acceleration.
