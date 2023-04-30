Download Link: https://assignmentchef.com/product/solved-ic20-homework1-sparse-matrices-formats
<br>
<strong>Sparse Matrices Formats – COO, CSR, CSC, MSR, BSR, SKY, DIAG, ELL-IT </strong>

<strong>The following exercise must be applied to (matrices are described below in <em>Set of matrices</em>): 1) generally sparse matrices  </strong>

<strong>2) one type among Banded sparse, Block sparse, Block diagonal sparse, at your choice  </strong>

<strong><em>Set of matrices </em></strong>

Matrices are square <em>n</em>x<em>n</em>, randomly generated with sparsity <em>s</em>=<em>nnz</em>/<em>n</em><sup>2</sup> equal to 20%, with nonzero entries in the interval [1,100] (integer or double). Matrices can be of the following type:

<ul>

 <li><strong>Generally sparse – </strong>sparse matrix with sparsity s o <strong><em>associated formats:</em></strong> <strong>COO, CSR, CSC </strong></li>

 <li><strong>Banded sparse – </strong>banded with parameter <strong>k</strong>, where the size <strong>b </strong>of the <strong>band</strong> is defined as b = 2k+1 (k is the number of diagonals under, or over, the main diagonal); all nonzero entries are in included in the band o <strong><em>associated formats:</em> Sky, diag, Ell-It </strong></li>

 <li><strong>Block sparse – </strong>blocks are disjoint and positioned wherever; all blocks have the same size (at least n/5) and can include zero entries (sparsity of matrix is 20%) o <strong><em>associated formats: </em>BSR, Ell-It, MSR </strong></li>

 <li><strong>Block diagonal sparse – </strong>blocks are along the main diagonal; consider blocks of different sizes that can include zero entries (sparsity of matrix is 20%) o <strong><em>associated formats: </em>BSR, Ell-It, diag </strong></li>

</ul>

<strong> </strong>

<strong>Exercise  </strong>

<ul>

 <li>Write a function that produces the (random valued) full matrix of the selected type</li>

 <li>Write the function <strong>toCompact</strong> that produces the compact representation of a given matrix for two of the <strong><em>formats associated to the selected matrix type</em></strong></li>

 <li>Write the function <strong>extractRow</strong> that takes in input the index <em>h</em> and the compact representation of the matrix and extracts row <em>h</em></li>

 <li>Write the function <strong>extractCol</strong> that takes in input the index <em>k</em> and the compact representation of the matrix and extracts column <em>k</em></li>

 <li>Write a script that calls the above functions and:

  <ul>

   <li>generates two sparse matrices A and B</li>

   <li>produces the compact matrices A-Comp and B-Comp (from matrices A and B) o computes the product <strong>C-Comp</strong>= A-Comp*B-Comp, using the compact format of operand matrices A-Comp and B-Comp, and producing the resulting product matrix C-Comp in compact format</li>

  </ul></li>

 <li>Calculate and show results for matrices of increasing size (for example <em>n</em>= 25, 50, 75, 100), giving a graph for:

  <ul>

   <li>The execution time, using commands tic…toc(consider also cputime and etime) o The memory occupation</li>

  </ul></li>

</ul>

<strong>Note that</strong> dealing with random matrices, <strong>execution time</strong> and <strong>memory occupation</strong> <strong>need to be averaged on a set of test matrices</strong> (at least 5 for each type/format)

<h1>Sparse Matrices in Matlab</h1>

<strong>S=sparse(A)</strong> converts a full matrix to sparse form by squeezing out any zero elements. If <sub>S</sub> is already sparse, <sub>sparse(S)</sub> returns <sub>S</sub>.

<strong>S=sparse(i,j,s,m,n,nzmax)</strong> uses vectors <sub>i</sub>, <sub>j</sub>, and <sub>s</sub> to generate an <sub>m</sub>-by-<sub>n</sub> sparse matrix with elements vector <sub>s</sub> with indices in vectors <sub>i </sub>and <sub>j</sub>, such that <sub>S(i(k),j(k)) = </sub>

(<sub>k)</sub>, with space allocated for <sub>nzmax</sub> nonzeros. Vectors <sub>i</sub>, <sub>j</sub>, and <sub>s</sub> are all the same length.

<strong>A=full(S)</strong> converts a sparse matrix <sub>S</sub> to full storage organization.

<strong>Example: </strong>

&gt;&gt; x =[5 9 1 7 3]

&gt;&gt; S=sparse ([2 4 1 3 6] ,[1 1 3 3 7],x)

S=

(2,1) 5

(4,1) 9

(1,3) 1

(3,3) 7

(6,7) 3

&gt;&gt; full(S) ans = 0 0 1 0 0 0 0

5 0 0 0 0 0 0

0 0 7 0 0 0 0

9 0 0 0 0 0 0

0 0 0 0 0 0 0

0 0 0 0 0 0 3

Matlab includes many commands for dealing with a sparse matrix:

<strong>nnz(A)</strong>          returns the number of nonzero matrix elements

<strong>nzmax(A)</strong>  returns the maximum number of nonzero matrix elements allocated <strong>find(A) </strong> returns all (i,j) indices of nonzero elements <strong>nonzeros(A)</strong> returns all the nonzero elements <strong>spy(S)</strong>  plots the sparsity pattern of any matrix S

<strong> </strong>

<strong>R=spones(S)</strong> generates a matrix R with the same sparsity structure as S, but with 1’s in the nonzero positions.

<strong> </strong>

<strong>TF = issparse(S)</strong> returns logical 1 (true) if the storage class of <sub>S</sub> is sparse and logical 0

(false) otherwise.




<strong>R=sprand(m,n,density)</strong> is a random, m-by-n, sparse matrix with approximately density*m*n uniformly distributed nonzero entries (0≤density≤1)<strong>  </strong>

<strong> </strong>

<strong>A=spdiags(b,d,m,n)</strong> creates an m-by-n sparse matrix by taking the columns of B and placing them along the diagonals specified by d.




<strong>sprandsym(S)</strong> returns a symmetric random matrix whose lower triangle and diagonal have the same structure as S. Its elements are normally distributed, mean 0 and variance 1.




<strong>Example: </strong>




&gt;&gt; n=10;

&gt;&gt; e=ones(n,1);

&gt;&gt; b=[e,-e,3*e,-e,2*e];

&gt;&gt; d=[-n/2 -1 0 1 n/2]; &gt;&gt; a=spdiags(b,d,n,n) a = (1,1) 3

(2,1) -1 (6,1) 1

(1,2) -1

(2,2) 3

(3,2) -1

………

&gt;&gt; aa=full(a) aa =

3 -1  0  0  0  2  0  0  0  0

-1  3 -1  0  0  0  2  0  0  0

0 -1  3 -1  0  0  0  2  0  0

0  0 -1  3 -1  0  0  0  2  0

<ul>

 <li>0 0 -1  3 -1  0  0  0  2</li>

 <li>0 0  0 -1  3 -1  0  0  0</li>

</ul>

0  1  0  0  0 -1  3 -1  0  0

0  0  1  0  0  0 -1  3 -1  0

0  0  0  1  0  0  0 -1  3 -1

0  0  0  0  1  0  0  0 -1  3




Example of tridiagonal matrix:




&gt;&gt; b=ones(4,1);

&gt;&gt; A=spdiags([b 3*b b],-1:1,4,4)

A =

(1,1) 3

(2,1) 1

(1,2) 1

(2,2) 3

(3,2) 1

(2,3) 1

(3,3) 3

(4,3) 1

(3,4) 1

(4,4) 3

&gt;&gt; d=full(A) d = 3 1 0 0

1 3 1 0

0 1 3 1

0 0 1 3







<strong> </strong>

<strong> </strong>

<strong>Example</strong>: comparison of memory occupation




&gt;&gt; b=ones(100,1);

&gt;&gt; A=spdiags([b 3*b b],-1:1,100,100)

&gt;&gt; d=full(A);




&gt;&gt; whos

Name      Size            Bytes  Class

A   100×100        3980      double array (sparse) b   100×1     800       double array d      100×100        80000  double array

<strong> </strong>

<strong>Example</strong>: comparison of execution time needed to compute the square of a matrix in the full and in the sparse representation




&gt;&gt; a=eye(1000);

&gt;&gt; t=cputime;

&gt;&gt; b=a^2; &gt;&gt; temp=cputime-t temp = 3.7454

&gt;&gt; a=sparse(1:1000,1:1000,1,1000,1000);

&gt;&gt; t=cputime;

&gt;&gt; c=a^2; &gt;&gt; temp=cputime-t temp =

0.4406




———




<strong>gplot(A,Coordinates)</strong> plots a graph of the nodes defined in <sub>Coordinates</sub> according to the <em>n</em>–

by-<em>n</em> adjacency matrix <sub>A</sub>, where <em>n</em> is the number of nodes. <sub>Coordinates</sub> is an <em>n</em>-by-2 matrix, where <em>n</em> is the number of nodes and each coordinate pair represents one node.




<strong>Example </strong>

One interesting construction for graph analysis is the <em>Bucky ball</em>. This is composed of 60 points distributed on the surface of a sphere in such a way that the distance from any point to its nearest neighbors is the same for all the points. Each point has exactly three neighbors. The Bucky ball models different physical objects, such as the C<sub>60</sub> molecule, a form of pure carbon with 60 atoms in a nearly spherical configuration and the seams in a soccer ball

[B,v]=bucky; % B= adjacency matrix, v= coordinate matrix

gplot(B,v)

axis square

——

[B,v]=bucky; axis(‘square’);hold on gplot(B(1:30,1:30),v) for k=1:30

text(v(k,1),v(k,2),num2str(k)) end