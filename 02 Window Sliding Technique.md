## Window Sliding Technique

This technique shows how a nested for loop in some problems can be converted to a single for loop to reduce the time complexity.
Let’s start with a problem for illustration where we can apply this technique – 

```
Given an array of integers of size ‘n’.
Our aim is to calculate the maximum sum of ‘k’ 
consecutive elements in the array.

Input  : arr[] = {100, 200, 300, 400}
         k = 2
Output : 700

Input  : arr[] = {1, 4, 2, 10, 23, 3, 1, 0, 20}
         k = 4 
Output : 39
We get maximum sum by adding subarray {4, 2, 10, 23}
of size 4.

Input  : arr[] = {2, 3}
         k = 3
Output : Invalid
There is no subarray of size 3 as size of whole
array is 2.
```

So, let’s analyze the problem with Brute Force Approach. We start with first index and sum till k-th element. We do it for all possible consecutive blocks or groups of k elements. This method requires nested for loop, the outer for loop starts with the starting element of the block of k elements and the inner or the nested loop will add up till the k-th element.

Consider the below implementation : 

```py

import sys
# O(n * k) solution for finding
# maximum sum of a subarray of size k
INT_MIN = -sys.maxsize - 1
 
# Returns maximum sum in a
# subarray of size k.
 
 
def maxSum(arr, n, k):
 
    # Initialize result
    max_sum = INT_MIN
 
    # Consider all blocks
    # starting with i.
    for i in range(n - k + 1):
        current_sum = 0
        for j in range(k):
            current_sum = current_sum + arr[i + j]
 
        # Update result if required.
        max_sum = max(current_sum, max_sum)
 
    return max_sum
 
 
# Driver code
arr = [1, 4, 2, 10, 2,
       3, 1, 0, 20]
k = 4
n = len(arr)
print(maxSum(arr, n, k))
 
 
```

It can be observed from the above code that the time complexity is O(k*n) as it contains two nested loops.


 > The technique can be best understood with the window pane in bus, consider a window of length n and the pane which is fixed in it of length k. Consider, initially the pane is at extreme left i.e., at 0 units from the left. Now, co-relate the window with array arr[] of size n and pane with current_sum of size k elements. Now, if we apply force on the window such that it moves a unit distance ahead. The pane will cover next k consecutive elements. 
Consider an array arr[] = {5, 2, -1, 0, 3} and value of k = 3 and n = 5

#### Applying sliding window technique : 

* We compute the sum of first k elements out of n terms using a linear loop and store the sum in variable window_sum.
* Then we will graze linearly over the array till it reaches the end and simultaneously keep track of maximum sum.
* To get the current sum of block of k elements just subtract the first element from the previous block and add the last element of the current block .
