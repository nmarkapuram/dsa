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


# DSA Notes – Part 2 (Linked List + Strings)

---

# Linked List

## Key Patterns
- Use **Sentinel (Dummy) Node** when deleting/modifying head
- Use **Two Pointers** for distance-based problems
- Use **Fast/Slow pointers** for traversal problems

---

## 19. Remove Nth Node From End of List

### Approach 1: Length Calculation

Steps:
1. Add sentinel node
2. Calculate length
3. Find `(len - n)` node
4. Remove next node

```js
var removeNthFromEnd = function (head, n) {
    let dummy = new ListNode();
    dummy.next = head;

    let len = 0, curr = head;

    while (curr) {
        len++;
        curr = curr.next;
    }

    let prev = dummy;
    for (let i = 0; i < len - n; i++) {
        prev = prev.next;
    }

    prev.next = prev.next.next;

    return dummy.next;
};
```

---

### Approach 2: Two Pointer (Optimal)

```js
var removeNthFromEnd = function (head, n) {
    let dummy = new ListNode();
    dummy.next = head;

    let first = dummy, second = dummy;

    for (let i = 0; i < n; i++) {
        first = first.next;
    }

    while (first.next) {
        first = first.next;
        second = second.next;
    }

    second.next = second.next.next;

    return dummy.next;
};
```

---

## 83. Remove Duplicates from Sorted List

```js
var deleteDuplicates = function(head) {
    let curr = head;

    while (curr && curr.next) {
        if (curr.val === curr.next.val) {
            curr.next = curr.next.next;
        } else {
            curr = curr.next;
        }
    }

    return head;
};
```

---

## 328. Odd Even Linked List

```js
var oddEvenList = function(head) {
    if (!head || !head.next) return head;

    let odd = head;
    let even = head.next;
    let evenHead = even;

    while (even && even.next) {
        odd.next = odd.next.next;
        even.next = even.next.next;

        odd = odd.next;
        even = even.next;
    }

    odd.next = evenHead;

    return head;
};
```

---

## 2. Add Two Numbers

Key Insight:
- Loop condition must include carry

```js
var addTwoNumbers = function(l1, l2) {
    let dummy = new ListNode();
    let curr = dummy;
    let carry = 0;

    while (l1 || l2 || carry) {
        let val1 = l1 ? l1.val : 0;
        let val2 = l2 ? l2.val : 0;

        let sum = val1 + val2 + carry;
        carry = Math.floor(sum / 10);

        curr.next = new ListNode(sum % 10);
        curr = curr.next;

        if (l1) l1 = l1.next;
        if (l2) l2 = l2.next;
    }

    return dummy.next;
};
```

---

## 21. Merge Two Sorted Lists

```js
var mergeTwoLists = function(list1, list2) {
    let dummy = new ListNode();
    let curr = dummy;

    while (list1 && list2) {
        if (list1.val < list2.val) {
            curr.next = list1;
            list1 = list1.next;
        } else {
            curr.next = list2;
            list2 = list2.next;
        }
        curr = curr.next;
    }

    curr.next = list1 || list2;

    return dummy.next;
};
```

---

## 61. Rotate List

Key Insight:
- Rotation depends on `k % length`

```js
var rotateRight = function(head, k) {
    if (!head || !head.next) return head;

    let len = 1;
    let tail = head;

    while (tail.next) {
        tail = tail.next;
        len++;
    }

    k = k % len;
    if (k === 0) return head;

    let slow = head;
    let fast = head;

    for (let i = 0; i < k; i++) {
        fast = fast.next;
    }

    while (fast.next) {
        slow = slow.next;
        fast = fast.next;
    }

    fast.next = head;
    let newHead = slow.next;
    slow.next = null;

    return newHead;
};
```

---

## 24. Swap Nodes in Pairs

```js
var swapPairs = function(head) {
    let dummy = new ListNode();
    dummy.next = head;

    let prev = dummy;

    while (prev.next && prev.next.next) {
        let first = prev.next;
        let second = first.next;

        first.next = second.next;
        second.next = first;
        prev.next = second;

        prev = first;
    }

    return dummy.next;
};
```

---

# Strings

---

## 58. Length of Last Word

```js
var lengthOfLastWord = function(s) {
    let i = s.length - 1;

    while (i >= 0 && s[i] === ' ') i--;

    let length = 0;

    while (i >= 0 && s[i] !== ' ') {
        length++;
        i--;
    }

    return length;
};
```

---

## 2942. Find Words Containing Character

```js
var findWordsContaining = function(words, x) {
    let result = [];

    for (let i = 0; i < words.length; i++) {
        if (words[i].includes(x)) {
            result.push(i);
        }
    }

    return result;
};
```

---

## 771. Jewels and Stones

### Using Set (Optimal)

```js
var numJewelsInStones = function(jewels, stones) {
    let set = new Set(jewels);
    let count = 0;

    for (let ch of stones) {
        if (set.has(ch)) count++;
    }

    return count;
};
```

Note:
- Max 52 characters → O(1) space effectively

---

## 3541. Most Frequent Vowel and Consonant

```js
var maxFreqSum = function (s) {
    let map = new Map();
    let vowels = new Set(['a','e','i','o','u']);

    for (let ch of s) {
        map.set(ch, (map.get(ch) || 0) + 1);
    }

    let maxVowel = 0;
    let maxConsonant = 0;

    for (let [ch, count] of map) {
        if (vowels.has(ch)) {
            maxVowel = Math.max(maxVowel, count);
        } else {
            maxConsonant = Math.max(maxConsonant, count);
        }
    }

    return maxVowel + maxConsonant;
};
```

---

## 1221. Split a String in Balanced Strings

```js
var balancedStringSplit = function(s) {
    let balance = 0, count = 0;

    for (let ch of s) {
        balance += (ch === 'R') ? 1 : -1;

        if (balance === 0) count++;
    }

    return count;
};
```

---

## 125. Valid Palindrome

```js
var isPalindrome = function(s) {
    let filtered = "";

    for (let ch of s.toLowerCase()) {
        if (/[a-z0-9]/.test(ch)) {
            filtered += ch;
        }
    }

    let reversed = filtered.split('').reverse().join('');

    return filtered === reversed;
};
```

---

## 1903. Largest Odd Number in String

```js
var largestOddNumber = function(num) {
    for (let i = num.length - 1; i >= 0; i--) {
        if (parseInt(num[i]) % 2 !== 0) {
            return num.substring(0, i + 1);
        }
    }
    return "";
};
```

---

## 14. Longest Common Prefix

```js
var longestCommonPrefix = function(strs) {
    let i = 0;

    while (i < strs[0].length) {
        let ch = strs[0][i];

        for (let j = 1; j < strs.length; j++) {
            if (i >= strs[j].length || strs[j][i] !== ch) {
                return strs[0].substring(0, i);
            }
        }

        i++;
    }

    return strs[0];
};
```

---

## 242. Valid Anagram

Idea:
- Same characters with same frequency

Optimal approach:

```js
var isAnagram = function(s, t) {
    if (s.length !== t.length) return false;

    let map = new Map();

    for (let ch of s) {
        map.set(ch, (map.get(ch) || 0) + 1);
    }

    for (let ch of t) {
        if (!map.has(ch) || map.get(ch) === 0) return false;
        map.set(ch, map.get(ch) - 1);
    }

    return true;
};
```

---

# Key Takeaways

## Linked List
- Dummy node avoids edge cases
- Two pointers for distance problems
- Fast/slow for traversal problems

## Strings
- Use reverse traversal for trimming problems
- Use Set/Map for frequency
- Avoid built-ins in interviews when possible

---

# Next Improvements (Optional)
- Add time & space complexity for each problem
- Tag problems by pattern
- Link to LeetCode URLs
- Add edge cases section