Using this algorithm, we can check whether two line segments intersect each other or not.

To check if a line segment $\overrightarrow{p_{0}p_{1}}$ intersects another line segment, we need to check whether it *straddles* the line containing the other points.
A line segment straddles a line segment if one point of the line lies on one side, while the other point lies on the other side.

*Conditions*:
- Each segment straddles the line containing the other.
- An endpoint of one segment lies on the other segment. (This comes under the boundary case)
*General Case*:
- If $(p_{1}, q_{1}, p_{2})$ and $(p_{1}, q_{1}, q_{2})$ have different orientations.
- If $(p_{2}, q_{2}, p_{1})$ and $(p_{2}, q_{2}, q_{1})$ have different orientations.

## **ALGORITHM and WORKING**:
- First, we define a function `SegmentsIntersect` that takes in the four points and return true if $\overrightarrow{p_{1}q_{1}}$ intersects the segment $\overrightarrow{p_{2}q_{2}}$. 
- This function calls the two functions: `Direction` which determines the relative orientation of one segment using the cross product method in [[Module 5 - Geometric Algorithms#**Determining whether two consecutive segments turn left or right**]], and also `On-Segment` which determines whether a point is known to be co-linear with the segment.

*Pseudocode*:
```python
SegmentIntersect(p1, p2, p3, p4):
	d1 = Direction(p3, p4, p1)
	d2 = Direction(p3, p4, p2)
	d3 = Direction(p1, p2, p3)
	d4 = Direction(p1, p2, p4)
	
	if ((d1 > 0 and d2 < 0) or (d1 < 0 and d2 > 0))
	and ((d3 > 0 and d4 < 0) or (d3 < 0 and d4 > 0)):
		return True
	elif d1 == 0 and OnSegment(p3, p4, p1):
		return True
	elif d2 == 0 and OnSegment(p3, p4, p2):
		return True
	elif d3 == 0 and OnSegment(p1, p2, p3):
		return True
	elif d4 == 0 and OnSegment(p1, p2, p4):
		return True
	return False

Direction(pi, pj, pk):
	return (pk - pi) X (pj - pi) # Cross Product

OnSegment(pi, pj, pk):
	if min(xi, xj) <= xk <= max(xi, xj) and
	min(yi, yj) <= yk <= max(yi, yj):
		return True
	return False
```

### *NOTES*:
- The value returned by `Direction()` determines the orientation of the line with respect to another point.
- If the value returned is positive, then the orientation is clockwise. Otherwise, the orientation is counter-clockwise.
- If the value returned is 0, then the points are co-linear.
