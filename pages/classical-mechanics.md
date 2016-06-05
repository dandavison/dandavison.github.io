Title: Classical Mechanics by John R. Taylor
Slug: taylor-classical-mechanics
Date: 2016-05-29


My notes on [Classical Mechanics](http://www.amazon.com/Classical-Mechanics-John-R-Taylor/dp/189138922X) by John R. Taylor.


$$
\newcommand{\vec}{\mathbf}
\newcommand{\ehat}{\vec{\hat e}}
\newcommand{\xhat}{\vec{\hat x}}
\newcommand{\yhat}{\vec{\hat y}}
\newcommand{\rhat}{\vec{\hat r}}
\newcommand{\phihat}{\vec{\hat \phi}}
\newcommand{\r}{\vec{r}}
\newcommand{\v}{\vec{v}}
\newcommand{\a}{\vec{a}}
\newcommand{\vector}[1]{\begin{bmatrix}#1\end{bmatrix}}
$$


# Chapter 1 - Newton's Laws of Motion


### Coordinate systems

This was the hard part of the first chapter for me. It's not that there's any
difficult math, just that I hadn't understood previously that unit vectors are
constant in Cartesian but not in other coordinate systems. Here's an attempt at
explaining.

-------------------------------------------------------------------------------

#### Basics

The basic object of interest is a moving particle. Its position at time $t$ is
$\r$. $\r$ is written in bold because it is a vector. A vector is something
that specifies a direction and a magnitude. Think of $\r$ as an arrow from the
origin pointing to the current position. Don't think of $\r$ yet as a column
vector containing numbers, because we haven't said what coordinate system
we're using. Regardless of what coordinate system we use, bold $\r$ is always
a vector pointing from the origin to the current position.

The particle is moving, i.e. the position changes over time. So instead of just
writing $\r$, we write $\r(t)$ which says that it's a function of time. Think
of that as giving the answer to a question: "At a given time $t$, what is the
position?". The answer (position) is a vector, so we can say that this is a
"vector-valued function" (i.e. whatever output it gives, it's always a vector).

Its velocity is a function $\v(t)$ whose value is also a vector (at time $t$
it's going at some speed in some direction). The velocity function $\v(t)$ is
the derivative with respect to time of the position function $\r(t)$. That
sounds very familiar, but what exactly is the derivative of a vector-valued
function?

In normal, non-vector, calculus we imagine some curve like $y = x^2$. So $y$ is
a function of $x$. The value of that function is not a vector; it's just a
number (a scalar). The derivative of the function with respect to $x$ is
saying: at a particular point along the x-axis, if I start advancing $x$ a tiny
bit, how fast is $y$ changing? So it's the slope of the curve at that point
(also just a number, not a vector).

In vector calculus, the derivative of $\r(t)$ with respect to $t$ is saying: at
some particular time $t$, if I start advance time a tiny bit, where is the
position going and how fast is it going there? So the derivative of a
vector-valued function is a vector -- an arrow with direction and magnitude
(speed).


#### Coordinate systems

Thinking of $\r(t)$ as an arrow with direction and magnitude is correct but a
bit abstract. How specifically do we use numbers to represent position? The
chapter covers two main coordinate systems. Let's say the particle is moving in
2D space for now.

- **Cartesian coordinates**: we write down how far the particle is in the
  x-direction ($x$), and how far it is in the y-direction ($y$).

- **Polar coordinates**: we write down how far the particle is ($r$) in the
  current direction to the particle.

Note that both coordinate systems involve recording how far it is in some
direction. The "in some direction" part corresponds to the concept of a *unit
vector*. A "unit vector" is basically a vector where the direction is of
interest, but the magnitude is just set to 1 for convenience.

Cartesian coordinates use two directions to specify the position. We'll write
these directions as the unit vectors $\xhat$ and $\yhat$. So in Cartesian
coordinates, the position is

$$\r(t) = x\xhat + y\yhat$$

(Go $x$ units in the $\xhat$ direction and $y$ units in the $\yhat$ direction.)

In contrast, polar coordinates just use one direction to specify the position:
the direction of a direct line to the particle's current position. This
direction is the unit vector $\rhat$. So in polar coordinates, the position is

$$\r(t) = r\rhat$$

(Go $r$ units in the $\rhat$ direction)
time" of a vector means, basically, you advance time an infinitesimally small
amount and look at how the position changed. The velocity is an arrow pointing
in the direction that the particle is moving and its length represents speed --
how far it got in that infinitesimally small amount of time.

The acceleration $\a(t)$ is the time derivative of velocity (second derivative
of position). Also a vector.

How do you calculate these derivatives if you have a mathematical expression
for the position?

Consider the harder case first: polar coordinates. This means that we give the
particle's position by saying how far away it currently is ($r$) and in what
direction ($\phi$). To write this as a vector, we define a unit vector
$\ehat_r$ of length 1 pointing in the particle's current direction, in which
case the position vector is $r$ times this unit vector:

$$\r(t) = r~\ehat_r.$$

Note that bold $\r$ is the position (a vector) whereas $r$ (a scalar) is its
distance from the origin, without any information about angle.

To get the velocity we differentiate this. Both the things multiplied together
are changing as $t$ changes: the distance $r$ changes because the particle is
moving, and the direction of the unit vector also changes because the particle
is moving. So two things multiplied together, neither of them constant; that
means "product rule" for differentiation:

$$\v(t) = r \frac{d \ehat_r}{dt} + \frac{dr}{dt}\ehat_r$$

The thing on the right is fine. The fact that we're "using polar coordinates"
means that we are happy dealing with $r$ or its derivative $\frac{dr}{dt}$. But
what is $\frac{d \ehat_r}{dt}$? That's the derivative of the unit vector.


I'd never studied polar coordinates and I was confronted with the fact that I was being mathematically naive/lazy previously when thinking about Cartesian coordinates.

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


### The second law as a differential equation

A key point seems to be: view Newton's second law $F = ma$ as a differential equation<sup>1</sup>:

$$m \ddot r = F$$

I'm understanding this as follows: You know what forces are acting on the body in question. You want to know how the position of the body will evolve through time: $r(t)$. This is a function satisfying the following differential equation: the second derivative with respect to time of $r(t)$, times $m$, is equal to the net force acting on the body.

In practice: in a typical problem you have some expression for $F$ derived from consideration of a diagram showing forces acting on the body. You might be able to discover $r(t)$ by finding a function whose second derivative is $F$.


### Conservation of momentum

Momentum is mass times velocity, $p = m\dot r$, so another way of stating the second law is: rate of change of momentum is equal to force. In a multi-particle system the forces-and-reaction-forces of the third law cancel each other out when summing the rate of change of momentum of the whole system. So, total momentum doesn't change due to internal forces (but it does if there are external forces).

pp 21-23 show that conservation of momentum does not hold when considering magnetic and electrostatic forces between charged particles moving close to the speed of light. However I am unfamiliar with those forces and with the "right-hand rule" for fields/forces and I haven't understood this section.


----------------------------------------------------------------------------

<sup>1</sup>The dot means "differentiated with respect to time". So if $r$ is position as a function of time then $\dot r$ is velocity and $\ddot r$ is acceleration.
