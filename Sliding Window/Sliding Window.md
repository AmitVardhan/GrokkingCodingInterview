Usage:

1.  Find the longest/shortest string
2.  The problem involves a data structure that is ordered and iterable like arrays, strings, lists etc.
3.  When we are asked to find or calculate something among all the contiguous subarrays (or sublists) of a given size.
4. The problem is asking to find a sub range in an array/string, contiguous longest, shortest, average or target value.
5. There is an apparent naive or brute force solution that runs in O(N2), O(2N) or some other large time complexity.

The amazing thing about sliding window problems is that most of the time they can be solved in O(N) time and O(1) space complexity.



Problem 1: Given an array, find the average of all contiguous subarrays of size ‘K’ in it.

LeetCode 643 - Maximum Average Subarray I [easy]
Let’s understand this problem with a real input:
```
Array: [1, 3, 2, 6, -1, 4, 1, 8, 2], K=5
```

Here, we are asked to find the average of all contiguous subarrays of size ‘5’ in the given array. Let’s solve this:
1. For the first 5 numbers (subarray from index 0-4), the average is: (1+3+2+6−1)/5 => 2.2
2. The average of next 5 numbers (subarray from index 1-5) is: (3+2+6−1+4)/5 => 2.8
3. For the next 5 numbers (subarray from index 2-6), the average is: (2+6−1+4+1)/5 => 2.4
    …

Here is the final output containing the averages of all contiguous subarrays of size 5:
```
Output: [2.2, 2.8, 2.4, 3.6, 2.8]
```

A brute-force algorithm  will calculate the sum of every 5-element contiguous subarray of the  given array and divide the sum by ‘5’ to find the average. This is what  the algorithm will look like:
```
function find_averages_of_subarrays(K, arr) { 
  const result = []; 
  for (let i = 0; i < arr.length - K + 1; i++) { 
    // find sum of next 'K' elements 
    sum = 0.0; 
    for (let j = i; j < i + K; j++) { 
      sum += arr[j]; 
    } 
    result.push(sum / K); // calculate average 
  } 
  return result; 
} 
const result = find_averages_of_subarrays(5, [1, 3, 2, 6, -1, 4, 1, 8, 2]); 
console.log(`Averages of subarrays of size K: ${result}`);
```

Time complexity:  Since for every element of the input array, we are calculating the sum  of its next ‘K’ elements, the time complexity of the above algorithm  will be O(N∗K) where ‘N’ is the number of elements in the input array.

Can we find a better solution? Do you see any inefficiency in the above approach?
The inefficiency is that  for any two consecutive subarrays of size ‘5’, the overlapping part  (which will contain four elements) will be evaluated twice. For example,  take the above-mentioned input:

As  you can see, there are four overlapping elements between the subarray  (indexed from 0-4) and the subarray (indexed from 1-5). Can we somehow  reuse the sum we have calculated for the overlapping elements?

The efficient way to solve  this problem would be to visualize each contiguous subarray as a  sliding window of ‘5’ elements. This means that we will slide the window  by one element when we move on to the next subarray. To reuse the sum  from the previous subarray, we will subtract the element going out of  the window and add the element now being included in the sliding window.  This will save us from going through the whole subarray to find the sum and, as a result, the algorithm complexity will reduce to O(N).


```
function find_averages_of_subarrays(K, arr) { 
  const result = []; 
  let windowSum = 0.0, 
    windowStart = 0; 
  for (let windowEnd = 0; windowEnd < arr.length; windowEnd++) { 
    windowSum += arr[windowEnd]; // add the next element 
    // slide the window, we don't need to slide if we've not hit the required window size of 'k' 
    if (windowEnd >= K - 1) { 
      result.push(windowSum / K); // calculate the average 
      windowSum -= arr[windowStart]; // subtract the element going out 
      windowStart += 1; // slide the window ahead 
    } 
  } 
  return result; 
} 
const result = find_averages_of_subarrays(5, [1, 3, 2, 6, -1, 4, 1, 8, 2]); 
console.log(`Averages of subarrays of size K: ${result}`);
```

The size  of the sliding window may or may not be fixed. 


Problem 2: Maximum Sum Subarray of Size K(easy)


Problem Statement 

Given an array of positive numbers and a positive number ‘k,’ find the maximum sum of any contiguous subarray of size ‘k’.
Example 1:
```
Input: [2, 1, 5, 1, 3, 2], k=3 
Output: 9
Explanation: Subarray with maximum sum is [5, 1, 3].
```
Example 2:
```
Input: [2, 3, 4, 1, 5], k=2 
Output: 7
Explanation: Subarray with maximum sum is [3, 4].
```

A basic brute force solution will be to calculate the sum of all ‘k’ sized subarrays of the given array to find the subarray with the highest sum. We can start from every index of the given array and add the next ‘k’ elements to find the subarray’s sum. Following is the visual representation of this algorithm for Example-1:


```
function max_sub_array_of_size_k(k, arr) {
  let maxSum = 0,
    windowSum = 0;
  for (i = 0; i < arr.length - k + 1; i++) {
    windowSum = 0;
    for (j = i; j < i + k; j++) {
      windowSum += arr[j];
    }
    maxSum = Math.max(maxSum, windowSum);
  }
  return maxSum;
}
console.log(`Maximum sum of a subarray of size K: ${max_sub_array_of_size_k(3, [2, 1, 5, 1, 3, 2])}`);
console.log(`Maximum sum of a subarray of size K: ${max_sub_array_of_size_k(2, [2, 3, 4, 1, 5])}`);
```

The above algorithm’s time complexity will be O(N∗K), where ‘N’ is the total number of elements in the given array. Is it possible to find a better algorithm than this?

Better approach 

If you observe closely,  you will realize that to calculate the sum of a contiguous subarray, we  can utilize the sum of the previous subarray. For this, consider each  subarray as a Sliding Window of size ‘k.’ To calculate  the sum of the next subarray, we need to slide the window ahead by one  element. So to slide the window forward and calculate the sum of the new  position of the sliding window, we need to do two things:
1. Subtract the element going out of the sliding window, i.e., subtract the first element of the window.
2. Add the new element getting included in the sliding window, i.e., the element coming right after the end of the window.

This approach will save us  from re-calculating the sum of the overlapping part of the sliding  window. Here is what our algorithm will look like:
```
function max_sub_array_of_size_k(k, arr) {
  let maxSum = 0,
    windowSum = 0,
    windowStart = 0;
  for (window_end = 0; window_end < arr.length; window_end++) {
    windowSum += arr[window_end]; // add the next element
    // slide the window, we don't need to slide if we've not hit the required window size of 'k'
    if (window_end >= k - 1) {
      maxSum = Math.max(maxSum, windowSum);
      windowSum -= arr[windowStart]; // subtract the element going out
      windowStart += 1; // slide the window ahead
    }
  }
  return maxSum;
}
console.log(`Maximum sum of a subarray of size K: ${max_sub_array_of_size_k(3, [2, 1, 5, 1, 3, 2])}`);
console.log(`Maximum sum of a subarray of size K: ${max_sub_array_of_size_k(2, [2, 3, 4, 1, 5])}`);
```

Time Complexity 

The time complexity of the above algorithm will be O(N).

Space Complexity 

The algorithm runs in constant space O(1).


Problem 3: Smallest Subarray with a given sum (easy)

Given an array of positive numbers and a positive number ‘S,’ find the length of the smallest contiguous subarray whose sum is greater than or equal to ‘S’. Return 0 if no such subarray exists.

Example 1:
```
Input: [2, 1, 5, 2, 3, 2], S=7 
Output: 2
Explanation: The smallest subarray with a sum great than or equal to '7' is [5, 2].
```

Example 2:
```
Input: [2, 1, 5, 2, 8], S=7 
Output: 1
Explanation: The smallest subarray with a sum greater than or equal to '7' is [8].
```

Example 3:
```
Input: [3, 4, 1, 1, 6], S=8 
Output: 3
Explanation: Smallest subarrays with a sum greater than or equal to '8' are [3, 4, 1] or [1, 1, 6].
```


Solution 

This problem follows the Sliding Window pattern, and we can use a similar strategy as discussed in Maximum Sum Subarray of Size K. There is one difference though: in this problem, the sliding window size is not fixed. 

Here is how we will solve this problem:
1. First, we will add-up elements from the beginning of the array until their sum becomes greater than or equal to ‘S.’
2. These elements will constitute our sliding window. We are asked to find the smallest such window having a sum greater than or equal to ‘S.’ We will remember the length of this window as the smallest window so far.
3. After this, we will keep adding one element in the sliding window (i.e., slide the window ahead) in a stepwise fashion.
4. In each step, we will also try to shrink the window from the beginning. We will shrink the window until the window’s sum is smaller than ‘S’ again. This is needed as we intend to find the smallest window. This shrinking will also happen in multiple steps; in each step, we will do two things:
	- Check if the current window length is the smallest so far, and if so, remember its length.
	- Subtract the first element of the window from the running sum to shrink the sliding window.

Here is the visual representation of this algorithm for the Example-1


Here is what out algorithm will look:
```
function smallest_subarray_with_given_sum(s, arr) {
  let windowSum = 0,
    minLength = Infinity,
    windowStart = 0;
  for (windowEnd = 0; windowEnd < arr.length; windowEnd++) {
    windowSum += arr[windowEnd]; // add the next element
    // shrink the window as small as possible until the 'window_sum' is smaller than 's'
    while (windowSum >= s) {
      minLength = Math.min(minLength, windowEnd - windowStart + 1);
      windowSum -= arr[windowStart];
      windowStart += 1;
    }
  }
  if (minLength === Infinity) {
    return 0;
  }
  return minLength;
}
console.log(`Smallest subarray length: ${smallest_subarray_with_given_sum(7, [2, 1, 5, 2, 3, 2])}`);
console.log(`Smallest subarray length: ${smallest_subarray_with_given_sum(7, [2, 1, 5, 2, 8])}`);
console.log(`Smallest subarray length: ${smallest_subarray_with_given_sum(8, [3, 4, 1, 1, 6])}`);
```

Time Complexity 

The time complexity of the above algorithm will be O(N). The outer for loop runs for all elements, and the inner while loop processes each element only once; therefore, the time complexity of the algorithm will be O(N+N), which is asymptotically equivalent to O(N).

Space Complexity 

The algorithm runs in constant space O(1).


Problem 4: Longest Substring with K Distinct Characters (medium)


Problem Statement 

Given a string, find the length of the longest substring in it with no more than K distinct characters.
Example 1:
```
Input: String="araaci", K=2
Output: 4
Explanation: The longest substring with no more than '2' distinct characters is "araa".
```

Example 2:
```
Input: String="araaci", K=1
Output: 2
Explanation: The longest substring with no more than '1' distinct characters is "aa".

```

Example 3:
```
Input: String="cbbebi", K=3
Output: 5
Explanation: The longest substrings with no more than '3' distinct characters are "cbbeb" & "bbebi".
```




Solution 

This problem follows the Sliding Window pattern, and we can use a similar dynamic sliding window strategy as discussed in Smallest Subarray with a given sum. We can use a HashMap to remember the frequency of each character we have processed. Here is how we will solve this problem:
1. First, we will insert characters from the beginning of the string until we have ‘K’ distinct characters in the HashMap.
2. These characters will constitute our sliding window. We are asked to find the longest such window having no more than ‘K’ distinct characters. We will remember the length of this window as the longest window so far.
3. After this, we will keep adding one character in the sliding window (i.e., slide the window ahead) in a stepwise fashion.
4. In each step, we will try to shrink the window from the beginning if the count of distinct characters in the HashMap is larger than ‘K.’ We will shrink the window until we have no more than ‘K’ distinct characters in the HashMap. This is needed as we intend to find the longest window.
5. While shrinking, we’ll decrement the character’s frequency going out of the window and remove it from the HashMap if its frequency becomes zero.
6. At the end of each step, we’ll check if the current window length is the longest so far, and if so, remember its length.

Here is the visual representation of this algorithm:


```
function longest_substring_with_k_distinct(str, k) {
  let windowStart = 0,
    maxLength = 0,
    charFrequency = {};
  // in the following loop we'll try to extend the range [window_start, window_end]
  for (let windowEnd = 0; windowEnd < str.length; windowEnd++) {
    const rightChar = str[windowEnd];
    if (!(rightChar in charFrequency)) {
      charFrequency[rightChar] = 0;
    }
    charFrequency[rightChar] += 1;
    // shrink the sliding window, until we are left with 'k' distinct characters in the char_frequency
    while (Object.keys(charFrequency).length > k) {
      const leftChar = str[windowStart];
      charFrequency[leftChar] -= 1;
      if (charFrequency[leftChar] === 0) {
        delete charFrequency[leftChar];
      }
      windowStart += 1; // shrink the window
    }
    // remember the maximum length so far
    maxLength = Math.max(maxLength, windowEnd - windowStart + 1);
  }
  return maxLength;
}
console.log(`Length of the longest substring: ${longest_substring_with_k_distinct('araaci', 2)}`);
console.log(`Length of the longest substring: ${longest_substring_with_k_distinct('araaci', 1)}`);
console.log(`Length of the longest substring: ${longest_substring_with_k_distinct('cbbebi', 3)}`);
```


Time Complexity 

The above algorithm’s time complexity will be O(N), where ‘N’ is the number of characters in the input string. The outer for loop runs for all characters, and the inner while loop processes each character only once; therefore, the time complexity of the algorithm will be O(N+N), which is asymptotically equivalent to O(N).

Space Complexity 

The algorithm’s space complexity is O(K), as we will be storing a maximum of ‘K+1’ characters in the HashMap.


Problem 5: Fruits into Baskets (medium)


Problem Statement 

Given an array of characters where each character represents a fruit tree, you are given two baskets, and your goal is to put maximum number of fruits in each basket. The only restriction is that each basket can have only one type of fruit.
You can start with any  tree, but you can’t skip a tree once you have started. You will pick one  fruit from each tree until you cannot, i.e., you will stop when you  have to pick from a third fruit type.
Write a function to return the maximum number of fruits in both the baskets.
Example 1:
```
Input: Fruit=['A', 'B', 'C', 'A', 'C']
Output: 3
Explanation: We can put 2 'C' in one basket and one 'A' in the other from the subarray ['C', 'A', 'C']

```
Example 2:
```
Input: Fruit=['A', 'B', 'C', 'B', 'B', 'C']
Output: 5
Explanation: We can put 3 'B' in one basket and two 'C' in the other basket. 
This can be done if we start with the second letter: ['B', 'C', 'B', 'B', 'C']
```


Solution 

This problem follows the Sliding Window pattern and is quite similar to Longest Substring with K Distinct Characters.  In this problem, we need to find the length of the longest subarray  with no more than two distinct characters (or fruit types!). This  transforms the current problem into Longest Substring with K Distinct Characters where K=2.

Code 

Here is what our algorithm will look like, only the highlighted lines are different from Longest Substring with K Distinct Characters:

```
function fruits_into_baskets(fruits) {
  let windowStart = 0,
    maxLength = 0,
    fruitFrequency = {};
  // try to extend the range [windowStart, windowEnd]
  for (let windowEnd = 0; windowEnd < fruits.length; windowEnd++) {
    const rightFruit = fruits[windowEnd];
    if (!(rightFruit in fruitFrequency)) {
      fruitFrequency[rightFruit] = 0;
    }
    fruitFrequency[rightFruit] += 1;
    // shrink the sliding window, until we are left with '2' fruits in the fruit frequency dictionary
    while (Object.keys(fruitFrequency).length > 2) {
      const leftFruit = fruits[windowStart];
      fruitFrequency[leftFruit] -= 1;
      if (fruitFrequency[leftFruit] === 0) {
        delete fruitFrequency[leftFruit];
      }
      windowStart += 1; // shrink the window
    }
    maxLength = Math.max(maxLength, windowEnd - windowStart + 1);
  }
  return maxLength;
}
console.log(`Maximum number of fruits: ${fruits_into_baskets(['A', 'B', 'C', 'A', 'C'])}`);
console.log(`Maximum number of fruits: ${fruits_into_baskets(['A', 'B', 'C', 'B', 'B', 'C'])}`);
```

Time Complexity 

The above algorithm’s time complexity will be O(N), where ‘N’ is the number of characters in the input array. The outer for loop runs for all characters, and the inner while loop processes each character only once; therefore, the time complexity of the algorithm will be O(N+N), which is asymptotically equivalent to O(N).

Space Complexity 

The algorithm runs in constant space O(1) as there can be a maximum of three types of fruits stored in the frequency map.

Similar Problems 

Problem 1: Longest Substring with at most 2 distinct characters
Given a string, find the length of the longest substring in it with at most two distinct characters.
Solution: This problem is exactly similar to our parent problem.


Problem 6: No-repeat Substring (hard)


Problem Statement 

Given a string, find the length of the longest substring, which has no repeating characters.
Example 1:
```
Input: String="aabccbb"
Output: 3
Explanation: The longest substring without any repeating characters is "abc".

```

Example 2:
```
Input: String="abbbb"
Output: 2
Explanation: The longest substring without any repeating characters is "ab".

```

Example 3:
```
Input: String="abccde"
Output: 3
Explanation: Longest substrings without any repeating characters are "abc" & "cde".

```

Solution 

This problem follows the Sliding Window pattern, and we can use a similar dynamic sliding window strategy as discussed in Longest Substring with K Distinct Characters. We can use a HashMap  to remember the last index of each character we have processed.  Whenever we get a repeating character, we will shrink our sliding window  to ensure that we always have distinct characters in the sliding  window.

Here is what our algorithm will look like:
```
function non_repeat_substring(str) {
  let windowStart = 0,
    maxLength = 0,
    charIndexMap = {};
  // try to extend the range [windowStart, windowEnd]
  for (let windowEnd = 0; windowEnd < str.length; windowEnd++) {
    const rightChar = str[windowEnd];
    // if the map already contains the 'rightChar', shrink the window from the beginning so that
    // we have only one occurrence of 'rightChar'
    if (rightChar in charIndexMap) {
      // this is tricky; in the current window, we will not have any 'rightChar' after its previous index
      // and if 'windowStart' is already ahead of the last index of 'rightChar', we'll keep 'windowStart'
      windowStart = Math.max(windowStart, charIndexMap[rightChar] + 1);
    }
    // insert the 'rightChar' into the map
    charIndexMap[rightChar] = windowEnd;
    // remember the maximum length so far
    maxLength = Math.max(maxLength, windowEnd - windowStart + 1);
  }
  return maxLength;
}
console.log(`Length of the longest substring: ${non_repeat_substring('aabccbb')}`);
console.log(`Length of the longest substring: ${non_repeat_substring('abbbb')}`);
console.log(`Length of the longest substring: ${non_repeat_substring('abccde')}`);
```

Time Complexity 

The above algorithm’s time complexity will be O(N), where ‘N’ is the number of characters in the input string.

Space Complexity 

The algorithm’s space complexity will be O(K), where K is the number of distinct characters in the input string. This also means K<=N, because in the worst case, the whole string might not have any repeating character, so the entire string will be added to the HashMap.  Having said that, since we can expect a fixed set of characters in the  input string (e.g., 26 for English letters), we can say that the  algorithm runs in fixed space O(1); in this case, we can use a fixed-size array instead of the HashMap.


Problem 7: Longest Substring with Same Letters after Replacement (hard)


Problem Statement 

Given a string with lowercase letters only, if you are allowed to replace no more than ‘k’ letters with any letter, find the length of the longest substring having the same letters after replacement.
Example 1:
```
Input: String="aabccbb", k=2
Output: 5
Explanation: Replace the two 'c' with 'b' to have a longest repeating substring "bbbbb".

```

Example 2:
```
Input: String="abbcb", k=1
Output: 4
Explanation: Replace the 'c' with 'b' to have a longest repeating substring "bbbb".

```

Example 3:
```
Input: String="abccde", k=1
Output: 3
Explanation: Replace the 'b' or 'd' with 'c' to have the longest repeating substring "ccc".
```


Solution 

This problem follows the Sliding Window pattern, and we can use a similar dynamic sliding window strategy as discussed in No-repeat Substring. We can use a HashMap to count the frequency of each letter.
- We’ll iterate through the string to add one letter at a time in the window.
- We’ll also keep track of the count of the maximum repeating letter in any window (let’s call it maxRepeatLetterCount).
- So, at any time, we know that we can have a window which has one letter repeating maxRepeatLetterCount times; this means we should try to replace the remaining letters.
- If we have more than ‘k’ remaining letters, we should shrink the window as we are not allowed to replace more than ‘k’ letters.
While shrinking the window, we don’t need to update maxRepeatLetterCount  (which makes it global count; hence, it is the maximum count for ANY  window). Why don’t we need to update this count when we shrink the  window? The answer: In any window, since we have to replace all the  remaining letters to get the longest substring having the same letter,  we can’t get a better answer from any other window even though all  occurrences of the letter with frequency maxRepeatLetterCount is not in the current window.



Here is what our algorithm will look like:
```
function length_of_longest_substring(str, k) {
  let windowStart = 0,
    maxLength = 0,
    maxRepeatLetterCount = 0,
    frequencyMap = {};
  // Try to extend the range [windowStart, windowEnd]
  for (let windowEnd = 0; windowEnd < str.length; windowEnd++) {
    const rightChar = str[windowEnd];
    if (!(rightChar in frequencyMap)) {
      frequencyMap[rightChar] = 0;
    }
    frequencyMap[rightChar] += 1;
    maxRepeatLetterCount = Math.max(maxRepeatLetterCount, frequencyMap[rightChar]);
    // Current window size is from windowStart to windowEnd, overall we have a letter which is
    // repeating 'maxRepeatLetterCount' times, this means we can have a window which has one letter
    // repeating 'maxRepeatLetterCount' times and the remaining letters we should replace.
    // if the remaining letters are more than 'k', it is the time to shrink the window as we
    // are not allowed to replace more than 'k' letters
    if ((windowEnd - windowStart + 1 - maxRepeatLetterCount) > k) {
      leftChar = str[windowStart];
      frequencyMap[leftChar] -= 1;
      windowStart += 1;
    }
    maxLength = Math.max(maxLength, windowEnd - windowStart + 1);
  }
  return maxLength;
}
console.log(length_of_longest_substring('aabccbb', 2));
console.log(length_of_longest_substring('abbcb', 1));
console.log(length_of_longest_substring('abccde', 1));
```

Time Complexity 

The above algorithm’s time complexity will be O(N), where ‘N’ is the number of letters in the input string.

Space Complexity 

As we expect only the lower case letters in the input string, we can conclude that the space complexity will be O(26) to store each letter’s frequency in the HashMap, which is asymptotically equal to O(1).


Longest Subarray with Ones after Replacement (hard)


Problem Statement 

Given an array containing 0s and 1s, if you are allowed to replace no more than ‘k’ 0s with 1s, find the length of the longest contiguous subarray having all 1s.
Example 1:
```
Input: Array=[0, 1, 1, 0, 0, 0, 1, 1, 0, 1, 1], k=2
Output: 6
Explanation: Replace the '0' at index 5 and 8 to have the longest contiguous subarray of 1s having length 6.

```
Example 2:
```
Input: Array=[0, 1, 0, 0, 1, 1, 0, 1, 1, 0, 0, 1, 1], k=3
Output: 9
Explanation: Replace the '0' at index 6, 9, and 10 to have the longest contiguous subarray of 1s having length 9.
```


Solution 

This problem follows the Sliding Window pattern and is quite similar to Longest Substring with same Letters after Replacement. The only difference is that, in the problem, we only have two characters (1s and 0s) in the input arrays.
Following a similar  approach, we’ll iterate through the array to add one number at a time in  the window. We’ll also keep track of the maximum number of repeating 1s  in the current window (let’s call it maxOnesCount). So at any time, we know that we can have a window with 1s repeating maxOnesCount  time, so we should try to replace the remaining 0s. If we have more  than ‘k’ remaining 0s, we should shrink the window as we are not allowed  to replace more than ‘k’ 0s.

Code 

Here is how our algorithm will look like:
```
function length_of_longest_substring(arr, k) {
  let windowStart = 0,
    maxLength = 0,
    maxOnesCount = 0;
  // Try to extend the range [windowStart, windowEnd]
  for (windowEnd = 0; windowEnd < arr.length; windowEnd++) {
    if (arr[windowEnd] === 1) {
      maxOnesCount += 1;
    }
    // Current window size is from windowStart to windowEnd, overall we have a maximum of 1s
    // repeating 'maxOnesCount' times, this means we can have a window with 'maxOnesCount' 1s
    // and the remaining are 0s which should replace with 1s.
    // now, if the remaining 0s are more than 'k', it is the time to shrink the window as we
    // are not allowed to replace more than 'k' 0s
    if ((windowEnd - windowStart + 1 - maxOnesCount) > k) {
      if (arr[windowStart] === 1) {
        maxOnesCount -= 1;
      }
      windowStart += 1;
    }
    maxLength = Math.max(maxLength, windowEnd - windowStart + 1);
  }
  return maxLength;
}
console.log(length_of_longest_substring([0, 1, 1, 0, 0, 0, 1, 1, 0, 1, 1], 2));
console.log(length_of_longest_substring([0, 1, 0, 0, 1, 1, 0, 1, 1, 0, 0, 1, 1], 3));
```

Time Complexity 

The above algorithm’s time complexity will be O(N), where ‘N’ is the count of numbers in the input array.

Space Complexity 

The algorithm runs in constant space O(1).


Problem Challenge 1


Permutation in a String (hard) 

Given a string and a pattern, find out if the string contains any permutation of the pattern.
Permutation is defined as the re-arranging of the characters of the string. For example, “abc” has the following six permutations:
1. abc
2. acb
3. bac
4. bca
5. cab
6. cba
If a string has ‘n’ distinct characters, it will have n!n!n! permutations.
Example 1:
```
Input: String="oidbcaf", Pattern="abc"
Output: true
Explanation: The string contains "bca" which is a permutation of the given pattern.

```
Example 2:
```
Input: String="odicf", Pattern="dc"
Output: false
Explanation: No permutation of the pattern is present in the given string as a substring.

```
Example 3:
```
Input: String="bcdxabcdy", Pattern="bcdyabcdx"
Output: true
Explanation: Both the string and the pattern are a permutation of each other.

```
Example 4:
```
Input: String="aaacb", Pattern="abc"
Output: true
Explanation: The string contains "acb" which is a permutation of the given pattern.
```


Solution 

This problem follows the Sliding Window pattern, and we can use a similar sliding window strategy as discussed in Longest Substring with K Distinct Characters. We can use a HashMap to remember the frequencies of all characters in the given pattern. Our goal will be to match all the characters from this HashMap with a sliding window in the given string. Here are the steps of our algorithm:
1. Create a HashMap to calculate the frequencies of all characters in the pattern.
2. Iterate through the string, adding one character at a time in the sliding window.
3. If the character being added matches a character in the HashMap, decrement its frequency in the map. If the character frequency becomes zero, we got a complete match.
4. If at any time, the number of characters matched is equal to the number of distinct characters in the pattern (i.e., total characters in the HashMap), we have gotten our required permutation.
5. If the window size is greater than the length of the pattern, shrink the window to make it equal to the pattern’s size. At the same time, if the character going out was part of the pattern, put it back in the frequency HashMap.

Code 

Here is what our algorithm will look like:
```
function find_permutation(str, pattern) {
  let windowStart = 0,
    matched = 0,
    charFrequency = {};
  for (i = 0; i < pattern.length; i++) {
    const chr = pattern[i];
    if (!(chr in charFrequency)) {
      charFrequency[chr] = 0;
    }
    charFrequency[chr] += 1;
  }
  // Our goal is to match all the characters from the 'charFrequency' with the current window
  // try to extend the range [windowStart, windowEnd]
  for (windowEnd = 0; windowEnd < str.length; windowEnd++) {
    const rightChar = str[windowEnd];
    if (rightChar in charFrequency) {
      // Decrement the frequency of matched character
      charFrequency[rightChar] -= 1;
      if (charFrequency[rightChar] === 0) {
        matched += 1;
      }
    }
    if (matched === Object.keys(charFrequency).length) {
      return true;
    }
    // Shrink the sliding window
    if (windowEnd >= pattern.length - 1) {
      leftChar = str[windowStart];
      windowStart += 1;
      if (leftChar in charFrequency) {
        if (charFrequency[leftChar] === 0) {
          matched -= 1;
        }
        charFrequency[leftChar] += 1;
      }
    }
  }
  return false;
}
console.log(`Permutation exist: ${find_permutation('oidbcaf', 'abc')}`);
console.log(`Permutation exist: ${find_permutation('odicf', 'dc')}`);
console.log(`Permutation exist: ${find_permutation('bcdxabcdy', 'bcdyabcdx')}`);
console.log(`Permutation exist: ${find_permutation('aaacb', 'abc')}`);
```

Time Complexity 

The above algorithm’s time complexity will be O(N+M), where ‘N’ and ‘M’ are the number of characters in the input string and the pattern, respectively.

Space Complexity 

The algorithm’s space complexity is O(M) since, in the worst case, the whole pattern can have distinct characters that will go into the HashMap.


Problem Challenge 2


String Anagrams (hard) 

Given a string and a pattern, find all anagrams of the pattern in the given string.
Anagram is actually a Permutation of a string. For example, “abc” has the following six anagrams:
1. abc
2. acb
3. bac
4. bca
5. cab
6. cba
Write a function to return a list of starting indices of the anagrams of the pattern in the given string.
Example 1:
```
Input: String="ppqp", Pattern="pq"
Output: [1, 2]
Explanation: The two anagrams of the pattern in the given string are "pq" and "qp".

```
Example 2:
```
Input: String="abbcabc", Pattern="abc"
Output: [2, 3, 4]
Explanation: The three anagrams of the pattern in the given string are "bca", "cab", and "abc".

```

Solution 

This problem follows the Sliding Window pattern and is very similar to Permutation in a String.  In this problem, we need to find every occurrence of any permutation of  the pattern in the string. We will use a list to store the starting  indices of the anagrams of the pattern in the string.

Code 

Here is what our algorithm will look like, only the highlighted lines have changed from Permutation in a String:
```
function find_string_anagrams(str, pattern) {
  let windowStart = 0,
    matched = 0,
    charFrequency = {};
  for (i = 0; i < pattern.length; i++) {
    const chr = pattern[i];
    if (!(chr in charFrequency)) {
      charFrequency[chr] = 0;
    }
    charFrequency[chr] += 1;
  }
  const resultIndices = [];
  // our goal is to match all the characters from the 'charFrequency' with the current window
  // try to extend the range [windowStart, windowEnd]
  for (windowEnd = 0; windowEnd < str.length; windowEnd++) {
    const rightChar = str[windowEnd];
    if (rightChar in charFrequency) {
      // decrement the frequency of matched character
      charFrequency[rightChar] -= 1;
      if (charFrequency[rightChar] === 0) {
        matched += 1;
      }
    }
    if (matched === Object.keys(charFrequency).length) { // have we found an anagram?
      resultIndices.push(windowStart);
    }
    // shrink the sliding window
    if (windowEnd >= pattern.length - 1) {
      leftChar = str[windowStart];
      windowStart += 1;
      if (leftChar in charFrequency) {
        if (charFrequency[leftChar] === 0) {
          matched -= 1; // before putting the character back, decrement the matched count
        }
        charFrequency[leftChar] += 1; // put the character back
      }
    }
  }
  return resultIndices;
}
console.log(find_string_anagrams('ppqp', 'pq'));
console.log(find_string_anagrams('abbcabc', 'abc'));
```


Time Complexity 

The time complexity of the above algorithm will be O(N+M) where ‘N’ and ‘M’ are the number of characters in the input string and the pattern respectively.

Space Complexity 

The space complexity of the algorithm is O(M) since in the worst case, the whole pattern can have distinct characters which will go into the HashMap. In the worst case, we also need O(N)  space for the result list, this will happen when the pattern has only  one character and the string contains only that character.


Problem Challenge 4


Words Concatenation (hard) 

Given a string and a list of words, find all the starting indices of substrings in the given string that are a concatenation of all the given words exactly once without any overlapping of words. It is given that all words are of the same length.
Example 1:
```
Input: String="catfoxcat", Words=["cat", "fox"]
Output: [0, 3]
Explanation: The two substring containing both the words are "catfox" & "foxcat".

```
Example 2:
```
Input: String="catcatfoxfox", Words=["cat", "fox"]
Output: [3]
Explanation: The only substring containing both the words is "catfox".

```

Solution 

This problem follows the Sliding Window pattern and has a lot of similarities with Maximum Sum Subarray of Size K. We will keep track of all the words in a HashMap and try to match them in the given string. Here are the set of steps for our algorithm:
1. Keep the frequency of every word in a HashMap.
2. Starting from every index in the string, try to match all the words.
3. In each iteration, keep track of all the words that we have already seen in another HashMap.
4. If a word is not found or has a higher frequency than required, we can move on to the next character in the string.
5. Store the index if we have found all the words.

Code 

Here is what our algorithm will look like:
```
function find_word_concatenation(str, words) {
  if (words.length === 0 || words[0].length === 0) {
    return [];
  }
  wordFrequency = {};
  words.forEach((word) => {
    if (!(word in wordFrequency)) {
      wordFrequency[word] = 0;
    }
    wordFrequency[word] += 1;
  });
  const resultIndices = [],
    wordsCount = words.length;
  wordLength = words[0].length;
  for (i = 0; i < (str.length - wordsCount * wordLength) + 1; i++) {
    const wordsSeen = {};
    for (j = 0; j < wordsCount; j++) {
      next_word_index = i + j * wordLength;
      // Get the next word from the string
      word = str.substring(next_word_index, next_word_index + wordLength);
      if (!(word in wordFrequency)) { // Break if we don't need this word
        break;
      }
      // Add the word to the 'wordsSeen' map
      if (!(word in wordsSeen)) {
        wordsSeen[word] = 0;
      }
      wordsSeen[word] += 1;
      // no need to process further if the word has higher frequency than required
      if (wordsSeen[word] > (wordFrequency[word] || 0)) {
        break;
      }
      if (j + 1 === wordsCount) { // Store index if we have found all the words
        resultIndices.push(i);
      }
    }
  }
  return resultIndices;
}
console.log(find_word_concatenation('catfoxcat', ['cat', 'fox']));
console.log(find_word_concatenation('catcatfoxfox', ['cat', 'fox']));
```

Time Complexity 

The time complexity of the above algorithm will be O(N∗M∗Len) where ‘N’ is the number of characters in the given string, ‘M’ is the total number of words, and ‘Len’ is the length of a word.

Space Complexity 

The space complexity of the algorithm is O(M) since at most, we will be storing all the words in the two HashMaps. In the worst case, we also need O(N) space for the resulting list. So, the overall space complexity of the algorithm will be  O(M+N).O(M+N).O(M+N).




Similar LeetCode Problems

- LeetCode 3 - Longest Substring Without Repeating Characters [medium]
- LeetCode 30 - Substring with Concatenation of All Words [hard]
- LeetCode 76 - Minimum Window Substring [hard]
- LeetCode 209 - Minimum Size Subarray Sum [medium]
- LeetCode 424 - Longest Repeating Character Replacement [medium]
- LeetCode 438 - Find All Anagrams in a String [medium]
- LeetCode 567 - Permutation in String [medium]
- LeetCode 904 - Fruit Into Baskets [medium]
- LeetCode 1004 - Max Consecutive Ones III [medium]