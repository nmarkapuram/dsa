# Data Structures & Algorithms Notes

Pattern-oriented notes from LeetCode and DSA practice.

---

# Core Problem-Solving Patterns

## Two Pointers
Use when:
- In-place array modification
- Comparing from both ends
- Fast/slow traversal
- Moving elements conditionally

Signals:
- "Modify in place"
- "Without extra space"
- "Sorted array"
- "Move X to end"
- "Find middle"
- "Cycle detection"

---

## Recursion

Template:

```js
function solve(n){
    if(baseCase) return answer;

    return solve(smallerProblem);
}
```

Use when:
- Problem breaks into subproblems
- Clear base case exists

---

## Sliding Window
Use when:
- Consecutive sequences
- Subarrays
- Running counts

---

## Hashing
Use when:
- Duplicate detection
- Frequency counting
- Fast lookups

---

# Arrays

## 26. Remove Duplicates from Sorted Array
Pattern: Two Pointers

```text
nums = [1,1,2]
Result = [1,2,_]
```

- `i` scans array  
- `k` stores next unique position

Time: O(n)  
Space: O(1)

---

## 27. Remove Element

```text
[3,2,2,3], val=3
-> [2,2,_,_]
```

- Copy only values not equal to target.

---

## 283. Move Zeroes

```text
[0,1,0,3,12]
-> [1,3,12,0,0]
```

- Move non-zeroes forward
- Fill remaining with zeroes

Two passes.

---

## 344 Reverse String

Swap:

```text
0 <-> n-1
1 <-> n-2
```

Formula:

```js
swap(i, n-i-1)
```

Loop only halfway.

---

## Merge Sorted Arrays

- Two pointers
- Compare values
- Insert smaller value
- Continue until `m+n`

---

## 121 Best Time to Buy and Sell Stock

Brute Force:
- Check all pairs  
- O(n²)

Optimal:

```js
profit = Math.max(profit, price-minPrice)
minPrice = Math.min(minPrice, price)
```

Time: O(n)

---

## Max Consecutive Ones

Maintain:

```js
currCount
maxCount
```

- Increment on `1`
- Reset otherwise

---

## 268 Missing Number

Formula:

```text
n*(n+1)/2
```

Missing:

```text
expectedSum - actualSum
```

---

## 136 Single Number

XOR trick:

```text
a ^ a = 0
a ^ 0 = a
```

```js
ans ^= num
```

---

# Recursion

## Sum of First N Numbers

```js
function sum(n){
    if(n==0) return 0;

    return n + sum(n-1);
}
```

---

## Sum of Array

```js
function sum(i){
   if(i<0) return 0;

   return arr[i] + sum(i-1);
}
```

---

## Factorial

```js
function fact(n){
   if(n==1) return 1;

   return n * fact(n-1);
}
```

---

## Power of Two

```js
function power(n){
   if(n==1) return true;

   if(n<1 || n%2!==0)
      return false;

   return power(n/2);
}
```

---

## 509 Fibonacci

```js
function fib(n){
   if(n<=1) return n;

   return fib(n-1)+fib(n-2);
}
```

---

# Searching

## Linear Search

```text
O(n)
```

---

## 704 Binary Search

Requires sorted array.

```js
while(left<=right){

 let mid=Math.floor((left+right)/2);

 if(nums[mid]==target)
    return mid;

 if(nums[mid]>target)
    right=mid-1;

 else
    left=mid+1;
}
```

Time:

```text
O(log n)
```

---

# Sorting

## Bubble Sort

```text
Compare i and i+1
Swap if needed
Bubble largest rightward
```

Time:

```text
O(n²)
```

---

## Selection Sort

- Find minimum
- Swap with current position

---

## Insertion Sort

Insert current element into correct place among previous sorted items.

Like sorting cards.

---

## Merge Sort

```js
left = mergeSort(arr.slice(0,mid))
right = mergeSort(arr.slice(mid))

return merge(left,right)
```

Time:

```text
O(n log n)
```

---

# Linked List

## Node

```js
function Node(val){
    this.val = val;
    this.next = null;
}
```

---

## 707 Design Linked List

```js
var MyLinkedList = function() {
   this.head = null;
   this.size = 0;
}
```

---

## 876 Middle of Linked List

Slow/Fast Pointer:

- Slow moves 1 step
- Fast moves 2 steps

When fast reaches end:
- Slow is middle.

---

## 206 Reverse Linked List

```js
prev=null
curr=head

while(curr){

 temp=curr.next
 curr.next=prev

 prev=curr
 curr=temp
}

return prev
```

---

## 141 Linked List Cycle

### Set Approach

```js
seen = new Set()
```

Detect repeated node.

---

### Floyd Cycle Detection

- Slow = 1 step
- Fast = 2 steps

If they meet → cycle exists

---

## 234 Palindrome Linked List

Steps:
1. Find middle
2. Reverse second half
3. Compare halves

---

## 160 Intersection of Two Linked Lists

- Put List B into Set
- Traverse List A
- First repeated node is answer

---

## 203 Remove Linked List Elements

Use sentinel node:

```js
dummy.next = head
```

Handles deleting head safely.

---

# Interview Heuristics

## In-place?
Think:
- Two pointers

---

## Sorted array?
Think:
- Binary Search
- Two Pointers

---

## Consecutive sequence?
Think:
- Sliding Window
- Counters

---

## Duplicate pairs cancel?
Think:
- XOR

---

## Middle or Cycle?
Think:
- Slow/Fast pointers

---

## Linked list deletions including head?
Think:
- Dummy / Sentinel node

---

# Priority Patterns to Master

1. Two Pointers  
2. Sliding Window  
3. Hash Map / Set  
4. Binary Search  
5. Recursion  
6. Linked List Slow/Fast  
7. Merge Sort  
8. XOR Tricks