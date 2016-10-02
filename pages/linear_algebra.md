Title: Linear Algebra
Slug: linear-algebra
Date: 2016-08-14

$$
\newcommand{\i}{\mathbf{i}}
\newcommand{\j}{\mathbf{j}}
\newcommand{\cvec}[2]{\begin{pmatrix}#1\\#2\end{pmatrix}}
\newcommand{\mat}[4]{\begin{bmatrix}#1 & #2\\#3 & #4\\ \end{bmatrix}}
\newcommand{\scvec}[2]{\tiny{\cvec{#1}{#2}}}
\newcommand{\smat}[4]{\tiny{\mat{#1}{#2}{#3}{#4}}}
\newcommand{\nth}{n^{\text{th}}}
$$


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


A matrix represents a linear transformation by showing where the basis vector are taken to.

-------------------------------------------------------------------------------
### Change of basis

Suppose person B uses some other basis vectors to describe locations in
space. Specifically, in our coordinates, their basis vectors are
$\scvec{2}{1}$ and $\scvec{-1}{1}$.


**When they state a vector, what is it in our coordinates?**

If they say $\scvec{-1}{2}$, what is that in our coordinates?

Well, if they say $\scvec{1}{0}$, that's $\scvec{2}{1}$ in our
coordinates. And if they say $\scvec{0}{1}$, that's $\scvec{-1}{1}$ in our
coordinates. So the matrix containing _their basis vectors expressed in our
coordinates_ transforms a point expressed in their language into one expressed
in ours. So, the answer is

$$
\mat{2}{-1}
    {1}{ 1} \cvec{-1}{2} = \cvec{-4}{1}.
$$


**When we state a vector, what is it in their coordinates?**

We give the vector $\scvec{3}{2}$. What is that in their coordinate system? By
definition, the answer is the weights that scales their basis vectors to hit $\scvec{3}{2}$. So, the solution to

$$
\mat{2}{-1}
    {1}{1} \cvec{a}{b} = \cvec{3}{2}.
$$


Computationally, we can see that we can get the solution by multiplying both sides by the inverse:

$$
\cvec{a}{b} = \mat{2}{-1}
                  {1}{1}^{-1} \cvec{3}{2}.
$$

Conceptually, we have

$$
\mat{2}{-1}
    {1}{1} =
\begin{bmatrix}\text{matrix converting their}\\\text{language to ours} \\ \end{bmatrix}
$$

and so the role played by the inverse is

$$
\cvec{a}{b} =
\begin{bmatrix}\text{matrix converting our}\\\text{language to theirs} \\ \end{bmatrix}
\cvec{3}{2}.
$$

**When we state a transformation, what is it in their coordinates?**

We state a 90° anticlockwise rotation of 2D space:

$$
\mat{1}{-1}
    {0}{0}
$$

what is that transformation in their coordinates? The answer is

$$
\begin{bmatrix}\text{matrix converting our}\\\text{language to theirs} \\ \end{bmatrix}
\mat{1}{-1}
    {0}{0}
\begin{bmatrix}\text{matrix converting their}\\\text{language to ours} \\ \end{bmatrix}
$$

Since the composition of those three transformations defines a single transformation that takes in a vector in their language, converts it to ours, transforms it as requested, and then converts back to theirs.


-------------------------------------------------------------------------------
### Eigenbasis Fibonacci proof

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

Define the Fibonacci numbers to be $F_0, F_1, F_2, F_3, F_4, F_5, F_6, ...$ = $0, 1, 1, 2, 3, 5, 8, ...$.

The matrix powers are generating the Fibonacci sequence:

$$
A^{n} = \mat{F_{n-1} }{F_n      }
            {F_n     }{F_{n+1} }
$$

So if there were an efficient algorithm for computing the $\nth$ power of the matrix, that would also be an efficient algorithm for computing the $\nth$ Fibonacci number "directly", i.e. without computing all the preceding Fibonacci numbers _en route_.

How can we do this? To state the problem in a different way, we need to construct a new matrix that performs exactly the same transformation as $A^n$, but which somehow does the exponentiation step "in one go" rather than by multiplying $A$ with itself $n$ times.

#### **Solution outline**

Matrices represent transformations, so we can talk about them as taking in some vector and producing some other vector. The approach we're going to take is to re-express the $A^n$ transformation as follows:

1. Convert the input vector to its representation in an alternative basis which uses the eigenvectors as the basis vectors (it's called an "eigenbasis").
2. In this alternative basis, compute the new position of the vector after carrying out the $A^n$ transformation.
3. Convert the resulting vector back to its representation in our original basis.

I.e., we're going to compute the overall transformation as this product of matrices:

$$
\begin{bmatrix}\text{matrix converting their}\\\text{representation to ours} \\ \end{bmatrix}
\begin{bmatrix}\text{matrix that does the A transformation}\\\text{in the alternative basis} \\ \end{bmatrix}^n
\begin{bmatrix}\text{matrix converting our}\\\text{representation to theirs} \\ \end{bmatrix}
$$

The key part of all this -- the crux of the trick -- is that the exponentiation is efficient in the eigenbasis. We'll see why below.

#### **Solution details**

Let's suppose we've already found the eigenvectors and that there are two of them and we've arranged them as the two columns of a matrix $V$. So $V$ holds the basis vectors of the alternative basis and therefore we know from the change of basis notes above that $V$ is the matrix that takes as input a vector expressed in the alternative basis and outputs its representation in our basis. So, step (3) is done by $V$, and step (1) is done by $V^{-1}$, and the matrix performing all three steps is going to look like

i.e.

$$
V
\begin{bmatrix}\text{matrix that does the A transformation}\\\text{in the alternative basis} \\ \end{bmatrix}^n
V^{-1}
$$

OK, so what is the matrix in the middle? The change of basis section above tells us that we can compute it as

$$
\begin{bmatrix}\text{matrix converting our}\\\text{representation to theirs} \\ \end{bmatrix}
A
\begin{bmatrix}\text{matrix converting their}\\\text{representation to ours} \\ \end{bmatrix}
$$

so in other words the matrix in the middle is

$$
V^{-1}AV
$$

and the entire transformation is


$$
V
\Big(V^{-1}AV\Big)^n
V^{-1}
$$


Recall that above we observed that the $\nth$ power of $A$ is a matrix with the nth Fibonacci number in its bottom left and top right entries. So the following tasks remain:

1. Find the eigenvectors and put them in a matrix $V$.
2. Find the inverse of $V$.
3. Compute the matrix product $V^{-1}AV$.
4. Compute the result of raising that to the $\nth$ power.
5. Plug the result of that into the overall expression.
6. Take the entry in the bottom left or top right (they should be the same!).

The result should be an expression giving the $\nth$ Fibonacci number as a function of $n$. It should be possible to give as input to that function the number one million, and have it output the one millionth Fibonacci number directly, without it having to go through the preceding 999,999 Fibonacci numbers.


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


#### **Calculations**

##### **1. Find the eigenvectors**
We follow the textbook approach: We have
$$
A = \mat{0}{1}
        {1}{1}
$$
An eigenvector $v$ satisfies $Av = \lambda v$ for some scalar $\lambda$. That equation can be rearranged as follows

\begin{align*}
A\vec v &= \lambda I\vec v
\\
A\vec v - \lambda I\vec v &= \vec 0
\\
(A - \lambda I)\vec v &= \vec 0
\end{align*}

which means that the matrix $A - \lambda I$ is a transformation that takes some non-zero vector $\vec v$ to the zero vector (i.e. it has a non-empty "null space"). This means that the transformation cannot be reversed, i.e. the matrix has no inverse, i.e. its determinant is zero. So, use that last fact to find the eigenvectors $\lambda$:

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

From the first equation [ref]Using the second equation gives the same
answer. TODO: Why?[/ref] we have $v_2 = \lambda v_1$. There are infinitely many
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
stretch space in the direction of one or both basis vectors. That's because (1)
we represent a transformation with a matrix saying where each of the basis
vectors are taken to, (2) the definition of an eigenvector of a transformation
is that it is a vector which is simply stretched by the transformation with no
change in direction, therefore (3) if the eigenvectors are the basis vectors,
then the matrix representing the transformation must just stretch space in the
two directions. A matrix which stretches space in the direction of the basis
vectors looks like $\smat{a}{0}{0}{b}$, i.e. it is diagonal. Therefore,
$V^{-1}AV$ _must_ be diagonal.

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

The matrix is diagonal so this is straightforward. Note that this is the whole point of converting to the eigenbasis: the exponentiation at this step just involves the usual operations of raising scalar numbers to a power; no need to multiply matrices together. A computer will be able to compute the $\nth$ power of a diagonal matrix much faster than that of a non-diagonal matrix.

$$
(V^{-1}AV)^n = \frac{1}{2^n} \mat{(1 + \sqrt 5)^n}{0          }
                                 {0              }{(1 - \sqrt 5)^n}
$$

##### **4. Plug the $\nth$ power into the overall expression**

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
