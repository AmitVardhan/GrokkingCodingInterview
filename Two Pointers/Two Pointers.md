In problems where we deal  with sorted arrays (or LinkedLists) and need to find a set of elements  that fulfill certain constraints, the Two Pointers approach becomes  quite useful. 
The set of elements could be a pair, a triplet or even a  subarray. 




Pair with Target Sum (easy)


Problem Statement

Given an array of sorted numbers and a target sum, find a pair in the array whose sum is equal to the given target.
Write a function to return the indices of the two numbers (i.e. the pair) such that they add up to the given target.
Example 1:
```
Input: [1, 2, 3, 4, 6], target=6
Output: [1, 3]
Explanation: The numbers at index 1 and 3 add up to 6: 2+4=6
```
Example 2:
```
Input: [2, 5, 9, 11], target=11
Output: [0, 2]
Explanation: The numbers at index 0 and 2 add up to 11: 2+9=11
```


Solution

Since the given array is  sorted, a brute-force solution could be to iterate through the array,  taking one number at a time and searching for the second number through Binary Search. The time complexity of this algorithm will be O(N ∗ logN). Can we do better than this?

We can follow the Two Pointers  approach. We will start with one pointer pointing to the beginning of  the array and another pointing at the end. At every step, we will see if  the numbers pointed by the two pointers add up to the target sum. If  they do, we have found our pair; otherwise, we will do one of two  things:

1.  If the sum of the two numbers pointed by the two pointers is greater than the target sum, this means that we need a pair with a smaller sum. So, to try more pairs, we can decrement the end-pointer.
2.  If the sum of the two numbers pointed by the two pointers is smaller than the target sum, this means that we need a pair with a larger sum. So, to try more pairs, we can increment the start-pointer.
Here is the visual representation of this algorithm for Example-1:


```
function pair_with_target_sum(arr, targetSum) {
  let left = 0,
    right = arr.length - 1;
  while (left < right) {
    const currentSum = arr[left] + arr[right];
    if (currentSum === targetSum) {
      return [left, right];
    }
    if (targetSum > currentSum) {
      left += 1; // we need a pair with a bigger sum
    } else {
      right -= 1; // we need a pair with a smaller sum
    }
  }
  return [-1, -1];
}
console.log(pair_with_target_sum([1, 2, 3, 4, 6], 6));
console.log(pair_with_target_sum([2, 5, 9, 11], 11));
```


Time Complexity : O(N)


Space Complexity:  O(1).



An Alternate approach

Instead of using a two-pointer or a binary search approach, we can utilize a HashTable  to search for the required pair. We can iterate through the array one  number at a time. Let’s say during our iteration we are at number ‘X’,  so we need to find ‘Y’ such that "X+Y==Target". We will do two things here:
1. Search for ‘Y’ (which is equivalent to Target−X) in the HashTable. If it is there, we have found the required pair.
2. Otherwise, insert “X” in the HashTable, so that we can search it for the later numbers.
Here is what our algorithm will look like:
```
function pair_with_target_sum(arr, targetSum) {
  const nums = {}; // to store numbers and their indices
  for (let i = 0; i < arr.length; i++) {
    const num = arr[i];
    if (targetSum - num in nums) {
      return [nums[targetSum - num], i];
    }
    nums[arr[i]] = i;
  }
  return [-1, -1];
}
console.log(pair_with_target_sum([1, 2, 3, 4, 6], 6));
console.log(pair_with_target_sum([2, 5, 9, 11], 11));
```

Time Complexity 

The time complexity of the above algorithm will be O(N), where ‘N’ is the total number of elements in the given array.

Space Complexity 

The space complexity will also be O(N), as, in the worst case, we will be pushing ‘N’ numbers in the HashTable.



Remove Duplicates (easy)


Problem Statement 

Given an array of sorted numbers, remove all duplicates from it. You should not use any extra space; after removing the duplicates in-place return the length of the subarray that has no duplicate in it.
Example 1:
```
Input: [2, 3, 3, 3, 6, 9, 9]
Output: 4
Explanation: The first four elements after removing the duplicates will be [2, 3, 6, 9].
```
Example 2:
```
Input: [2, 2, 2, 11]
Output: 2
Explanation: The first two elements after removing the duplicates will be [2, 11].
```

Solution 

In this problem, we need  to remove the duplicates in-place such that the resultant length of the  array remains sorted. As the input array is sorted, therefore, one way  to do this is to shift the elements left whenever we encounter  duplicates. In other words, we will keep one pointer for iterating the  array and one pointer for placing the next non-duplicate number. So our  algorithm will be to iterate the array and whenever we see a  non-duplicate number we move it next to the last non-duplicate number  we’ve seen.
Here is the visual representation of this algorithm for Example-1:


```
function remove_duplicates(arr) {
  // index of the next non-duplicate element
  let nextNonDuplicate = 1;
  let i = 1;
  while (i < arr.length) {
    if (arr[nextNonDuplicate - 1] !== arr[i]) {
      arr[nextNonDuplicate] = arr[i];
      nextNonDuplicate += 1;
    }
    i += 1;
  }
  return nextNonDuplicate;
}
console.log(remove_duplicates([2, 3, 3, 3, 6, 9, 9]));
console.log(remove_duplicates([2, 2, 2, 11]));
```

Time Complexity : O(1)


Space Complexity: O(1)



Similar Questions 

Problem 1:  Given an unsorted array of numbers and a target ‘key’, remove all  instances of ‘key’ in-place and return the new length of the array.
Example 1:
```
Input: [3, 2, 3, 6, 3, 10, 9, 3], Key=3
Output: 4
Explanation: The first four elements after removing every 'Key' will be [2, 6, 10, 9].
```
Example 2:
```
Input: [2, 11, 2, 2, 1], Key=2
Output: 2
Explanation: The first two elements after removing every 'Key' will be [11, 1].
```
Solution:  This problem is quite similar to our parent problem. We can follow a  two-pointer approach and shift numbers left upon encountering the ‘key’.  Here is what the code will look like:
```
function remove_element(arr, key) {
  let nextElement = 0; // index of the next element which is not 'key'
  for (i = 0; i < arr.length; i++) {
    if (arr[i] !== key) {
      arr[nextElement] = arr[i];
      nextElement += 1;
    }
  }
  return nextElement;
}
console.log(`Array new length: ${remove_element([3, 2, 3, 6, 3, 10, 9, 3], 3)}`);
console.log(`Array new length: ${remove_element([2, 11, 2, 2, 1], 2)}`);
```

Time Complexity: O(N)
Space Complexity: O(1).


Squaring a Sorted Array (easy)


Problem Statement 

Given a sorted array, create a new array containing squares of all the numbers of the input array in the sorted order.
Example 1:
```
Input: [-2, -1, 0, 2, 3]
Output: [0, 1, 4, 4, 9]

```
Example 2:
```
Input: [-3, -1, 0, 1, 2]
Output: [0, 1, 1, 4, 9]
```




Solution 

This is a straightforward  question. The only trick is that we can have negative numbers in the  input array, which will make it a bit difficult to generate the output  array with squares in sorted order.
An easier approach could be to first find the index of the first non-negative number in the array. After that, we can use Two Pointers  to iterate the array. One pointer will move forward to iterate the  non-negative numbers, and the other pointer will move backward to  iterate the negative numbers. At any step, whichever number gives us a  bigger square will be added to the output array. For the above-mentioned  Example-1, we will do something like this:

Since the numbers at both ends can give us the largest square, an alternate approach could be to use two pointers starting at both ends of the input array. At any step, whichever pointer gives us the bigger square, we add it to the result array and move to the next/previous number according to the pointer. For the above-mentioned Example-1, we will do something like this:


```
function make_squares(arr) {
  const n = arr.length;
  squares = Array(n).fill(0);
  let highestSquareIdx = n - 1;
  let left = 0,
    right = n - 1;
  while (left <= right) {
    let leftSquare = arr[left] * arr[left],
      rightSquare = arr[right] * arr[right];
    if (leftSquare > rightSquare) {
      squares[highestSquareIdx] = leftSquare;
      left += 1;
    } else {
      squares[highestSquareIdx] = rightSquare;
      right -= 1;
    }
    highestSquareIdx -= 1;
  }
  return squares;
}
console.log(`Squares: ${make_squares([-2, -1, 0, 2, 3])}`);
console.log(`Squares: ${make_squares([-3, -1, 0, 1, 2])}`);
```

Time complexity 

The above algorithm’s time complexity will be O(N) as we are iterating the input array only once.

Space complexity 

The above algorithm’s space complexity will also be O(N); this space will be used for the output array.


Triplet Sum to Zero (medium)


Problem Statement 

Given an array of unsorted numbers, find all unique triplets in it that add up to zero.
Example 1:
```
Input: [-3, 0, 1, 2, -1, 1, -2]
Output: [-3, 1, 2], [-2, 0, 2], [-2, 1, 1], [-1, 0, 1]
Explanation: There are four unique triplets whose sum is equal to zero.

```
Example 2:
```
Input: [-5, 2, -1, -2, 3]
Output: [[-5, 2, 3], [-2, -1, 3]]
Explanation: There are two unique triplets whose sum is equal to zero.
```


Solution 

This problem follows the Two Pointers pattern and shares similarities with Pair with Target Sum.  A couple of differences are that the input array is not sorted and  instead of a pair we need to find triplets with a target sum of zero.
To follow a similar  approach, first, we will sort the array and then iterate through it  taking one number at a time.  Let’s say during our iteration we are at  number ‘X’, so we need to find ‘Y’ and ‘Z’ such that X+Y+Z==0. At this stage, our problem translates into finding a pair whose sum is equal to “−X” (as from the above equation Y+Z==−X).
Another difference from Pair with Target Sum  is that we need to find all the unique triplets. To handle this, we  have to skip any duplicate number. Since we will be sorting the array,  so all the duplicate numbers will be next to each other and are easier  to skip.

```
function search_triplets(arr) {
  arr.sort((a, b) => a - b);
  const triplets = [];
  for (i = 0; i < arr.length; i++) {
    if (i > 0 && arr[i] === arr[i - 1]) { // skip same element to avoid duplicate triplets
      continue;
    }
    search_pair(arr, -arr[i], i + 1, triplets);
  }
  return triplets;
}
function search_pair(arr, target_sum, left, triplets) {
  let right = arr.length - 1;
  while (left < right) {
    const current_sum = arr[left] + arr[right];
    if (current_sum === target_sum) { // found the triplet
      triplets.push([-target_sum, arr[left], arr[right]]);
      left += 1;
      right -= 1;
      while (left < right && arr[left] === arr[left - 1]) {
        left += 1; // skip same element to avoid duplicate triplets
      }
      while (left < right && arr[right] === arr[right + 1]) {
        right -= 1; // skip same element to avoid duplicate triplets
      }
    } else if (target_sum > current_sum) {
      left += 1; // we need a pair with a bigger sum
    } else {
      right -= 1; // we need a pair with a smaller sum
    }
  }
}
console.log(search_triplets([-3, 0, 1, 2, -1, 1, -2]));
console.log(search_triplets([-5, 2, -1, -2, 3]));
```


Time complexity 

Sorting the array will take O(N∗logN)O(N * logN). The searchPair() function will take O(N). As we are calling searchPair() for every number in the input array, this means that overall searchTriplets() will take O(N∗logN+N2), which is asymptotically equivalent to O(N2).

Space complexity 

Ignoring the space required for the output array, the space complexity of the above algorithm will be O(N) which is required for sorting.


Triplet Sum Close to Target (medium)


Problem Statement 

Given an array of unsorted numbers and a target number, find a triplet in the array whose sum is as close to the target number as possible, return the sum of the triplet. If there are more than one such triplet, return the sum of the triplet with the smallest sum.
Example 1:
```
Input: [-2, 0, 1, 2], target=2
Output: 1
Explanation: The triplet [-2, 1, 2] has the closest sum to the target.

```
Example 2:
```
Input: [-3, -1, 1, 2], target=1
Output: 0
Explanation: The triplet [-3, 1, 2] has the closest sum to the target.

```
Example 3:
```
Input: [1, 0, 1, 1], target=100
Output: 3
Explanation: The triplet [1, 1, 1] has the closest sum to the target.
```


Solution 

This problem follows the Two Pointers pattern and is quite similar to Triplet Sum to Zero.
We can follow a similar  approach to iterate through the array, taking one number at a time. At  every step, we will save the difference between the triplet and the  target number, so that in the end, we can return the triplet with the  closest sum.

Code 

Here is what our algorithm will look like:
```
function triplet_sum_close_to_target(arr, targetSum) {
  arr.sort((a, b) => a - b);
  let smallest_difference = Infinity;
  for (let i = 0; i < arr.length - 2; i++) {
    let left = i + 1,
      right = arr.length - 1;
    while (left < right) {
      const target_diff = targetSum - arr[i] - arr[left] - arr[right];
      if (target_diff === 0) { // we've found a triplet with an exact sum
        return targetSum - target_diff; // return sum of all the numbers
      }
      if (Math.abs(target_diff) < Math.abs(smallest_difference)) {
        smallest_difference = target_diff; // save the closest difference
      }
      // the second part of the following 'if' is to handle the smallest sum when we have more than one solution
      if (Math.abs(target_diff) < Math.abs(smallest_difference) ||
        (Math.abs(target_diff) === Math.abs(smallest_difference) && target_diff > smallest_difference)) {
        smallest_difference = target_diff; // save the closest and the biggest difference
      }
      if (target_diff > 0) {
        left += 1; // we need a triplet with a bigger sum
      } else {
        right -= 1; // we need a triplet with a smaller sum
      }
    }
  }
  return targetSum - smallest_difference;
}
console.log(triplet_sum_close_to_target([-2, 0, 1, 2], 2));
console.log(triplet_sum_close_to_target([-3, -1, 1, 2], 1));
console.log(triplet_sum_close_to_target([1, 0, 1, 1], 100));
```


Time complexity 

Sorting the array will take O(N∗logN). Overall, the function will take O(N∗logN+N2), which is asymptotically equivalent to O(N2).

Space complexity 

The above algorithm’s space complexity will be O(N), which is required for sorting.


Triplets with Smaller Sum (medium)


Problem Statement 

Given an array arr of unsorted numbers and a target sum, count all triplets in it such that arr[i] + arr[j] + arr[k] < target where i, j, and k are three different indices. Write a function to return the count of such triplets.
Example 1:
```
Input: [-1, 0, 2, 3], target=3 
Output: 2
Explanation: There are two triplets whose sum is less than the target: [-1, 0, 3], [-1, 0, 2]

```
Example 2:
```
Input: [-1, 4, 2, 1, 3], target=5 
Output: 4
Explanation: There are four triplets whose sum is less than the target: 
   [-1, 1, 4], [-1, 1, 3], [-1, 1, 2], [-1, 2, 3]
```

Solution 

This problem follows the Two Pointers pattern and shares similarities with Triplet Sum to Zero.  The only difference is that, in this problem, we need to find the  triplets whose sum is less than the given target. To meet the condition i != j != k we need to make sure that each number is not used more than once.
Following a similar  approach, first, we can sort the array and then iterate through it,  taking one number at a time.  Let’s say during our iteration we are at  number ‘X’, so we need to find ‘Y’ and ‘Z’ such that X+Y+Z<target. At this stage, our problem translates into finding a pair whose sum is less than "target−X" (as from the above equation Y+Z==target−X). We can use a similar approach as discussed in Triplet Sum to Zero.

Code 

Here is what our algorithm will look like:

```
function triplet_with_smaller_sum(arr, target) {
  arr.sort((a, b) => a - b);
  let count = 0;
  for (i = 0; i < arr.length - 2; i++) {
    count += search_pair(arr, target - arr[i], i);
  }
  return count;
}
function search_pair(arr, target_sum, first) {
  let count = 0;
  let left = first + 1,
    right = arr.length - 1;
  while (left < right) {
    if (arr[left] + arr[right] < target_sum) { // found the triplet
      // since arr[right] >= arr[left], therefore, we can replace arr[right] by any number between
      // left and right to get a sum less than the target sum
      count += right - left;
      left += 1;
    } else {
      right -= 1; // we need a pair with a smaller sum
    }
  }
  return count;
}
console.log(triplet_with_smaller_sum([-1, 0, 2, 3], 3));
console.log(triplet_with_smaller_sum([-1, 4, 2, 1, 3], 5));
```

Time complexity 

Sorting the array will take O(N∗logN). The searchPair() will take O(N). So, overall searchTriplets() will take O(N∗logN+N2), which is asymptotically equivalent to O(N2).

Space complexity 

The space complexity of the above algorithm will be O(N) which is required for sorting if we are not using an in-place sorting algorithm.

Similar Problems 

Problem:  Write a function to return the list of all such triplets instead of the  count. How will the time complexity change in this case?
Solution:  Following a similar approach we can create a list containing all the  triplets. Here is the code - only the highlighted lines have changed:
```
function triplet_with_smaller_sum(arr, target) {
  arr.sort((a, b) => a - b);
  const triplets = [];
  for (i = 0; i < arr.length - 2; i++) {
    search_pair(arr, target - arr[i], i, triplets);
  }
  return triplets;
}
function search_pair(arr, target_sum, first, triplets) {
  let left = first + 1,
    right = arr.length - 1;
  while ((left < right)) {
    if (arr[left] + arr[right] < target_sum) { // found the triplet
      // since arr[right] >= arr[left], therefore, we can replace arr[right] by any number between
      // left and right to get a sum less than the target sum
      for (i = right; i > left; i--) {
        triplets.push([arr[first], arr[left], arr[i]]);
      }
      left += 1;
    } else {
      right -= 1; // we need a pair with a smaller sum
    }
  }
}
console.log(triplet_with_smaller_sum([-1, 0, 2, 3], 3));
console.log(triplet_with_smaller_sum([-1, 4, 2, 1, 3], 5));
```
Another  simpler approach could be to check every triplet of the array with  three nested loops and create a list of triplets that meet the required  condition.

Time complexity 

Sorting the array will take O(N∗logN). The searchPair(), in this case, will take O(N2); the main while loop will run in O(N) but the nested for loop can also take  O(N) - this will happen when the target sum is bigger than every triplet in the array.
So, overall searchTriplets() will take O(N∗logN+N3), which is asymptotically equivalent to O(N3).

Space complexity 

Ignoring the space required for the output array, the space complexity of the above algorithm will be O(N) which is required for sorting.


Subarrays with Product Less than a Target (medium)


Problem Statement 

Given an array with positive numbers and a target number, find all of its contiguous subarrays whose product is less than the target number.
Example 1:
```
Input: [2, 5, 3, 10], target=30 
Output: [2], [5], [2, 5], [3], [5, 3], [10]
Explanation: There are six contiguous subarrays whose product is less than the target.

```
Example 2:
```
Input: [8, 2, 6, 5], target=50 
Output: [8], [2], [8, 2], [6], [2, 6], [5], [6, 5] 
Explanation: There are seven contiguous subarrays whose product is less than the target.
```

Solution 

This problem follows the Sliding Window and the Two Pointers pattern and shares similarities with Triplets with Smaller Sum with two differences:
1. In this problem, the input array is not sorted.
2. Instead of finding triplets with sum less than a target, we need to find all subarrays having a product less than the target.
The implementation will be quite similar to Triplets with Smaller Sum.

Code 

Here is what our algorithm will look like:
```
const Deque = require('./collections/deque'); //http://www.collectionsjs.com
function find_subarrays(arr, target) {
  let result = [],
    product = 1,
    left = 0;
  for (right = 0; right < arr.length; right++) {
    product *= arr[right];
    while ((product >= target && left < arr.length)) {
      product /= arr[left];
      left += 1;
    }
    // since the product of all numbers from left to right is less than the target therefore,
    // all subarrays from left to right will have a product less than the target too; to avoid
    // duplicates, we will start with a subarray containing only arr[right] and then extend it
    const tempList = new Deque();
    for (let i = right; i > left - 1; i--) {
      tempList.unshift(arr[i]);
      result.push(tempList.toArray());
    }
  }
  return result;
}
console.log(find_subarrays([2, 5, 3, 10], 30));
console.log(find_subarrays([8, 2, 6, 5], 50));
```

Time complexity 

The main for-loop managing the sliding window takes O(N) but creating subarrays can take up to O(N2) in the worst case. Therefore overall, our algorithm will take O(N3)O(N^3)O(N3).

Space complexity 

Ignoring the space required for the output list, the algorithm runs in O(N) space which is used for the temp list.
Can you try estimating how much space will be required for the output list?

Hint: 
1. The worst-case will happen when every subarray has a product less than the target!
2. So the question will be, how many contiguous subarrays an array can have?
3. It is definitely not all Permutations of the given array; is it all Combinations of the given array?

It is not all the Combinations of all elements of the array!
For an array with distinct  elements, finding all of its contiguous subarrays is like finding the  number of ways to choose two indices, i and j, in the array such that i <= j.
If there are a total of n elements in the array, here is how we can count all the contiguous subarrays:
- When i = 0, j can have any value from 0 to n-1, giving a total of n choices.
- When i = 1, j can have any value from 1 to n-1, giving a total of n-1 choices.
- Similarly, when i = 2, j can have n-2 choices.
   …
   …
- When i = n-1, j can only have only 1 choice.
Let’s combine all the choices:
```
    n + (n-1) + (n-2) + ... 3 + 2 + 1
```
Which gives us a total of: n∗(n+1)/2n*(n+1)/2n∗(n+1)/2
So, at most, we need space for O(n2)O(n^2)O(n2) output lists. At worst, each subarray can take O(n)O(n)O(n) space, so overall, our algorithm’s space complexity will be O(n3)O(n^3)O(n3).


Dutch National Flag Problem (medium)


Problem Statement 

Given an array containing  0s, 1s and 2s, sort the array in-place. You should treat numbers of the  array as objects, hence, we can’t count 0s, 1s, and 2s to recreate the  array.
The flag of the  Netherlands consists of three colors: red, white and blue; and since our  input array also consists of three different numbers that is why it is  called Dutch National Flag problem.
Example 1:
```
Input: [1, 0, 2, 1, 0]
Output: [0 0 1 1 2]

```
Example 2:
```
Input: [2, 2, 0, 1, 2, 0]
Output: [0 0 1 2 2 2 ]
```


Solution 

The brute force solution will be to use an in-place sorting algorithm like Heapsort which will take O(N∗logN)O(N*logN)O(N∗logN). Can we do better than this? Is it possible to sort the array in one iteration?
We can use a Two Pointers approach while iterating through the array. Let’s say the two pointers are called low and high which are pointing to the first and the last element of the array respectively. So while iterating, we will move all 0s before low and all 2s after high so that in the end, all 1s will be between low and high.

Code 

Here is what our algorithm will look like:
```
function dutch_flag_sort(arr) {
  // all elements < low are 0, and all elements > high are 2
  // all elements from >= low < i are 1
  let low = 0,
    high = arr.length - 1,
    i = 0;
  while (i <= high) {
    if (arr[i] === 0) {
      [arr[i], arr[low]] = [arr[low], arr[i]]; // swap
      // increment 'i' and 'low'
      i += 1;
      low += 1;
    } else if (arr[i] === 1) {
      i += 1;
    } else { // the case for arr[i] === 2
      [arr[i], arr[high]] = [arr[high], arr[i]]; // swap
      // decrement 'high' only, after the swap the number at index 'i' could be 0, 1, or 2
      high -= 1;
    }
  }
}
let arr = [1, 0, 2, 1, 0];
dutch_flag_sort(arr);
console.log(arr);
arr = [2, 2, 0, 1, 2, 0];
dutch_flag_sort(arr);
console.log(arr);
```

Time complexity : O(N) as we are iterating the input array only once.


Space complexity :  O(1)



Quadruple Sum to Target (medium) 

Given an array of unsorted numbers and a target number, find all unique quadruplets in it, whose sum is equal to the target number.
Example 1:
```
Input: [4, 1, 2, -1, 1, -3], target=1
Output: [-3, -1, 1, 4], [-3, 1, 1, 2]
Explanation: Both the quadruplets add up to the target.
```
Example 2:
```
Input: [2, 0, -1, 1, -2, 2], target=2
Output: [-2, 0, 2, 2], [-1, 0, 1, 2]
Explanation: Both the quadruplets add up to the target.
```

Solution 

This problem follows the Two Pointers pattern and shares similarities with Triplet Sum to Zero.
We can follow a similar  approach to iterate through the array, taking one number at a time. At  every step during the iteration, we will search for the quadruplets  similar to Triplet Sum to Zero whose sum is equal to the given target.

Code 

Here is what our algorithm will look like:
```
function search_quadruplets(arr, target) {
  arr.sort((a, b) => a - b)
  const quadruplets = [];
  for (let i = 0; i < arr.length - 3; i++) {
    // skip same element to avoid duplicate quadruplets
    if (i > 0 && arr[i] === arr[i - 1]) {
      continue;
    }
    for (let j = i + 1; j < arr.length - 2; j++) {
      // skip same element to avoid duplicate quadruplets
      if (j > i + 1 && arr[j] === arr[j - 1]) {
        continue;
      }
      search_pairs(arr, target, i, j, quadruplets);
    }
  }
  return quadruplets;
}
function search_pairs(arr, targetSum, first, second, quadruplets) {
  let left = second + 1,
    right = arr.length - 1;
  while ((left < right)) {
    sum = arr[first] + arr[second] + arr[left] + arr[right];
    if (sum === targetSum) { // found the quadruplet
      quadruplets.push([arr[first], arr[second], arr[left], arr[right]]);
      left += 1;
      right -= 1;
      while ((left < right && arr[left] === arr[left - 1])) {
        left += 1; // skip same element to avoid duplicate quadruplets
      }
      while ((left < right && arr[right] === arr[right + 1])) {
        right -= 1; // skip same element to avoid duplicate quadruplets
      }
    } else if (sum < targetSum) {
      left += 1; // we need a pair with a bigger sum
    } else {
      right -= 1; // we need a pair with a smaller sum
    }
  }
}
console.log(search_quadruplets([4, 1, 2, -1, 1, -3], 1));
console.log(search_quadruplets([2, 0, -1, 1, -2, 2], 2));
```


Time complexity 

Sorting the array will take O(N∗logN)O(N*logN)O(N∗logN). Overall searchQuadruplets() will take O(N∗logN+N3), which is asymptotically equivalent to O(N3).

Space complexity 

The space complexity of the above algorithm will be O(N) which is required for sorting.


Comparing Strings containing Backspaces (medium) 

Given two strings containing backspaces (identified by the character ‘’), check if the two strings are equal.
Example 1:
```
Input: str1="xyz", str2="xzz"
Output: true
Explanation: After applying backspaces the strings become "xz" and "xz" respectively.
```

Example 2:
```
Input: str1="xyz", str2="xyz"
Output: false
Explanation: After applying backspaces the strings become "xz" and "xy" respectively.
```

Example 3:
```
Input: str1="xp", str2="xyz"
Output: true
Explanation: After applying backspaces the strings become "x" and "x" respectively.
In "xyz", the first '' removes the character 'z' and the second '' removes the character 'y'.
```

Example 4:
```
Input: str1="xywrrmp", str2="xywrrmup"
Output: true
Explanation: After applying backspaces the strings become "xywrrmp" and "xywrrmp" respectively.
```

Solution 

To compare the given  strings, first, we need to apply the backspaces. An efficient way to do  this would be from the end of both the strings. We can have separate  pointers, pointing to the last element of the given strings. We can  start comparing the characters pointed out by both the pointers to see  if the strings are equal. If, at any stage, the character pointed out by  any of the pointers is a backspace (’’), we will skip and apply the  backspace until we have a valid character available for comparison.

Code 

Here is what our algorithm will look like:

```
function backspace_compare(str1, str2) {
  // use two pointer approach to compare the strings
  let index1 = str1.length - 1,
    index2 = str2.length - 1;
  while (index1 >= 0 || index2 >= 0) {
    let i1 = get_next_valid_char_index(str1, index1),
      i2 = get_next_valid_char_index(str2, index2);
    if (i1 < 0 && i2 < 0) { // reached the end of both the strings
      return true;
    }
    if (i1 < 0 || i2 < 0) { // reached the end of one of the strings
      return false;
    }
    if (str1[i1] !== str2[i2]) { // check if the characters are equal
      return false;
    }
    index1 = i1 - 1;
    index2 = i2 - 1;
  }
  return true;
}
function get_next_valid_char_index(str, index) {
  let backspaceCount = 0;
  while (index >= 0) {
    if (str[index] === '') { // found a backspace character
      backspaceCount += 1;
    } else if (backspaceCount > 0) { // a non-backspace character
      backspaceCount -= 1;
    } else {
      break;
    }
    index -= 1; // skip a backspace or a valid character
  }
  return index;
}
console.log(backspace_compare('xyz', 'xzz'));
console.log(backspace_compare('xyz', 'xyz'));
console.log(backspace_compare('xp', 'xyz'));
console.log(backspace_compare('xywrrmp', 'xywrrmup'));
```

Time complexity 

The time complexity of the above algorithm will be O(M+N) where ‘M’ and ‘N’ are the lengths of the two input strings respectively.

Space complexity 

The algorithm runs in constant space O(1).


Minimum Window Sort (medium) 

Given an array, find the length of the smallest subarray in it which when sorted will sort the whole array.
Example 1:
```
Input: [1, 2, 5, 3, 7, 10, 9, 12]
Output: 5
Explanation: We need to sort only the subarray [5, 3, 7, 10, 9] to make the whole array sorted

```
Example 2:
```
Input: [1, 3, 2, 0, -1, 7, 10]
Output: 5
Explanation: We need to sort only the subarray [1, 3, 2, 0, -1] to make the whole array sorted

```
Example 3:
```
Input: [1, 2, 3]
Output: 0
Explanation: The array is already sorted

```
Example 4:
```
Input: [3, 2, 1]
Output: 3
Explanation: The whole array needs to be sorted.

```




Solution 

As we know, once an array  is sorted (in ascending order), the smallest number is at the beginning  and the largest number is at the end of the array. So if we start from  the beginning of the array to find the first element which is out of  sorting order i.e., which is smaller than its previous element, and  similarly from the end of array to find the first element which is  bigger than its previous element, will sorting the subarray between  these two numbers result in the whole array being sorted?
Let’s try to understand  this with Example-2 mentioned above. In the following array, what are  the first numbers out of sorting order from the beginning and the end of  the array:
```
    [1, 3, 2, 0, -1, 7, 10]
```
1. Starting from the beginning of the array the first number out of the sorting order is ‘2’ as it is smaller than its previous element which is ‘3’.
2. Starting from the end of the array the first number out of the sorting order is ‘0’ as it is bigger than its previous element which is ‘-1’
As you can see, sorting  the numbers between ‘3’ and ‘-1’ will not sort the whole array. To see  this, the following will be our original array after the sorted  subarray:
```
    [1, -1, 0, 2, 3, 7, 10]
```

The problem here is that  the smallest number of our subarray is ‘-1’ which dictates that we need  to include more numbers from the beginning of the array to make the  whole array sorted. We will have a similar problem if the maximum of the  subarray is bigger than some elements at the end of the array. To sort  the whole array we need to include all such elements that are smaller  than the biggest element of the subarray. So our final algorithm will  look like:
1. From the beginning and end of the array, find the first elements that are out of the sorting order. The two elements will be our candidate subarray.
2. Find the maximum and minimum of this subarray.
3. Extend the subarray from beginning to include any number which is bigger than the minimum of the subarray.
4. Similarly, extend the subarray from the end to include any number which is smaller than the maximum of the subarray.

Code 

Here is what our algorithm will look like:
```
function shortest_window_sort(arr) {
  let low = 0,
    high = arr.length - 1;
  // find the first number out of sorting order from the beginning
  while ((low < arr.length - 1 && arr[low] <= arr[low + 1])) {
    low += 1;
  }
  if (low === arr.length - 1) { // if the array is sorted
    return 0;
  }
  // find the first number out of sorting order from the end
  while (high > 0 && arr[high] >= arr[high - 1]) {
    high -= 1;
  }
  // find the maximum and minimum of the subarray
  let subarrayMax = -Infinity,
    subarrayMin = Infinity;
  for (k = low; k < high + 1; k++) {
    subarrayMax = Math.max(subarrayMax, arr[k]);
    subarrayMin = Math.min(subarrayMin, arr[k]);
  }
  // extend the subarray to include any number which is bigger than the minimum of the subarray
  while (low > 0 && arr[low - 1] > subarrayMin) {
    low -= 1;
  }
  // extend the subarray to include any number which is smaller than the maximum of the subarray
  while (high < arr.length - 1 && arr[high + 1] < subarrayMax) {
    high += 1;
  }
  return high - low + 1;
}
console.log(shortest_window_sort([1, 2, 5, 3, 7, 10, 9, 12]));
console.log(shortest_window_sort([1, 3, 2, 0, -1, 7, 10]));
console.log(shortest_window_sort([1, 2, 3]));
console.log(shortest_window_sort([3, 2, 1]));
```

Time complexity : O(N)


Space complexity :O(1)



---
Problems where we deal with sorted arrays (or LinkedLists) and need to find a set of elements that fulfill certain constraints, the Two Pointers approach becomes quite useful. The set of elements could be a pair, a triplet or even a subarray.

Problem: Given a sorted array A (sorted in ascending order), having N integers, find if there exists any pair of elements (A[i], A[j]) such that their sum is equal to X.

```
// Naive solution to find if there is a  pair in A[0..N-1] with given sum. 
function isPairSum(arr, N, x) 
{ 
    for(var i = 0; i < N; i++) 
    { 
        for(var j = 0; j <N; j++) 
        { 
            if(arr[i] + arr[j] == x) 
            { 
                return true; 
            } 
            if(arr[i] + arr[j] > x) 
                break; 
        } 
    } 
    return false; 
} 

var arr = [3,5,9,2,8,10,11], Sum = 17;
isPairSum(arr, arr.length, Sum);
```

Time Complexity: O(n^2).

Two Pointer Technique:
1. We take two pointers, one representing the first element and other representing the last element of the array, and then we add the values kept at both the pointers. 
2. If their sum is smaller than X then we shift the left pointer to right or if their sum is greater than X then we shift the right pointer to left, in order to get closer to the sum. 
3. We keep moving the pointers until we get the sum as X. 




```
function isPairSum(arr, N, x) 
{ 
    var left = 0, right = arr.length - 1; 
    while (left < right) 
    { 
        var sum = arr[left] + arr[right]; 
        if(sum == x) 
        { 
            return [left, right]; 
        } 
        if(sum > x) 
        { 
            right--; 
        } 
        if(sum < x) 
        { 
            left++ 
        } 
    } 
    return [-1,-1]; 
} 
isPairSum([3,5,9,2,8,10,11], 7, 17);
```

Complexity Analysis:  
- Time Complexity: Depends on what sorting algorithm we use. 
	- If Merge Sort or Heap Sort is used then (N), (nlogn) in worst case.
	- If Quick Sort is used then O(n^2) in worst case.
- Space Complexity: This too depends on sorting algorithm. The auxiliary space is O(n) for merge sort and O(1) for Heap Sort.


An Alternative Solution

Instead of using the Two Pointers Solution, we can use a HashTable to solve the problem.

We are searching the array for 2 items, x and y where x + y = target. This means that, during our iteration when we are at number x, we are looking for a y (which is equivalent to target - x, basic maths!).

If we found a target - x value in HashTable, we found our pair! If not, we will insert x into the HashTable, so that we can search for it later.

```
deftwoSum(self,nums:List[int],target:int)->List[int]:
    num_map={}    # to store numbers and their indices
    for i,num in enumerate(nums):
        if target - num in num_map:
            return[num_map[target-num],i]
        else:
        num_map[nums[i]] = i
    return[-1,-1]
```

Time Complexity: O(N) where N is the number of elements in the input array (nums).
Space Complexity: O(N), in the worst case, we will be pushing N numbers to HashMap.


How to identify?

So we want to be able to identify the problems that Two Pointers pattern works.
- The problem involve sorted arrays (or Linked Lists), a set of pair elements, or a triplet or even a subarray.
- There is a target value to match or duplicates to be removed.
Most of these type of problems can be solved in O(N) time complexity and O(1) or O(N) space complexity.


Similar LeetCode Problems

- LeetCode 15 - 3Sum [medium]
- LeetCode 16 - 3Sum Closest [medium]
- LeetCode 26 - Remove Duplicates from Sorted Array [easy]
- LeetCode 27 - Remove Element [easy]
- LeetCode 42 - Trapping Rain Water [hard]
- LeetCode 75 - Sort Colors [medium]
- LeetCode 125 - Valid Palindrome [easy]
- LeetCode 259 - 3Sum Smaller [medium] [premium]
- LeetCode 349 - Intersection of Two Arrays [easy]
- LeetCode 350 - Intersection of Two Arrays II [easy]
- LeetCode 680 - Valid Palindrome II [easy]
- LeetCode 713 - Subarray Product Less Than K [medium]
- LeetCode 977 - Squares of a Sorted Array [easy]
