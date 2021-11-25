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

Finally time complexity to convert and iterate over ranges is ![asdf](https://render.githubusercontent.com/render/math?math={\mathcal{O}(n\log{}n)%2Bm})

### 2. Rain Water Trapping

e.g. input = [0, 1, 0, 0, 2, 0, 1, 5];
     output = 5;

    input array contains, non-negative integers representing an elevation map where the width of each bar is 1. Compute amount of water trapped after raining.

First step is to figure out properties of rain:
<img width="1065" alt="Screenshot 2021-11-25 at 9 29 37 PM" src="https://user-images.githubusercontent.com/29271117/143472771-1a6a24af-e232-4806-9ffa-74092ce29900.png">


