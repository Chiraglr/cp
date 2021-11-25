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

2. The first wall after the leftmost wall satisfying conditions

i) height ![asdf](https://render.githubusercontent.com/render/math?math={\ge}) leftmost wall

ii) height ![asdf](https://render.githubusercontent.com/render/math?math={>}) height of bar to it's left

If such a bar exists, then we can simplify problem. For array A if bar is at index r, then

total rain trapped = rain trapped b/w leftmost wall and bar![asdf](https://render.githubusercontent.com/render/math?math={%2B}) rain trapped in A[r ... ]

rain trapped b/w leftmost wall and bar = sum of (leftmost wall height - H), ![asdf](https://render.githubusercontent.com/render/math?math={\forall}H) from leftmost wall to the bar;

![image](https://user-images.githubusercontent.com/29271117/143490392-ce492ee8-6d14-4a41-b75a-1bee5e3ff70f.png)

after rain is filled b/w them, then the rain trapped is like a bar. On treating the trapped rain as a bar, we will get a new leftmost block. Hence the above equations are valid.

3. let l = height of leftmost wall,
let w = [ l ];

let's iterate from the leftmost wall till we find a bar satisfying 2nd property. For each sequence that is increasing,

i) find the tallest bar in the sequence,

ii) if bar is not taller then last element of w, then push it's index. Else keep popping elements in w from last till an element![asdf](https://render.githubusercontent.com/render/math?math={>})height of current bar is found, then push it's index. Do this till bar satisfying 2nd property is found. In final array, there is water trapped between consecutive bars in the array so we can calculate.

Applying above properties, following is the algo,
 popping elements from last and pushing to last means stack should be used.
 
 ```
 var l = index of leftmost wall;
 var i = l + 1;
 var result = 0;
 stack b = [ l ];
 while(i < A.length) {
   while(i < A.length && A[i] <= A[i-1])
     i++;
   if(i==A.length)
     break;
   while(i < A.length && A[i] >= A[i-1])
     i++;
   i--;
   while(b.length > 1 && b[b.length -1] <= A[i]) {
     b.pop();
   }
   b.push(i);
   if(A[i] >= b[0]) {
     result += getRainTrapped(b, A);
     l = i;
     b = [ l ];
   }
   i++;
 }
 result += getRainTrapped(b, A);
 ```



