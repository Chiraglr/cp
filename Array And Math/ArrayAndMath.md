### 1. Array of Overlapping Ranges

Array A = [[1, 10], [5, 20], [7, 9], [23, 40]];         Array B = [[1, 10], [11, 20], [23, 40]];

Here A is an array of overlapping ranges. B is array of sorted non-overlapping ranges.

If we iterate over each point of each range in A,

time complexity = n*m,   n=sizeOfA  m=maxRangeLength

Same in B,

time complexity = m,    m=maxRangeLength

Algorithm to convert ![asdf](https://render.githubusercontent.com/render/math?math=A{\rightarrow}B),
1. Sort using this function,
  ```
  func cmp(a, b) {
    if(a[0] < b[0])
      return true;
    if(a[0] > b[0])
      return false;
    if(a[1] < b[1])
      return true;
    return false;
  }
  ```
2. Result array will contain sorted overlapping ranges. Now we have to merge/divide overlapping ranges. Final array will contain sorted non-overlapping ranges.

time complexity is ![asdf](https://render.githubusercontent.com/render/math?math={\mathcal{O}(n\log{}n)}) ,

Finally time complexity to convert and iterate over ranges is ![asdf](https://render.githubusercontent.com/render/math?math={\large \mathcal{O}(n\log{}n)%2Bm})
