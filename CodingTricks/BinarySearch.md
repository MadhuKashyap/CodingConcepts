### Pattern : 
Whenever a problem asks for:
- minimum / maximum value of something
- subject to a condition ("can she finish?")

Why? Because:
- If K is too small → she cannot finish (condition fails).
- If K is large enough → she can always finish (condition passes).

### How to identify binary search problems from DP
👉 Binary Search
- There is a monotonic condition (if x works, then all larger x work; or if x fails, then all smaller x fail).
- You're not building a sequence of choices. You're searching for the smallest/largest number (capacity, speed, time, size, threshold)
- such that a condition is satisfied.
👉 Dynamic Programming
- Problem involves optimal substructure and overlapping subproblems
- Do I need to combine results of smaller subproblems to solve this?” If yes → DP.
- The minimum/maximum is a result of sequence of choices (partitioning, subsequences, substring, paths).

### How to solve?
Code Template :
```
// Minimize k , s.t. condition(k) is True

def binary_search(array) -> int:
    def condition(value) -> bool:
        pass

    left, right = min(search_space), max(search_space) # could be [0, n], [1, n] etc. Depends on problem
    while left < right:
        mid = left + (right - left) // 2
        if condition(mid):
            right = mid
        else:
            left = mid + 1
    return left
```
**How to Decide search space** ? 
The trickiest part is always deciding the search space i.e. selecting left and right?
- Identify what you are searching for, generally the parameter that you have to maximize or minimize.
- In most cases
    - Selecting lowerBound
          - When the answer is a rate/time/pace,  low = 1 e.g. koko eating bananas
          - You cannot split an element across multiple groups, low = max(elem) e.g. ship package in D days
    - Selecting upper bound
          - If it’s a rate/time problem, the worst case is "do everything at once", high = max(elem)
          - If it's a capacity/partition problem, the worst case is "no splitting" high = sum(elem)

- So generally range is 1 to max(elem) or max(elem) to sum(elem).
Problems :
1. https://leetcode.com/problems/split-array-largest-sum/description/
2. https://leetcode.com/problems/koko-eating-bananas/description/
3. https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/description/
4. https://leetcode.com/problems/minimum-number-of-days-to-make-m-bouquets/description/
5. https://leetcode.com/problems/kth-smallest-number-in-multiplication-table/description/
6. https://leetcode.com/problems/find-k-th-smallest-pair-distance/description/
7. https://leetcode.com/problems/ugly-number-iii/
8. https://leetcode.com/problems/find-the-smallest-divisor-given-a-threshold/
9. 
