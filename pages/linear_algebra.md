Title: Linear Algebra
Slug: linear-algebra
Date: 2016-08-14

$$
\newcommand{\i}{\mathbf{i}}
\newcommand{\j}{\mathbf{j}}
\newcommand{\vec}[2]{\begin{pmatrix}#1\\#2\end{pmatrix}}
\newcommand{\mat}[4]{\begin{bmatrix}#1 & #2\\#3 & #4\\ \end{bmatrix}}
\newcommand{\svec}[2]{\tiny{\vec{#1}{#2}}}
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
2-dimensional space that we're considering. But, in physics at least, they will
often be unit vectors in "normal 2D space".

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
