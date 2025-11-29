### This “template” is a general sliding window + hashmap/array approach for solving a lot of substring problems (like "minimum window substring", "longest substring without repeating characters", "longest substring with at most k distinct characters", etc.). 
###  Steps to solve : 
1. Use two pointers (begin / end or start / end) to represent the current window in the string.
2. Use a map or fixed-size array to store character counts inside that window.
3. Keep a counter to track when your current window meets the problem’s condition (e.g., contains all required characters).
4. Move end to expand the window until it becomes valid.
5. Move begin to shrink the window when you can, to either find a smaller valid window (for min problems) or drop extra characters (for max problems).
6. The key difference between min and max problems:
   6.1. Minimum substring: update the answer inside the inner loop (while shrinking) because you only want valid, smallest windows.
   6.2. Maximum substring: update the answer after the inner loop because you want the largest valid window.


### Example questions

#### 1️⃣ Minimum Window Substring
```
public String minWindow(String s, String t) {
    int[] map = new int[128]; // ASCII char frequency
    for (char c : t.toCharArray()) {
        map[c]++; // store needed char count
    }

    int start = 0, end = 0, minStart = 0;
    int minLen = Integer.MAX_VALUE;
    int counter = t.length(); // how many chars still needed

    while (end < s.length()) {
        char cEnd = s.charAt(end);
        if (map[cEnd] > 0) counter--; // char is needed
        map[cEnd]--; // decrease count (may go negative if extra char)
        end++;

        while (counter == 0) { // valid window
            if (end - start < minLen) {
                minLen = end - start;
                minStart = start;
            }

            char cStart = s.charAt(start);
            map[cStart]++;
            if (map[cStart] > 0) counter++; // lost a needed char
            start++;
        }
    }

    return minLen == Integer.MAX_VALUE ? "" : s.substring(minStart, minStart + minLen);
}
```
#### 2️⃣ Longest Substring Without Repeating Characters
```
public int lengthOfLongestSubstring(String s) {
    int[] map = new int[128]; // count occurrences of chars
    int start = 0, end = 0, counter = 0, maxLen = 0;

    while (end < s.length()) {
        char cEnd = s.charAt(end);
        if (map[cEnd] > 0) counter++; // duplicate found
        map[cEnd]++;
        end++;

        while (counter > 0) { // remove duplicates
            char cStart = s.charAt(start);
            if (map[cStart] > 1) counter--;
            map[cStart]--;
            start++;
        }

        maxLen = Math.max(maxLen, end - start);
    }

    return maxLen;
}
```
#### 3️⃣ Longest Substring With At Most K Distinct Characters
```
public int lengthOfLongestSubstringKDistinct(String s, int k) {
    int[] map = new int[128];
    int start = 0, end = 0, counter = 0, maxLen = 0;

    while (end < s.length()) {
        char cEnd = s.charAt(end);
        if (map[cEnd] == 0) counter++; // new distinct char
        map[cEnd]++;
        end++;

        while (counter > k) { // too many distinct chars
            char cStart = s.charAt(start);
            if (map[cStart] == 1) counter--; // removing a distinct char
            map[cStart]--;
            start++;
        }

        maxLen = Math.max(maxLen, end - start);
    }

    return maxLen;
}
```

### Other similar questions

🔹 Minimum-type problems

(✅ Update result inside the inner loop while shrinking)

Minimum Window Substring
Given s and t, find the smallest substring of s containing all characters of t.
(Classic example we already did)

Smallest Substring with All Distinct Characters of String
Given a string s, find the smallest substring that contains all distinct characters present in s.

Minimum Size Subarray Sum
Given an array of positive integers and a number target, find the minimal length of a contiguous subarray whose sum ≥ target.
(Instead of char counts, your “counter” is sum comparison)

Minimum Window Subsequence
Given strings S and T, find the minimum window in S which contains T in sequence order (not necessarily contiguous).
(Trickier but still fits template with slight adjustments)

🔹 Maximum-type problems

(✅ Update result outside the inner loop after shrinking)

Longest Substring Without Repeating Characters
Find the length of the longest substring without repeating characters.
(We already did this)

Longest Substring With At Most K Distinct Characters
Find the length of the longest substring that contains at most k distinct characters.
(We also did this)

Longest Substring With At Least K Distinct Characters
Similar to #6, but must have at least k distinct characters.

Longest Substring with Exactly K Distinct Characters
Trick: Solve atMostK - atMost(K-1) and take the difference.

Longest Repeating Character Replacement (LeetCode 424)
Given a string that you can replace at most k characters, find the length of the longest substring containing the same letter after at most k replacements.

Fruit Into Baskets (LeetCode 904)
Given a row of trees, you can collect fruits from at most two types of trees — find the longest subarray containing at most 2 distinct integers.

Longest Subarray of Ones After Deleting One Element
Given a binary array, you may delete one element — find the length of the longest subarray containing only 1’s.

🔹 Sum/array variants (still sliding window)

These are still the same template, just with integers instead of characters:

Maximum Average Subarray of Size K
Fixed-size sliding window (simpler version — no shrinking).

Longest Subarray With Sum ≤ K
Maintain current sum and shrink when sum > K.

Longest Subarray With Sum Exactly K
Requires prefix sums + hashmap, but the two-pointer variant works for positive integers.

Subarrays with K Different Integers (LeetCode 992)
Count subarrays that have exactly K distinct integers.

Max Consecutive Ones II,
You are given a binary array nums containing only 0s and 1s. You are allowed to flip at most one 0 to 1. Return the maximum number of consecutive 1s
