### What is BIT?

Binary Indexed Tree or Fenwick Tree is a way to represent an array of numbers as an array of prefix Sum of the numbers. <br/>
Let us consider the following problem to understand Binary Indexed Tree.
<b> We have an array arr[0 . . . n-1]. We would like to </b>
1. Compute the sum of the first i elements i.e. [0, i]
2. Modify the value of a specified element of the array arr[i] = x where 0 <= i <= n-1.

A simple solution is to run a loop from 0 to i-1 and calculate the sum of the elements. To update a value, simply do arr[i] = x. 
The first operation takes <mark>O(n)</mark> time and the second operation takes <mark>O(1)</mark> time. 

Another simple solution is to create an extra array and store the sum of the first i-th elements at the i-th index in this new array. 
The sum of a given range can now be calculated in <mark>O(1)</mark> time, but the update operation takes <mark>O(n)</mark> time now.

The most efficient solution is to use a BIT which performs both operation in <mark>O(log n)</mark> time. Binary Indexed Tree is represented as an array. 
Let's see how a  BITree[] is constructed from an array arr[n] with an example.
arr[] = {2, 1, 1, 3, 2, 3, 4, 5, 6, 7, 8, 9}

1. If arr has size 12 BITree has size 13 as 0th index of BITree is dummy value;
2. Let's now check parent for each index. This can be calculated with formula index + (index & -index) where -index is 2's compliment of index. This can also be done by flipping the least significant set bit of the number.
     1 = 000<ins>1</ins> = 0000
     2 = 00<ins>1</ins>0 = 0000
     3 = 001<ins>1</ins> = 0010

This will result in a tree like this
<img width="652" alt="image" src="https://github.com/user-attachments/assets/6a6bc985-20ce-4bf4-9934-29d090e4b387">

Let's now get all the values for each index in BITree[]. This can be done by using the fact that each number can be represented as sum of
power of 2

1 = 0 + 2<sup>0</sup> (Starting from index 0 take next 2<sup>0</sup> elements i.e. 1 element)
2 = 0 + 2<sup>1</sup> (Starting from index 0 take next 2 element)
3 = 2<sup>1</sup> + 2<sup>0</sup> (Starting from index 2<sup>1</sup> i.e 2 take next 1 element)
11 = 2<sup>3</sup> + 2<sup>1</sup> + 2<sup>0</sup> (Starting from index 2<sup>3</sup> + 2<sup>1</sup> i.e 10 take next 1 element)

<img width="647" alt="image" src="https://github.com/user-attachments/assets/6085a1f8-1d6a-426f-bc64-9092e6633d08">









