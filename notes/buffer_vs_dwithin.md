## A word of caution regarding ST_Buffer

In class we looked at the use of `ST_Buffer` to derive new, larger geometries
on the basis of 1. a provided geometry/geography and 2. the distance from the
original geometry/geography of the buffer periphery. Given a point and a distance
of 500m, `ST_Buffer` should produce a circle whose diameter is 1000m.

In practice, `ST_Buffer` is rarely used due to performance limitations. When
attempting to find all the points within some distance of a geometry, if you
find yourself first building a buffered geometry and then checking to see if
the points in question happen to reside within it: you're doing it wrong.
Instead, you should take advantage of the comparison predicate PostGIS provides
for this very case: `ST_DWithin`. It is much faster.
