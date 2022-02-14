



What is Bit Manipulation?

Bit manipulation is the act of algorithmically manipulating bits or other pieces of data shorter than a word. Bitwise operators are usually fast compared to arithmetic and other math operations as it has constant time complexity.Bit manipulation, in some cases, can obviate or reduce the need to loop over a data structure and can give many-fold speed ups, as bit manipulations are processed in parallel.


Computer programming tasks that require bit manipulation include:

- Low-level device control
- Error detection and correction algorithms
- Data compression
- Encryption algorithms
- Optimization


What is Binary Number System?

Binary code refers to the numeric system that only consists of two numbers, 0 and 1, which are used to represent data and instructions. The numbers 0 and 1 are called bits of binary digits. A bit . A bit as being "set" or "clear" is just another way of saying that the bit has the value 1 (set) or 0 (clear).

If a number system has n digits, we say that the base of the number system is n. So the binary number system can also be called the base-2 number system.


2. If binary code is something only computers can understand, why should you learn about it?

Binary codes are essential because without them, computers will not understand your instructions in programming. Even if the computer allows you to view text, images, or videos, they cannot understand any of these, and the only way for them to do it is through binary codes. Even though we do need a few more digits than we did with the decimal system, the binary system is just as good as the decimal system for displaying numbers. Well, in fact, we are not limited to numbers, different types of information can also be represented in binary code, too! To be able to represent text in binary code, we can use simple numbers to represent the different letters in the alphabet. So, A could be 1, B could be 2, and so on. Also, images and graphics displayed on your screen consists of pixels and each pixel in an image has a numerical value that determines the color it should display. This means that, we can represent images and graphics with binary code.



3. How does the binary number system works?

When learning binary, remember that 0 and 1 stand for off and on. In other words, they act as a switch, a device that allows current to pass through a circuit. With switches, electricity will run on computers. The binary that acts as a switch uses a simple principle called Boolean logic. This is used to control how electricity coordinates with computer operations. Suppose the Boolean logic translates to true, the switch is turned on, whereas when Boolean logic translates to false, the switch is turned off.

To be able to understand the binary number system, we need to take a closer look to the decimal number system. In the decimal system, each digit in a certain number represents the 1’s, the 10’s, the 100’s, and so on, starting from the right hand side.


So, with the number 123, for example, we have a 3 representing the 1’s, a 2 representing the 10’s, and finally a 1 to represent the 100’s and total of them are 123. We are starting from 10 to the power of 0 and increasing the powers while moving to left 1, 2, 3 and so on.

In the binary system, instead of using powers of 10, we use powers of 2.


In the binary system, each digit in a certain number represents 1’s, 2’s, 4’s, 8’s, 16’s, 32’s, 64’s, 128’s, 256’s and so on, starting from the right hand side.


4. What about negative numbers?


Computers use a method called Two’s Complement  to represent negative numbers. Also this method can be more effective when performing mathematical operations like adding and subtracting.

In this method, the bit at the far left side of the bit pattern is the most significant bit or MSB is used to indicate positive or negative numbers. Positive numbers always start with a 0 and the remaining bits are used to store the actual size of the number. Four-bit, positive, two’s complement numbers would be 0000 = 0, 0001 = 1, up to 0111 = 7. The smallest positive number is the smallest binary value.

The most significant (leftmost) bit is called the sign bit. The sign bit is always 0 for positive integers, and 1 for negative integers.


Negative numbers always start with a 1 and the remaining bits are used to store the actual size of the number. The biggest negative number is the largest binary value. (e.g. 1111 is -1)






 5. Using Two's Complement method to convert positive binary number to its negative value


 1.  Find the positive binary value for the negative number you want to represent.
 2. Add a 0 to the front of the number, to indicate that it is positive.
 3. Invert or find the complement of each bit in the number.
 4. Add 1 to this number.

Ben Eater is explaining these steps very clearly in this video.



6. Bitwise Operators

Working with primitive data types like bytes, booleans , ints, floats, doubles or with data structures is normal for a programmer. Sometimes in Computer Science, you need to go beyond this to a more deeper level where you need to understand the importance of bits. This is especially important if you are working on data compression and encryption algorithms, optimization, data correction and error detection algorithms and so on. Bitwise operators operate on integers and characters but not on data types float or double.

The operands are converted to 32-bit integers and expressed by a series of bits (zeroes and ones).  Numbers with more than 32 bits get their most significant bits discarded. For example, the following integer with more than 32 bits will be converted to a 32 bit integer:
```
Before: 11100110111110100000000000000110000000000001
After:              10100000000000000110000000000001
```

Followings are the bitwise operators that we can use in many programming languages.
Operator
Description
Usage
&
AND
Mask particular part of byte
|
OR

^
XOR (Exclusive OR)

~
One’s Complement
Turn a bit on/off
<<
Left Shift
Shift the bit to left
>>
Right Shift
Shift the bit to right

AND Operator

AND operator (&) returns a 1 in each bit position for which the corresponding bits of both operands are 1s. Bitwise ANDing any number x with 0 yields 0.
A
B
A&B
0
0
0
0
1
0
1
0
0
1
1
1

```
const a = 5;        // 00000000000000000000000000000101
const b = 3;        // 00000000000000000000000000000011

console.log(a & b); // 00000000000000000000000000000001
// expected output: 1
```





Use 0:  Brian Kernighan’s Algorithm to count set bits in an integer

Subtracting 1 from a decimal number flips all the bits after the rightmost set bit(which is 1) including the rightmost set bit. 
```
10 in binary is 00001010  
9 in binary is 00001001  
8 in binary is 00001000  
7 in binary is 00000111
```

So if we subtract a number by 1 and do it bitwise & with itself (n & (n-1)), we unset the rightmost set bit. If we do n & (n-1) in a loop and count the number of times the loop executes, we get the set bit count.  The beauty of this solution is the number of times it loops is equal to the number of set bits in a given integer. 

Use 1: Even or odd

For integers, the least significant bit (first bit or rightmost bit) can be used to determine whether the number is even or odd. If the least significant bit is turned on (set to 1), the number is odd; otherwise, the number is even.

```
function isOddOrEven(int){ 
    if((int & 1) === 0) { 
        console.log(`${int} is Even!`); 
    } 
    else { 
        console.log(`${int} is Odd!`); 
    } 
} 
isOddOrEven(37);    // 37 is Odd! 
isOddOrEven(54);    // 54 is Even!
```

Explanation

```
   0010 0101  (binary of 37) 
   0000 0001  (binary of 1) 
& ----------- 
   0000 0001  --> 1, so 37 is ODD

   0011 0110  (binary of 54)  
   0000 0001  (binary of 1)  
& -----------  
   0000 0000  --> 0, so 54 is EVEN
```




Use 2: Test if the n-th bit is set

This bit trick uses the same logic with the previous one to check if n-th bit is set or not.
```
function check_nth_bit(num, n) { 
  if (num & (1 << n)) { 
    console.log(`${num} = ${dec2bin(num)} (binary) and ${n}th bit is set`); 
  } else { 
    console.log(`${num} = ${dec2bin(num)} (binary) and ${n}th bit is NOT set`); 
  } 
} 
// This method converts decimal to binary 
function dec2bin(dec) { 
  return number.toString(2); 
}
```

Left shift (<<) finds the correct position of the bit which we want to test
```
1         0000 0001
1 << 1    0000 0010
1 << 2    0000 0100
1 << 3    0000 1000
1 << 4    0001 0000
1 << 5    0010 0000
and so on...
```

If the result after this AND (&) operation is 0, then checked bit is 0, otherwise that bit was set.
Let’s try with 175 and check if 5th bit is set;
```
   1010 1111  (binary of 175)  
   0010 0000  (1 << 5)
& -----------
   0010 0000 --> 5th bit is set
```







OR Operator

OR operator (|) returns a 1 in each bit position for which the corresponding bits of either or both operands are 1s. Bitwise ORing any number x with 0 yields x.
A
B
A|B
0
0
0
0
1
1
1
0
1
1
1
1

```
const a = 5;        // 00000000000000000000000000000101
const b = 3;        // 00000000000000000000000000000011

console.log(a | b); // 00000000000000000000000000000111
// expected output: 7
```


Use 1: Turning on bits

In bit masking applications, the | operator can be used to ensure that certain bits in a sequence of bits are turned on (set to 1). This is based on the fact that for any given bit A:

- (A | 0 = A) — The bit remains unchanged when paired with a corresponding 0 bit.
- (A | 1 = 1) — The bit is always turned on by a corresponding 1 bit.

For example, say we have an 8-bit integer and we want to ensure that all the even-position bits (second, fourth, sixth, eighth) are turned on (set to 1). The | operator can be used to achieve this as follows:
- First, create a bit mask whose effect will be to turn on every even-positioned bit of an 8-bit integer. That bit mask will be 0b10101010. Note that the even-positioned bits of the bit mask are set to 1, while every other bit is set to 0.
- Next, perform an | operation using the 8-bit integer and the created bit mask:
```
const mask = 0b10101010;

// 208 => 11010000

// (208 | mask)
// ------------
//   11010000
// | 10101010
// ------------
// = 11111010
// ------------
// = 250 (decimal)

console.log(208 | mask); // 250
```




XOR Operator

XOR  (^)is a logical bitwise operator that returns 0 (false) if both bits are  the same and returns 1 (true) otherwise.  

Properties: 
- Taking XOR of a number with itself returns 0, e.g.,
	- 1 ^ 1 = 0
	- 29 ^ 29 = 0
- Taking XOR of a number with 0 returns the same number, e.g.,
	- 1 ^ 0 = 1
	- 31 ^ 0 = 31
- XOR is Associative & Commutative, which means:
	- (a ^ b) ^ c = a ^ (b ^ c)
	- a ^ b = b ^ a

A
B
A^B
0
0
0
0
1
1
1
0
1
1
1
0

```
const a = 5;        // 00000000000000000000000000000101
const b = 3;        // 00000000000000000000000000000011

console.log(a ^ b); // 00000000000000000000000000000110
// expected output: 6
```


Single Number (easy)

LeetCode 136 - Single Number [easy]
In a non-empty array of integers, every number appears twice except for one, find that single number.
Example 1:
```
Input: 1, 4, 2, 1, 3, 2, 3
Output: 4
```

Example 2:
```
Input: 7, 9, 7
Output: 9
```




Solution 

One straight forward solution can be to use a HashMap kind of data structure and iterate through the input:
- If number is already present in HashMap, remove it.
- If number is not present in HashMap, add it.
- In the end, only number left in the HashMap is our required single number.

Time and space complexity Time Complexity of the above solution will be O(n) and space complexity will also be O(n).
Can we do better than this using the XOR Pattern?

Solution with XOR 

Recall the following two properties of XOR:
- It returns zero if we take XOR of two same numbers.
- It returns the same number if we XOR with zero.
So we can XOR all the  numbers in the input; duplicate numbers will zero out each other and we  will be left with the single number.

Code 

Here is what our algorithm will look like:
```
function find_single_number(arr) {
  let num = 0;
  for (i = 0; i < arr.length; i++){
    num ^= arr[i];
  }
  return num;
}
  
console.log(find_single_number([1, 4, 2, 1, 3, 2, 3]));
```
Time Complexity: Time complexity of this solution is O(n) as we iterate through all numbers of the input once.
Space Complexity: The algorithm runs in constant space O(1).

Two Single Numbers (medium)
LeetCode 260 - Single Number III [medium]
In a non-empty array of  numbers, every number appears exactly twice except two numbers that  appear only once. Find the two numbers that appear only once.
Example 1:
```
Input: [1, 4, 2, 1, 3, 5, 6, 2, 3, 5]
Output: [4, 6]
```
Example 2:
```
Input: [2, 1, 3, 2]
Output: [1, 3]
```


Solution 

This problem is quite similar to Single Number,  the only difference is that, in this problem, we have two single  numbers instead of one. Can we still use XOR to solve this problem?
Let’s assume num1 and num2 are the two single numbers. If we do XOR of all elements of the given array, we will be left with XOR of num1 and num2 as all other numbers will cancel each other because all of them appeared twice. Let’s call this XOR n1xn2. 

Now that we have XOR of num1 and num2, how can we find these two single numbers?
As we know that num1 and num2 are two different numbers, therefore, they should have at least one bit different between them. If a bit in n1xn2 is ‘1’, this means that num1 and num2 have different bits in that place, as we know that we can get ‘1’ only when we do XOR  of two different bits.

We can take any bit which is ‘1’ in n1 x n2  and partition all numbers in the given array into two groups based on  that bit. One group will have all those numbers with that bit set to ‘0’  and the other with the bit set to ‘1’. This will ensure that num1 will be in one group and num2 will be in the other. We can take XOR of all numbers in each group separately to get num1 and num2, as all other numbers in each group will cancel each other. 

Here are the steps of our algorithm:
1. Taking XOR of all numbers in the given array will give us XOR of num1 and num2, calling this XOR as n1xn2.
2. Find any bit which is set in n1xn2. We can take the rightmost bit which is ‘1’. Let’s call this rightmostSetBit.
3. Iterate through all numbers of the input array to partition them into two groups based on rightmostSetBit. Take XOR of all numbers in both the groups separately. Both these XORs are our required numbers.

Code 

Here is what our algorithm will look like:
```
function find_single_numbers(nums) {
  // get the XOR of the all the numbers
  let n1xn2 = 0;
  nums.forEach((num) => {
    n1xn2 ^= num;
  });
  // get the rightmost bit that is '1'
  let rightmost_set_bit = 1;
  while ((rightmost_set_bit & n1xn2) === 0) {
    rightmost_set_bit = rightmost_set_bit << 1;
  }
  let num1 = 0,
    num2 = 0;
  nums.forEach((num) => {
    if ((num & rightmost_set_bit) !== 0) // the bit is set
      num1 ^= num;
    else // the bit is not set
      num2 ^= num;
  });
  return [num1, num2];
}
console.log(`Single numbers are: ${find_single_numbers([1, 4, 2, 1, 3, 5, 6, 2, 3, 5])}`);
console.log(`Single numbers are: ${find_single_numbers([2, 1, 3, 2])}`);
```


Time Complexity 

The time complexity of this solution is O(n) where ‘n’ is the number of elements in the input array.

Space Complexity 

The algorithm runs in constant space O(1).

Complement of Base 10 Number (medium)
Every non-negative integer  N has a binary representation, for example, 8 can be represented as  “1000” in binary and 7 as “0111” in binary.
The complement of a binary  representation is the number in binary that we get when we change every  1 to a 0 and every 0 to a 1.  For example, the binary complement of  “1010” is “0101”.
For a given positive number N in base-10, return the complement of its binary representation as a base-10 integer.
Example 1:
```
Input: 8
Output: 7
Explanation: 8 is 1000 in binary, its complement is 0111 in binary, which is 7 in base-10.
```
Example 2:
```
Input: 10
Output: 5
Explanation: 10 is 1010 in binary, its complement is 0101 in binary, which is 5 in base-10.
```


Solution 

Recall the following properties of XOR:
1. It will return 1 if we take XOR of two different bits i.e. 1^0 = 0^1 = 1.
2. It will return 0 if we take XOR of two same bits i.e. 0^0 = 1^1 = 0. In other words, XOR of two same numbers is 0.
3. It returns the same number if we XOR with 0.
From the above-mentioned  first property, we can conclude that XOR of a number with its complement  will result in a number that has all of its bits set to 1. For example,  the binary complement of “101” is “010”; and if we take XOR of these  two numbers, we will get a number with all bits set to 1, i.e., 101 ^ 010 = 111
We can write this fact in the following equation:
```
number ^ complement = all_bits_set
```
Let’s add ‘number’ on both sides:
```
number ^ number ^ complement = number ^ all_bits_set
```
From the above-mentioned second property:
```
0 ^ complement = number ^ all_bits_set
```
From the above-mentioned third property:
```
complement = number ^ all_bits_set
```

We can use the above fact to find the complement of any number.

How do we calculate ‘all_bits_set’? 
One way to calculate all_bits_set will be to first count  the bits required to store the given number. We can then use the fact  that for a number which is a complete power of ‘2’ i.e., it can be  written as pow(2, n), if we subtract ‘1’ from such a number, we get a  number which has ‘n’ least significant bits set to ‘1’. For example, ‘4’  which is a complete power of ‘2’, and ‘3’ (which is one less than 4)  has a binary representation of ‘11’ i.e., it has ‘2’ least significant  bits set to ‘1’.

Code 

Here is what our algorithm will look like:
```
function calculate_bitwise_complement(num) {
  // count number of total bits in 'num'
  let bit_count = 0;
  let n = num;
  while (n > 0) {
    bit_count++;
    n = n >> 1;
  }
  // for a number which is a complete power of '2' i.e., it can be written as pow(2, n), if we
  // subtract '1' from such a number, we get a number which has 'n' least significant bits set to '1'.
  // For example, '4' which is a complete power of '2', and '3' (which is one less than 4) has a binary 
  // representation of '11' i.e., it has '2' least significant bits set to '1' 
  let all_bits_set = Math.pow(2, bit_count) - 1;
  // from the solution description: complement = number ^ all_bits_set
  return num ^ all_bits_set;
}
console.log(`Bitwise complement is: ${calculate_bitwise_complement(8)}`);
console.log(`Bitwise complement is: ${calculate_bitwise_complement(10)}`);
```


Time Complexity 

Time complexity of this solution is O(b) where ‘b’ is the number of bits required to store the given number.

Space Complexity 

Space complexity of this solution is O(1).


Problem Statement (hard) 

Given a binary matrix representing an image, we want to flip the image horizontally, then invert it.
To flip an image  horizontally means that each row of the image is reversed.  For example,  flipping [0, 1, 1] horizontally results in [1, 1, 0].
To invert an image means  that each 0 is replaced by 1, and each 1 is replaced by 0. For example,  inverting [1, 1, 0] results in [0, 0, 1].
Example 1:
```
Input: [
  [1,0,1],
  [1,1,1],
  [0,1,1]
]
Output: [
  [0,1,0],
  [0,0,0],
  [0,0,1]
]

```
Explanation: First reverse each row: [[1,0,1],[1,1,1],[1,1,0]]. Then, invert the image: [[0,1,0],[0,0,0],[0,0,1]]
Example 2:
```
Input: [
  [1,1,0,0],
  [1,0,0,1],
  [0,1,1,1], 
  [1,0,1,0]
]
Output: [
  [1,1,0,0],
  [0,1,1,0],
  [0,0,0,1],
  [1,0,1,0]
]

```
Explanation: First reverse each row: [[0,0,1,1],[1,0,0,1],[1,1,1,0],[0,1,0,1]]. Then invert the image: [[1,1,0,0],[0,1,1,0],[0,0,0,1],[1,0,1,0]]

Solution

- Flip: We can flip the image in place by replacing ith element from left with the ith element from the right.
- Invert: We can take XOR of each element with 1. If it is 1 then it will become 0 and if it is 0 then it will become 1.

Code 

Here is what our algorithm will look like:
```
function flip_and_invert_image(matrix) {
  const C = matrix.length;
  for (var row = 0; row < C; ++row) {
    for (var col = 0; col < Math.floor((C + 1) / 2); ++col) {
      var tmp = matrix[row][col] ^ 1;
      matrix[row][col] = matrix[row][C - 1 - col] ^ 1;
      matrix[row][C - 1 - col] = tmp;
    }
  }
  return matrix;
}
console.log(flip_and_invert_image([[1,0,1], [1,1,1], [0,1,1]]))
console.log(flip_and_invert_image([[1,1,0,0],[1,0,0,1],[0,1,1,1],[1,0,1,0]]))
```


Time Complexity 

The time complexity of this solution is O(n) as we iterate through all elements of the input.

Space Complexity 

The space complexity of this solution is O(1).




Problem: Given an array of n−1 integers in the range from 1 to n, find the one number that is missing from the array.

Example:
```
Input: 1, 5, 2, 6, 4
Answer: 3
```

A straight forward approach to solve this problem can be:
1. Find the sum of all integers from 1 to n; let’s call it s1.
2. Subtract all the numbers in the input array from s1; this will give us the missing number.

This is what the algorithm will look like:
```
function find_missing_number(arr) {
  const n = arr.length + 1;
  // find sum of all numbers from 1 to n.
  let s1 = 0;
  for (let i = 1; i <= n; i++)
    s1 += i;
  // subtract all numbers in input from sum.
  arr.forEach((num) => {
    s1 -= num;
  });
  // s1, now, is the missing number
  return s1;
}
console.log(`Missing number is: ${find_missing_number([1, 5, 2, 6, 4])}`);
```

Time & Space complexity: The time complexity of the above algorithm is O(n) and the space complexity is O(1).




What could go wrong with the above algorithm? 

While finding the sum of numbers from 1 to n, we can get integer overflow when n is large.

How can we avoid this? Can XOR help us here?
Remember the important  property of XOR that it returns 0 if both the bits in comparison are the  same. In other words, XOR of a number with itself will always result in  0. This means that if we XOR all the numbers in the input array with  all numbers from the range 1 to n  then each number in the input is going to get zeroed out except the  missing number. 

Following are the set of steps to find the missing  number using XOR:
1. XOR all the numbers from 1 to n let’s call it x1.
2. XOR all the numbers in the input array, let’s call it x2.
3. The missing number can be found by x1 XOR x2.
Here is what the algorithm will look like:
```
function find_missing_number(arr) {
  const n = arr.length + 1;
  // x1 represents XOR of all values from 1 to n
  // find sum of all numbers from 1 to n.
  let x1 = 1;
  for (let i = 2; i <= n; i++)
    x1 = x1 ^ i;
  // x2 represents XOR of all values in arr
  let x2 = arr[0];
  for (let i = 1; i < n-1; i++)
    x2 = x2 ^ arr[i];
  // missing number is the xor of x1 and x2
  return x1 ^ x2;
}
console.log(`Missing number is: ${find_missing_number([1, 5, 2, 6, 4])}`);
```

Time & Space complexity: The time complexity of the above algorithm is O(n) and the space complexity is O(1), which is same as that of the previous  solution but, in this algorithm, we will not have any integer overflow  problem.





How to identify?

Knowing XOR properties well opens some surprising doors in your problem solving skills. To be able to identify XOR related problems are mostly coming from previous experiences. But if you need to eliminate the same numbers from an integer array, using Bit Manipulation Tricks is extremely helpful.


Similar LeetCode Problems

- LeetCode 137 - Single Number II [medium]




Toggling bits

In bit masking applications, the ^ operator is commonly used for toggling or flipping certain bits in a sequence of bits. This is based on the fact that for any given bit A:

- The bit remains unchanged when paired with a corresponding 0 bit.
  (A ^ 0 = A)
- The bit is always toggled when paired with a corresponding 1 bit.
  (A ^ 1 = 1) — if A is 0
  (A ^ 1 = 0) — if A is 1

For example, say we have an 8-bit integer and we want to ensure that every bit is toggled except the least significant (first) and most significant (eighth) bits. The ^ operator can be used to achieve this as follows:
- First, create a bit mask whose effect will be to toggle every bit of an 8-bit integer except the least significant and most significant bits. That bit mask will be 0b01111110. Note that the bits to be toggled are set to 1, while every other bit is set to 0.
- Next, perform an ^ operation using the 8-bit integer and the created bit mask:
```
const mask = 0b01111110;

// 208 => 11010000

// (208 ^ mask)
// ------------
// 11010000
// ^ 01111110
// ------------
// = 10101110
// ------------
// = 174 (decimal)

console.log(208 ^ mask); // 174
```




NOT (One’s Complement) Operator

NOT operator (~) inverts the bits of its operand. Like other bitwise operators, it converts the operand to a 32-bit signed integer. 
The 32-bit signed integer operand is inverted according to two's complement. That is, the presence of the most significant bit is used to express negative integers.
Bitwise NOTing any number x yields -(x + 1). For example, ~-5 yields 4. 
Note that due to using 32-bit representation for numbers both ~-1 and ~4294967295 (2^32 - 1) results in 0.
A
~A
0
1
0
0

```
const a = 5;     // 00000000000000000000000000000101
const b = -3;    // 11111111111111111111111111111101

console.log(~a); // 11111111111111111111111111111010
// expected output: -6

console.log(~b); // 00000000000000000000000000000010
// expected output: 2
```




Left Shift Operator

Left shift operator (<<) shifts the first operand the specified number of bits to the left. Excess bits shifted off to the left are discarded. Zero bits are shifted in from the right.
Bitwise shifting any number x to the left by y bits yields x * 2 ** y. So e.g.: 9 << 3 translates to: 9 * (2 ** 3) = 9 * (8) = 72
```
const a = 5;         // 00000000000000000000000000000101
const b = 2;         // 00000000000000000000000000000010

console.log(a << b); // 00000000000000000000000000010100
// expected output: 20
```


Color conversion: RGB to hex

One very useful application of the left shift (<<) operator is converting colors from an RGB representation to a hexadecimal representation.

The color value for each component of an RGB color is between 0 - 255. Simply put, each color value can be represented perfectly by 8 bits.

```
  0 => 0b00000000 (binary) => 0x00 (hexadecimal)
255 => 0b11111111 (binary) => 0xff (hexadecimal)
```
Thus, the color itself can be perfectly represented by 24 bits (8 bits each for red, green, and blue components). The first 8 bits starting from the right will represent the blue component, the next 8 bits will represent the green component, and the 8 bits after that will represent the red component.

```
(binary) => 11111111 00100011 00010100

   (red) => 11111111 => ff => 255
 (green) => 00100011 => 23 => 35
  (blue) => 00010100 => 14 => 20

   (hex) => ff2314
```
Now that we understand how to represent the color as a 24-bit sequence, let’s see how we can compose the 24 bits of the color from the values of the color’s individual components. Let’s say we have a color represented by rgb(255, 35, 20). Here is how we can compose the bits:

```
  (red) => 255 => 00000000 00000000 00000000 11111111
(green) =>  35 => 00000000 00000000 00000000 00100011
 (blue) =>  20 => 00000000 00000000 00000000 00010100

// Rearrange the component bits and pad with zeroes as necessary
// Use the left shift operator

  (red << 16) => 00000000 11111111 00000000 00000000
 (green << 8) => 00000000 00000000 00100011 00000000
       (blue) => 00000000 00000000 00000000 00010100

// Combine the component bits together using the OR (|) operator
// ( red << 16 | green << 8 | blue )

      00000000 11111111 00000000 00000000
    | 00000000 00000000 00100011 00000000
    | 00000000 00000000 00000000 00010100
// -----------------------------------------
      00000000 11111111 00100011 00010100
// -----------------------------------------
```

Now that the procedure is pretty clear, here is a simple function that takes the RGB values of a color as an input array and returns the corresponding hexadecimal representation of the color based on the above procedure:
```
function rgbToHex ([red = 0, green = 0, blue = 0] = []) {
  return `#${(red << 16 | green << 8 | blue).toString(16)}`;
}
```




Right Shift Operator

Right shift operator (>>) shifts the first operand the specified number of bits to the right. Excess bits shifted off to the right are discarded. Copies of the leftmost bit are shifted in from the left. Since the new leftmost bit has the same value as the previous leftmost bit, the sign bit (the leftmost bit) does not change. Hence the name "sign-propagating".
```
const a = 5;          //  00000000000000000000000000000101
const b = 2;          //  00000000000000000000000000000010
const c = -5;         // -00000000000000000000000000000101

console.log(a >> b);  //  00000000000000000000000000000001
// expected output: 1

console.log(c >> b);  // -00000000000000000000000000000010
// expected output: -2
```


Color extraction

One very good application of the right shift (>>) operator is extracting RGB color values from a color. When the color is represented in RGB, it is very easy to distinguish between the red, green, and blue color component values. However, it will take a bit more effort for a color represented as hexadecimal.

In the previous section, we saw the procedure for composing the bits of a color from the bits of its individual components (red, green, and blue). If we work through that procedure backwards, we will be able to extract the values of the individual components of the color. Let’s give that a shot.

Let’s say we have a color represented by the hexadecimal notation #ff2314. Here is the signed 32-bit representation of the color:
```
(color) => ff2314 (hexadecimal) => 11111111 00100011 00010100 (binary)

// 32-bit representation of color
00000000 11111111 00100011 00010100
```

To get the individual components, we will right-shift the color bits by multiples of 8 as necessary until we get the target component bits as the first 8 bits from the right. Since the most significant bit of the 32 bits for the color is 0, we can safely use the sign-propagating right shift (>>) operator for this.
```
color => 00000000 11111111 00100011 00010100

// Right shift the color bits by multiples of 8
// Until the target component bits are the first 8 bits from the right

  red => color >> 16
      => 00000000 11111111 00100011 00010100 >> 16
      => 00000000 00000000 00000000 11111111

green => color >> 8
      => 00000000 11111111 00100011 00010100 >> 8
      => 00000000 00000000 11111111 00100011

 blue => color >> 0 => color
      => 00000000 11111111 00100011 00010100
```

Now that we have the target component bits as the first 8 bits from the right, we need a way to mask out every other bits except the first 8 bits. That brings us back to the AND (&) operator. Remember that the & operator can be used to ensure that certain bits are turned off.

Let’s start by creating the required bit mask. That would look like this:
```
mask => 00000000 00000000 00000000 11111111
     => 0b11111111 (binary)
     => 0xff (hexadecimal)
```

With the bit mask ready, we can carry out an AND (&) operation on each of the results from the previous right-shifting operations using the bit mask to extract the target component bits.
```
  red => color >> 16 & 0xff
      =>   00000000 00000000 00000000 11111111
      => & 00000000 00000000 00000000 11111111
      => = 00000000 00000000 00000000 11111111
      =>   255 (decimal)

green => color >> 8 & 0xff
      =>   00000000 00000000 11111111 00100011
      => & 00000000 00000000 00000000 11111111
      => = 00000000 00000000 00000000 00100011
      =>   35 (decimal)

 blue => color & 0xff
      =>   00000000 11111111 00100011 00010100
      => & 00000000 00000000 00000000 11111111
      => = 00000000 00000000 00000000 00010100
      =>   20 (decimal)
```

Based on the above procedure, here is a simple function that takes a hex color string (with six hexadecimal digits) as input and returns the corresponding array of RGB color component values.
```
function hexToRgb (hex) {
  hex = hex.replace(/^#?([0-9a-f]{6})$/i, '$1');
  hex = Number(`0x${hex}`);

  return [
    hex >> 16 & 0xff, // red
    hex >> 8 & 0xff,  // green
    hex & 0xff        // blue
  ];
}
```


Config flags

Another pretty common application of bitwise operators and bit masking: config flags.

Let’s say we have a function that accepts a couple of boolean options that can be used to control how the function runs or the kind of value it returns. One possible way to create this function is by passing all the options as arguments to the function, probably with some default values, like so:

```
function doSomething (optA = true, optB = true, optC = false, optD = true, ...) {
  // something happens here...
}
```

Surely, this isn’t so convenient. Here are two cases in which this approach starts getting quite problematic:
- Imagine that we have more than 10 boolean options. We just can’t define our function with that many parameters.
- Imagine that we just want to specify a different value for the fifth and ninth options and leave the others with their default values. We will need to call the function, passing the default values as arguments for all the other options while passing the desired values for the fifth and ninth options.

One way to solve the issues with the previous approach would be to use an object for the config options, like so:
```
const defaultOptions = {
  optA: true,
  optB: true,
  optC: false,
  optD: true,
  ...
};

function doSomething (options = defaultOptions) {
  // something happens here...
}
```

This approach is very elegant, and you’ve most likely seen it used, or even used it yourself at some point or another. With this approach, however, the options argument will always be an object, which can be considered overkill for just configuration options.

If all the options take boolean values, we could use an integer instead of an object to represent the options. In this case, certain bits of the integer will be mapped to designated options. If a bit is turned on (set to 1), the designated option’s value is true;otherwise, it is false.

We can demonstrate this approach using a simple example. Let’s say we have a function that normalizes the items of an array list containing numbers and returns the normalized array. The returned array can be controlled by three options, namely:
- fraction: divides each item of the array by the maximum item in the array
- unique: removes duplicate items from the array
- sorted: sorts the items of the array from lowest to highest

We can use an integer with 3 bits to represent these options, each bit being mapped to an option. The following code snippet shows the option flags:
```
const LIST_FRACTION = 0x1; // (001)
const LIST_UNIQUE = 0x2;   // (010)
const LIST_SORTED = 0x4;   // (100)
```

To activate one or more options, the | operator can be used to combine the corresponding flags as necessary. For example, we can create a flag that activates all the options, as follows:
```
const LIST_ALL = LIST_FRACTION | LIST_UNIQUE | LIST_SORTED; // (111)
```

Again, let’s say we want only the fraction and sorted options to be activated by default. We could use the | operator again, as follows:
```
const LIST_DEFAULT = LIST_FRACTION | LIST_SORTED; // (101)
```

While this doesn’t look bad with just three options, it tends to become quite messy when there are so many options, and a lot of them are required to be activated by default. In such a scenario, a better approach will be to deactivate the unwanted options using the ^ operator:
```
const LIST_DEFAULT = LIST_ALL ^ LIST_UNIQUE; // (101)
```

Here, we have the LIST_ALL flag that activates all the options. We then use the ^ operator to deactivate the unique option, leaving other options activated as required.
Now that we have the option flags ready, we can go ahead and define the normalizeList() function:
```
function normalizeList (list, flag = LIST_DEFAULT) {
  if (flag & LIST_FRACTION) {
    const max = Math.max(...list);
    list = list.map(value => Number((value / max).toFixed(2)));
  }
  if (flag & LIST_UNIQUE) {
    list = [...new Set(list)];
  }
  if (flag & LIST_SORTED) {
    list = list.sort((a, b) => a - b);
  }
  return list;
}
```

To check if an option is activated, we use the & operator to check if the corresponding bit of the option is turned on (set to 1). The & operation is carried out with the flag argument passed to the function and the corresponding flag for the option, as demonstrated in the following code snippet:
```
// Checking if the unique option is activated
// (flag & LIST_UNIQUE) === LIST_UNIQUE (activated)
// (flag & LIST_UNIQUE) === 0 (deactivated)

flag & LIST_UNIQUE
```
