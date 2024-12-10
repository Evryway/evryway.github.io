---
layout: post
title: Largest Interior Rectangle V2 - new and improved
category: DevBlog
tags: DevBlog
keywords: Largest Interior Rectangle Simple Polygon Implementation Unity3d Mathematics
---
Back in 2020, [I wrote a post][post_1] about implementing a solution to the problem
of finding the **axis aligned largest interior rectangle inside a simple polygon**. The code is available [here][the_repo]. 
A few kind folks provided bug reports, and one of the reports in particular, from 2023, poked a very large
hole in my flawed process for marking interior cells. I've had that bug on my todo list for over a year now,
but only recently found a few days to dig into it.

## The Flaw

My original implementation, referred to in [section 3.4 of the first post][post_1_section_3_4] describes a process
for marking cells as interior (completely contained within the polygon) or exterior (both completely outside, and
also cells that have polygon edges crossing them). The provided algorithm correctly marks cells that are being
crossed - but it incorrectly marks exterior cells as interior cells in certain cases, and that has some very
bad consequences for certain shapes of polygon.

Figure 1 shows this flaw in action. Some of the cells inside the blue "best fit" region have been incorrectly marked
as interior.


![Figure 1](/assets/images/lirv2/lirv2_flawed.png "Figure 1: I'm not certain, but I don't think that's completely inside the polygon."){:width="640px"}


## The improved implementation

The new algorithm starts out in the same way. We determine the unique Xs and Ys for all the vertices (with some
non-exact duplicate removal, based on an epsilon threshold). Using these, we build a cell grid - a 2D array of cells
for each X,Y point.

![Figure 2](/assets/images/lirv2/lirv2_cellarray.png "Figure 2: The cell array."){:width="640px"}

Using the cell array, we then test every polygon edge (the line from point Q to point Q+1 in the array of polygon
points) against the cells it can potentially cross. We retain information about whether the polygon edge crosses a cell,
touches a cell or straddles a cell.

Once we have all the crossing information for all polygon edges, we sweep the cell grid, from bottom to
top for all rows and then from left to right inside each row. We can determine if a cell is interior or exterior
to the polygon using the crossing information as described in more detail below.

![Figure 3](/assets/images/lirv2/lirv2_interiorcells.png "Figure 3: Interior cells."){:width="640px"}

## Cell crossing

Polygon edges can interact with cells in a few different ways. Firstly, it can miss a cell entirely, in which case that cell
is "inside" or "outside" the edge - but it may be crossed by any other cell, so the resulting cell state is unknown
until all other edges are tested.

Secondly, The edge can cross the cell - some portion of the polygon edge is inside the cell edges. In this case, the
polygon edge intersects two cell edges, or two cell points, or one cell point and one cell edge.

Thirdly, the edge can align with one of the cell edges (colinear) or touch a single point.

## Interior sweep

If we examine a horizontal row of cells, we know that the starting state at the boundary (before the first cell is examined) is
"exterior". We can then proceed with each cell in turn from left to right (moving positive X) and look to see if an edge
has crossed the cell.

If the cell is empty (has no crossings), then we mark it with the current state.

If the cell is crossed, then that cell is by definition not interior (because some part of the cell is outside the polygon)
but the next empty cell along should be the opposite of the current state. If the current state is exterior, then a single crossing
in the cell would make the next adjacent cell state interior.

If the cell is crossed more than once, then the next cell state would change state for each crossing. For example, if the
cell had two edges cross it and the current state is exterior, the next state would also be exterior. If three edges
crossed it, it would flip once more to interior.

![Figure 4a](/assets/images/lirv2/lirv2_sweep.png "Figure 4a: Cell state during sweep."){:width="640px"}

## Edge cases for the interior sweep

There are some edge cases (geometry joke, haha) which affect this simple view. Some are important, some have no effect on
the sweep.

If an edge touches a single point on a cell, it has no impact on the state of the next cell - by definition, the edge
has not crossed the cell.

If an edge is colinear with the top cell edge, or bottom cell edge, we can ignore it - we only care about horizontal
traversal, we don't care what's happening in rows above or below the current row.

If an edge is colinear with the right cell edge, we can ignore it, because we will deal with the same edge being
colinear with the left cell edge of the adjacent cell, and it cannot affect the current cell state.

If an edge is colinear with the left cell edge, we treat this as a crossing - and can immediately change the state
of the current cell, because the polygon edge is not inside the cell itself.

![Figure 4b](/assets/images/lirv2/lirv2_cellcross.png "Figure 4b: Types of cell crossing."){:width="640px"}

If an edge crosses a cell and intersects with the right cell edge, we class this as straddling the cells. This means
we cannot simply mark the next cell state as a new state, because at least some segment of the edge will be crossing
the next cell too. If the current state is exterior, then the next state will remain exterior, until the straddle
finishes, and the subsequent cell state can move from exterior to interior.

It should not be possible to have multiple cell left edge crossings in any single cell, as the input polygon would not
be a simple polygon in that case. However, the implementation attempts to cater for the case where multiple polygon
edges are colinear with a cell left edge by counting up and down crossings. If this is ever less than -1 or more than 1,
we cannot use the crossing data.

It is possible to have multiple edges cross, or straddle, single cells. By summing up the crossings, straddles and
left edges, we can determine if the next state is interior or exterior.

## Calculate the LIR

Given the correct state of interior and exterior cells, the algorithm can proceed to identify the best area using
the cell adjacency information and cell areas.

![Figure 5](/assets/images/lirv2/lirv2_working.png "Figure 5: Correct LIR."){:width="640px"}
![Figure 6](/assets/images/lirv2/lirv2_working2.png "Figure 6: Correct LIR for issue 6."){:width="640px"}
![Figure 7](/assets/images/lirv2/lirv2_working4.png "Figure 7: Correct LIR for issue 7."){:width="640px"}

## Conclusion

Thanks to all the folks who have reported issues so far, your feedback is much appreciated!

I'm certain there will be many more problems found - if you use the code and it doesn't work for you, make some noise.
I can't promise I'll fix it, but I'll certainly try.






[post_1]: https://evryway.com/largest-interior/
[post_1_section_3_4]: https://evryway.com/largest-interior/#step4

[the_repo]: https://github.com/Evryway/lir

