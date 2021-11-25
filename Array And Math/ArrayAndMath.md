### Array of Overlapping Ranges

Array A = [[1, 10], [5, 20], [7, 9], [23, 40]];         Array B = [[1, 10], [11, 20], [23, 40]];

Here A is an array of overlapping ranges. B is array of sorted non-overlapping ranges.
If we iterate over each point of each range in A,

time complexity = n*m,   n=sizeOfA  m=maxRangeLength

Same in B,

time complexity = m,    m=maxRangeLength

Converting A [asdf](https://render.githubusercontent.com/render/math?math={\rightarrow})
