
-------------------------------------------------------------------------------
<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>


A vector $\cvec{f}{g}$ is really $f\i + g\j$. If $\i$ and $\j$ are unit
vectors, this is

$$
\mat{1}{0}
    {0}{1} \cvec{f}{g}
$$

And in the transformed space, $\cvec{f}{g}$ is at

$$
\mat{a}{c}
    {b}{d} \cvec{f}{g}
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
