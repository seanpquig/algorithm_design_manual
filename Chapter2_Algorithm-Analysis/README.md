Chapter 2 - Algorithm Analysis
===

- Algorithms need a way to be tested an compared in a machine and language-independent manner.
- The two most important tools for this are:
	1. the RAM model of compuatation
	2. Asymtotic analysis of worst-case complexity

###The RAM Model of Computation
- model characteristics
	1. Each simple operation (+, *, -, =, if, call) takes exactly one time step.
	2. Loops and subroutines are a composition of simple operations.
	3. Each memory access takes exactly one time step.  There is no notice of whether an item is in cache or on disk.

- while not a perfect repersentation of a real computer, this is still an *excellent* tool for understanding algorithm performance on a real computer.

###The Big Oh Notation
- the formal definitions associated with Big Oh notation:
	- `f(n) = O(g(n))` means `c * g(n)` is an *upper bound* on `f(n)`.  There exists some constant *c* such that `f(n)` is always `<= c * g(n)`, for all `n >= n_0` for some constant *n_0*.
	- `f(n) = Ω(g(n))` means `c * g(n)` is an *lower bound* on `f(n)`.  There exists some constant *c* such that `f(n)` is always `>= c * g(n)`, for all `n >= n_0` for some constant *n_0*.
	- `f(n) = θ(g(n))` means `c_1 * g(n)` is an upper bound on `f(n)` and `c_2 * g(n)` is a lower bound on `f(n)`, for `n >= n_0`.  This means `g(n)` provides a nice, tight bound on `f(n)`.

###Dominance Relations
- Common function classes listed in order of increasing dominance in running time
	- *Constant functions*
	- *Logarithmic functions*
	- *Linear functions*
	- *Superlinear functions*
	- *Quadratic functions*
	- *Cubic functions*
	- *Exponential functions*
	- *Factorial functions*
- `n! >> 2^n >> n^3 >> n^2 >> n log(n) >> n >> log(n) >> 1`

###Selection Sort
in Python:

	def selection_sort(list_s, len_s):
    	for i in xrange(len_s):
        	min_i = i
        	for j in xrange(i+1, len_s):
            	if list_s[j] < list_s[min_i]:
                	min_i = j
        	list_s[i], list_s[min_i] = list_s[min_i], list_s[i]
        	
- Selection sort is quadtratic: `θ(n^2)`


###Insertion Sort
in Python:

    def insertion_sort(list_s, len_s):
        for i in xrange(1, len_s):
            j = i
            while j > 0 and (list_s[j] < list_s[j-1]):
                list_s[j-1], list_s[j] = list_s[j], list_s[j-1]
                j -= 1

- Insertion sort is quadtratic: `θ(n^2)`

###String Pattern Matching
- *Problem*: Substring Pattern Matching
- *Input*: A text string t and a pattern string p.
- *Output*: Does t contain the pattern p as a substring, and if so where?

in Python:

	def findmatch(p, t):
    	m = len(p)
    	n = len(t)

    	for i in xrange(n-m+1):
        	j = 0
        	while (j < m) and (t[i+j] == p[j]):
            	j += 1
            	if j == m:
                	return i

        return -1

- This algorithm is `O(nm)` where n is length of the text and m is the length of the pattern to find.


###Matrix Multiplication
- *Problem*: Matrix Multiplication
- *Input*: Two matrices, A (dim x * y) and B (dim y * z)
- *Output*: Matrix C (dim x * z) where C[i][j] is dot product of the *ith* row of A and the *jth* column of B.`

in Python:

	def multiply(A, B):
        """
        A of dimension x * y
        B of dimension y * z
        return C of dimension x * z
        """
        x = len(A)
        y = len(A[0])
        z = len(B[0])
        assert(y == len(B))

        C = [r[:] for r in [[0] * z] * x]

        for i in xrange(x):
            for j in xrange(z):
                for k in xrange(y):
                    C[i][j] += (A[i][k] * B[k][j])

        return C

- This algorithm is `O(xyx)` or `O(n^3)` assuming all three dimensions are the same.

###Logarithms and Their Applications
- binary search is an example for an `O(log(n))` algorithm.
- the height of a binary search tree grows logarithmically with the number of leaf nodes.
	- because of this they are fundamental to the design of fast data structures.
- the number of bits needed to represent *n* unique items grows logarithmically with *n*.
- `log(x * y) = log(x) + log(y)`
- logarithms and exponents arise whenever things are repeatedly halved or doubled.

###Logarithms and Their Applications
- The base of a logarithm has not real impact on its growth rate.
	- because logs can simply be converted by others with a constant factor.
- Logarithms cut functions down to size.
	- the growth rate of the log of any polynomial function is `O(lg(n)))` because the exponent gets pulled out as a constant multiplicative factor.

###Advanced Analyisis (*)
- **esoteric functions:**
	- *Inverse Ackermann's function*
	- `log(log(n))`
	- `log(n)/log(log(n))`
	- `log(n)^2`
	- *Subliner Polynomials* like square root of *n*.
	- `n ^ (1 + ϵ)` where *ϵ* is arbitrarily small.