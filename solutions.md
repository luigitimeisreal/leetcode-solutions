# leetcode-solutions
All of my Leetcode solutions. Some are efficient and optimized for memory, while others are more of a work in progress and may have bad practices. Some of them feature explanations.
## Problem 69. Sqrt(x)
We start by creating a counter which goes up and in every iteration it's multiplied by itself and the result is saved in a variable called power. Then, if the power of any number is bigger than x, we return the previous number. We check if it's bigger because any x in the range of the power of the previous number and the current one is guaranteed to be truncated to the previous number (For example, every number in the range 4-9 will give the result of 2). Language: JavaScript
```javascript
var mySqrt = function(x) {
    let count = 1, power = 0;
    while (true) {
        power = count * count;
        if (power > x) {
            return count - 1;
        }
        count += 1;
    }
};
```
## Problem 171. Excel Sheet Column Number
I think you can understand the solution if you know how to transform binary to decimal. We need to iterate through both in normal order and in reverse order (similar as two pointers). Every character has an index counting down to zero that is represented by "i" variable and the "j" variable iterates normally starting from the start. In binary, we would take the number represented by that index and multiply by 2 (the number of possible characters in binary) powered by its index. Now we need to represent 26 characters instead of 2, but the logic is the same. The numeric value of each character is taken with the ord() function and by sustracting 64 to get numbers 1 to 26 starting from A.
Language: Python
```python
class Solution:
    def titleToNumber(self, columnTitle: str) -> int:
        res, j = 0, 0
        for i in range(len(columnTitle) - 1, -1, -1):
            res += 26 ** i * (ord(columnTitle[j]) - 64)
            j += 1
        return res
````
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
