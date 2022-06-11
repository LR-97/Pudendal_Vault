# Bezier.py
## What is this script for?
This script essentially upsamples a given trajectory, described as a list of 3D points, by approximating it as a [Bezier curve](https://en.wikipedia.org/wiki/B%C3%A9zier_curve). It takes as input a trajectory, P, and a variable for parametrizing, t, that ranges from 0 to 1. The number of values in t is equal to the number of points to be approximated. The script generates the parametrized Bezier curve approximation as a linear sum of [Bernstein basis polynomials](https://en.wikipedia.org/wiki/Bernstein_polynomial) weighted by the control points.

## Dependencies
- numpy
- factorial from math

## Functions
### Bezier
-  **Parameters**
	- *P:* List of 3D points describing a trajectory, also serve as control points for the approximation
	- *t:* Evenly spaced values calculated over the interval [0, 1]
- **Description**
	- Evaluates Bezier curve approximation of a trajectory *P* as a function of *t*. Can be thought of as an upsampling of the trajectory. Mathematically, this function evalutes the following equation:
		- **$B(t)=\sum_{j=0}^{n} P_j b_{j,n}(t), t \in [0,1]$**
- **Outputs**
	- *Q:* List of 3D points describing the computed Bezier approximation

- **Step-by-Step**
	- Initialize *Q* as a zeros array of size (*Len( t ),  3*)
	- **For each evaluation point *k* in t:**
		- **For each Bernstein Basis Polynomial for a Bernstein Polynomial of degree n:**
			- *Note: the degree of the polynomial is set by the number of control points. A polynomial of degree n has n+1 basis polynomials*
			- Sum the current polynomial basis (the jth polynomial basis) weighted by jth control point to the approximation at evaluation point k
				- The Bernstein polynomial basis is computed using the [[Bezier.py#Bernstein|Bernstein function]].
	- Return *Q*, the Bezier curve approximation of the trajectory *P*

### Bernstein
-  **Parameters**
	- *n:* Degree of the Bernstein polynomial
	- *j:* integer belonging to (0, ..., n), corresponds to the basis being evaluated
	- *t:* the current evaluation point
- **Description**
	- Given n and j, calculates the respective Bernstein basis polynomial and evaluates it at the provided t.
-  **Outputs**
	- *B:* Respective Bernstein basis evaluated at *t*

- **Step-by-Step**
	- Evaluate the basis polynomial using the following equation:
		- **$b_{j,n}(t) = \begin{pmatrix} n\\ j \end{pmatrix} t^j (1-t)^{n-j}$**
			- Where $\begin{pmatrix} n\\ j \end{pmatrix}$ is a [binomial coefficient](https://en.wikipedia.org/wiki/Binomial_coefficient)
		- Return $b_{j,n}(t)$

## Tags
#complete #axonTrajectories 

## Suggestions for improvement
- The bezier function uses nested for loops. It may be possible to improve performance if mathematical operations are conducted in matrix forms instead. 



