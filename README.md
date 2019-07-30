# LAMBDA
Least Squares Ambiguity Decorrelation Adjustment Algorithm
This is a Pythonic translation of Dr P.J. Teunissen's LAMBDA algorithm for fixing integer ambiguities.
The original LAMBDA was written in MATLAB by Dr Sandra Verhagan and Dr Bofeng Li, TU Delft / Curtin University.
This Pythonic translation employs the default integer least-squares (ILS) with search-and-shrink method.
It decorrelates float ambiguities based on the covariance matrix search-and-shrink, and then fixes ambiguities.
Although it was intended for GNSS ambiguity fixing, it can fix integers for other applications like InSAR
Credits to PJ Teunissen, Jonge, J Tiberius, S. Verhagen, and Bofeng Li.

'''
###############################################################################
###############################################################################
##                                                                           ##
## FILE DESCRIPTION:                                                         ##
##                                                                           ##
## This is the classical LAMBDA method that was originally authored by       ##
## Teunissen, Jonge, and Tiberius (1993). The code was later written in      ##
## MATLAB by Dr Sandra Verhagen and Dr Bofeng Li. It takes in a vector of    ##
## float ambiguities to the integer least-squares problem, and covariance    ##
## of the float ambiguities. It then runs the LAMBDA's ILS search-&-shrink   ##
## and spits out the ambiguity integers. The other 5 methods in original     ##
## LAMBDA MATLAB code are not supported here (feel free to edit the code     ##
## and implement it youself!). The default ncands = 2, as per original code. ##
## All support functions from the original MATLAB code (decorrel, ldldecom)  ##
## have been nested within the main function as sub functions.               ##
##                                                                           ##
## INPUTS:                                                                   ##
##                                                                           ##
##   - ahat    : numpy array of float ambiguities                            ##
##   - Qahat   : numpy covariance matrix for float ambiguities               ##
##   - ncands  : number of candidates (optional parameter, default = 2)      ##
##                                                                           ##
## OUTPUT:                                                                   ##
##                                                                           ##
##   - afixed1 : Best estimated integer candidates                           ##
##   - afixed2 : 2nd best estimated integer candidates                       ##
##   - sqnorm  : Distance between integer candidate and float ambiguity      ##
##               vectors in the metric of the variance-covariance matrix     ##
##                                                                           ##
## REMARKS:                                                                  ##
##                                                                           ##
## Changes to the Python version of this code:                               ##
##   - Everything is identical EXCEPT MATLAB is ones-based indexing.         ##
##   - Python is zero-based indexing, and range function does not            ##
##     include the upper limit index. Thus, only indices have changed.       ##
##   - Example in MATLAB: for i = 1:5 => {1,2,3,4,5}                         ##
##   - Equivalently in Python: for i in range(0,5) => {0,1,2,3,4}            ##
##   - Indices are thus updated accordingly.                                 ##
##                                                                           ##
##                                                                           ##
## WRITTEN BY:                                                               ##
##                                                                           ##
##   - Original Authors: Sandra Verhagen / Bofeng Li                         ##
##   - Translated by: Samuel Low, 29-07-2019,                                ##
##                                                                           ##
###############################################################################
###############################################################################
'''
