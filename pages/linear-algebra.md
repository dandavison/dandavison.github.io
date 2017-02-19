Title: Linear Algebra
Slug: linear-algebra
Date: 2016-08-14

<style type="text/css">
body {color: black;}
</style>

$$
\newcommand{\i}{\mathbf{i}}
\newcommand{\j}{\mathbf{j}}
\newcommand{\cvec}[2]{\begin{pmatrix}#1\\#2\end{pmatrix}}
\newcommand{\mat}[4]{\begin{bmatrix}#1 & #2\\#3 & #4\\ \end{bmatrix}}
\newcommand{\scvec}[2]{\tiny{\cvec{#1}{#2}}}
\newcommand{\smat}[4]{\tiny{\mat{#1}{#2}{#3}{#4}}}
\newcommand{\nth}{n^{\text{th}}}
\newcommand{\R}{\mathbb{R}}
\renewcommand{\vec}[1]{\mathbf{#1}}
$$

Notes from the
[Essence of Linear Algebra](https://www.youtube.com/playlist?list=PLZHQObOWTQDPD3MizzM2xVFitgF8hE_ab)
video series by [3blue1brown](http://www.3blue1brown.com/).

-------------------------------------------------------------------------------
### Linear transformations and matrices

A linear transformation is completely specified by

1. Some basis vectors $\i$ and $\j$
2. Where those basis vectors are taken to by the transformation.

How the transformation affects any other point follows from those two pieces of
information.

So $\i$ might be taken to $a\i + b\j$, and $\j$ might be taken to $c\i + d\j$.
In this case we would use the following matrix to describe the
transformation:

$$
\mat{a}{c}
    {b}{d}
$$

Some examples are

$$
\begin{array}{ll}
\text{stretch by a in the i-direction} & \mat{a}{0}
                                             {0}{1}
\\\\
\text{stretch by a in the i-direction and shear right} & \mat{a}{b}
                                                             {0}{1}
\\\\
\text{rotate anticlockwise 90°} & \mat{0}{-1}
                                      {1}{ 0}
\end{array}
$$

Note that we haven't said what $\i$ and $\j$ are yet; they _define_ the
2-dimensional space that we're considering. But, we can think of them for now
as the usual orthogonal unit vectors in 2D space.

So the matrix tells us where the basis vectors have been taken to. Any other
vector $f\i + g\j$ is taken to wherever that is using the transformed basis
vectors:

$$
f\i + g\j \longrightarrow f\cvec{a}{b} + g\cvec{c}{d} = \cvec{fa + gc}{fb + gd}
$$


And that's how matrix multiplication is defined:

$$
\mat{a}{c}
    {b}{d} \cvec{f}{g} = \cvec{fa + gc}{fb + gd}
$$


A matrix represents a linear transformation by showing where the basis vector
are taken to.

-------------------------------------------------------------------------------
### Change of basis

Suppose person B uses some other basis vectors to describe locations in
space. Specifically, in our coordinates, their basis vectors are
$\scvec{2}{1}$ and $\scvec{-1}{1}$.


**When they state a vector, what is it in our coordinates?**

If they say $\scvec{-1}{2}$, what is that in our coordinates?

Well, if they say $\scvec{1}{0}$, that's $\scvec{2}{1}$ in our coordinates. And
if they say $\scvec{0}{1}$, that's $\scvec{-1}{1}$ in our coordinates. So the
matrix containing _their basis vectors expressed using our coordinate system_
transforms a point expressed in their coordinate system into one expressed in
ours. That last sentence is critical, so hopefully it makes sense! So, the answer is

$$
\mat{2}{-1}
    {1}{ 1} \cvec{-1}{2} = \cvec{-4}{1}.
$$


**When we state a vector, what is it in their coordinates?**

We give the vector $\scvec{3}{2}$. What is that in their coordinate system? By
definition, the answer is the weights that scales their basis vectors to hit
$\scvec{3}{2}$. So, the solution to

$$
\mat{2}{-1}
    {1}{1} \cvec{a}{b} = \cvec{3}{2}.
$$


Computationally, we can see that we can get the solution by multiplying both
sides by the inverse:

$$
\cvec{a}{b} = \mat{2}{-1}
                  {1}{1}^{-1} \cvec{3}{2}.
$$

Conceptually, we have

$$
\mat{2}{-1}
    {1}{1} =
\begin{bmatrix}\text{matrix converting their}\\\text{representation to ours} \\ \end{bmatrix}
$$

where "their representation" means the vector expressed using their coordinate
system. So the role played by the inverse is

$$
\cvec{a}{b} =
\begin{bmatrix}\text{matrix converting our}\\\text{representation to theirs} \\ \end{bmatrix}
\cvec{3}{2}.
$$

**When we state a transformation, what is it in their coordinates?**

We state a 90° anticlockwise rotation of 2D space:

$$
\mat{0}{-1}
    {1}{0}
$$

what is that transformation in their coordinates? The answer is

$$
\begin{bmatrix}\text{matrix converting our}\\\text{representation to theirs} \\ \end{bmatrix}
\mat{0}{-1}
    {1}{0}
\begin{bmatrix}\text{matrix converting their}\\\text{representation to ours} \\ \end{bmatrix}
$$

since the composition of those three transformations defines a single
transformation that takes in a vector expressed in their coordinate system,
converts it to our coordinate system, transforms it as requested, and then
converts back to theirs.

-------------------------------------------------------------------------------
### Linear and quadratic approximations to a function

<!-- https://www.khanacademy.org/math/multivariable-calculus/applications-of-multivariable-derivatives/quadratic-approximations/v/vector-form-of-multivariable-quadratic-approximation -->

**Linear approximation to a function $f(x, y)$ near $(x_0, y_0)$:**

\begin{align*}
f(x, y) &\approx
~
f(x_0, y_0) ~+
(x - x_0)f_x(x_0,y_0) +
(y - y_0)f_y(x_0,y_0)
\\\\
&= f(\vec x) + (\vec x - \vec x_0) \cdot \nabla_f(\vec x_0)
\end{align*}


**Quadratic approximation to a function $f(x, y)$ near $(x_0, y_0)$:**


\begin{align*}
Q(x, y) =
~
&f(x_0, y_0) ~+
\\
&(x - x_0)f_x(x_0,y_0) +
(y - y_0)f_y(x_0,y_0) ~+
\\
&(x - x_0)^2 f_{xx}(x_0, y_0) ~+
\\
&(y - y_0)^2 f_{yy}(x_0, y_0) ~+
\end{align*}


-------------------------------------------------------------------------------
### Positive definiteness

A square matrix $A \in \R^{n \times n}$ is positive definite if $x^TAx > 0$ for
every $x \in \R^n - \{0\}$. Basically, this means that the image of the vector
$x$ is correlated with the original vector; has some component in the same
direction.

<!-- https://www.reddit.com/r/math/comments/3uoa6d/motivation_for_positive_definite_matrices_brief/cxh21jg/ -->

Consider first two terms of Taylor approximation to $f$ at $x_0$:

$$
f(x_0) \approx x_0 + f'(x_0)(x - x_0) + \frac{1}{2}f''(x_0) (x - x_0)^2
$$

Now suppose $x_0$ is a critical point (local minimum/maximum) and consider the difference $f(x_0) - f(x)$:
$$
f(x_0) - f(x) \approx \frac{1}{2}f''(x_0) (x - x_0)^2.
$$

So if the second derivative is negative, then $f$ has decreased as we moved
away from $x_0$, showing that it was a maximum. Similarly, positive second
derivative indicates minimum.

The multivariable analog of the second derivative condition uses the Hessian
$H$ of $f$, evaluated at $x_0$.
$$ (x - x_0)^T H (x - x_0) $$
So a positive definite Hessian indicates a minimum, and negative definite
Hessian indicates a maximum.
