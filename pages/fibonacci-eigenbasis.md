Title: Finding the nth Fibonacci number via an eigenvector change of basis
Slug: fibonacci-eigenbasis
Date: 2016-10-01

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
$$


This is the problem given at the end of the eigenvectors video in the
[Essence of Linear Algebra](https://www.youtube.com/playlist?list=PLZHQObOWTQDPD3MizzM2xVFitgF8hE_ab)
series by [3blue1brown](http://www.3blue1brown.com/).

-------------------------------------------------------------------------------
#### **Introduction**

Consider the matrix

$$
A = \mat{0}{1}
        {1}{1}
$$

The first few powers are

\begin{align*}
&A^{1} &= \mat{0}{1}
              {1}{1}
\\
&A^{2} = \mat{0}{1}
             {1}{1} \mat{0}{1}
                        {1}{1} &= \mat{1}{1}
                                      {1}{2}
\\
&A^{3} = \mat{0}{1}
             {1}{1} \mat{1}{1}
                        {1}{2} &= \mat{1}{2}
                                      {2}{3}
\\
&A^{4} = \mat{0}{1}
             {1}{1} \mat{1}{2}
                        {2}{3} &= \mat{2}{3}
                                      {3}{5}
\end{align*}

The Fibonacci sequence is the sequence you get by starting with $0,
1$ and after that always forming the next number by adding the two previous ones:
$F_0, F_1, F_2, F_3, F_4, F_5, F_6, F_7, ...$ = $0, 1, 1, 2, 3, 5, 8, 13, ...$.

The matrix powers are generating the Fibonacci sequence:

$$
A^{n} = \mat{F_{n-1} }{F_n      }
            {F_n     }{F_{n+1} }
$$

So if there were a way to compute the $\nth$ power of that matrix "directly",
that would also be a way to compute the $\nth$ Fibonacci number "directly",
i.e. without computing all the preceding Fibonacci numbers _en route_.

How can we do this? To state the problem in a different way, we need to
construct a new matrix that performs exactly the same transformation as $A^n$,
but which somehow does the exponentiation step "in one go" rather than by
multiplying $A$ with itself $n$ times.

#### **Solution outline**

Matrices represent transformations, so we can talk about them as taking in some
vector and producing some other vector. The approach we're going to take is to
re-express the $A^n$ transformation as follows:

1. Convert the input vector to its representation in an alternative basis which
   uses the eigenvectors as the basis vectors (it's called an "eigenbasis").
2. In this alternative basis, compute the new position of the vector after
   carrying out the $A^n$ transformation.
3. Convert the resulting vector back to its representation in our original
   basis.

I.e., we're going to compute the overall transformation as this product of
matrices (remember that one reads these things right-to-left):

$$
\begin{bmatrix}\text{matrix converting their}\\\text{representation to ours} \\ \end{bmatrix}
\begin{bmatrix}\text{matrix that does the A transformation}\\\text{in the alternative basis} \\ \end{bmatrix}^n
\begin{bmatrix}\text{matrix converting our}\\\text{representation to theirs} \\ \end{bmatrix}
$$

The key part of all this -- the crux of the trick -- is that the exponentiation
is efficient in the eigenbasis. That's because, in the eigenbasis, the
transformation is just stretching space in the directions of the two basis
vectors. So to do the transformation $n$ times in the eigenbasis, you just
stretch by the stretch-factor raised to the $\nth$ power, rather than doing $n$
matrix multiplications.

#### **Solution details**

Let's suppose we've already found the eigenvectors, and that there are two of
them, and that we've arranged them as the two columns of a matrix $V$. $V$ holds
the basis vectors of the alternative basis, and therefore we know from the
[change of basis](./linear-algebra.html#change-of-basis) notes that $V$ is the
matrix that takes as input a vector expressed in the alternative basis and
outputs its representation in our basis.

So, step (3) is done by $V$, and step (1) is done by $V^{-1}$, and the matrix
performing all three steps is going to look like

$$
V
\begin{bmatrix}\text{matrix that does the A transformation}\\\text{in the alternative basis} \\ \end{bmatrix}^n
V^{-1}
$$

OK, so what is the matrix in the middle? The
[change of basis](./linear-algebra.html#change-of-basis) notes tell us that we
can compute it as

$$
\begin{bmatrix}\text{matrix converting our}\\\text{representation to theirs} \\ \end{bmatrix}
A
\begin{bmatrix}\text{matrix converting their}\\\text{representation to ours} \\ \end{bmatrix}
$$

In other words the matrix in the middle is

$$
V^{-1}AV
$$

and the entire transformation is

$$
V
\Big(V^{-1}AV\Big)^n
V^{-1}
$$

Put back into words, that's

$$
\begin{bmatrix}\text{matrix converting their}\\\text{representation to ours} \\ \end{bmatrix}
\Bigg(
    \begin{bmatrix}\text{matrix converting our}\\\text{representation to theirs} \\ \end{bmatrix}
    A
    \begin{bmatrix}\text{matrix converting their}\\\text{representation to ours} \\ \end{bmatrix}
\Bigg)^n
\begin{bmatrix}\text{matrix converting our}\\\text{representation to theirs} \\ \end{bmatrix}
$$




Recall that above we observed that the $\nth$ power of $A$ is a matrix with the
nth Fibonacci number in its bottom left and top right entries. So the following
tasks remain:

1. Find the eigenvectors and put them in a matrix $V$.
2. Find the inverse of $V$.
3. Compute the matrix product $V^{-1}AV$.
4. Compute the result of raising that to the $\nth$ power.
5. Plug the result of that into the overall expression.
6. Take the entry in the bottom left or top right (they should be the same!).

The result should be an expression giving the $\nth$ Fibonacci number as a
function of $n$. It should be possible to give as input to that function the
number one million, and have it output the one millionth Fibonacci number
directly, without it having to go through the preceding 999,999 Fibonacci
numbers.


#### **The answer without showing the calculations**

\begin{align*}
&\text{The eigenvectors are}
\\\\
&V &= \mat{2          }{2          }
        {1 + \sqrt 5}{1 - \sqrt 5}
\\\\
&\text{which has inverse}
\\\\
&V^{-1} &= \frac{-1}{4\sqrt 5} \mat{1 - \sqrt 5 }{-2}
                                 {-1 - \sqrt 5}{2}
\\\\
&\text{Therefore}
\\\\
&V^{-1}AV &= \frac{1}{2} \mat{1 + \sqrt 5}{0          }
                            {0          }{1 - \sqrt 5}
\\\\
&\text{and}
\\\\
&(V^{-1}AV)^n &= \frac{1}{2^n} \mat{(1 + \sqrt 5)^n}{0          }
                                   {0                }{(1 - \sqrt 5)^n}
\\\\
&\text{and}
\\\\
&V \Big(V^{-1}AV\Big)^n V^{-1} &=
\mat{\frac{\big((1 + \sqrt 5)^{n-1} - (1 - \sqrt 5)^{n-1}\big)}{2^{n-1}\sqrt 5}}{\frac{\big((1 + \sqrt 5)^n     - (1 - \sqrt 5)^n    \big)}{2^n    \sqrt 5}}
    {\frac{\big((1 + \sqrt 5)^n     - (1 - \sqrt 5)^n    \big)}{2^n    \sqrt 5}}{\frac{\big((1 + \sqrt 5)^{n+1} - (1 - \sqrt 5)^{n+1}\big)}{2^{n+1}\sqrt 5}}
\\\\
&\text{Therefore the nth Fibonacci number is}
\\\\
&F_n &= \frac{(1 + \sqrt 5)^n     - (1 - \sqrt 5)^n}
             {2^n    \sqrt 5}
\end{align*}

#### **Does this actually work?**

Yes.

    :::python
    from math import sqrt

    def fib(n):
        return (
            ( (1 + sqrt(5))**n - (1 - sqrt(5))**n )
            /
            float(2**n * sqrt(5)))

    for i in range(10):
        print i, fib(i)

    0 0.0
    1 1.0
    2 1.0
    3 2.0
    4 3.0
    5 5.0
    6 8.0
    7 13.0
    8 21.0
    9 34.0

#### **History**

The formula is known as
[Binet's formula](https://en.wikipedia.org/wiki/Fibonacci_number#Closed-form_expression)
(1843) but was apparently known to Euler, Daniel Bernoulli and de Moivre more
than a century earlier. It can be derived without using linear algebra
techniques; I don't know when the style of proof attempted here would first
have been done. The result can be written as

$$
F_n = \frac{\phi^n - (1-\phi)^n}{\sqrt{5}}
$$

where $\phi = \frac{1+\sqrt{5}}{2}$ is the
[golden ratio](https://en.wikipedia.org/wiki/Golden_ratio).


#### **Calculations**

##### **1. Find the eigenvectors**
We follow the textbook approach: We have
$$
A = \mat{0}{1}
        {1}{1}
$$

An eigenvector $v$ satisfies $Av = \lambda v$ for some scalar $\lambda$. That
equation can be rearranged as follows

\begin{align*}
A\vec v &= \lambda I\vec v
\\
A\vec v - \lambda I\vec v &= \vec 0
\\
(A - \lambda I)\vec v &= \vec 0
\end{align*}

which means that the matrix $A - \lambda I$ is a transformation that takes some
non-zero vector $\vec v$ to the zero vector (i.e. it has a non-empty "null
space"). This means that the transformation cannot be reversed, i.e. the matrix
has no inverse, i.e. its determinant is zero. So, use that last fact to find
the eigenvectors $\lambda$:

\begin{align*}
\det (A - \lambda I) &= 0
\\
\\
\det \mat{-\lambda}{1}
         {1          }{1 - \lambda} &= 0
% \\
% \\
% (-\lambda)(1 - \lambda) - 1 &= 0
\\
\\
\lambda^2 - \lambda - 1 = 0
\end{align*}

Using the quadratic formula we have $a=1, b=-1, c=-1$ and

\begin{align*}
\lambda
= \frac{-b ± \sqrt{b^2 - 4ac}}{2a}
= \frac{1 ± \sqrt{5}}{2}
\end{align*}

which are the two eigenvalues.

To find eigenvectors associated with the eigenvalues, go back to the equations

\begin{align*}
(A - \lambda I)\vec v &= \vec 0
\\
\\
\mat{-\lambda}{1}
    {1       }{1 - \lambda} \vec v &= \vec 0
\end{align*}

Let an eigenvector $v$ be $\scvec{v_1}{v_2}$. The matrix equation corresponds
to this system of equations:

$$
\begin{cases}
-\lambda v_1 &+ v_2               &= 0\\
v_1          &+ (1 - \lambda) v_2 &= 0
\end{cases}
$$

From the first equation we have $v_2 = \lambda v_1$. There are infinitely many
eigenvectors (a line of them) associated with any given eigenvalue, so we can
pick an arbitrary value for $v_1$. If we choose $v_1=2$ then we have
eigenvectors $\scvec{2}{1+\sqrt 5}$ and $\scvec{2}{1-\sqrt 5}$. The matrix
containing the eigenvectors is

$$
V = \mat{2          }{2          }
        {1 + \sqrt 5}{1 - \sqrt 5}
$$


##### **2. Find inverse of $V$**

The inverse of a 2x2 matrix is given by

$$
\mat{a}{c}
    {b}{d} ^ {-1}
=
\frac{1}{\text{det}} \mat{d}{-c}
                         {-b}{a}
$$

where $\text{det} = ad - cb$. Therefore

\begin{align*}
V^{-1}
&= \frac{1}{2(1 - \sqrt 5) - 2(1 + \sqrt 5)} \mat{1 - \sqrt 5 }{-2}
                                                 {-(1 + \sqrt 5)}{2}
\\\\
&= \frac{-1}{4\sqrt 5} \mat{1 - \sqrt 5 }{-2}
                           {-(1 + \sqrt 5)}{2}
\end{align*}


##### **3. Find the matrix product $V^{-1}AV$**

Before we get lost in the calculation, let's remember what this is. It's a
matrix that does the $A$ transformation, but _in the coordinate system defined
by $A$'s eigenvectors_. So, the resulting matrix _must_ do nothing other than
stretch space in the direction of one or both basis vectors in that coordinate
system. That's because (1) we represent a transformation with a matrix saying
where each of the basis vectors are taken to, (2) the definition of an
eigenvector of a transformation is that it is a vector which is simply
stretched by the transformation with no change in direction, therefore (3) if
the eigenvectors are the basis vectors, then the matrix representing the
transformation must just stretch space in the two directions. A matrix which
stretches space in the direction of the basis vectors looks like
$\smat{a}{0}{0}{b}$, i.e. it is diagonal. Therefore, $V^{-1}AV$ _must_ be
diagonal.

\begin{align*}
V^{-1}AV &=
\frac{-1}{4\sqrt 5}
\mat{1 - \sqrt 5 }{-2}
    {-(1 + \sqrt 5)}{2}
\mat{0}{1}
    {1}{1}
\mat{2          }{2          }
    {1 + \sqrt 5}{1 - \sqrt 5}
\\\\
&=
\frac{-1}{4\sqrt 5}
\mat{1 - \sqrt 5 }{-2}
    {-(1 + \sqrt 5)}{2}
\mat{1 + \sqrt 5}{1 - \sqrt 5}
    {3 + \sqrt 5}{3 - \sqrt 5}
\\\\
&=
\frac{-1}{4\sqrt 5}
\mat{-4 - 2(3 + \sqrt 5)             }{6 - 2\sqrt 5 - 2(3 - \sqrt 5)}
    {-(6 + 2\sqrt 5) + 2(3 + \sqrt 5)}{4 + 2(3 - \sqrt 5)}
\\\\
&=
\frac{-1}{2\sqrt 5}
\mat{-2 - 3 - \sqrt 5}{3 - \sqrt 5 - 3 + \sqrt 5}
    {-3 - \sqrt 5 + 3 + \sqrt 5}{2 + 3 - \sqrt 5}
\\\\
&=
\frac{-1}{2\sqrt 5}
\mat{-5 - \sqrt 5}{0          }
    {0           }{5 - \sqrt 5}
\\\\
&=
\frac{1}{2}
\mat{1 + \sqrt 5}{0          }
    {0          }{1 - \sqrt 5}
\end{align*}

##### **4. Compute $(V^{-1}AV)^n$**

The matrix is diagonal so this is straightforward. Note that this is the whole
point of converting to the eigenbasis: the exponentiation at this step just
involves the usual operations of raising scalar numbers to a power; no need to
multiply matrices together. A computer will be able to compute the $\nth$ power
of a diagonal matrix much faster than that of a non-diagonal matrix.

$$
(V^{-1}AV)^n = \frac{1}{2^n} \mat{(1 + \sqrt 5)^n}{0          }
                                 {0              }{(1 - \sqrt 5)^n}
$$

##### **5. Plug the $\nth$ power into the overall expression**

\begin{align*}
V \Big(V^{-1}AV\Big)^n V^{-1}
&=
\frac{-1}{4\sqrt 5}
\frac{1}{2^n}
\mat{2          }{2          }
    {1 + \sqrt 5}{1 - \sqrt 5}
\mat{(1 + \sqrt 5)^n}{0              }
    {0              }{(1 - \sqrt 5)^n}
\mat{1 - \sqrt 5 }{-2}
    {-(1 + \sqrt 5)}{2}
\\\\
&=
\frac{-1}{4\sqrt 5}
\frac{1}{2^n}
\mat{2          }{2          }
    {1 + \sqrt 5}{1 - \sqrt 5}
\mat{(1 - \sqrt 5)(1 + \sqrt 5)^n}{-2(1 + \sqrt 5)^n}
    {-(1 + \sqrt 5)(1 - \sqrt 5)^n}{2(1 - \sqrt 5)^n}
\\\\
&=
\frac{-1}{4\sqrt 5}
\frac{1}{2^n}
\mat{2(-4)\big((1 + \sqrt 5)^{n-1} - (1 - \sqrt 5)^{n-1}\big)}{-4\big((1 + \sqrt 5)^n     - (1 - \sqrt 5)^n    \big)}
    {   -4\big((1 + \sqrt 5)^n     - (1 - \sqrt 5)^n    \big)}{-2\big((1 + \sqrt 5)^{n+1} - (1 - \sqrt 5)^{n+1}\big)}
\\\\
&=
\frac{1}{4\sqrt 5}
\mat{4\frac{\big((1 + \sqrt 5)^{n-1} - (1 - \sqrt 5)^{n-1}\big)}{2^{n-1}}}{4\frac{\big((1 + \sqrt 5)^n     - (1 - \sqrt 5)^n    \big)}{2^n    }}
    {4\frac{\big((1 + \sqrt 5)^n     - (1 - \sqrt 5)^n    \big)}{2^n    }}{ \frac{\big((1 + \sqrt 5)^{n+1} - (1 - \sqrt 5)^{n+1}\big)}{2^{n-1}}}
\\\\
&=
\mat{\frac{\big((1 + \sqrt 5)^{n-1} - (1 - \sqrt 5)^{n-1}\big)}{2^{n-1}\sqrt 5}}{\frac{\big((1 + \sqrt 5)^n     - (1 - \sqrt 5)^n    \big)}{2^n    \sqrt 5}}
    {\frac{\big((1 + \sqrt 5)^n     - (1 - \sqrt 5)^n    \big)}{2^n    \sqrt 5}}{\frac{\big((1 + \sqrt 5)^{n+1} - (1 - \sqrt 5)^{n+1}\big)}{2^{n+1}\sqrt 5}}
\end{align*}
