Title: Linear Algebra
Slug: linear-algebra
Date: 2016-08-14

$$
\newcommand{\i}{\mathbf{i}}
\newcommand{\j}{\mathbf{j}}
\newcommand{\vec}[2]{\begin{pmatrix}#1\\#2\end{pmatrix}}
\newcommand{\mat}[4]{\begin{bmatrix}#1 & #2\\#3 & #4\\ \end{bmatrix}}
\newcommand{\svec}[2]{\tiny{\vec{#1}{#2}}}
\newcommand{\nth}{n^{\text{th}}}
$$


-------------------------------------------------------------------------------
### Linear transformations and matrices
To specify a linear transformation, you specify:

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

Note that we haven't said what $\i$ and $\j$ are yet; they _define_ the
2-dimensional space that we're considering. But, we can think of them for now
as the usual unit vectors in 2D space.

So the matrix tells us where the basis vectors have been taken to. Any other
vector $f\i + g\j$ is taken to wherever that is using the transformed basis
vectors:

$$
f\i + g\j \longrightarrow f\vec{a}{b} + g\vec{c}{d} = \vec{fa + gc}{fb + gd}
$$


And that's how matrix multiplication is defined:

$$
\mat{a}{c}
    {b}{d} \vec{f}{g} = \vec{fa + gc}{fb + gd}
$$


A matrix represents a linear transformation by offering up some new basis
vectors (its columns) for linear combinations of them to be made (a vector in
the transformed space).

-------------------------------------------------------------------------------
### Change of basis

Suppose person B uses some other basis vectors to describe locations in
space. Specifically, in our coordinates, their basis vectors are
$\svec{2}{1}$ and $\svec{-1}{1}$.


**When they state a vector, what is it in our coordinates?**

If they say $\svec{-1}{2}$, what is that in our coordinates?

Well, if they say $\svec{1}{0}$, that's $\svec{2}{1}$ in our
coordinates. And if they say $\svec{0}{1}$, that's $\svec{-1}{1}$ in our
coordinates. So the matrix containing _their basis vectors expressed in our
coordinates_ transforms a point expressed in their language into one expressed
in ours. So, the answer is

$$
\mat{2}{-1}
    {1}{1} \vec{-1}{2} = \vec{-4}{1}.
$$


**When we state a vector, what is it in their coordinates?**

We give the vector $\svec{3}{2}$. What is that in their coordinate system? By
definition, the answer is the weights that scales their basis vectors to hit $\svec{3}{2}$. So, the solution to

$$
\mat{2}{-1}
    {1}{1} \vec{a}{b} = \vec{3}{2}.
$$


Computationally, we can see that we can get the solution by multiplying both sides by the inverse:

$$
\vec{a}{b} = \mat{2}{-1}
                 {1}{1}^{-1} \vec{3}{2}.
$$

Conceptually, we have

$$
\mat{2}{-1}
    {1}{1} =
\begin{bmatrix}\text{matrix converting their}\\\text{language to ours} \\ \end{bmatrix}
$$

and so the role played by the inverse is

$$
\vec{a}{b} =
\begin{bmatrix}\text{matrix converting our}\\\text{language to theirs} \\ \end{bmatrix}
\vec{3}{2}.
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

1. Find the eigenvectors and put them in a matrix $V$
2. Find the inverse of $V$
3. Compute the matrix product $V^{-1}AV$
4. Compute the result of raising that to the $\nth$ power
5. Plug the result of that into the overall expression
6. Take the entry in the bottom left or top right (they should be the same!) and simplify.

The result should be an expression giving the $\nth$ Fibonacci number as a function of $n$. It should be possible to give as input to that function the number one million, and have it output the one millionth Fibonacci number directly, without it having to go through the preceding 999,999 Fibonacci numbers.


-------------------------------------------------------------------------------
<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>


A vector $\vec{f}{g}$ is really $f\i + g\j$. If $\i$ and $\j$ are unit
vectors, this is

$$
\mat{1}{0}
    {0}{1} \vec{f}{g}
$$

And in the transformed space, $\vec{f}{g}$ is at

$$
\mat{a}{c}
    {b}{d} \vec{f}{g}
$$


- A matrix can represent a linear transformation: it contains the new basis
  vectors as its columns

- In general, a matrix provides some columns and multiplying a matrix by a
  vector is forming a linear combination of the matrix's columns, with weights
  given by the elements of the vector.

- So we read Ax = b as saying "Using the new basis vectors given by A, what
  vector in the input space is taken to b" Careful: Are the keeping the same
  coordinate system or not?

- $A(BC) == (AB)C$ is obviously true since both say "do the C transformation,
  then B, then A".

- With square matrices, the input space and output space can be represented in
  the same coordinate system. We are discussing things as if the basis vectors
  of the input space are the orthogonal unit vectors, and the basis vectors in
  the output space are something else.

- A 3x2 matrix contains 2 columns (i.e. it is describing where the 2 basis
  vectors of a 2D space will end up), each one being a 3-vector (so they end up
  in a 3D space). I.e. it maps vectors from a 2D input space into a 3D
  space. However, they will lie on a 2D plane in that 3D space.

- A 2x3 matrix contains 3 columns (input space is 3D) each one being a 2-vector
  (output is 2D). So the 3 basis vectors are flattened out and end up on a
  plane.


Questions

- Does it make sense to view all matrices as linear transformations? For
  example, what about a covariance matrix, or a hessian, or a design matrix in
  linear models?
