# leetcode-solutions
All of my Leetcode solutions. Some are efficient and optimized for memory, while others are more of a work in progress.
## Problem 2176. Count Equal and Divisible Pairs in an Array
Language: JavaScript
```javascript
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number}
 */
var countPairs = function(nums, k) {
    pairs = [];
    for (let i = 0; i < nums.length; i++) {
        for (let j = 0; j < nums.length; j++) {
            currentPair = [i, j].sort();
            if (nums[i] === nums[j] && i < j && ((i * j) % k === 0) && !pairs.includes(currentPair)) {
                pairs.push(currentPair);
            }
        }
    }
    return pairs.length;
};
```
## Problem 441. Arranging Coins
Basically, we simulate the pyramid shown in the example. The for loop iterates through the rows and when the counter is negative it means that the row is incomplete, so we return the previous row. In each row there can be exactly the same coins as the number of the row.
Language: Python
```python
class Solution:
    def arrangeCoins(self, n: int) -> int:
        coins = n
        for row in range(1, n + 1):
            coins -= row
            if coins < 0:
                return row - 1
        return n
```
