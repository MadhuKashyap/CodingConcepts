### If a question falls in the sliding window category
**Pattern** : Best/worst subarray/substring under some conditions like **distinct count, sum >= k, distinct frequency etc, containsAll**. <br/>
**How to solve** : Maintain a window [l, r) that’s either valid or minimal valid. Expand r to approach validity; shrink l to restore minimality.<br/>
**Time Complexity** : O(n)
 
