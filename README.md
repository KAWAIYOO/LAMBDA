# LAMBDA
Least Squares Ambiguity Decorrelation Adjustment Algorithm
This is a Pythonic translation of Dr P.J. Teunissen's LAMBDA algorithm for fixing integer ambiguities.
The original LAMBDA was written in MATLAB by Dr Sandra Verhagan and Dr Bofeng Li, TU Delft / Curtin University.
This Pythonic translation employs the default integer least-squares (ILS) with search-and-shrink method.
It decorrelates float ambiguities based on the covariance matrix search-and-shrink, and then fixes ambiguities.
Although it was intended for GNSS ambiguity fixing, it can fix integers for other applications like InSAR
Credits to PJ Teunissen, Jonge, J Tiberius, S. Verhagen, and Bofeng Li.

INPUTS:

  - ahat    : numpy array of float ambiguities
  - Qahat   : numpy covariance matrix for float ambiguities
  - ncands  : number of candidates (optional parameter, default = 2)

OUTPUT:

  - afixed1 : Best estimated integer candidates
  - afixed2 : 2nd best estimated integer candidates
  - sqnorm  : Distance between integer candidate and float ambiguity
              vectors in the metric of the variance-covariance matrix
