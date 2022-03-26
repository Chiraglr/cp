### 1. Array of Overlapping Ranges

Array A = [[1, 10], [5, 20], [7, 9], [23, 40]];         Array B = [[1, 10], [11, 20], [23, 40]];

Here A is an array of overlapping ranges. B is array of sorted non-overlapping ranges.

If we iterate over each point of each range in A,

time complexity = n*m,   n=sizeOfA  m=maxRangeLength

Same in B,

time complexity = m,    m=maxRangeLength

Instead of updating each point ranging from i to j, we could just update index i with +S and index j + 1 with -S, where S is value. So if you want to know value at position k, you just need to find prefix sum of all the values from 0 to k.

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

### 3. Maximum Absolute Difference

You are given an array of N integers, A1, A2, …. AN.

Return the maximum value of f(i, j) for all 1 ≤ i, j ≤ N. f(i, j) is defined as |A[i] - A[j]| + |i - j|, where |x| denotes absolute value of x.

property: Say elements giving max value for f is at i,j index. Say A[i] > A[j] and i < j . We need to create an array rightMin where rightMin[x] gives the best element from x .. A.length which will give max val for f, given an appropriate point in 0 .. x-1. We create this array be starting from end of A and going left. As we go left, distance that is |i - j| will reduce so an element is considered better than last element of A if it's value is atleast lesser by the distance from end of A + 1. If we find that value we keep updating in rightMin else we use the previous. Similarly we create a leftMax. Using rightMin and leftMax we can get the max value of f where the left point is greater than the left one. We have to do similarly to get points where left point is less than the right one. We can then get the higher of the 2.

### 4. Maximum Consecutive Gap

Given an unsorted integer array A of size N.
Find the maximum difference between the successive elements in its sorted form.

property: min and max are the minimum and maximum elements of A respectively. Maximum Gap is possible when the only elements in A are min and max, so

maxGap = max - min

Also there are n elements, so the minimum possible gap is when the elements are evenly distributed, so

minGap = (max - min) / (N - 1);

So we should split elements into (N - 1) buckets with ranges [min, min + minGap], [min + minGap, min + 2*minGap], ... , [min + (N-2)*minGap, max];
In each bucket we have to find minBucket and maxBucket.

we know maxBucket - minBucket <= minGap. So no point searching inside a bucket. So naturally we have to search between buckets. Answer lies in comparing max of previous bucket with minBucket.

principle: In unsorted array A of size N, maximum difference between successive elements in A's sorted form cannot be less than minGap. So let's bucket elements with gap = minGap so that we don't have to check inside a bucket for the maximum difference between elements.

### 5. Repeating Number more than N/x of Array, for every x = 2, 3, 4, etc..

principle: Repeatedly remove x numbers from array. Numbers removed should be unique for a single removal. Once we can't find x unique numbers for removal, then the number satisfying above condition will be in these numbers. **So finally we have to iterate over original array and check.

problems: i) You're given a read only array of n integers. Find out if any integer occurs more than n/3 times in the array.

### 6. Get Minimum number of ranges from array of sorted ranges to cover entire range

priniple: Let minRange be the start of the range. Find the range covering largest area and enclosing the minRange. The large area occupied will help to reduce count of ranges required. Next consider point just 1 greater than the range occupied by previous range. Find the next range covering the largest area of uncovered range and enclosing new point. Keep repeating till entire range is covered and keep count of ranges.

problem: i) There is a corridor in a Jail which is N units long. Given an array A of size N. The ith index of this array is 0 if the light at ith position is faulty otherwise it is 1.

All the lights are of specific power B which if is placed at position X, it can light the corridor from [ X-B+1, X+B-1].

Initially all lights are off.

Return the minimum number of lights to be turned ON to light the whole corridor or -1 if the whole corridor cannot be lighted.

### 7. Max Distance

problem: Given an array A of integers, find the maximum of j - i subjected to the constraint of A[i] <= A[j].

principle: If max is given by (i,j), then there cannot be a (x,y) where x>i, y>j and A[x]>=A[i] as then this gives rise to a new max (i,y) which is a contradiction.

solution: Binary search is also used.
