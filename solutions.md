# leetcode-solutions
All of my Leetcode solutions. some are efficient and optimized for memory, while others are more of a work in progress.
# Problem 2176. Count Equal and Divisible Pairs in an Array
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
