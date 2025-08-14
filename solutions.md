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
## Problem 151. Reverse Words in a String
I don`t know if using rstrip() is allowed.
```python
class Solution:
    def reverseWords(self, s: str) -> str:
        res = ""
        words = s.split(" ")
        for i in range(len(words) - 1, -1, -1):
            if words[i] != "":
                res = f"{res}{words[i]} "
        return res.rstrip()
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
## Problem 242. Valid Anagram
Language: Python
```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        appearances_s = {}
        appearances_t = {}
        for letter in s:
            if letter not in appearances_s.keys():
                appearances_s[letter] = 1
            else:
                appearances_s[letter] += 1
        for letter in t:
            if letter not in appearances_t.keys():
                appearances_t[letter] = 1
            else:
                appearances_t[letter] += 1
        return dict(sorted(appearances_s.items())) == dict(sorted(appearances_t.items()))
```
## Problem 345. Reverse Vowels of a String
We are using two pointers, one at the left and one at the right. At the moment the left pointer reaches the right one we'll stop iterating. The left and right pointers will move in one iteration if the letter is a consonant. If the two letters are vowels, we swap them and continue to the next iteration.
```python
class Solution:
    def reverseVowels(self, s: str) -> str:
        vowels = "aeiouAEIOU"
        i, j = 0, len(s) - 1
        s = list(s)
        while i < j:
            if s[i] in vowels and s[j] in vowels:
                s[i], s[j] = s[j], s[i]
                j -= 1
                i += 1
            elif s[i] not in vowels:
                i += 1
            elif s[j] not in vowels:
                j -= 1
        return ''.join(s)
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
## Problem 504. Base 7
Language: JavaScript
```javascript
/**
 * @param {number} num
 * @return {string}
 */
var convertToBase7 = function(num) {
    let res = "";
    let isNegative = false;
    if (num === 0) return "0";
    if (num < 0) {
        isNegative = true;
    }
    num = Math.abs(num);
    while (num != 0) {
        digit = num % 7;
        res = `${digit}${res}`
        num = ~~(num / 7)
    }
    if (isNegative) {
        res = `-${res}`
    }
    return res;
};
```
## Problem 692. Top K Frequent Words
Language:Python
```python
class Solution:
    def topKFrequent(self, words: List[str], k: int) -> List[str]:
        frequencies = {}
        res = []
        for word in words:
            if word not in frequencies.keys():
                frequencies[word] = 1
            else:
                frequencies[word] += 1
        for i in range(k):
            for word in sorted(frequencies.keys()):
                if frequencies[word] == max(frequencies.values()):
                    res.append(word)
                    frequencies.pop(word)
                    break
        return res
```
## Problem 804. Unique Morse Code Words
Language: Python
```python
class Solution:
    def uniqueMorseRepresentations(self, words: List[str]) -> int:
        alphabet = [".-","-...","-.-.","-..",".","..-.","--.","....","..",".---","-.-",".-..","--","-.","---",".--.","--.-",".-.","...","-","..-","...-",".--","-..-","-.--","--.."]
        res = set()
        for word in words:
            morse = ""
            for letter in word:
                morse = f"{morse}{alphabet[ord(letter) - 97]}"
            res.add(morse)
        return len(res)
```
## Problem 965. Univalued Binary Tree
Language: Python
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isUnivalTree(self, root: Optional[TreeNode]) -> bool:
        queue = [root]
        value = root.val
        while len(queue) > 0:
            current = queue.pop()
            if current.val != value:
                return False
            if current.left:
                queue.append(current.left)
            if current.right:
                queue.append(current.right)
        return True
```
## Problem 1078. Occurrences After Bigram
Language: JavaScript
```javascript
/**
 * @param {string} text
 * @param {string} first
 * @param {string} second
 * @return {string[]}
 */
var findOcurrences = function(text, first, second) {
    let words = text.split(" ");
    let res = [];
    for(let i = 0; i < words.length - 2; i++) {
        let j = i + 1;
        let k = i + 2;
        if (words[i] === first && words[j] === second) {
            res.push(words[k]);
        }
    }
    return res;
};
```
## Problem 1464. Maximum Product of Two Elements in an Array
Language: Python
```python
class Solution:
    def maxProduct(self, nums: List[int]) -> int:
        nums = sorted(nums)
        return (nums[len(nums) - 1] - 1) * (nums[len(nums) - 2] - 1)
```
## Problem 1684. Count the Number of Consistent Strings
```python
class Solution:
    def countConsistentStrings(self, allowed: str, words: List[str]) -> int:
        res = 0
        for word in words:
            consistent = True
            for letter in word:
                if letter not in allowed:
                    consistent = False
                    break
            if consistent:
                res += 1
        return res

```
## Problem 1716. Calculate Money in Leetcode Bank
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
## Problem 2124. Check if All A's Appears Before All B's
We initialize a boolean variable at the start of the program checking if whle iterating the string, we have reached the first B. If we then find an a after b, we return false. Otherwise, we return true at the end of the string.
Language: JavaScript
```javascript
/**
 * @param {string} s
 * @return {boolean}
 */
var checkString = function(s) {
    firstBReached = false;
    for (let i = 0; i < s.length; i++) {
        if (s[i] === "b") {
            firstBReached = true;
        }
        if (s[i] === "a" && firstBReached) {
            return false;
        }
    }
    return true;
};
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
## Problem 2185. Counting Words With a Given Prefix
Language: Python
```python
class Solution:
    def prefixCount(self, words: List[str], pref: str) -> int:
        res = 0
        for word in words:
            if word[0:len(pref)] == pref:
                res += 1
        return res
```
## Problem 2190. Most Frequent Number Following Key In an Array
Language: Python
```python
class Solution:
    def mostFrequent(self, nums: List[int], key: int) -> int:
        targets = {}

        for i in range(len(nums) - 1):
            if nums[i] == key:
                if nums[i + 1] not in targets.keys():
                    targets[nums[i + 1]] = 1
                else:
                    targets[nums[i + 1]] += 1
        
        return max(targets, key=targets.get)
```
## Problem 2264. Largest 3-Same-Digit Number in String
Language: Python
```python
class Solution:
    def largestGoodInteger(self, num: str) -> str:
        res = ""
        max_num = 0
        for i in range(len(num) - 2):
            if num[i] == num[i + 1] == num[i + 2]:
                digit = ord(num[i])
                if digit > max_num:
                    max_num = digit
                    res = num[i:i + 3]
        return res
```
## Problem 2395. Find Subarrays With Equal Sum
Language: Python
```python
class Solution:
    def findSubarrays(self, nums: List[int]) -> bool:
        sums = []
        for i in range(len(nums) - 1):
            j = i + 1
            if nums[i] + nums[j] in sums:
                return True
            sums.append(nums[i] + nums[j])
        return False

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
## Problem 2710. Remove Trailing Zeros From a String
First, we need to check if the last character is a zero. If it is, we count the number of zeros starting from the last digit. Then we return the substring from the start up to the first trailing zero. Language: Python
```python
class Solution:
    def removeTrailingZeros(self, num: str) -> str:
        res = []
        zeros = 0
        if num[len(num) - 1] == "0":
            for i in range(len(num) - 1, -1, -1):
                zeros += 1
                if num[i - 1] != "0":
                    break
        return num[0:len(num) - zeros]
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
## Problem 3083. Existence of a Substring in a String and Its Reverse
Language: Python
```python
class Solution:
    def isSubstringPresent(self, s: str) -> bool:
        reversed = s[::-1]
        for i in range(len(s) - 1):
            if s[i:i+2] in reversed:
                return True
        return False
```
## Problem 3099. Harshad Number
Language: Python
```python
class Solution:
    def sumOfTheDigitsOfHarshadNumber(self, x: int) -> int:
        sum = 0
        num = x
        while num != 0:
            sum += num % 10
            num //= 10
        return sum if x % sum == 0 else -1
```
## Problem 3110. Score of a String
Language: Python
```python
class Solution:
    def scoreOfString(self, s: str) -> int:
        res = 0
        for i in range(len(s) - 1):
            res += abs(ord(s[i]) - ord(s[i + 1]))
        return res

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
## Problem 3174. Clear Digits
Language: Python
```python
class Solution:
    def clearDigits(self, s: str) -> str:
        digit = True
        while digit:
            digit = False
            for i in range(len(s) - 1):
                j = i + 1
                if s[j].isdigit():
                    digit = True
                    s = s[:i] + s[j+1:]
                    print(i, j, s)
                    break
        return s
            
```
## Problem 3178. Find the Child Who Has the Ball After K Seconds
Language: Python
```python
class Solution:
    def numberOfChild(self, n: int, k: int) -> int:
        ball = -1
        moves_right = True

        for i in range(k + 1):
            if ball < n - 1 and moves_right:
                ball += 1
            elif ball == n - 1 and moves_right:
                moves_right = False
                ball -= 1
            elif ball == 0:
                moves_right = True
                ball += 1
            elif ball < n - 1 and not moves_right:
                ball -= 1
        
        return ball
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
## Problem 3340. Check Balanced String
Language: JavaScript
```javascript
/**
 * @param {string} num
 * @return {boolean}
 */
var isBalanced = function(num) {
    let sumOdd = 0;
    let sumEven = 0;

    for (let i = 0; i < num.length; i++) {
        digit = +num[i]
        if (i % 2 == 0) {
            sumOdd += digit;
        } else {
            sumEven += digit;
        }
    }

    return sumOdd === sumEven;

};
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
## Problem 3541. Find Most Frequent Vowel and Consonant
Language: Python
```python
class Solution:
    def maxFreqSum(self, s: str) -> int:
        vowels = "aeiou"
        freq_vowels = {}
        freq_cons = {}
        for letter in s:
            if letter in vowels:
                if letter not in freq_vowels.keys():
                    freq_vowels[letter] = 1
                else:
                    freq_vowels[letter] += 1
            else:
                if letter not in freq_cons.keys():
                    freq_cons[letter] = 1
                else:
                    freq_cons[letter] += 1
        max_vowel = max(freq_vowels.values()) if freq_vowels else 0
        max_cons = max(freq_cons.values()) if freq_cons else 0
        return max_vowel + max_cons
```
## Problem 3602. Hexadecimal and Hexatrigesimal Conversion
Language: Python
```python
class Solution:
    def concatHex36(self, n: int) -> str:
        return f"{self.toBase(n * n, 16)}{self.toBase(n * n * n, 36)}"

    def toBase(self, num, b) -> str:
        res = ""
        while num > 0:
            digit = num % b
            if len(str(digit)) >= 2:
                digit = chr(digit + 55)
            res = f"{digit}{res}"
            num = num // b
        return res
```
