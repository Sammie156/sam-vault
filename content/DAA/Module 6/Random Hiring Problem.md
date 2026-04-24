**Problem**:
A company receives candidate scores in random order. The rules for selecting candidates are as follows:
- Hire candidate only if score is greater than all previously seen candidates.
- Organize candidates using randomized partitioning similar to Quick Sort.
To find the number of hires:
```python
HiringProblem(arr[], n):
	best <- -inf
	hire_count = 0
	
	for i = 1 to n:
		if A[i] > best:
			best <- A[i]
			hire_count++
	
	return hire_count
```

To compute the *time complexity* of this problem, we first consider a few base cases:
- The input is sorted in ascending order. In this case, everyone is hired as the next value will always be higher than the previous value. Hence, $O(n)$.
- The input is sorted in descending order. In this case, only the first candidate is hired as all the rest are lower than their score. Hence, $O(1)$.
Now if the input was randomized, then the calculation changes.

The first candidate is always hired. And then the probability changes as such:
$$E[hires] = 1 + \frac{1}{2} + \frac{1}{3}+\frac{1}{4}+...\frac{1}{n}$$
Which roughly evaluates to: $$E[hires] \approx \ln n$$
Thus we can calculate the chance of a candidate at `i` getting hired using the probability $\frac{1}{i}$ . 