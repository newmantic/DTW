# DTW


Dynamic Time Warping (DTW) is an algorithm used to measure the similarity between two temporal sequences, which may vary in time or speed. It finds an optimal alignment between the sequences by "warping" the time axis to minimize the distance between them.


A time series is a sequence of values measured at successive points in time. For example, X = (x_1, x_2, ..., x_n) and Y = (y_1, y_2, ..., y_m) are two time series of length n and m, respectively.

The Euclidean distance between two points x_i and y_j is given by:
d(x_i, y_j) = |x_i - y_j|

If we align X and Y without any warping, the distance between the two sequences is simply the sum of the Euclidean distances between corresponding points:
D(X, Y) = sum_{i=1}^n |x_i - y_i|
However, this direct alignment may not be meaningful if the sequences differ in speed or timing.

Warping:
To align sequences of different lengths or those that have different speeds, we "warp" the time axis of one sequence to match the other. Warping allows non-linear alignment, meaning that a single point in one sequence can be matched to multiple points in the other.

DTW computes the optimal alignment between two sequences by minimizing the overall distance after warping. The DTW distance is the minimum cumulative cost required to align the two sequences.

Cost Matrix:
We construct an n x m cost matrix D, where D(i, j) represents the cumulative cost of aligning x_1, ..., x_i with y_1, ..., y_j.
The cost at each position (i, j) is calculated as:
D(i, j) = |x_i - y_j| + min(D(i-1, j), D(i, j-1), D(i-1, j-1))
The first row and first column are initialized to infinity (except D(0, 0) = 0) to avoid boundary issues.

Boundary Conditions:
The first cell, D(1, 1), is simply the Euclidean distance between the first points of the two sequences:
D(1, 1) = |x_1 - y_1|

Optimal Path:
The optimal warping path is found by backtracking from D(n, m) to D(1, 1), selecting the cell with the minimum cumulative cost at each step.

DTW Distance:
The DTW distance is the value in the bottom-right cell of the cost matrix:
DTW(X, Y) = D(n, m)

