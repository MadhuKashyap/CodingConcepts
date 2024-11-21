### What is BIT?

Binary Indexed Tree or Fenwick Tree is a way to represent an array of numbers as an array of prefix Sum of the numbers. <br/>
Let us consider the following problem to understand Binary Indexed Tree.
<b> We have an array arr[0 . . . n-1]. We would like to </b>
1. Compute the sum of the first i elements i.e. [0, i]
2. Modify the value of a specified element of the array arr[i] += x where 0 <= i <= n-1.

A simple solution is to run a loop from 0 to i-1 and calculate the sum of the elements. To update a value, simply do arr[i] = x. 
The first operation takes <mark>O(n)</mark> time and the second operation takes <mark>O(1)</mark> time. 

Another simple solution is to create an extra array and store the sum of the first i-th elements at the i-th index in this new array. 
The sum of a given range can now be calculated in <mark>O(1)</mark> time, but the update operation takes <mark>O(n)</mark> time now.

The most efficient solution is to use a BIT which performs both operation in <mark>O(log n)</mark> time. Binary Indexed Tree is represented as an array. 
Let's see how a  BITree[] is constructed from an array arr[n] with an example.
arr[] = {2, 1, 1, 3, 2, 3, 4, 5, 6, 7, 8, 9}

1. If arr has size 12 BITree has size 13 as 0th index of BITree is dummy value;
2. Let's now check parent for each index. This can be calculated with formula index + (index & -index) where -index is 2's compliment of index. This can also be done by flipping the least significant set bit of the number.<br/>
     1 = 000<ins>1</ins> = 0000<br/>
     2 = 00<ins>1</ins>0 = 0000<br/>
     3 = 001<ins>1</ins> = 0010<br/>

This will result in a tree like this
<img width="652" alt="image" src="https://github.com/user-attachments/assets/6a6bc985-20ce-4bf4-9934-29d090e4b387">

Let's now get all the values for each index in BITree[]. This can be done by using the fact that each number can be represented as sum of
power of 2<br/>

1 = 0 + 2<sup>0</sup> (Starting from index 0 take next 2<sup>0</sup> elements i.e. 1 element)<br/>
2 = 0 + 2<sup>1</sup> (Starting from index 0 take next 2 element)<br/>
3 = 2<sup>1</sup> + 2<sup>0</sup> (Starting from index 2<sup>1</sup> i.e 2 take next 1 element)<br/>
11 = 2<sup>3</sup> + 2<sup>1</sup> + 2<sup>0</sup> (Starting from index 2<sup>3</sup> + 2<sup>1</sup> i.e 10 take next 1 element)<br/>

<img width="644" alt="image" src="https://github.com/user-attachments/assets/cbf4fa2e-3105-4a90-b2e2-3e88abb64b02">


Now let's see how both operations i.e. getSum(x) and update(x, value) work on BITree.

<ins>pseudo code for getSum(x)</ins> :

<b>getSum(x) : Returns the sum of the sub-array arr[0,…,x].</b>
1. Initialize the output sum as 0, the current index as x+1. 
2. Do following while the current index is greater than 0. <br/>
     a. Add BITree[index] to sum <br/>
     b. Go to the parent of BITree[index]. The parent can be obtained by altering the last set bit from the current index, i.e., index = index – (index & (-index)) 
3. Return sum.

In array arr[] = {2, 1, 1, 3, 2, 3, 4, 5, 6, 7, 8, 9} we want to perform getSum(6) i.e. get the sum of [0, 6] :

1. Start from index x + 1 i.e. 7. It has value 4 and covers range (6, 6).
2. Go to parent of 7 i.e. 6. It has a value 5 and covers range (4, 5).
3. Go to parent of 6 i.e. 4. It has value 7 and covers range (0, 3).
4. Thus we covered the entire range (0, 6).


<ins> pseudo code for update(x, value) </ins> : 
<b> update(x, val): Updates the Binary Indexed Tree (BIT) by performing arr[index] += val </b>

1. Initialize the current index as x+1. 
2. Do the following while the current index is smaller than or equal to n. <br/>
     a. Add the val to BITree[index] <br/>
     b. Go to next element of BITree[index]. The next element can be obtained by incrementing the last set bit of the current index, i.e., index = index + (index & (-index))

In array arr[] = {2, 1, 1, 3, 2, 3, 4, 5, 6, 7, 8, 9} we want to perform update(6, 3) :

1. current index = 7, add 3 at index 7 in BITree[]. This covers range (6,6)
2. Next element of 7 is 7 + (7 & -7) i.e. 8. So add 3 at index 3. This covers range (0,7).
3. Next of 8 is 8 + (8 & -8) i.e. 16 which is out of range so we stop here.

Below is the coding implementation of BITree

```
import java.util.*; 
import java.lang.*; 
import java.io.*; 

class BinaryIndexedTree 
{ 
	// Max tree size 
	final static int MAX = 1000;	 

	static int BITree[] = new int[MAX]; 
	
	/* n --> No. of elements present in input array. 
	BITree[0..n] --> Array that represents Binary 
					Indexed Tree. 
	arr[0..n-1] --> Input array for which prefix sum 
					is evaluated. */

	// Returns sum of arr[0..index].
	int getSum(int index) 
	{ 
		int sum = 0;
	
		// index in BITree[] is 1 more than the index in arr[] 
		index = index + 1; 
	
		// Traverse ancestors of BITree[index] 
		while(index>0) 
		{ 
			// Add current element of BITree to sum 
			sum += BITree[index]; 
	
			// Move index to parent node 
			index -= index & (-index); 
		} 
		return sum; 
	} 

	// Updates a node in Binary Index Tree (BITree) 
	// at given index in BITree. The given value 
	// 'val' is added to BITree[i] and all of 
	// its ancestors in tree. 
	public static void updateBIT(int n, int index, int val) 
	{ 
		// index in BITree[] is 1 more than 
		// the index in arr[] 
		index = index + 1; 
	
		// Traverse all ancestors and add 'val' 
		while(index <= n) 
		{ 
		// Add 'val' to current node of BIT Tree 
		BITree[index] += val; 
	
		// Update index to that of parent 
		// in update View 
		index += index & (-index); 
		} 
	} 

	void constructBITree(int arr[], int n) 
	{ 
		for(int i=1; i<=n; i++) 
			BITree[i] = 0; 
	
		// Store the actual values in BITree[] using update() 
		for(int i = 0; i < n; i++) 
			updateBIT(n, i, arr[i]); 
	} 

	public static void main(String args[]) 
	{ 
		int freq[] = {2, 1, 1, 3, 2, 3, 
					4, 5, 6, 7, 8, 9}; 
		int n = freq.length; 
		BinaryIndexedTree tree = new BinaryIndexedTree(); 

		tree.constructBITree(freq, n); 

		System.out.println("Sum of elements in arr[0..5]"+ " is "+ tree.getSum(5)); 
		freq[3] += 6; 
		
		// Update BIT for above change in arr[] 
		updateBIT(n, 3, 6); 

		// Find sum after the value is updated 
		System.out.println("Sum of elements in arr[0..5]"+ " after update is " + tree.getSum(5)); 
	} 
} 
```





