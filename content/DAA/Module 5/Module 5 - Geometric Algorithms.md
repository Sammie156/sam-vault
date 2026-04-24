## **Line Segment Properties**:
- For any two points $p_{1} = (x_{1}, y_{1})$ and $p_{2}=(x_{2}, y_{2})$ , the convex combination is any point $p_{3}=(x_{3}, y_{3})$ such that for some $\alpha$ in the range $0\leq \alpha \leq 1$ , we have $p_{3}=\alpha p_{1} + (1-\alpha)p_{2}$ 
- Intuitively, it is any point that lies on the line segment joining $p_{1}$ and $p_{2}$ .
- Cross product of two points can be defined as the area of the parallelogram formed by the points $(0, 0),\space p_{1}, \space p_{2}$ and $p_{1}+p_{2}$ . 
  ![[Pasted image 20260423191247.png]]
- Another definition of cross product would be:$$p_{1} \times p_{2} = \det\begin{pmatrix}x1&x2 \\ y1&y2\end{pmatrix}$$Thus, the value is:
$$p_{1}\times p_{2} = x_{1}y_{2}-x_{2}y_{1}$$

### **Determining whether two consecutive segments turn left or right**:
To check whether the segment $\overrightarrow{p_{0}p_{2}}$ is clockwise or counter-clockwise with respect to the segment $\overrightarrow{p_{0}p_{1}}$ :
- First, we compute the cross product: $(p_{2} - p_{0})\times(p_{1}-p_{0})$ .
- If the sign of this cross product is negative, then $p_{0}p_{2}$ is counterclockwise and thus we need to make a left turn.
THUS:
- *A positive cross product depicts a clockwise orientation and a right turn*
- *A cross product of 0 means that the points are co-linear*

Using this, we can determine whether two segments intersect each other or not.
Check [[Line Segment Intersection]].
## **Convex Hull**:
Convex Hull of a set of points Q is the smallest convex polygon P for which each point of Q lies either on the boundary or inside of the polygon.
It is the smallest set from Q, with the minimum perimeter.
![[Pasted image 20260423233928.png]]
There are 2 algorithms by which we can compute the Convex Hull of Q:
- [[Graham's Scan]]
- [[Jarvis' March]]
