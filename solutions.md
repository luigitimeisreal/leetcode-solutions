# leetcode-solutions
All of my Leetcode solutions. Some are efficient and optimized for memory, while others are more of a work in progress and may have bad practices. Some of them feature explanations.
## Problem 28. Find the Index of the First Occurrence in a String
We start by looping through the haystack string and using a "sliding window" of the same length as needle and checking if the substring is the same as needle.
(I don't know if this is the official solution)
```python
class Solution:
    def strStr(self, haystack: str, needle: str) -> int:
        for i in range(0, len(haystack)):
            j = i + len(needle)
            if haystack[i:j] == needle:
                return i
        return -1
```
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
## Prblem 1716. Calculate Money in Leetcode Bank
Language: Python
```python
class Solution:
    def totalMoney(self, n: int) -> int:
        normal_day, mondays, total = 1, 1, 0
        for i in range(n):
            if i % 7 == 0 and i > 0:
                mondays += 1
                total += mondays
                normal_day = mondays + 1
            else:
                total += normal_day
                normal_day += 1
        return total
```
## Problem 1920. Build Array from Permutation
Language: Python
```python
class Solution:
    def buildArray(self, nums: List[int]) -> List[int]:
        res = []
        for i, num in enumerate(nums):
            res.append(nums[nums[i]])
        return res
```
## Problem 2016. Maximum Difference Between Increasing Elements
Language: Python
```python
class Solution:
    def maximumDifference(self, nums: List[int]) -> int:
        max_difference = 0
        for i in range(len(nums)):
            for j in range(i + 1, len(nums)):
                if nums[j] - nums[i] > max_difference:
                    max_difference = nums[j] - nums[i]
        if max_difference == 0: 
            return -1
        return max_difference
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
## Problem 2460. Apply Operations to an Array
Language: JavaScript
```javascript
/**
 * @param {number[]} nums
 * @return {number[]}
 */
var applyOperations = function(nums) {
    for(let i = 0; i < nums.length - 1; i++) {
        j = i + 1;
        if (nums[i] === nums[j]) {
            nums[i] *= 2;
            nums[j] = 0;
        }
    }
    let res = [];
    let zeroes = 0;
    for(let i = 0; i < nums.length; i++) {
        if (nums[i] === 0) {
            zeroes++;
        } else {
            res.push(nums[i]);
        }
    }
    for (let i = 0; i < zeroes; i++) {
        res.push(0);
    }
    return res;
};
```
## Problem 2529. Maximum Count of Positive Integer and Negative Integer
Language: JavaScript
```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var maximumCount = function(nums) {
    let positive = 0;
    let negative = 0;
    for (let num of nums) {
        if (num < 0) {
            negative++;
        }
        if (num > 0) {
            positive++;
        }
    }
    if (negative > positive) {
        return negative;
    } else {
        return positive;
    }
    
};
```
## Problem 2942. Find Words Containing Character
Language: Python
```python
class Solution:
    def findWordsContaining(self, words: List[str], x: str) -> List[int]:
        res = []
        for i in range(len(words)):
            if x in words[i]:
                res.append(i)
        return res
```
## Problem 2965. Find Missing and Repeated Values
Language: Python
```python
class Solution:
    def findMissingAndRepeatedValues(self, grid: List[List[int]]) -> List[int]:
        appearances = {}
        res = []
        for i in range(len(grid)):
            for j in range(len(grid)):
                if grid[i][j] not in appearances.keys():
                    appearances[grid[i][j]] = 1
                else:
                    appearances[grid[i][j]] += 1
        for appearance in appearances.keys():
            if appearances[appearance] == 2:
                res.append(appearance)
                break
        for num in range(1, len(grid) * len(grid) + 1):
            if num not in appearances.keys():
                res.append(num)
                break
        return res
```
## Problem 3024. Type of Triangle
The solution can only have four cases. The first one is described in one of the examples and it consists in calculating the sum of two sides and checking if they are less or equal to the remaining side to check if the triangle exists. In the second case we check that all the sides are equal. Since there are only three sides we can directly check. In the third case we check if 2 sides are equal (there are only 3 possible combinations). Finally, in the last case there are again 3 combinations that check the 3 sides are different.
Language: Python
```python3 []
class Solution:
    def triangleType(self, nums: List[int]) -> str:
        if nums[0] + nums[1] <= nums[2] or nums[0] + nums[2] <= nums[1] or nums[1] + nums[2] <= nums[0]:
            return "none"
        if nums[0] == nums[1] and nums[1] == nums[2]:
            return "equilateral"
        if nums[0] == nums[1] or nums[0] == nums[2] or nums[1] == nums[2]:
            return "isosceles"
        if nums[0] != nums[1] and nums[0] != nums[2] and nums[1] != nums[2]:
            return "scalene"
```
## Problem 3136. Valid Word
Language: Python
```python
class Solution:
    def isValid(self, word: str) -> bool:
        vowels = "aeiouAEIOU"
        num_vowels = 0
        num_consonants = 0
        for char in word:
            if not char.isalnum():
                return False
            else:
                if char in vowels:
                    num_vowels += 1
                else:
                    if not char.isdigit():
                        num_consonants += 1
        if len(word) >= 3 and num_vowels >= 1 and num_consonants >= 1:
            return True
        return False

```
## Problem 3289. The Two Sneaky Numbers of Digitville
We start by creating a dictionary tracking the appearances of every number. Then we loop through that dictionary and if we find any number appearing 2 times, we add it to the result array.
Language: Python
```python
class Solution:
    def getSneakyNumbers(self, nums: List[int]) -> List[int]:
        appearances = {}
        res = []
        for num in nums:
            if num not in appearances.keys():
                appearances[num] = 1
            else:
                appearances[num] += 1
        for num in appearances.keys():
            if appearances[num] == 2:
                res.append(num)
        return res
```
## Problem 3423. Maximum Difference Between Adjacent Elements in a Circular Array
Basically, we calculate the sum of the same array twice generating 2 cycles of the first array. Then we iterate with every number(i) and the next one(j), comparing the absolute value of the substraction using abs(). If we find a higher difference, we update the value and keep searching leading to the end result.
Language: Python
```python
class Solution:
    def maxAdjacentDistance(self, nums: List[int]) -> int:
        new_nums = nums + nums
        max_difference = 0
        for i in range(len(new_nums) - 1):
            j = i + 1
            if abs(new_nums[j] - new_nums[i]) > max_difference:
                max_difference = abs(new_nums[j] - new_nums[i])
        return max_difference
```
## Problem 3442. Maximum Difference Between Even and Odd Frequency I
Language: Python
```python
class Solution:
    def maxDifference(self, s: str) -> int:
        frequencies = {}
        for char in s:
            if char in frequencies.keys():
                frequencies[char] += 1
            else:
                frequencies[char] = 1
        max_odd = 0
        min_even = float('inf')
        for char2 in frequencies.keys():
            if frequencies[char2] % 2 == 0 and frequencies[char2] < min_even:
                min_even = frequencies[char2]
            if frequencies[char2] % 2 == 1 and frequencies[char2] > max_odd:
                max_odd = frequencies[char2]
        return max_odd - min_even
```
