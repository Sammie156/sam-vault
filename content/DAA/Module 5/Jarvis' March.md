This algorithm is also known as *Gift Wrapping Algorithm*.
It works by wrapping points like a rubber band, finding the convex hull using the points at the boundary.

> [!NOTE] From GFG:
> The idea of Jarvis's Algorithm is simple, we start from the leftmost point (or point with minimum x coordinate value) and we keep wrapping points in counterclockwise direction.

How do find the next point? We use the `Direction()` from [[Line Segment Intersection]] to determine the orientation. We use it as such:
*The next point is `q` if for any other point `r`, the value of `Direction(p, q, r)` is Counter-Clockwise.*

## **ALGORITHM and WORKING**:
1. Initialize `p` as the leftmost point, i.e., with the least `x` co-ordinate value.
2. Do the following, until we come back to the first point:
   - The next point is q, such that the triplet `(p, q, r)` is counter-clockwise for any other point `r`.
   - Simply, initialize `q` as the next point, and then traverse through all points.
   - For any point `i`, if `i` is more counter-clockwise, i.e., `Direction(p, i, q)` is counter-clockwise, then update `q` as `i`.
   - Our final value of `q` is the most counter-clockwise point `p`.
   - Store `q` as the next point in our convex-hull. 
   - `p = q`, update `p` for the next iteration.

*Pseudocode*:
```python
JarvisMarch(points):
	n = number of points
	if n < 3:
		return "Convex Hull not possible"
	
	hull = []
	
	l = index of point with minimum x co-ordinate
	
	p = l
	repeat until p == l:
		add points[p] to hull
		
		q = (p + 1) mod n
		
		for i from 0 to n-1:
			if direction(points[p], points[i], points[q]) == COUNTER:
				q = i
		p = q
	
	return hull

direction(p, q, r):
	cross = (q.y - p.y)*(r.x - q.x) - (q.x - p.x)*(r.y - q.y)
	
	if cross < 0: return COUNTER
	elif cross > 0: return CLOCK
	else return COLLINEAR
```

### **Program Implementation**:
```cpp
#include <iostream>
#include <vector>

inline int min(int a, int b) {
    return (a < b)? a : b;
}

inline int max(int a, int b) {
    return (a > b)? a : b;
}

typedef struct Point {
    int x;
    int y;
}Point;

int orientation(Point a, Point b, Point c) {
    int cross = (b.y - a.y)*(c.x - b.x) - (b.x - a.x)*(c.y - b.y);

    if (cross < 0) return 2;
    else if (cross > 0) return 1;
    else return 0;
}

std::vector<Point> jarvis_march(std::vector<Point> points) {
    int n = points.size();
    std::vector<Point> hull;

    if (n < 3) {
        std::cout << "Convex Hull not possible" << std::endl;
        return hull;
    }

    int l = 0;
    for (int i = 1; i < n; i++) {
        if (points[i].x < points[l].x) l = i;
    }

    int p = l, q;
    do {
        hull.push_back(points[p]);

        q = (p + 1) % n;
        for (int i = 0; i < n; i++) {
            if (orientation(points[p], points[i], points[q]) == 2) {
                q = i;
            }
        }

        p = q;
    } while (p != l);

    return hull;
}

int main(int argc, const char* argv[]) {
    int n;
    std::cout << "Enter number of points: ";
    std::cin >> n;

    std::vector<Point> points;

    for (int i = 0; i < n; i++) {
        int x, y;
        std::cin >> x >> y;

        Point point = {x, y};

        points.push_back(point);
    }

    std::vector<Point> hull = jarvis_march(points);

    for (int i = 0; i < hull.size(); i++) {
        std::cout << "(" << hull[i].x << "," << hull[i].y << ")" << std::endl;
    }
}
```

**Time Complexity**: $O(n*h)$ , where $n$ is the number of points and $h$ is the number of points in the convex hull.
**Worst Case**: $O(n^{2})$ when all the points are part of the convex hull.

### *Applications*:
- Computer Graphics
- Image Processing
- Robotics Path Planning
### *Advantages*:
- Simple to understand and implement
- No sorting required
- Works well for small datasets
### *Disadvantages*:
- Works poorly on large datasets
- Time increases with hull points
