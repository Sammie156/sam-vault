Same as [[Jarvis' March]], this algorithm finds the convex hull using *rotational sweeping*, processing vertices in the order of the polar angle they form with a reference vertex, basically their orientation(clockwise or counter-clockwise).

> [!NOTE] From GFG
> - The algorithm starts by finding the point with the smallest y-coordinate. This point is always on the convex hull. The algorithm then sorts the remaining points by their polar angle with respect to the starting point.
> - The algorithm then iteratively adds points to the *convex hull*. At each step, the algorithm checks whether the last two points added to the convex hull form a right turn. If they do, then the last point is removed from the convex hull. Otherwise, the next point in the sorted list is added to the convex hull.

## **ALGORITHM and WORKING**:
1. First, we find the lowermost point in the set of points, and assign that as $p_{0}$, basically the co-ordinate with the lowermost y-coordinate.
2. Then, we sort the rest of co-ordinates and store them as ${p_{1}, p_{2}, ... p_{n}}$, sorted by polar angle in counter-clockwise order around $p_{0}$.
3. Let $S$ be an empty stack.
4. Push $p_{0}$ into S.
5. Push $p_{1}$ into S.
6. Push $p_{2}$ into S.
7. for i = 3 to n:
   - While the angle formed by points Next to top(S) and Top(S) and $p_{i}$ makes a non-left turn(could be right, or co-linear): Pop S.
   - Push $p_{i}$ into S.
8. return S

#### **Program not added for now, as implementation is a bit complex**.

**Time Complexity**: $O(n\log n)$ 

