Title: Classical Mechanics by John R. Taylor
Slug: taylor-classical-mechanics
Date: 2016-05-29


My notes on [Classical Mechanics](http://www.amazon.com/Classical-Mechanics-John-R-Taylor/dp/189138922X) by John R. Taylor.


$$
\newcommand{\xhat}{\vec{e_x}}
\newcommand{\yhat}{\vec{e_y}}
\newcommand{\rhat}{\vec{e_r}}
\newcommand{\phihat}{\vec{e_\phi}}
\newcommand{\r}{\vec{r}}
\newcommand{\v}{\vec{v}}
\newcommand{\p}{\vec{p}}
\newcommand{\a}{\vec{a}}
\newcommand{\F}{\vec{F}}
\newcommand{\vector}[1]{\begin{bmatrix}#1\end{bmatrix}}
$$


# Chapter 1 - Newton's Laws of Motion






#### Basics

The basic object of interest is a moving particle. Its position at time $t$ is
$\r$. It has that arrow over it because it is a vector. A vector is something
that specifies a direction and a magnitude. Think of $\r$ as an arrow from the
origin pointing to the current position. Don't think of $\r$ yet as a column
vector containing numbers, because we haven't said what coordinate system we're
using. Regardless of what coordinate system we use, $\r$ is always a vector
pointing from the origin to the current position.

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
number (a scalar). The derivative of that function with respect to $x$ is
saying: at a particular point along the x-axis, if I start advancing $x$ a tiny
bit, how fast is $y$ changing? So, it's the slope of the curve at that point
(also just a number, not a vector).

In vector calculus, the derivative of $\r(t)$ with respect to $t$ is saying: at
some particular time $t$, if I start advancing time a tiny bit, where is the
position going and how fast is it going there? So the derivative of a
vector-valued function is a vector -- an arrow with direction and magnitude
(speed).


#### Coordinate systems

Thinking of $\r(t)$ as an arrow with direction and magnitude is correct but a
bit abstract. How specifically do we use numbers to represent position? The
chapter covers two main coordinate systems. Let's say the particle is moving in
2D space for now.

- **Cartesian coordinates**: we write down how far the particle currently is in
  the x-direction, $x(t)$, and how far it currently is in the y-direction,
  $y(t)$.

- **Polar coordinates**: we write down how far the particle currently is,
  $r(t)$, in the current direction to the particle.

Note that $x(t)$, $y(t)$, and $r(t)$ were not written with arrows. They are
just numbers, saying how far the particle is *in some direction*. The "in some
direction" part corresponds to the concept of a *unit vector*. A "unit vector"
is basically a vector where the direction is of interest, but the magnitude is
just set to 1 for convenience.

Cartesian coordinates use two directions to specify the position. We'll write
these directions as the unit vectors $\xhat$ and $\yhat$. So in Cartesian
coordinates, the position is

<table style="width:100%">
  <tr>
    <td> $$\r(t) = x(t)\xhat + y(t)\yhat$$ </td>
    <td> $$\mathrm{Go~} x(t) \mathrm{~units~in~the~} \xhat \mathrm{~direction} \mathrm{~and~} y(t) \mathrm{~units~in~the~} \yhat \mathrm{~direction}$$ </td>
  </tr>
</table>

In contrast, polar coordinates just use one direction to specify the position:
the direction of a direct line to the particle's current position. This
direction is the unit vector $\rhat(t)$. So in polar
coordinates, the position is


<table style="width:100%">
  <tr>
    <td> $$\r(t) = r(t)\rhat(t)$$ </td>
    <td> $$\mathrm{Go~} r(t) \mathrm{~units~in~the~} \rhat(t) \mathrm{~direction}$$ </td>
  </tr>
</table>


Notice (and this is pretty important; it's basically the reason the chapter is
covering polar coordinates) that in polar coordinates the unit vector
$\rhat(t)$ is a function of time (its direction changes as the particle moves);
in contrast, in Cartesian coordinates, $\xhat$ and $\yhat$ are constant; they
always point in the same direction. The polar unit vector is a function of time
because it is the direction to wherever-the-particle-currently-is. The
Cartesian unit vectors are not functions of time because they are just the
x-axis direction and the y-axis direction and these do not change.

#### Velocity


We can now differentiate these position functions to get the velocity. Recall
that the answer is going to be a vector because it is the derivative of a
vector-valued function.

**Cartesian coordinates**

Because $\xhat$ and $\yhat$ are not functions of time, differentiating is
straightforward:

$$\v(t) = \frac{d}{dt}\bigg(x(t)\xhat + y(t)\yhat\bigg) = \frac{d x(t)}{dt}\xhat + \frac{d y(t)}{dt} \yhat$$

Physicists use a dot to represent derivative-with-respect-to-time. So they
might write this as

$$\v(t) =  \dot x(t) \xhat + \dot y(t) \yhat$$

Either way, what this is saying is that in Cartesian coordinates, the velocity
function is a vector comprised of current x-speed in the x-direction and
current y-speed in the y-direction. In other words, it's what you expect.

**Polar coordinates**

$$\v(t) = \frac{d}{dt}\bigg(r(t)\rhat(t)\bigg)$$

That's a product of two things that are both a function of time, so we use the
"product rule"[ref] The product rule is the thing when you studied
differentiation that says: when you're differentiating the product of two
functions you differentiate one and keep the other as-is, then you
differentiate the other while keeping the first as-is, and you add the two
things together: $\frac{d(f(t)g(t))}{dt} = \dot f(t) g(t) + f(t) \dot g(t)$
[/ref] to differentiate it:

$$\frac{d}{dt}\bigg(r(t)\rhat(t)\bigg) = \dot r(t) \rhat(t) + r(t)\frac{d \rhat(t)}{dt}$$

There's quite a few $r$s there and it's important at this stage not to get lost
in the symbols. We know that the answer (velocity) is a vector. That means we
can write it as a bunch of things added together, where each thing is a number
times some unit vector. And we're using polar coordinates, so the unit vectors
are going to be the polar unit vectors. So the thing on the left $\dot r(t)
\rhat(t)$ is fine: that's saying that the velocity has one component which is
the current radial speed (a number $\dot r(t)$) in the current radial direction
(the unit vector $\rhat(t)$).

What about the thing on the right? It's the current radial distance times the
current derivative of the unit vector function. We've said that in polar
coordinates the unit vector $\rhat(t)$ changes over time, so it does make sense
that we could ask what its derivative with respect to time is. So what is it?
The answer is that it's a vector-valued function whose current value always
points at right-angles to the current radial direction, but that requires
explaining:

Going back to the informal definition of derivatives above, we're at some point
$t$ in time, and we imagine starting to advance time a tiny bit, and we look at
the change in where the unit vector points, after this infinitesimally small
amount of time passes. A unit vector always has length 1, so it can't grow in
length. There's only one thing it can do: it can point in a slightly different
direction. What direction has it gone in? It's basically like the hand of a
clock. It's not too hard to see that if the hand of a clock changes just a tiny
bit, then the tip moves in a direction that's almost a tangent to the
circle. Change "tiny" to "infinitesimally small" and the "almost" goes away: so
the time derivative of the radial unit vector is a vector pointing at right
angles to the radial vector. This unit vector in that direction is called
$\phihat$, because it points in the direction that you go in when you increase
the angle $\phi$, as opposed to $\rhat$ which points in the direction you go in
if you increase the radius $r$. How fast does the radial unit vector move in
the $\phihat$ direction? The answer is that it moves at the speed that the
angle is increasing, so $\dot \phi$[ref]You can prove this by writing the unit
vector in Cartesian coordinates, $cos(\phi) \xhat + sin(\phi) \yhat$, and then
differentiating it to give $\dot \phi\big(-sin(\phi)\xhat +
cos(\phi)\yhat\big)$ which is $\dot \phi$ times a vector orthogonal to the
original one.[/ref]. In other words, the time derivative of the radial unit
vector is $\dot \phi(t) \phihat(t)$

The conclusion of all that is that in polar coordinates, the velocity vector is

$$\v(t) = \dot r(t) \rhat(t) + r(t) \dot \phi(t) \phihat(t)$$

Compare this with the expression for velocity in Cartesian coordinates

$$\v(t) =  \dot x(t) \xhat + \dot y(t) \yhat$$

and we see it's a bit more complicated in polar coordinates.

I understand the polar coordinates version as follows. At time $t$ the particle
might be moving radially, and its angle might also be changing. The velocity
vector has two components, one in the radial direction, and one in the tangent
direction. In the radial direction, it's moving at whatever speed the radius is
changing with. In the tangent direction it's moving at the speed that the angle
is changing, multiplied by the current radius. That multiplication by radius
makes sense informally, because if you are further out from the center of a
circle, and the circle rotates by a few degrees, then you move further in space
than if you were closer in to the center.


#### Acceleration


The acceleration function is the derivative of the velocity function with
respect to time. Therefore, it is also a vector: at time $t$ the particle is
accelerating by some amount, in some direction.

**Cartesian coordinates**

Again, because the unit vectors do not change with time, it's as you expect:
there's an x-acceleration in the x-direction, and a y-acceleration in the
y-direction.

$$\a(t) = \ddot x(t) \xhat + \ddot y(t) \yhat$$

**Polar coordinates**

Above we saw that because, in polar coordinates, the directions of the
coordinate system change with time, the function for velocity was more
complicated than when using Cartesian coordinates. For acceleration, we
differentiate the velocity expression and of course it gets even more
complicated. But basically the answer is still a function of the form

$$\a(t) = \bigg( \text{Some function of } t \bigg) \rhat(t) + \bigg( \text{Another function of } t \bigg) \phihat(t)$$

The functions of $t$ involve the current radius length, the speed and
acceleration in the current radius direction, and the speed and acceleration of
the angle parameter $\phi$. The full expression is in the footnote[ref]In polar
coordinates, if you suppose that you know functions $r(t)$ and $\phi(t)$ giving
the angle and distance at time $t$, then the accelerations in the two
orthogonal directions at time $t$ are
$\a(t) = \bigg( \ddot r(t) - r(t) \dot\phi(t)^2 \bigg) \rhat(t) + \bigg( 2\dot r(t) \dot \phi(t) + r(t) \ddot \phi(t)\bigg) \phihat(t)$
[/ref].


### Newton's second law as a differential equation

A key point seems to be: view Newton's second law $\F = m\a$ as a differential
equation[ref]The dot means "differentiated with respect to time". So if $r$ is
position as a function of time then $\dot r$ is velocity and $\ddot r$ is
acceleration.[/ref]:

$$m \ddot \r(t) = \F$$

I'm understanding this as follows: You know what forces are acting on the body
in question. You want to know how the position of the body will evolve through
time: $\r(t)$. This is a function satisfying the following differential
equation: the second derivative with respect to time of $\r(t)$, times $m$, is
equal to the net force acting on the body.

In practice: in a typical problem you have some expression for $\F$ derived from
consideration of a diagram showing forces acting on the body. You might be able
to discover $\r(t)$ by finding a function whose second derivative is $\F$.

#### Example problems

**Cartesian coordinates**

> 1.37 A student kicks a frictionless puck with initial speed $v_0$, so that it
> slides up a plane that is inclined at an angle $\theta$ above the
> horizontal. **(a)** Write down Newton's second law for the puck and solve to
> give its position as a function of time.

This is a simple example of using the Second Law as a differential equation. We
write down the forces acting on the particle, set them equal to $m\ddot r(t)$
and integrate twice to get position.

The only force acting on the puck is its weight, i.e. its mass times
acceleration due to gravity: $mg$. The puck can only move along the surface of
the plane, so we are only interested in the component of the force that acts
parallel to the plane. This component is $-mg sin(\theta)$. So taking $x$ as the
direction up the plane, Newton's second law is

$$ m\ddot x(t) = -mgsin(\theta)$$

Integrating once gives velocity

$$ \dot x(t) = -g sin(\theta) t + v_0$$

Integrating again gives position

$$ x(t) = -\frac{1}{2} g sin(\theta) t^2 + v_0t + x_0$$

and $x_0=0$ since we start measuring from its starting position.

> **(b)** How long will the puck take to return to its starting point?

The puck is at its starting point whenever $x = 0$:

$$0 = t\bigg(-\frac{1}{2} g sin(\theta) t + v_0\bigg)$$

The solutions of that are either $t=0$ (which we already knew) or (the solution
we want)

$t = \frac{2v_0}{g sin(\theta)}$

**Polar coordinates**

> A "halfpipe" at a skateboard park consists of a concrete trough with a
> semicircular cross section of radius $R = 5m$. I hold a frictionless
> skateboard on the side of the trough pointing down toward the bottom and
> release it. Discuss the subsequent motion using Newton's second law. In
> particular, if I release the skateboard just a short way from the bottom, how
> long will it take to come back to the point of release?

Conceptually, we do the same thing as for the problem using Cartesian
coordinates: we write down Newton's second law resolved into two orthogonal
directions. It's just that with polar coordinates, these orthogonal directions
are constantly changing.

The weight of the skateboard acts downwards. This results in a tangent force
causing the skateboard to move along the halfpipe, and also presses the
skateboard into the halfpipe a bit, with an associated reaction force. We
ignore the force/reaction force between the skateboard and the pipe and focus
only on the tangent force: $-mg sin(\phi)$.

The equation for acceleration says that, at time $t$, acceleration in the
current tangent direction is $R\ddot \phi(t)$ (halfpipe radius times current
angular acceleration[ref]To see this, start with the $\phihat(t)$ (tangent
direction) part of the full expression for acceleration and note that the
radial distance of the skateboard is fixed by the presence of the half-pipe, so
speed $\dot r(t)$ (and acceleration) in the radial direction is
zero.[/ref]). So Newton's second law in this context is the differential
equation

$$mR \ddot \phi(t) = -mg sin(\phi(t))$$

We read this as saying:

> We don't know how the angle is changing over time $\phi(t)$ -- that is
> precisely what we want to know. But what we do know is that whatever that
> function is, its second derivative at time $t$ is equal to the sin of the
> current angle (times $g/R$ and with a minus sign because the way we've
> defined the angle it gets smaller as the weight force takes the skateboard
> towards the bottom).

Once we've got to that point, finding the angle function $\phi(t)$ is just
math. It turns out that the only function for which it is true that the second
derivative has this property[ref]Actually the solution is a function with
second derivative having a different property, but one which is very similar to
the desired property as long as we're restricting ourselves to the angle being
fairly small.[/ref] is

$$\phi(t) = \phi_0 cos\bigg(\sqrt\frac{g}{R}t\bigg)$$

where $\phi_0$ is the angle that the skateboard was released at at time $t=0$.
This is the "solution" of the differential equation: a function matching the
criteria that the differential equation specified.

So we have our answer: the forces acting on the skateboard imply (via Newton's
second law) that the way the angle of the skateboard changes is a cosine
function of time. So the skateboard angle does what cosines do: it starts off
at its maximum, decreases to zero, crosses zero and becomes negative for a
while, starts turning back towards zero, crosses zero and becomes positive
again and gets back to its maximum where it turns around again.


### Conservation of momentum

Momentum is mass times velocity, $\p(t) = m\dot \r(t)$, so another way of
stating the second law is: rate of change of momentum is equal to force. In a
multi-particle system the forces-and-reaction-forces of the third law cancel
each other out when summing the rate of change of momentum of the whole
system. So, total momentum doesn't change due to internal forces (but it does
if there are external forces).

pp 21-23 show that conservation of momentum does not hold when considering
magnetic and electrostatic forces between charged particles moving close to the
speed of light. However I am unfamiliar with those forces and with the
"right-hand rule" for fields/forces and I haven't understood this section.

-------------------------------------------------------------------------------