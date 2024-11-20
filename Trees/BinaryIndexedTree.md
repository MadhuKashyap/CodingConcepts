### What is BIT?

Binary Indexed Tree or Fenwick Tree is a way to represent an array of numbers as an array of prefix Sum of the numbers. <br>
Let us consider the following problem to understand Binary Indexed Tree.
<b> We have an array arr[0 . . . n-1]. We would like to </b>
1. Compute the sum of the first i elements i.e. [0, i]
2. Modify the value of a specified element of the array arr[i] = x where 0 <= i <= n-1.

A simple solution is to run a loop from 0 to i-1 and calculate the sum of the elements. To update a value, simply do arr[i] = x. 
The first operation takes O(n) time and the second operation takes O(1) time. 

Another simple solution is to create an extra array and store the sum of the first i-th elements at the i-th index in this new array. 
The sum of a given range can now be calculated in O(1) time, but the update operation takes O(n) time now.

The most efficient solution is to use a BIT which performs both operation in O(log n) time
