# 📚 Data Structures & Algorithms in JavaScript
### Beginner to Super Advanced — Complete Reference Guide
> *Every concept explained clearly with code examples, visual diagrams, complexity analysis, and real-world use cases*

---

## Table of Contents

**PART 1 — FOUNDATIONS**
1. [Big O Notation & Complexity Analysis](#1-big-o-notation--complexity-analysis)
2. [Arrays](#2-arrays)
3. [Strings](#3-strings)
4. [Objects & Hash Maps](#4-objects--hash-maps)

**PART 2 — LINEAR DATA STRUCTURES**

5. [Linked Lists](#5-linked-lists)
6. [Stacks](#6-stacks)
7. [Queues](#7-queues)
8. [Deque (Double-Ended Queue)](#8-deque-double-ended-queue)

**PART 3 — NON-LINEAR DATA STRUCTURES**

9. [Trees — Binary Tree & BST](#9-trees--binary-tree--bst)
10. [AVL Trees (Self-Balancing BST)](#10-avl-trees-self-balancing-bst)
11. [Heaps & Priority Queues](#11-heaps--priority-queues)
12. [Tries (Prefix Trees)](#12-tries-prefix-trees)
13. [Graphs](#13-graphs)
14. [Disjoint Set (Union-Find)](#14-disjoint-set-union-find)
15. [Segment Trees](#15-segment-trees)
16. [Fenwick Tree (Binary Indexed Tree)](#16-fenwick-tree-binary-indexed-tree)

**PART 4 — SORTING ALGORITHMS**

17. [Bubble Sort](#17-bubble-sort)
18. [Selection Sort](#18-selection-sort)
19. [Insertion Sort](#19-insertion-sort)
20. [Merge Sort](#20-merge-sort)
21. [Quick Sort](#21-quick-sort)
22. [Heap Sort](#22-heap-sort)
23. [Counting Sort](#23-counting-sort)
24. [Radix Sort](#24-radix-sort)
25. [Bucket Sort](#25-bucket-sort)

**PART 5 — SEARCHING ALGORITHMS**

26. [Linear Search](#26-linear-search)
27. [Binary Search](#27-binary-search)
28. [Interpolation & Exponential Search](#28-interpolation--exponential-search)

**PART 6 — GRAPH ALGORITHMS**

29. [BFS — Breadth-First Search](#29-bfs--breadth-first-search)
30. [DFS — Depth-First Search](#30-dfs--depth-first-search)
31. [Dijkstra's Shortest Path](#31-dijkstras-shortest-path)
32. [Bellman-Ford Algorithm](#32-bellman-ford-algorithm)
33. [Floyd-Warshall Algorithm](#33-floyd-warshall-algorithm)
34. [Topological Sort](#34-topological-sort)
35. [Minimum Spanning Tree — Kruskal & Prim](#35-minimum-spanning-tree--kruskal--prim)

**PART 7 — ALGORITHM PARADIGMS**

36. [Recursion & Backtracking](#36-recursion--backtracking)
37. [Divide and Conquer](#37-divide-and-conquer)
38. [Dynamic Programming](#38-dynamic-programming)
39. [Greedy Algorithms](#39-greedy-algorithms)
40. [Sliding Window & Two Pointers](#40-sliding-window--two-pointers)
41. [Bit Manipulation](#41-bit-manipulation)

**PART 8 — ADVANCED TOPICS**

42. [Advanced String Algorithms — KMP & Rabin-Karp](#42-advanced-string-algorithms--kmp--rabin-karp)
43. [Advanced Graph — Tarjan's & Kosaraju's SCC](#43-advanced-graph--tarjans--kosarajus-scc)
44. [LRU Cache & LFU Cache](#44-lru-cache--lfu-cache)
45. [Interview Patterns & Cheat Sheet](#45-interview-patterns--cheat-sheet)

---

# PART 1 — FOUNDATIONS

---

## 1. Big O Notation & Complexity Analysis

Big O notation is the language we use to describe **how an algorithm's runtime or space grows** as the input size grows. It helps us compare algorithms and predict performance.

### Why It Matters

If you have 1 million users, a O(n²) algorithm might take hours while a O(n log n) solution takes seconds.

### Common Complexities (Best → Worst)

```
O(1)        →  Constant    — Array index access
O(log n)    →  Logarithmic — Binary search
O(n)        →  Linear      — Loop through array
O(n log n)  →  Linearithmic— Merge sort
O(n²)       →  Quadratic   — Nested loops
O(2ⁿ)       →  Exponential — Recursive fibonacci
O(n!)       →  Factorial   — Permutations
```

### Visual Growth Comparison

```
n = 10        → O(1)=1,  O(log n)=3,  O(n)=10,   O(n²)=100,   O(2ⁿ)=1024
n = 100       → O(1)=1,  O(log n)=7,  O(n)=100,  O(n²)=10000, O(2ⁿ)=HUGE
n = 1,000,000 → O(1)=1,  O(log n)=20, O(n)=1M,   O(n²)=1T+    💀
```

### Code Examples with Analysis

```javascript
// ─── O(1) — Constant Time ───────────────────────
// Always takes the same time, regardless of input size
function getFirst(arr) {
  return arr[0];  // just one operation, no matter how big arr is
}

function isEven(n) {
  return n % 2 === 0;  // one operation always
}

// ─── O(log n) — Logarithmic Time ────────────────
// Each step cuts the problem in HALF
// Example: binary search on a sorted array
function binarySearch(arr, target) {
  let left = 0;
  let right = arr.length - 1;

  while (left <= right) {
    const mid = Math.floor((left + right) / 2);

    if (arr[mid] === target) return mid;       // found it!
    else if (arr[mid] < target) left = mid + 1; // search right half
    else right = mid - 1;                       // search left half
    // each iteration: problem size is HALVED → O(log n)
  }
  return -1;
}
// On 1,000,000 elements, this takes ~20 steps! log₂(1000000) ≈ 20

// ─── O(n) — Linear Time ─────────────────────────
// One operation per element
function findMax(arr) {
  let max = arr[0];
  for (let i = 1; i < arr.length; i++) {  // loops n times
    if (arr[i] > max) max = arr[i];
  }
  return max;
}

// ─── O(n log n) — Linearithmic ──────────────────
// Typical of efficient sorting algorithms
// "Do something O(log n) for each of the n elements"
// Merge Sort, Heap Sort, Quick Sort (average) are O(n log n)

// ─── O(n²) — Quadratic Time ─────────────────────
// Nested loops — every element compared to every other element
function hasDuplicates(arr) {
  for (let i = 0; i < arr.length; i++) {        // n iterations
    for (let j = i + 1; j < arr.length; j++) {  // n iterations
      if (arr[i] === arr[j]) return true;
    }
  }
  return false;
}
// Better solution: use a Set → O(n) time

// ─── O(2ⁿ) — Exponential Time ───────────────────
// Each call creates TWO more calls — doubles with every n
function fibNaive(n) {
  if (n <= 1) return n;
  return fibNaive(n - 1) + fibNaive(n - 2);  // 2 recursive calls!
}
// fib(50) makes ~2^50 calls ≈ 1 quadrillion calls 💀
// Solution: memoization → O(n)

// ─── O(n!) — Factorial Time ─────────────────────
// Generating all permutations of n elements
function permutations(arr) {
  if (arr.length <= 1) return [arr];
  const result = [];
  for (let i = 0; i < arr.length; i++) {
    const rest = [...arr.slice(0, i), ...arr.slice(i + 1)];
    for (const perm of permutations(rest)) {
      result.push([arr[i], ...perm]);
    }
  }
  return result;
}
// permutations([1,2,3,4,5]) → 120 results (5! = 120)
```

### Space Complexity

```javascript
// O(1) Space — uses same amount of memory regardless of input
function reverseInPlace(arr) {
  let left = 0;
  let right = arr.length - 1;
  while (left < right) {
    [arr[left], arr[right]] = [arr[right], arr[left]]; // swap
    left++;
    right--;
  }
  return arr;
}

// O(n) Space — creates new array proportional to input size
function reverseNew(arr) {
  return arr.slice().reverse();  // creates a copy → O(n) space
}

// O(n) Space — recursion uses call stack
function recursiveSum(n) {
  if (n <= 0) return 0;
  return n + recursiveSum(n - 1);  // n frames on the call stack
}
// This will crash with a "Maximum call stack size exceeded" for large n!

// O(1) Space — iterative version of the same
function iterativeSum(n) {
  let total = 0;
  for (let i = 1; i <= n; i++) total += i;
  return total;
  // Or even better: O(1) with formula: n*(n+1)/2
}
```

### Rules for Calculating Big O

```javascript
// Rule 1: Drop Constants — O(2n) → O(n)
function printTwice(arr) {
  for (let x of arr) console.log(x);  // O(n)
  for (let x of arr) console.log(x);  // O(n)
  // Total: O(2n) → simplified to O(n)
}

// Rule 2: Drop Non-Dominant Terms — O(n² + n) → O(n²)
function mixed(arr) {
  for (let i = 0; i < arr.length; i++)           // O(n)
    for (let j = 0; j < arr.length; j++)         // O(n²) total
      console.log(arr[i] + arr[j]);
  for (let x of arr) console.log(x);             // O(n)
  // Total: O(n² + n) → simplified to O(n²)
}

// Rule 3: Different variables for different inputs
function multiInputs(arrA, arrB) {
  for (let a of arrA)  // O(a)
    for (let b of arrB) // O(b)
      console.log(a, b);
  // This is O(a × b), NOT O(n²)!
}
```

### Complexity Cheat Sheet

| Operation | Array | Linked List | BST (avg) | Hash Map |
|-----------|-------|-------------|-----------|----------|
| Access | O(1) | O(n) | O(log n) | O(1) |
| Search | O(n) | O(n) | O(log n) | O(1) |
| Insert | O(n) | O(1) | O(log n) | O(1) |
| Delete | O(n) | O(1) | O(log n) | O(1) |

---

## 2. Arrays

Arrays are the most fundamental data structure. In JavaScript, arrays are **dynamic** (they resize automatically) and can hold mixed types.

### Basics

```javascript
// Declaration
const nums = [1, 2, 3, 4, 5];
const mixed = [1, "two", true, null, { x: 3 }];
const matrix = [[1,2,3],[4,5,6],[7,8,9]];  // 2D array
const empty = new Array(5).fill(0);         // [0,0,0,0,0]

// Access — O(1)
console.log(nums[0]);    // 1   (first)
console.log(nums.at(-1)); // 5  (last — modern syntax)

// Length
console.log(nums.length);  // 5
```

### Core Operations & Their Complexities

```javascript
const arr = [1, 2, 3, 4, 5];

// ─── O(1) Operations ────────────────────────────
arr.push(6);          // add to END       → [1,2,3,4,5,6]
arr.pop();            // remove from END  → [1,2,3,4,5]

// ─── O(n) Operations ────────────────────────────
arr.unshift(0);       // add to FRONT (shifts all elements right) → [0,1,2,3,4,5]
arr.shift();          // remove from FRONT (shifts all elements left) → [1,2,3,4,5]
arr.splice(2, 1);     // remove 1 element at index 2 → [1,2,4,5]
arr.splice(2, 0, 3);  // insert 3 at index 2 → [1,2,3,4,5]
arr.indexOf(3);       // find index of value → 2   (O(n) linear search)
arr.includes(3);      // check if value exists → true

// ─── Non-mutating methods (return new array) ────
arr.slice(1, 3);      // [2, 3]  (from index 1, up to not including 3)
[...arr, 6];          // spread into new array
arr.concat([6, 7]);   // [1,2,3,4,5,6,7]
```

### Iteration & Functional Methods

```javascript
const nums = [1, 2, 3, 4, 5];

// forEach — execute for each element, returns undefined
nums.forEach((num, index) => {
  console.log(`Index ${index}: ${num}`);
});

// map — transform each element, returns NEW array
const doubled = nums.map(n => n * 2);         // [2,4,6,8,10]
const objects = nums.map(n => ({ value: n })); // [{value:1},...]

// filter — keep elements where condition is true
const evens = nums.filter(n => n % 2 === 0);  // [2, 4]

// reduce — fold array into single value
const sum     = nums.reduce((acc, n) => acc + n, 0);    // 15
const product = nums.reduce((acc, n) => acc * n, 1);    // 120

// Count occurrences using reduce
const text = ['apple','banana','apple','cherry','banana','apple'];
const count = text.reduce((acc, word) => {
  acc[word] = (acc[word] || 0) + 1;
  return acc;
}, {});
// { apple: 3, banana: 2, cherry: 1 }

// find / findIndex — first match
const first = nums.find(n => n > 3);          // 4
const idx   = nums.findIndex(n => n > 3);     // 3

// some / every — boolean checks
nums.some(n => n > 4);    // true  (at least one > 4)
nums.every(n => n > 0);   // true  (all > 0)

// flat / flatMap
[[1,2],[3,4],[5]].flat();             // [1,2,3,4,5]
[1,2,3].flatMap(n => [n, n * 2]);    // [1,2,2,4,3,6]

// sort — O(n log n)  ⚠️ MUTATES original array!
[3,1,4,1,5].sort();               // [1,1,3,4,5] (lexicographic by default!)
[3,1,4,1,5].sort((a,b) => a - b); // [1,1,3,4,5] (numeric ascending)
[3,1,4,1,5].sort((a,b) => b - a); // [5,4,3,1,1] (numeric descending)

// Sort objects
const people = [{name:'Charlie',age:30},{name:'Alice',age:25}];
people.sort((a, b) => a.name.localeCompare(b.name));   // by name
people.sort((a, b) => a.age - b.age);                  // by age
```

### Common Array Patterns

```javascript
// ─── Remove Duplicates ───────────────────────────
const withDups = [1, 2, 2, 3, 3, 3, 4];
const unique = [...new Set(withDups)];         // [1, 2, 3, 4]
const unique2 = Array.from(new Set(withDups)); // same

// ─── Flatten Nested Array ───────────────────────
const nested = [1, [2, [3, [4]]]];
nested.flat(Infinity);   // [1, 2, 3, 4]

// ─── Chunk Array ────────────────────────────────
function chunk(arr, size) {
  const result = [];
  for (let i = 0; i < arr.length; i += size) {
    result.push(arr.slice(i, i + size));
  }
  return result;
}
chunk([1,2,3,4,5,6,7], 3);   // [[1,2,3],[4,5,6],[7]]

// ─── Zip Two Arrays ─────────────────────────────
function zip(a, b) {
  return a.map((item, i) => [item, b[i]]);
}
zip([1,2,3], ['a','b','c']);  // [[1,'a'],[2,'b'],[3,'c']]

// ─── Range Generator ────────────────────────────
function range(start, end, step = 1) {
  const result = [];
  for (let i = start; i < end; i += step) result.push(i);
  return result;
}
range(0, 10, 2);   // [0, 2, 4, 6, 8]

// ─── Rotate Array ───────────────────────────────
function rotate(arr, k) {
  const n = arr.length;
  k = k % n;
  return [...arr.slice(n - k), ...arr.slice(0, n - k)];
}
rotate([1,2,3,4,5], 2);   // [4, 5, 1, 2, 3]

// ─── Matrix Operations ──────────────────────────
// Transpose a matrix
function transpose(matrix) {
  return matrix[0].map((_, colIdx) => matrix.map(row => row[colIdx]));
}
transpose([[1,2,3],[4,5,6],[7,8,9]]);
// [[1,4,7],[2,5,8],[3,6,9]]

// Rotate matrix 90° clockwise
function rotatMatrix90(matrix) {
  return transpose(matrix).map(row => row.reverse());
}
```

### Prefix Sums — Powerful Pattern

```javascript
// Prefix sum allows O(1) range sum queries after O(n) preprocessing

function buildPrefixSum(arr) {
  const prefix = new Array(arr.length + 1).fill(0);
  for (let i = 0; i < arr.length; i++) {
    prefix[i + 1] = prefix[i] + arr[i];
  }
  return prefix;
}

// Sum of elements from index l to r (inclusive) — O(1)!
function rangeSum(prefix, l, r) {
  return prefix[r + 1] - prefix[l];
}

const arr = [3, 1, 4, 1, 5, 9, 2, 6];
const prefix = buildPrefixSum(arr);
// prefix = [0, 3, 4, 8, 9, 14, 23, 25, 31]

console.log(rangeSum(prefix, 1, 4));  // 1+4+1+5 = 11   O(1)!
console.log(rangeSum(prefix, 0, 7));  // sum of all = 31
```

---

## 3. Strings

Strings in JavaScript are **immutable** sequences of UTF-16 characters. Any string operation returns a NEW string.

### Basics & Common Methods

```javascript
const s = "Hello, World!";

// Access
s[0];              // 'H'
s.charAt(0);       // 'H'
s.at(-1);          // '!'  (last character)
s.charCodeAt(0);   // 72   (Unicode code point)
String.fromCharCode(72);  // 'H'

// Length
s.length;          // 13

// Substring
s.slice(7, 12);    // 'World'
s.slice(-6);       // 'orld!'
s.substring(7, 12); // 'World' (no negative indices)

// Search
s.indexOf('o');      // 4    (first occurrence)
s.lastIndexOf('o');  // 8    (last occurrence)
s.includes('World'); // true
s.startsWith('Hello'); // true
s.endsWith('!');     // true
s.search(/\d/);      // -1   (regex search)

// Modify (returns NEW string)
s.replace('World', 'JS');     // 'Hello, JS!'
s.replaceAll('l', 'L');       // 'HeLLo, WorLd!'
s.toLowerCase();               // 'hello, world!'
s.toUpperCase();               // 'HELLO, WORLD!'
s.trim();                      // removes leading/trailing whitespace
s.trimStart();                 // removes leading whitespace
s.trimEnd();                   // removes trailing whitespace

// Split & Join
s.split(', ');     // ['Hello', 'World!']
s.split('');       // ['H','e','l','l','o',',',...]  (to char array)
['H','e','l','l','o'].join('');  // 'Hello'

// Pad
'5'.padStart(3, '0');    // '005'
'5'.padEnd(3, '-');      // '5--'

// Repeat
'ab'.repeat(3);          // 'ababab'
```

### String Algorithms

```javascript
// ─── Reverse a String ───────────────────────────
function reverse(str) {
  return str.split('').reverse().join('');
}

// More efficient — two pointers
function reverseEfficient(str) {
  const chars = str.split('');
  let left = 0, right = chars.length - 1;
  while (left < right) {
    [chars[left], chars[right]] = [chars[right], chars[left]];
    left++;
    right--;
  }
  return chars.join('');
}

// ─── Check Palindrome ───────────────────────────
function isPalindrome(str) {
  const clean = str.toLowerCase().replace(/[^a-z0-9]/g, '');
  let left = 0, right = clean.length - 1;
  while (left < right) {
    if (clean[left] !== clean[right]) return false;
    left++; right--;
  }
  return true;
}
isPalindrome("A man, a plan, a canal: Panama");  // true

// ─── Anagram Check ──────────────────────────────
function isAnagram(s, t) {
  if (s.length !== t.length) return false;
  const count = {};
  for (const char of s) count[char] = (count[char] || 0) + 1;
  for (const char of t) {
    if (!count[char]) return false;
    count[char]--;
  }
  return true;
}
isAnagram("listen", "silent");  // true

// ─── Count Characters ───────────────────────────
function charCount(str) {
  const count = {};
  for (const char of str.toLowerCase()) {
    if (/[a-z]/.test(char)) {
      count[char] = (count[char] || 0) + 1;
    }
  }
  return count;
}

// ─── Longest Common Prefix ──────────────────────
function longestCommonPrefix(strs) {
  if (!strs.length) return '';
  let prefix = strs[0];
  for (let i = 1; i < strs.length; i++) {
    while (!strs[i].startsWith(prefix)) {
      prefix = prefix.slice(0, -1);  // shorten prefix by 1
      if (!prefix) return '';
    }
  }
  return prefix;
}
longestCommonPrefix(['flower','flow','flight']);  // 'fl'

// ─── String Compression ─────────────────────────
function compress(str) {
  let result = '';
  let i = 0;
  while (i < str.length) {
    const char = str[i];
    let count = 0;
    while (i < str.length && str[i] === char) {
      count++;
      i++;
    }
    result += count > 1 ? char + count : char;
  }
  return result.length < str.length ? result : str;
}
compress('aabcccdddd');  // 'a2bc3d4'
compress('abc');         // 'abc' (no compression benefit)

// ─── Valid Parentheses ──────────────────────────
function isValidParentheses(s) {
  const stack = [];
  const map = { ')': '(', '}': '{', ']': '[' };

  for (const char of s) {
    if ('({['.includes(char)) {
      stack.push(char);           // opening bracket — push
    } else {
      if (stack.pop() !== map[char]) return false;  // mismatch!
    }
  }
  return stack.length === 0;  // stack must be empty at the end
}
isValidParentheses('({[]})');  // true
isValidParentheses('({[)]}');  // false
```

---

## 4. Objects & Hash Maps

JavaScript objects (`{}`) are essentially **hash maps** — key-value stores with O(1) average lookup, insertion, and deletion.

```javascript
// Plain Object as Hash Map
const map = {};
map['key'] = 'value';   // insert O(1)
map['key'];             // lookup O(1)
delete map['key'];      // delete O(1)
'key' in map;           // check existence O(1)
Object.keys(map);       // all keys   O(n)
Object.values(map);     // all values O(n)
Object.entries(map);    // all [key,value] pairs O(n)

// ─── Map — Better for Hash Map Use Cases ────────
// Map preserves insertion order, allows any key type (not just strings)
const hashMap = new Map();

hashMap.set('name', 'Alice');    // insert
hashMap.set(42, 'answer');       // non-string key!
hashMap.set({id: 1}, 'object'); // even object key!

hashMap.get('name');             // 'Alice'  O(1)
hashMap.has('name');             // true     O(1)
hashMap.delete('name');          // O(1)
hashMap.size;                    // 2        (not .length!)

// Iterate Map
for (const [key, value] of hashMap) {
  console.log(key, value);
}
[...hashMap.entries()];  // to array
[...hashMap.keys()];
[...hashMap.values()];

// ─── Set — Unique Values ─────────────────────────
const set = new Set([1, 2, 2, 3, 3, 3]);
console.log(set);       // Set {1, 2, 3}

set.add(4);             // O(1)
set.has(2);             // true  O(1)
set.delete(2);          // O(1)
set.size;               // 3

// ─── Hash Map Patterns ──────────────────────────

// Pattern 1: Frequency counter
function frequencyCounter(arr) {
  const freq = new Map();
  for (const item of arr) {
    freq.set(item, (freq.get(item) || 0) + 1);
  }
  return freq;
}

// Pattern 2: Two Sum — classic hash map problem
function twoSum(nums, target) {
  const seen = new Map();  // value → index
  for (let i = 0; i < nums.length; i++) {
    const complement = target - nums[i];
    if (seen.has(complement)) {
      return [seen.get(complement), i];  // found the pair!
    }
    seen.set(nums[i], i);  // store current value
  }
  return [];
}
twoSum([2, 7, 11, 15], 9);  // [0, 1]  because 2+7=9
// Time: O(n), Space: O(n)  ← much better than O(n²) brute force!

// Pattern 3: Group Anagrams
function groupAnagrams(words) {
  const groups = new Map();
  for (const word of words) {
    const key = word.split('').sort().join('');  // sorted word as key
    if (!groups.has(key)) groups.set(key, []);
    groups.get(key).push(word);
  }
  return [...groups.values()];
}
groupAnagrams(['eat','tea','tan','ate','nat','bat']);
// [['eat','tea','ate'], ['tan','nat'], ['bat']]

// Pattern 4: Subarray sum equals K
function subarraySum(nums, k) {
  // Count subarrays whose sum equals k
  const prefixCount = new Map([[0, 1]]);  // prefix sum 0 seen once
  let count = 0, sum = 0;

  for (const num of nums) {
    sum += num;
    // If (sum - k) was seen before, there's a subarray summing to k
    count += prefixCount.get(sum - k) || 0;
    prefixCount.set(sum, (prefixCount.get(sum) || 0) + 1);
  }
  return count;
}
subarraySum([1, 1, 1], 2);  // 2  ([1,1] at positions [0,1] and [1,2])
```

---

# PART 2 — LINEAR DATA STRUCTURES

---

## 5. Linked Lists

A linked list is a chain of **nodes**, where each node holds a value and a **pointer** to the next node. Unlike arrays, nodes are NOT stored contiguously in memory.

```
Array:        [1][2][3][4][5]   ← contiguous memory
Linked List:  1→2→3→4→5→null   ← scattered in memory, connected by pointers
```

### When to use Linked Lists vs Arrays

| | Array | Linked List |
|-|-------|-------------|
| Access by index | O(1) ✅ | O(n) ❌ |
| Insert/Delete at front | O(n) ❌ | O(1) ✅ |
| Insert/Delete at end | O(1) ✅ | O(1) ✅ (with tail ptr) |
| Insert/Delete middle | O(n) ❌ | O(n) ❌ (find) + O(1) (do it) |
| Memory | Contiguous | Scattered + pointer overhead |

### Singly Linked List — Full Implementation

```javascript
// ─── Node ────────────────────────────────────────
class ListNode {
  constructor(val) {
    this.val = val;
    this.next = null;  // points to next node
  }
}

// ─── Singly Linked List ──────────────────────────
class LinkedList {
  constructor() {
    this.head = null;  // first node
    this.tail = null;  // last node (for O(1) append)
    this.size = 0;
  }

  // Add to end — O(1) with tail pointer
  append(val) {
    const node = new ListNode(val);
    if (!this.head) {
      this.head = this.tail = node;
    } else {
      this.tail.next = node;  // link last node to new node
      this.tail = node;       // update tail
    }
    this.size++;
    return this;  // enable chaining
  }

  // Add to front — O(1)
  prepend(val) {
    const node = new ListNode(val);
    node.next = this.head;  // new node points to old head
    this.head = node;       // update head
    if (!this.tail) this.tail = node;  // first node
    this.size++;
    return this;
  }

  // Insert at index — O(n)
  insertAt(val, index) {
    if (index < 0 || index > this.size) return false;
    if (index === 0) return this.prepend(val);
    if (index === this.size) return this.append(val);

    const node = new ListNode(val);
    let current = this.head;
    for (let i = 0; i < index - 1; i++) {
      current = current.next;  // traverse to node BEFORE index
    }
    node.next = current.next;  // new node points to next
    current.next = node;       // previous node points to new node
    this.size++;
    return true;
  }

  // Remove from front — O(1)
  removeFirst() {
    if (!this.head) return null;
    const val = this.head.val;
    this.head = this.head.next;
    if (!this.head) this.tail = null;  // list became empty
    this.size--;
    return val;
  }

  // Remove from end — O(n) for singly linked list
  removeLast() {
    if (!this.head) return null;
    if (this.head === this.tail) {  // only one node
      const val = this.head.val;
      this.head = this.tail = null;
      this.size--;
      return val;
    }
    // Traverse to second-to-last node
    let current = this.head;
    while (current.next !== this.tail) {
      current = current.next;
    }
    const val = this.tail.val;
    current.next = null;   // disconnect last node
    this.tail = current;   // update tail
    this.size--;
    return val;
  }

  // Remove by value — O(n)
  remove(val) {
    if (!this.head) return false;
    if (this.head.val === val) {
      this.removeFirst();
      return true;
    }
    let current = this.head;
    while (current.next) {
      if (current.next.val === val) {
        if (current.next === this.tail) this.tail = current;
        current.next = current.next.next;  // skip over the node
        this.size--;
        return true;
      }
      current = current.next;
    }
    return false;
  }

  // Get node at index — O(n)
  get(index) {
    if (index < 0 || index >= this.size) return null;
    let current = this.head;
    for (let i = 0; i < index; i++) current = current.next;
    return current.val;
  }

  // Search — O(n)
  contains(val) {
    let current = this.head;
    while (current) {
      if (current.val === val) return true;
      current = current.next;
    }
    return false;
  }

  // Convert to array (for easy viewing)
  toArray() {
    const result = [];
    let current = this.head;
    while (current) {
      result.push(current.val);
      current = current.next;
    }
    return result;
  }

  toString() {
    return this.toArray().join(' → ') + ' → null';
  }
}

// Usage
const list = new LinkedList();
list.append(1).append(2).append(3);
list.prepend(0);
console.log(list.toString());   // 0 → 1 → 2 → 3 → null
console.log(list.size);         // 4
```

### Classic Linked List Problems

```javascript
// ─── Reverse a Linked List ───────────────────────
// Iterative — O(n) time, O(1) space
function reverseList(head) {
  let prev = null;
  let current = head;

  while (current) {
    const next = current.next;  // save next
    current.next = prev;         // reverse the pointer
    prev = current;              // move prev forward
    current = next;              // move current forward
  }
  return prev;  // prev is now the new head
}

// Recursive — O(n) time, O(n) space (call stack)
function reverseListRecursive(head) {
  if (!head || !head.next) return head;  // base case
  const newHead = reverseListRecursive(head.next);  // reverse the rest
  head.next.next = head;   // make next node point back to current
  head.next = null;        // disconnect current's forward pointer
  return newHead;
}

// ─── Detect Cycle — Floyd's Algorithm ───────────
// "Tortoise and Hare" — genius technique!
function hasCycle(head) {
  let slow = head;  // moves 1 step at a time
  let fast = head;  // moves 2 steps at a time

  while (fast && fast.next) {
    slow = slow.next;        // 1 step
    fast = fast.next.next;   // 2 steps
    if (slow === fast) return true;  // they met → cycle exists!
  }
  return false;  // fast reached end → no cycle
}

// Find START of cycle
function detectCycleStart(head) {
  let slow = head, fast = head;

  // Phase 1: detect meeting point
  while (fast && fast.next) {
    slow = slow.next;
    fast = fast.next.next;
    if (slow === fast) break;
  }
  if (!fast || !fast.next) return null;  // no cycle

  // Phase 2: find start (mathematical proof!)
  slow = head;
  while (slow !== fast) {
    slow = slow.next;
    fast = fast.next;  // both move 1 step now
  }
  return slow;  // start of cycle
}

// ─── Find Middle Node ────────────────────────────
function findMiddle(head) {
  let slow = head;
  let fast = head;

  while (fast && fast.next) {
    slow = slow.next;        // 1 step
    fast = fast.next.next;   // 2 steps
  }
  return slow;  // when fast reaches end, slow is at middle!
}

// ─── Merge Two Sorted Lists ──────────────────────
function mergeSortedLists(l1, l2) {
  const dummy = new ListNode(0);  // dummy head to simplify logic
  let current = dummy;

  while (l1 && l2) {
    if (l1.val <= l2.val) {
      current.next = l1;
      l1 = l1.next;
    } else {
      current.next = l2;
      l2 = l2.next;
    }
    current = current.next;
  }
  current.next = l1 || l2;  // attach remaining nodes
  return dummy.next;
}

// ─── Find Nth Node from End ──────────────────────
function removeNthFromEnd(head, n) {
  const dummy = new ListNode(0);
  dummy.next = head;
  let fast = dummy, slow = dummy;

  // Move fast n+1 steps ahead
  for (let i = 0; i <= n; i++) fast = fast.next;

  // Move both until fast reaches end
  while (fast) {
    slow = slow.next;
    fast = fast.next;
  }

  // slow.next is the node to remove
  slow.next = slow.next.next;
  return dummy.next;
}
```

### Doubly Linked List

```javascript
class DListNode {
  constructor(val) {
    this.val = val;
    this.prev = null;  // ← points backwards
    this.next = null;  // → points forwards
  }
}

class DoublyLinkedList {
  constructor() {
    // Use sentinel (dummy) nodes to simplify edge cases
    this.head = new DListNode(null);  // dummy head
    this.tail = new DListNode(null);  // dummy tail
    this.head.next = this.tail;
    this.tail.prev = this.head;
    this.size = 0;
  }

  // Insert node after a given node — O(1)
  insertAfter(node, val) {
    const newNode = new DListNode(val);
    newNode.prev = node;
    newNode.next = node.next;
    node.next.prev = newNode;
    node.next = newNode;
    this.size++;
    return newNode;
  }

  // Remove a specific node — O(1)! (no traversal needed)
  removeNode(node) {
    node.prev.next = node.next;
    node.next.prev = node.prev;
    node.prev = null;
    node.next = null;
    this.size--;
    return node.val;
  }

  addFirst(val) { return this.insertAfter(this.head, val); }
  addLast(val)  { return this.insertAfter(this.tail.prev, val); }
  removeFirst() { return this.removeNode(this.head.next); }
  removeLast()  { return this.removeNode(this.tail.prev); }
}
```

---

## 6. Stacks

A stack is a **Last-In, First-Out (LIFO)** data structure — like a pile of plates. The last plate you put on is the first one you take off.

```
Push: add to top        Pop: remove from top
       ┌───┐
       │ 3 │  ← top
       │ 2 │
       │ 1 │  ← bottom
       └───┘
```

### Stack Implementations

```javascript
// ─── Array-based Stack (simplest) ───────────────
class Stack {
  constructor() {
    this.items = [];
  }

  push(item) {
    this.items.push(item);       // O(1) amortized
  }

  pop() {
    if (this.isEmpty()) throw new Error("Stack underflow");
    return this.items.pop();     // O(1)
  }

  peek() {
    if (this.isEmpty()) return null;
    return this.items[this.items.length - 1];  // view top without removing
  }

  isEmpty() {
    return this.items.length === 0;
  }

  size() {
    return this.items.length;
  }

  toString() {
    return `[${this.items.join(', ')}] ← top`;
  }
}

// Usage
const stack = new Stack();
stack.push(1); stack.push(2); stack.push(3);
console.log(stack.peek());  // 3
console.log(stack.pop());   // 3
console.log(stack.pop());   // 2
console.log(stack.size());  // 1
```

### Stack Applications

```javascript
// ─── 1. Valid Parentheses ────────────────────────
function isValidParens(s) {
  const stack = [];
  const pairs = { ')': '(', '}': '{', ']': '[' };

  for (const char of s) {
    if ('({['.includes(char)) {
      stack.push(char);
    } else if (char in pairs) {
      if (stack.pop() !== pairs[char]) return false;
    }
  }
  return stack.length === 0;
}

// ─── 2. Evaluate Reverse Polish Notation (RPN) ──
// "2 1 + 3 *"  = (2 + 1) * 3 = 9
function evalRPN(tokens) {
  const stack = [];
  const ops = {
    '+': (a, b) => a + b,
    '-': (a, b) => a - b,
    '*': (a, b) => a * b,
    '/': (a, b) => Math.trunc(a / b),
  };

  for (const token of tokens) {
    if (token in ops) {
      const b = stack.pop();   // second operand
      const a = stack.pop();   // first operand
      stack.push(ops[token](a, b));
    } else {
      stack.push(Number(token));
    }
  }
  return stack.pop();
}
evalRPN(['2','1','+','3','*']);  // 9

// ─── 3. Monotonic Stack — Next Greater Element ──
// For each element, find the first element to its right that is greater
function nextGreaterElement(nums) {
  const result = new Array(nums.length).fill(-1);
  const stack = [];  // stores indices

  for (let i = 0; i < nums.length; i++) {
    // While stack not empty AND current element > element at top of stack
    while (stack.length > 0 && nums[i] > nums[stack[stack.length - 1]]) {
      const idx = stack.pop();
      result[idx] = nums[i];  // nums[i] is the next greater element for idx
    }
    stack.push(i);
  }
  return result;
}
nextGreaterElement([2, 1, 5, 3, 4]);  // [5, 5, -1, 4, -1]

// ─── 4. Largest Rectangle in Histogram ──────────
// Classic monotonic stack problem
function largestRectangleArea(heights) {
  const stack = [];  // stores indices of bars in increasing height order
  let maxArea = 0;
  heights.push(0);   // sentinel to flush remaining bars

  for (let i = 0; i < heights.length; i++) {
    while (stack.length > 0 && heights[i] < heights[stack[stack.length - 1]]) {
      const h = heights[stack.pop()];
      const w = stack.length === 0 ? i : i - stack[stack.length - 1] - 1;
      maxArea = Math.max(maxArea, h * w);
    }
    stack.push(i);
  }
  return maxArea;
}

// ─── 5. Min Stack — O(1) getMin() ───────────────
class MinStack {
  constructor() {
    this.stack = [];
    this.minStack = [];  // tracks minimum at each level
  }

  push(val) {
    this.stack.push(val);
    const currentMin = this.minStack.length === 0
      ? val
      : Math.min(val, this.minStack[this.minStack.length - 1]);
    this.minStack.push(currentMin);
  }

  pop() {
    this.minStack.pop();
    return this.stack.pop();
  }

  getMin() {
    return this.minStack[this.minStack.length - 1];  // O(1)!
  }
}
```

---

## 7. Queues

A queue is a **First-In, First-Out (FIFO)** data structure — like a line at a store. The first person in line is the first one served.

```
Enqueue (add to back):    1 ← 2 ← 3  ← 4 (new)
Dequeue (remove from front):  → 1  2  3  4
```

### Queue Implementations

```javascript
// ─── Array-based Queue (⚠️ inefficient — shift is O(n)) ─
class SimpleQueue {
  constructor() { this.items = []; }
  enqueue(item) { this.items.push(item); }     // O(1)
  dequeue()     { return this.items.shift(); } // O(n) ← bad!
  peek()        { return this.items[0]; }
  isEmpty()     { return this.items.length === 0; }
}

// ─── Efficient Queue Using Linked List ──────────
class QueueNode {
  constructor(val) {
    this.val = val;
    this.next = null;
  }
}

class Queue {
  constructor() {
    this.front = null;  // dequeue from here
    this.back  = null;  // enqueue from here
    this.size  = 0;
  }

  enqueue(val) {
    const node = new QueueNode(val);
    if (!this.back) {
      this.front = this.back = node;
    } else {
      this.back.next = node;
      this.back = node;
    }
    this.size++;
  }

  dequeue() {
    if (!this.front) throw new Error("Queue is empty");
    const val = this.front.val;
    this.front = this.front.next;
    if (!this.front) this.back = null;
    this.size--;
    return val;
  }

  peek()    { return this.front?.val; }
  isEmpty() { return this.size === 0; }
}

// ─── Circular Queue (Fixed Size) ─────────────────
class CircularQueue {
  constructor(capacity) {
    this.queue = new Array(capacity);
    this.head  = 0;
    this.tail  = 0;
    this.size  = 0;
    this.capacity = capacity;
  }

  enqueue(val) {
    if (this.isFull()) return false;
    this.queue[this.tail] = val;
    this.tail = (this.tail + 1) % this.capacity;  // wrap around!
    this.size++;
    return true;
  }

  dequeue() {
    if (this.isEmpty()) return null;
    const val = this.queue[this.head];
    this.head = (this.head + 1) % this.capacity;  // wrap around!
    this.size--;
    return val;
  }

  peek()     { return this.queue[this.head]; }
  isEmpty()  { return this.size === 0; }
  isFull()   { return this.size === this.capacity; }
}
```

### Queue Applications

```javascript
// ─── BFS Level-Order Traversal ───────────────────
// (See full BFS section for graphs)
function bfsTree(root) {
  if (!root) return [];
  const queue = [root];
  const result = [];

  while (queue.length > 0) {
    const levelSize = queue.length;    // snapshot of current level size
    const level = [];

    for (let i = 0; i < levelSize; i++) {
      const node = queue.shift();
      level.push(node.val);
      if (node.left)  queue.push(node.left);
      if (node.right) queue.push(node.right);
    }
    result.push(level);
  }
  return result;
}

// ─── Task Scheduler ──────────────────────────────
class TaskScheduler {
  constructor() {
    this.queue = new Queue();
  }

  addTask(task) {
    this.queue.enqueue(task);
    console.log(`Task added: ${task}`);
  }

  processNext() {
    if (this.queue.isEmpty()) {
      console.log("No tasks to process");
      return;
    }
    const task = this.queue.dequeue();
    console.log(`Processing: ${task}`);
    return task;
  }
}
```

---

## 8. Deque (Double-Ended Queue)

A deque allows adding and removing from **both ends** in O(1).

```javascript
class Deque {
  constructor() {
    this.items = {};
    this.front = 0;
    this.back  = 0;
  }

  addFront(val) {
    this.front--;
    this.items[this.front] = val;
  }

  addBack(val) {
    this.items[this.back] = val;
    this.back++;
  }

  removeFront() {
    if (this.isEmpty()) return null;
    const val = this.items[this.front];
    delete this.items[this.front];
    this.front++;
    return val;
  }

  removeBack() {
    if (this.isEmpty()) return null;
    this.back--;
    const val = this.items[this.back];
    delete this.items[this.back];
    return val;
  }

  peekFront() { return this.items[this.front]; }
  peekBack()  { return this.items[this.back - 1]; }
  isEmpty()   { return this.front === this.back; }
  size()      { return this.back - this.front; }
}

// ─── Sliding Window Maximum ──────────────────────
// Find maximum in every window of size k — O(n) using deque!
function slidingWindowMax(nums, k) {
  const deque = [];  // stores indices, keeps decreasing order of values
  const result = [];

  for (let i = 0; i < nums.length; i++) {
    // Remove elements outside the window
    while (deque.length > 0 && deque[0] < i - k + 1) {
      deque.shift();
    }
    // Remove elements smaller than current (they're useless)
    while (deque.length > 0 && nums[deque[deque.length - 1]] < nums[i]) {
      deque.pop();
    }
    deque.push(i);
    if (i >= k - 1) result.push(nums[deque[0]]);  // front is always max
  }
  return result;
}
slidingWindowMax([1,3,-1,-3,5,3,6,7], 3);  // [3,3,5,5,6,7]
```

---

# PART 3 — NON-LINEAR DATA STRUCTURES

---

## 9. Trees — Binary Tree & BST

A tree is a hierarchical data structure. A **binary tree** is a tree where each node has **at most 2 children** (left and right).

```
         10          ← root
        /  \
       5    15       ← internal nodes
      / \     \
     3   7    20     ← leaf nodes

Terminology:
- Root: topmost node (10)
- Leaf: node with no children (3, 7, 20)
- Height: longest path from root to leaf (here: 2)
- Depth: distance from root to node
```

### Binary Tree Node & Traversals

```javascript
class TreeNode {
  constructor(val) {
    this.val = val;
    this.left = null;
    this.right = null;
  }
}

// Build a simple tree
//       1
//      / \
//     2   3
//    / \
//   4   5
const root = new TreeNode(1);
root.left = new TreeNode(2);
root.right = new TreeNode(3);
root.left.left = new TreeNode(4);
root.left.right = new TreeNode(5);

// ─── Traversals ──────────────────────────────────
// 1. Inorder: Left → Root → Right
//    Result for BST: sorted order! Great for range queries
function inorder(root) {
  const result = [];
  function dfs(node) {
    if (!node) return;
    dfs(node.left);        // go left first
    result.push(node.val); // visit root in MIDDLE
    dfs(node.right);       // go right last
  }
  dfs(root);
  return result;
}
inorder(root);  // [4, 2, 5, 1, 3]

// 2. Preorder: Root → Left → Right
//    Useful for: copying/serializing trees
function preorder(root) {
  const result = [];
  function dfs(node) {
    if (!node) return;
    result.push(node.val); // visit root FIRST
    dfs(node.left);
    dfs(node.right);
  }
  dfs(root);
  return result;
}
preorder(root);  // [1, 2, 4, 5, 3]

// 3. Postorder: Left → Right → Root
//    Useful for: deleting trees, calculating directory sizes
function postorder(root) {
  const result = [];
  function dfs(node) {
    if (!node) return;
    dfs(node.left);
    dfs(node.right);
    result.push(node.val); // visit root LAST
  }
  dfs(root);
  return result;
}
postorder(root);  // [4, 5, 2, 3, 1]

// 4. Level-Order (BFS): level by level, left to right
function levelOrder(root) {
  if (!root) return [];
  const queue = [root], result = [];

  while (queue.length > 0) {
    const size = queue.length;
    const level = [];
    for (let i = 0; i < size; i++) {
      const node = queue.shift();
      level.push(node.val);
      if (node.left)  queue.push(node.left);
      if (node.right) queue.push(node.right);
    }
    result.push(level);
  }
  return result;
}
levelOrder(root);  // [[1], [2,3], [4,5]]

// ─── Iterative Inorder (using stack) ────────────
function inorderIterative(root) {
  const result = [], stack = [];
  let current = root;

  while (current || stack.length > 0) {
    while (current) {
      stack.push(current);
      current = current.left;   // go as far left as possible
    }
    current = stack.pop();
    result.push(current.val);   // visit
    current = current.right;    // move to right subtree
  }
  return result;
}
```

### Tree Properties

```javascript
// ─── Height of Binary Tree ───────────────────────
function height(root) {
  if (!root) return -1;  // or 0 if counting nodes not edges
  return 1 + Math.max(height(root.left), height(root.right));
}

// ─── Count Nodes ────────────────────────────────
function countNodes(root) {
  if (!root) return 0;
  return 1 + countNodes(root.left) + countNodes(root.right);
}

// ─── Is Balanced? ────────────────────────────────
// A tree is balanced if height difference of left/right subtree ≤ 1 for ALL nodes
function isBalanced(root) {
  function checkHeight(node) {
    if (!node) return 0;
    const left  = checkHeight(node.left);
    const right = checkHeight(node.right);
    if (left === -1 || right === -1) return -1;       // already unbalanced
    if (Math.abs(left - right) > 1)  return -1;       // current is unbalanced
    return 1 + Math.max(left, right);                 // return height
  }
  return checkHeight(root) !== -1;
}

// ─── Diameter (Longest Path between any two nodes) ─
function diameterOfBinaryTree(root) {
  let maxDiameter = 0;

  function depth(node) {
    if (!node) return 0;
    const left  = depth(node.left);
    const right = depth(node.right);
    maxDiameter = Math.max(maxDiameter, left + right);  // path through current node
    return 1 + Math.max(left, right);
  }

  depth(root);
  return maxDiameter;
}

// ─── Lowest Common Ancestor ──────────────────────
function lowestCommonAncestor(root, p, q) {
  if (!root || root === p || root === q) return root;

  const left  = lowestCommonAncestor(root.left,  p, q);
  const right = lowestCommonAncestor(root.right, p, q);

  // If both sides found a node, current node is LCA
  if (left && right) return root;
  return left || right;
}

// ─── Serialize and Deserialize ───────────────────
function serialize(root) {
  if (!root) return 'null';
  return `${root.val},${serialize(root.left)},${serialize(root.right)}`;
}

function deserialize(data) {
  const nodes = data.split(',');
  let index = 0;

  function build() {
    if (nodes[index] === 'null') { index++; return null; }
    const node = new TreeNode(parseInt(nodes[index++]));
    node.left  = build();
    node.right = build();
    return node;
  }
  return build();
}
```

### Binary Search Tree (BST)

In a BST: **left child < parent < right child** for EVERY node.

```javascript
class BST {
  constructor() {
    this.root = null;
  }

  // Insert — O(log n) average, O(n) worst case (unbalanced)
  insert(val) {
    const node = new TreeNode(val);
    if (!this.root) { this.root = node; return; }

    let current = this.root;
    while (true) {
      if (val < current.val) {
        if (!current.left) { current.left = node; break; }
        current = current.left;
      } else if (val > current.val) {
        if (!current.right) { current.right = node; break; }
        current = current.right;
      } else {
        break;  // duplicate, ignore
      }
    }
  }

  // Search — O(log n) average
  search(val) {
    let current = this.root;
    while (current) {
      if (val === current.val) return current;
      current = val < current.val ? current.left : current.right;
    }
    return null;
  }

  // Delete — O(log n) average
  delete(val) {
    this.root = this._deleteNode(this.root, val);
  }

  _deleteNode(node, val) {
    if (!node) return null;

    if (val < node.val) {
      node.left = this._deleteNode(node.left, val);
    } else if (val > node.val) {
      node.right = this._deleteNode(node.right, val);
    } else {
      // Found node to delete — 3 cases:
      // Case 1: No children (leaf)
      if (!node.left && !node.right) return null;

      // Case 2: One child
      if (!node.left)  return node.right;
      if (!node.right) return node.left;

      // Case 3: Two children — replace with inorder successor
      // (smallest node in right subtree)
      let successor = node.right;
      while (successor.left) successor = successor.left;
      node.val = successor.val;                          // copy successor value
      node.right = this._deleteNode(node.right, successor.val); // delete successor
    }
    return node;
  }

  // Get sorted values — O(n)  (inorder traversal of BST = sorted!)
  getSorted() {
    const result = [];
    function inorder(node) {
      if (!node) return;
      inorder(node.left);
      result.push(node.val);
      inorder(node.right);
    }
    inorder(this.root);
    return result;
  }

  // Find kth smallest — O(k)
  kthSmallest(k) {
    let count = 0, result = null;
    function inorder(node) {
      if (!node || result !== null) return;
      inorder(node.left);
      if (++count === k) { result = node.val; return; }
      inorder(node.right);
    }
    inorder(this.root);
    return result;
  }
}

// Usage
const bst = new BST();
[5, 3, 7, 1, 4, 6, 8].forEach(v => bst.insert(v));
console.log(bst.getSorted());    // [1, 3, 4, 5, 6, 7, 8]
console.log(bst.kthSmallest(3)); // 4
```

---

## 10. AVL Trees (Self-Balancing BST)

An AVL tree is a BST that **automatically rebalances** itself after insertions and deletions, guaranteeing O(log n) for all operations.

**Balance Factor** = height(left subtree) - height(right subtree). Must always be -1, 0, or 1.

```javascript
class AVLNode {
  constructor(val) {
    this.val    = val;
    this.left   = null;
    this.right  = null;
    this.height = 1;    // new node starts at height 1
  }
}

class AVLTree {
  constructor() {
    this.root = null;
  }

  height(node) {
    return node ? node.height : 0;
  }

  balanceFactor(node) {
    return node ? this.height(node.left) - this.height(node.right) : 0;
  }

  updateHeight(node) {
    node.height = 1 + Math.max(this.height(node.left), this.height(node.right));
  }

  // ─── Rotations — The Core of AVL ─────────────
  // Right Rotation (fixes left-heavy imbalance):
  //      y               x
  //     / \    →        / \
  //    x   T3          T1  y
  //   / \                 / \
  //  T1  T2             T2  T3
  rotateRight(y) {
    const x  = y.left;
    const T2 = x.right;

    x.right = y;   // perform rotation
    y.left  = T2;

    this.updateHeight(y);  // update y first (it's lower now)
    this.updateHeight(x);
    return x;  // x is new root
  }

  // Left Rotation (fixes right-heavy imbalance):
  rotateLeft(x) {
    const y  = x.right;
    const T2 = y.left;

    y.left  = x;
    x.right = T2;

    this.updateHeight(x);
    this.updateHeight(y);
    return y;
  }

  // Rebalance node after insertion/deletion
  rebalance(node) {
    this.updateHeight(node);
    const bf = this.balanceFactor(node);

    // Left-Left Case → Right Rotation
    if (bf > 1 && this.balanceFactor(node.left) >= 0)
      return this.rotateRight(node);

    // Right-Right Case → Left Rotation
    if (bf < -1 && this.balanceFactor(node.right) <= 0)
      return this.rotateLeft(node);

    // Left-Right Case → Left Rotation on left child, then Right Rotation
    if (bf > 1 && this.balanceFactor(node.left) < 0) {
      node.left = this.rotateLeft(node.left);
      return this.rotateRight(node);
    }

    // Right-Left Case → Right Rotation on right child, then Left Rotation
    if (bf < -1 && this.balanceFactor(node.right) > 0) {
      node.right = this.rotateRight(node.right);
      return this.rotateLeft(node);
    }

    return node;  // already balanced
  }

  insert(val) {
    this.root = this._insert(this.root, val);
  }

  _insert(node, val) {
    if (!node) return new AVLNode(val);

    if (val < node.val)      node.left  = this._insert(node.left,  val);
    else if (val > node.val) node.right = this._insert(node.right, val);
    else return node;  // duplicate

    return this.rebalance(node);  // rebalance on the way back up!
  }
}
```

---

## 11. Heaps & Priority Queues

A **heap** is a complete binary tree satisfying the heap property:
- **Max-Heap**: parent ≥ children (root is the MAXIMUM)
- **Min-Heap**: parent ≤ children (root is the MINIMUM)

The clever trick: **store the tree in an array** using index math!

```
Index:  0  1  2  3  4  5  6
Array: [10, 8, 9, 4, 7, 3, 5]

Represents:
          10         (index 0)
         /  \
        8    9       (index 1, 2)
       / \  / \
      4  7 3   5     (index 3, 4, 5, 6)

For node at index i:
  Left child:  2*i + 1
  Right child: 2*i + 2
  Parent:      Math.floor((i-1) / 2)
```

### Min-Heap Implementation

```javascript
class MinHeap {
  constructor() {
    this.heap = [];
  }

  // Helper: get parent/child indices
  parent(i)  { return Math.floor((i - 1) / 2); }
  left(i)    { return 2 * i + 1; }
  right(i)   { return 2 * i + 2; }

  swap(i, j) {
    [this.heap[i], this.heap[j]] = [this.heap[j], this.heap[i]];
  }

  // ─── Insert — O(log n) ───────────────────────
  push(val) {
    this.heap.push(val);           // add to end
    this._bubbleUp(this.heap.length - 1);  // fix heap property
  }

  _bubbleUp(i) {
    while (i > 0 && this.heap[i] < this.heap[this.parent(i)]) {
      this.swap(i, this.parent(i));  // swap with parent if smaller
      i = this.parent(i);            // move up
    }
  }

  // ─── Remove Min — O(log n) ───────────────────
  pop() {
    if (this.heap.length === 0) return null;
    if (this.heap.length === 1) return this.heap.pop();

    const min = this.heap[0];                     // save min (root)
    this.heap[0] = this.heap.pop();               // move last to root
    this._siftDown(0);                            // fix heap property
    return min;
  }

  _siftDown(i) {
    const n = this.heap.length;
    let smallest = i;

    const l = this.left(i);
    const r = this.right(i);

    if (l < n && this.heap[l] < this.heap[smallest]) smallest = l;
    if (r < n && this.heap[r] < this.heap[smallest]) smallest = r;

    if (smallest !== i) {
      this.swap(i, smallest);
      this._siftDown(smallest);  // continue sifting down
    }
  }

  peek()     { return this.heap[0]; }
  size()     { return this.heap.length; }
  isEmpty()  { return this.heap.length === 0; }

  // ─── Build Heap from Array — O(n) ────────────
  // Much better than inserting n items one by one (O(n log n))!
  buildHeap(arr) {
    this.heap = [...arr];
    // Start from last non-leaf node and sift down
    for (let i = Math.floor(arr.length / 2) - 1; i >= 0; i--) {
      this._siftDown(i);
    }
  }
}

// ─── Priority Queue ──────────────────────────────
// Generalized heap where each element has a priority
class PriorityQueue {
  constructor(compareFn = (a, b) => a.priority - b.priority) {
    this.heap = [];
    this.compare = compareFn;
  }

  push(item, priority) {
    this.heap.push({ item, priority });
    this._bubbleUp(this.heap.length - 1);
  }

  pop() {
    if (this.isEmpty()) return null;
    if (this.heap.length === 1) return this.heap.pop().item;
    const top = this.heap[0].item;
    this.heap[0] = this.heap.pop();
    this._siftDown(0);
    return top;
  }

  _bubbleUp(i) {
    const parent = Math.floor((i - 1) / 2);
    if (i > 0 && this.compare(this.heap[i], this.heap[parent]) < 0) {
      [this.heap[i], this.heap[parent]] = [this.heap[parent], this.heap[i]];
      this._bubbleUp(parent);
    }
  }

  _siftDown(i) {
    const n = this.heap.length;
    let min = i;
    const l = 2*i+1, r = 2*i+2;
    if (l < n && this.compare(this.heap[l], this.heap[min]) < 0) min = l;
    if (r < n && this.compare(this.heap[r], this.heap[min]) < 0) min = r;
    if (min !== i) {
      [this.heap[i], this.heap[min]] = [this.heap[min], this.heap[i]];
      this._siftDown(min);
    }
  }

  peek()    { return this.heap[0]?.item; }
  isEmpty() { return this.heap.length === 0; }
  size()    { return this.heap.length; }
}

// ─── Top K Frequent Elements — O(n log k) ────────
function topKFrequent(nums, k) {
  // Count frequencies
  const freq = new Map();
  for (const n of nums) freq.set(n, (freq.get(n) || 0) + 1);

  // Use min-heap of size k
  const heap = new MinHeap();
  for (const [num, count] of freq) {
    heap.push(count);
    if (heap.size() > k) heap.pop();  // remove smallest
  }

  // Simpler approach: sort by frequency
  return [...freq.entries()]
    .sort((a, b) => b[1] - a[1])
    .slice(0, k)
    .map(([num]) => num);
}

// ─── K-th Largest Element ────────────────────────
function kthLargest(nums, k) {
  const heap = new MinHeap();
  for (const n of nums) {
    heap.push(n);
    if (heap.size() > k) heap.pop();  // always keep top k
  }
  return heap.peek();  // smallest of top k = k-th largest
}
kthLargest([3,2,1,5,6,4], 2);  // 5
```

---

## 12. Tries (Prefix Trees)

A Trie is a tree where each path from root to a node represents a prefix of some word. Perfect for **autocomplete**, **spell-checking**, and **IP routing**.

```
Insert: "cat", "car", "card", "care", "dog"

        root
       /    \
      c      d
      |      |
      a      o
     / \     |
    t   r    g*
   *   / \
      d   e
      *   *

* = end of a word
```

### Trie Implementation

```javascript
class TrieNode {
  constructor() {
    this.children = {};  // char → TrieNode
    this.isEnd = false;  // marks end of a complete word
    this.count = 0;      // how many words pass through this node
  }
}

class Trie {
  constructor() {
    this.root = new TrieNode();
  }

  // Insert a word — O(m) where m = word length
  insert(word) {
    let node = this.root;
    for (const char of word) {
      if (!node.children[char]) {
        node.children[char] = new TrieNode();
      }
      node = node.children[char];
      node.count++;
    }
    node.isEnd = true;
  }

  // Search for exact word — O(m)
  search(word) {
    let node = this.root;
    for (const char of word) {
      if (!node.children[char]) return false;
      node = node.children[char];
    }
    return node.isEnd;  // must end at a word boundary
  }

  // Check if any word starts with this prefix — O(m)
  startsWith(prefix) {
    let node = this.root;
    for (const char of prefix) {
      if (!node.children[char]) return false;
      node = node.children[char];
    }
    return true;
  }

  // Delete a word — O(m)
  delete(word) {
    function del(node, word, depth) {
      if (!node) return false;
      if (depth === word.length) {
        if (!node.isEnd) return false;
        node.isEnd = false;
        return Object.keys(node.children).length === 0;
      }
      const char = word[depth];
      const shouldDelete = del(node.children[char], word, depth + 1);
      if (shouldDelete) {
        delete node.children[char];
        return !node.isEnd && Object.keys(node.children).length === 0;
      }
      return false;
    }
    del(this.root, word, 0);
  }

  // Autocomplete — return all words with given prefix — O(m + k)
  autocomplete(prefix) {
    let node = this.root;
    for (const char of prefix) {
      if (!node.children[char]) return [];
      node = node.children[char];
    }
    const results = [];
    this._dfs(node, prefix, results);
    return results;
  }

  _dfs(node, current, results) {
    if (node.isEnd) results.push(current);
    for (const [char, child] of Object.entries(node.children)) {
      this._dfs(child, current + char, results);
    }
  }

  // Count words with prefix
  countWordsWithPrefix(prefix) {
    let node = this.root;
    for (const char of prefix) {
      if (!node.children[char]) return 0;
      node = node.children[char];
    }
    return node.count;
  }
}

// Usage
const trie = new Trie();
['apple','app','application','apply','banana'].forEach(w => trie.insert(w));

console.log(trie.search('app'));         // true
console.log(trie.search('ap'));          // false (not a complete word)
console.log(trie.startsWith('app'));     // true
console.log(trie.autocomplete('app'));   // ['app','apple','application','apply']
```

---

## 13. Graphs

A graph is a set of **vertices** (nodes) connected by **edges**. Graphs model networks, relationships, paths — the most versatile data structure.

```
Types:
  Undirected: A — B  (edge has no direction)
  Directed:   A → B  (edge has direction)
  Weighted:   A -5→ B (edge has weight/cost)
  Cyclic:     A→B→C→A (has cycles)
  Acyclic:    trees, DAGs (no cycles)
```

### Graph Representations

```javascript
// ─── 1. Adjacency List (most common) ─────────────
// Space: O(V + E)  — efficient for sparse graphs
class Graph {
  constructor(directed = false) {
    this.adjacencyList = new Map();
    this.directed = directed;
  }

  addVertex(vertex) {
    if (!this.adjacencyList.has(vertex)) {
      this.adjacencyList.set(vertex, []);
    }
  }

  addEdge(v1, v2, weight = 1) {
    if (!this.adjacencyList.has(v1)) this.addVertex(v1);
    if (!this.adjacencyList.has(v2)) this.addVertex(v2);

    this.adjacencyList.get(v1).push({ node: v2, weight });
    if (!this.directed) {
      this.adjacencyList.get(v2).push({ node: v1, weight });
    }
  }

  getNeighbors(vertex) {
    return this.adjacencyList.get(vertex) || [];
  }

  hasEdge(v1, v2) {
    return this.adjacencyList.get(v1)?.some(n => n.node === v2) || false;
  }

  removeEdge(v1, v2) {
    this.adjacencyList.set(v1,
      this.adjacencyList.get(v1).filter(n => n.node !== v2));
    if (!this.directed) {
      this.adjacencyList.set(v2,
        this.adjacencyList.get(v2).filter(n => n.node !== v1));
    }
  }

  getVertices() { return [...this.adjacencyList.keys()]; }
}

// ─── 2. Adjacency Matrix ─────────────────────────
// Space: O(V²) — for dense graphs, O(1) edge lookup
class GraphMatrix {
  constructor(numVertices) {
    this.n = numVertices;
    this.matrix = Array.from({ length: numVertices },
                              () => new Array(numVertices).fill(0));
  }

  addEdge(v1, v2, weight = 1) {
    this.matrix[v1][v2] = weight;
    this.matrix[v2][v1] = weight;  // undirected
  }

  hasEdge(v1, v2) {
    return this.matrix[v1][v2] !== 0;
  }
}

// Build example graph:
// A -- B
// |    |
// C -- D -- E
const g = new Graph();
[['A','B'], ['A','C'], ['B','D'], ['C','D'], ['D','E']].forEach(
  ([v1, v2]) => g.addEdge(v1, v2)
);
```

---

## 14. Disjoint Set (Union-Find)

Union-Find efficiently answers: **"Are these two elements in the same group?"** Used in Kruskal's algorithm, network connectivity, etc.

```javascript
class UnionFind {
  constructor(n) {
    this.parent = Array.from({ length: n }, (_, i) => i);  // each is its own parent
    this.rank   = new Array(n).fill(0);   // tree height estimate
    this.count  = n;                      // number of components
  }

  // Find root with PATH COMPRESSION — O(α(n)) ≈ O(1)
  find(x) {
    if (this.parent[x] !== x) {
      this.parent[x] = this.find(this.parent[x]);  // path compression!
    }
    return this.parent[x];
  }

  // Union by rank — keeps trees shallow
  union(x, y) {
    const px = this.find(x);
    const py = this.find(y);
    if (px === py) return false;  // already in same set

    // Attach smaller tree under larger tree
    if (this.rank[px] < this.rank[py]) {
      this.parent[px] = py;
    } else if (this.rank[px] > this.rank[py]) {
      this.parent[py] = px;
    } else {
      this.parent[py] = px;
      this.rank[px]++;
    }
    this.count--;
    return true;
  }

  connected(x, y) {
    return this.find(x) === this.find(y);
  }
}

// ─── Number of Islands — classic Union-Find ──────
function numIslands(grid) {
  const rows = grid.length, cols = grid[0].length;
  const uf = new UnionFind(rows * cols);
  let waterCount = 0;

  for (let r = 0; r < rows; r++) {
    for (let c = 0; c < cols; c++) {
      if (grid[r][c] === '0') { waterCount++; continue; }
      // Connect with right and down neighbors
      if (c + 1 < cols && grid[r][c+1] === '1')
        uf.union(r*cols+c, r*cols+c+1);
      if (r + 1 < rows && grid[r+1][c] === '1')
        uf.union(r*cols+c, (r+1)*cols+c);
    }
  }
  return uf.count - waterCount;
}
```

---

## 15. Segment Trees

Segment trees support **range queries** (sum, min, max) and **point updates** in O(log n).

```javascript
class SegmentTree {
  constructor(arr) {
    this.n = arr.length;
    this.tree = new Array(4 * this.n).fill(0);
    this.build(arr, 0, 0, this.n - 1);
  }

  build(arr, node, start, end) {
    if (start === end) {
      this.tree[node] = arr[start];
      return;
    }
    const mid = Math.floor((start + end) / 2);
    this.build(arr, 2*node+1, start, mid);
    this.build(arr, 2*node+2, mid+1, end);
    this.tree[node] = this.tree[2*node+1] + this.tree[2*node+2];
  }

  // Range sum query [l, r] — O(log n)
  query(l, r, node = 0, start = 0, end = this.n - 1) {
    if (r < start || end < l) return 0;         // out of range
    if (l <= start && end <= r) return this.tree[node];  // fully in range
    const mid = Math.floor((start + end) / 2);
    return this.query(l, r, 2*node+1, start, mid) +
           this.query(l, r, 2*node+2, mid+1, end);
  }

  // Point update — O(log n)
  update(idx, val, node = 0, start = 0, end = this.n - 1) {
    if (start === end) {
      this.tree[node] = val;
      return;
    }
    const mid = Math.floor((start + end) / 2);
    if (idx <= mid) this.update(idx, val, 2*node+1, start, mid);
    else            this.update(idx, val, 2*node+2, mid+1, end);
    this.tree[node] = this.tree[2*node+1] + this.tree[2*node+2];
  }
}

const st = new SegmentTree([1,3,5,7,9,11]);
console.log(st.query(1, 3));  // 3+5+7 = 15
st.update(1, 10);             // arr[1] = 10
console.log(st.query(1, 3));  // 10+5+7 = 22
```

---

## 16. Fenwick Tree (Binary Indexed Tree)

Simpler than Segment Tree, Fenwick tree supports prefix sum queries and point updates in O(log n) with very low constant.

```javascript
class FenwickTree {
  constructor(n) {
    this.n = n;
    this.tree = new Array(n + 1).fill(0);  // 1-indexed!
  }

  // Update index i by delta — O(log n)
  update(i, delta) {
    for (; i <= this.n; i += i & (-i))  // lowbit trick!
      this.tree[i] += delta;
  }

  // Prefix sum [1..i] — O(log n)
  prefixSum(i) {
    let sum = 0;
    for (; i > 0; i -= i & (-i))  // lowbit trick!
      sum += this.tree[i];
    return sum;
  }

  // Range sum [l..r] — O(log n)
  rangeSum(l, r) {
    return this.prefixSum(r) - this.prefixSum(l - 1);
  }

  // Build from array — O(n log n)
  build(arr) {
    for (let i = 0; i < arr.length; i++) {
      this.update(i + 1, arr[i]);
    }
  }
}

const bit = new FenwickTree(6);
bit.build([1, 3, 5, 7, 9, 11]);
console.log(bit.prefixSum(3));   // 1+3+5 = 9
console.log(bit.rangeSum(2, 4)); // 3+5+7 = 15
bit.update(2, 5);                // arr[2] += 5 → now 8
console.log(bit.rangeSum(2, 4)); // 8+5+7 = 20
```

---

# PART 4 — SORTING ALGORITHMS

---

## 17. Bubble Sort

The simplest sorting algorithm. Repeatedly **bubbles** the largest unsorted element to its correct position.

**Complexity:** Time O(n²), Space O(1)

```javascript
function bubbleSort(arr) {
  const n = arr.length;
  // After each pass, the LARGEST unsorted element is at its final position
  for (let i = 0; i < n - 1; i++) {
    let swapped = false;

    for (let j = 0; j < n - i - 1; j++) {
      // Compare adjacent elements
      if (arr[j] > arr[j + 1]) {
        [arr[j], arr[j + 1]] = [arr[j + 1], arr[j]]; // swap!
        swapped = true;
      }
    }
    // Optimization: if no swaps occurred, array is already sorted
    if (!swapped) break;  // ← O(n) best case with this optimization
  }
  return arr;
}

bubbleSort([64, 34, 25, 12, 22, 11, 90]);
// Pass 1: [34,25,12,22,11,64,90] — 90 bubbled to end
// Pass 2: [25,12,22,11,34,64,90] — 64 in place
// ...continues
// Result: [11,12,22,25,34,64,90]
```

---

## 18. Selection Sort

Find the minimum element and place it at the front. Repeat for remaining elements.

**Complexity:** Time O(n²), Space O(1). Makes fewer swaps than Bubble Sort.

```javascript
function selectionSort(arr) {
  const n = arr.length;

  for (let i = 0; i < n - 1; i++) {
    // Find index of minimum element in remaining unsorted portion
    let minIdx = i;
    for (let j = i + 1; j < n; j++) {
      if (arr[j] < arr[minIdx]) minIdx = j;
    }
    // Swap minimum element to its correct position
    if (minIdx !== i) {
      [arr[i], arr[minIdx]] = [arr[minIdx], arr[i]];
    }
  }
  return arr;
}

selectionSort([64, 25, 12, 22, 11]);
// i=0: min=11 at idx 4, swap → [11, 25, 12, 22, 64]
// i=1: min=12 at idx 2, swap → [11, 12, 25, 22, 64]
// i=2: min=22 at idx 3, swap → [11, 12, 22, 25, 64]
// i=3: min=25 at idx 3, no swap needed
// Result: [11, 12, 22, 25, 64]
```

---

## 19. Insertion Sort

Build a sorted array one element at a time by inserting each new element in the right position.

**Complexity:** Time O(n²) worst, **O(n) best** (nearly sorted). Space O(1). Excellent for small/nearly-sorted arrays.

```javascript
function insertionSort(arr) {
  for (let i = 1; i < arr.length; i++) {
    const current = arr[i];  // element to insert
    let j = i - 1;

    // Shift elements greater than current to the right
    while (j >= 0 && arr[j] > current) {
      arr[j + 1] = arr[j];
      j--;
    }
    arr[j + 1] = current;  // insert in correct position
  }
  return arr;
}

insertionSort([12, 11, 13, 5, 6]);
// i=1: current=11. 12>11 → shift. Insert: [11,12,13,5,6]
// i=2: current=13. 12<13 → stop. Insert: [11,12,13,5,6]
// i=3: current=5.  Shift 13,12,11. Insert: [5,11,12,13,6]
// i=4: current=6.  Shift 13,12,11. Insert: [5,6,11,12,13]
```

---

## 20. Merge Sort

**Divide and conquer**: split array in half, recursively sort each half, merge the sorted halves.

**Complexity:** Time O(n log n) always. Space O(n). Stable sort.

```javascript
function mergeSort(arr) {
  // Base case: arrays of 0 or 1 element are already sorted
  if (arr.length <= 1) return arr;

  // Divide
  const mid = Math.floor(arr.length / 2);
  const left  = mergeSort(arr.slice(0, mid));   // sort left half
  const right = mergeSort(arr.slice(mid));       // sort right half

  // Conquer: merge sorted halves
  return merge(left, right);
}

function merge(left, right) {
  const result = [];
  let i = 0, j = 0;

  // Compare elements from both halves and take the smaller one
  while (i < left.length && j < right.length) {
    if (left[i] <= right[j]) {
      result.push(left[i++]);
    } else {
      result.push(right[j++]);
    }
  }

  // Add remaining elements (one of the arrays will be exhausted)
  return [...result, ...left.slice(i), ...right.slice(j)];
}

// Visualizing the recursion for [38, 27, 43, 3, 9, 82, 10]:
// Split: [38,27,43,3] | [9,82,10]
// Split: [38,27]|[43,3] | [9,82]|[10]
// Split: [38]|[27] | [43]|[3] | [9]|[82] | [10]
// Merge: [27,38] | [3,43] | [9,82] | [10]
// Merge: [3,27,38,43] | [9,10,82]
// Merge: [3,9,10,27,38,43,82] ✓
```

---

## 21. Quick Sort

**Divide and conquer** using a **pivot**. Partition array around pivot, then recursively sort each partition.

**Complexity:** Time O(n log n) average, O(n²) worst. Space O(log n). Fastest in practice.

```javascript
function quickSort(arr, low = 0, high = arr.length - 1) {
  if (low < high) {
    // Partition array and get pivot's final position
    const pivotIdx = partition(arr, low, high);
    quickSort(arr, low, pivotIdx - 1);   // sort left of pivot
    quickSort(arr, pivotIdx + 1, high);  // sort right of pivot
  }
  return arr;
}

function partition(arr, low, high) {
  // Choose last element as pivot (many strategies exist)
  const pivot = arr[high];
  let i = low - 1;  // index of smaller element

  for (let j = low; j < high; j++) {
    // If current element is ≤ pivot, place it on the left side
    if (arr[j] <= pivot) {
      i++;
      [arr[i], arr[j]] = [arr[j], arr[i]];  // swap
    }
  }
  // Place pivot in its correct position
  [arr[i + 1], arr[high]] = [arr[high], arr[i + 1]];
  return i + 1;  // pivot's final index
}

// Example: [10, 80, 30, 90, 40, 50, 70]  pivot = 70
// j=0: 10≤70 → swap with itself, i=0
// j=1: 80>70 → no action
// j=2: 30≤70 → swap arr[1] and arr[2], i=1 → [10,30,80,90,40,50,70]
// ...
// Final: [10,30,40,50,70,80,90] with 70 in position 4

// ─── Randomized Quick Sort (avoids worst case) ───
function randomizedQuickSort(arr, low = 0, high = arr.length - 1) {
  if (low < high) {
    // Randomly choose pivot to avoid O(n²) on sorted arrays
    const randomIdx = low + Math.floor(Math.random() * (high - low + 1));
    [arr[randomIdx], arr[high]] = [arr[high], arr[randomIdx]];
    const pivotIdx = partition(arr, low, high);
    randomizedQuickSort(arr, low, pivotIdx - 1);
    randomizedQuickSort(arr, pivotIdx + 1, high);
  }
  return arr;
}
```

---

## 22. Heap Sort

Build a max-heap, then repeatedly extract the maximum.

**Complexity:** Time O(n log n) always. Space O(1). Not stable.

```javascript
function heapSort(arr) {
  const n = arr.length;

  // Phase 1: Build max-heap — O(n)
  // Start from last non-leaf and sift down each node
  for (let i = Math.floor(n / 2) - 1; i >= 0; i--) {
    heapify(arr, n, i);
  }

  // Phase 2: Extract elements from heap one by one — O(n log n)
  for (let i = n - 1; i > 0; i--) {
    // Move current max (root) to end
    [arr[0], arr[i]] = [arr[i], arr[0]];
    // Heapify the reduced heap
    heapify(arr, i, 0);
  }
  return arr;
}

// Sift down to maintain max-heap property
function heapify(arr, n, i) {
  let largest = i;       // assume root is largest
  const left  = 2*i + 1;
  const right = 2*i + 2;

  if (left  < n && arr[left]  > arr[largest]) largest = left;
  if (right < n && arr[right] > arr[largest]) largest = right;

  if (largest !== i) {
    [arr[i], arr[largest]] = [arr[largest], arr[i]];
    heapify(arr, n, largest);  // recursively heapify affected subtree
  }
}

heapSort([12, 11, 13, 5, 6, 7]);
// Build max-heap: [13, 11, 12, 5, 6, 7]
// Extract 13 → [7,11,12,5,6] | [13]  → heapify → [12,11,7,5,6]
// Extract 12 → [6,11,7,5] | [12,13] → heapify → [11,6,7,5]
// ... → [5,6,7,11,12,13]
```

---

## 23. Counting Sort

Instead of comparing elements, count occurrences. Only works for integers in a known range.

**Complexity:** Time O(n + k), Space O(k), where k = range of values.

```javascript
function countingSort(arr) {
  if (arr.length === 0) return arr;

  const min = Math.min(...arr);
  const max = Math.max(...arr);
  const range = max - min + 1;

  // Step 1: Count occurrences
  const count = new Array(range).fill(0);
  for (const num of arr) count[num - min]++;

  // Step 2: Build sorted output
  const result = [];
  for (let i = 0; i < range; i++) {
    while (count[i] > 0) {
      result.push(i + min);
      count[i]--;
    }
  }
  return result;
}

countingSort([4, 2, 2, 8, 3, 3, 1]);
// count = [0,1,2,2,1,0,0,0,1]  (index = value - 1)
// output = [1,2,2,3,3,4,8]
```

---

## 24. Radix Sort

Sort integers digit by digit from least significant to most significant.

**Complexity:** Time O(d × (n + b)), Space O(n + b), where d = digits, b = base.

```javascript
function radixSort(arr) {
  const max = Math.max(...arr);

  // Sort by each digit — from least significant to most
  for (let exp = 1; Math.floor(max / exp) > 0; exp *= 10) {
    arr = countingSortByDigit(arr, exp);
  }
  return arr;
}

function countingSortByDigit(arr, exp) {
  const n = arr.length;
  const output = new Array(n);
  const count  = new Array(10).fill(0);

  // Count occurrences of each digit
  for (const num of arr) count[Math.floor(num / exp) % 10]++;

  // Cumulative count (position in output)
  for (let i = 1; i < 10; i++) count[i] += count[i - 1];

  // Build output (traverse right to left for stability)
  for (let i = n - 1; i >= 0; i--) {
    const digit = Math.floor(arr[i] / exp) % 10;
    output[--count[digit]] = arr[i];
  }
  return output;
}

radixSort([170, 45, 75, 90, 802, 24, 2, 66]);
// exp=1 (units):    [170,90,802,2,24,45,75,66]
// exp=10 (tens):    [802,2,24,45,66,170,75,90]
// exp=100 (hundreds):[2,24,45,66,75,90,170,802]
```

---

## 25. Bucket Sort

Distribute elements into buckets, sort each bucket, concatenate.

**Complexity:** Time O(n + k) average. Space O(n + k).

```javascript
function bucketSort(arr, bucketCount = 5) {
  if (arr.length <= 1) return arr;

  const min = Math.min(...arr);
  const max = Math.max(...arr);
  const bucketSize = (max - min) / bucketCount;

  // Create buckets
  const buckets = Array.from({ length: bucketCount }, () => []);

  // Distribute elements into buckets
  for (const num of arr) {
    let idx = Math.floor((num - min) / bucketSize);
    if (idx === bucketCount) idx--;  // handle max value
    buckets[idx].push(num);
  }

  // Sort each bucket and concatenate
  return buckets.flatMap(bucket => bucket.sort((a, b) => a - b));
}

bucketSort([0.78, 0.17, 0.39, 0.26, 0.72, 0.94, 0.21, 0.12, 0.23, 0.68]);
```

### Sorting Algorithm Comparison

| Algorithm | Best | Average | Worst | Space | Stable |
|-----------|------|---------|-------|-------|--------|
| Bubble | O(n) | O(n²) | O(n²) | O(1) | ✅ |
| Selection | O(n²) | O(n²) | O(n²) | O(1) | ❌ |
| Insertion | O(n) | O(n²) | O(n²) | O(1) | ✅ |
| Merge | O(n log n) | O(n log n) | O(n log n) | O(n) | ✅ |
| Quick | O(n log n) | O(n log n) | O(n²) | O(log n) | ❌ |
| Heap | O(n log n) | O(n log n) | O(n log n) | O(1) | ❌ |
| Counting | O(n+k) | O(n+k) | O(n+k) | O(k) | ✅ |
| Radix | O(nk) | O(nk) | O(nk) | O(n+k) | ✅ |

---

# PART 5 — SEARCHING ALGORITHMS

---

## 26. Linear Search

Check every element one by one. Works on **unsorted** data.

**Complexity:** Time O(n), Space O(1).

```javascript
function linearSearch(arr, target) {
  for (let i = 0; i < arr.length; i++) {
    if (arr[i] === target) return i;  // found! return index
  }
  return -1;  // not found
}

// Find ALL occurrences
function findAll(arr, target) {
  return arr.reduce((indices, val, idx) => {
    if (val === target) indices.push(idx);
    return indices;
  }, []);
}

// Linear search on objects
function findUser(users, id) {
  return users.find(user => user.id === id) || null;
}
```

---

## 27. Binary Search

Works ONLY on **sorted arrays**. Cuts search space in HALF each step.

**Complexity:** Time O(log n), Space O(1).

```javascript
// ─── Classic Binary Search ───────────────────────
function binarySearch(arr, target) {
  let left = 0, right = arr.length - 1;

  while (left <= right) {
    // Avoid integer overflow: (left + right) / 2 might overflow in other languages
    const mid = left + Math.floor((right - left) / 2);

    if (arr[mid] === target) return mid;       // found
    if (arr[mid] < target)   left = mid + 1;   // search right half
    else                     right = mid - 1;  // search left half
  }
  return -1;
}

// ─── Find First Occurrence ───────────────────────
function findFirst(arr, target) {
  let left = 0, right = arr.length - 1, result = -1;
  while (left <= right) {
    const mid = Math.floor((left + right) / 2);
    if (arr[mid] === target) {
      result = mid;        // found one, but keep searching LEFT
      right = mid - 1;     // ← this is the key difference
    } else if (arr[mid] < target) {
      left = mid + 1;
    } else {
      right = mid - 1;
    }
  }
  return result;
}

// ─── Find Last Occurrence ────────────────────────
function findLast(arr, target) {
  let left = 0, right = arr.length - 1, result = -1;
  while (left <= right) {
    const mid = Math.floor((left + right) / 2);
    if (arr[mid] === target) {
      result = mid;
      left = mid + 1;  // ← keep searching RIGHT
    } else if (arr[mid] < target) {
      left = mid + 1;
    } else {
      right = mid - 1;
    }
  }
  return result;
}

// ─── Search in Rotated Sorted Array ──────────────
// [4,5,6,7,0,1,2] — originally sorted, then rotated
function searchRotated(arr, target) {
  let left = 0, right = arr.length - 1;

  while (left <= right) {
    const mid = Math.floor((left + right) / 2);
    if (arr[mid] === target) return mid;

    // Determine which half is sorted
    if (arr[left] <= arr[mid]) {  // left half is sorted
      if (arr[left] <= target && target < arr[mid]) {
        right = mid - 1;  // target is in sorted left half
      } else {
        left = mid + 1;
      }
    } else {  // right half is sorted
      if (arr[mid] < target && target <= arr[right]) {
        left = mid + 1;   // target is in sorted right half
      } else {
        right = mid - 1;
      }
    }
  }
  return -1;
}

// ─── Find Minimum in Rotated Array ───────────────
function findMinRotated(arr) {
  let left = 0, right = arr.length - 1;

  while (left < right) {
    const mid = Math.floor((left + right) / 2);
    if (arr[mid] > arr[right]) {
      left = mid + 1;   // minimum is in right half
    } else {
      right = mid;      // minimum is in left half (including mid)
    }
  }
  return arr[left];
}

// ─── Binary Search on Answer Space ───────────────
// "Find minimum speed to eat all bananas in H hours"
function minEatingSpeed(piles, H) {
  let left = 1, right = Math.max(...piles);

  while (left < right) {
    const mid = Math.floor((left + right) / 2);
    const hours = piles.reduce((sum, p) => sum + Math.ceil(p / mid), 0);

    if (hours <= H) right = mid;   // can eat slower
    else            left = mid + 1; // need to eat faster
  }
  return left;
}
```

---

## 28. Interpolation & Exponential Search

```javascript
// ─── Interpolation Search ────────────────────────
// Better than binary search for UNIFORMLY distributed sorted arrays
// Complexity: O(log log n) average for uniform data
function interpolationSearch(arr, target) {
  let left = 0, right = arr.length - 1;

  while (left <= right && target >= arr[left] && target <= arr[right]) {
    if (left === right) return arr[left] === target ? left : -1;

    // Estimate position using linear interpolation (not just midpoint)
    const pos = left + Math.floor(
      ((target - arr[left]) * (right - left)) / (arr[right] - arr[left])
    );

    if (arr[pos] === target) return pos;
    if (arr[pos] < target)   left = pos + 1;
    else                     right = pos - 1;
  }
  return -1;
}

// ─── Exponential Search ──────────────────────────
// Useful for unbounded/infinite arrays
// Complexity: O(log n)
function exponentialSearch(arr, target) {
  if (arr[0] === target) return 0;

  // Find range where element might be present by doubling index
  let i = 1;
  while (i < arr.length && arr[i] <= target) i *= 2;

  // Binary search in found range
  return binarySearch(arr.slice(i / 2, Math.min(i, arr.length)), target);
}
```

---

# PART 6 — GRAPH ALGORITHMS

---

## 29. BFS — Breadth-First Search

Explores graph **level by level** using a queue. Finds **shortest path** in unweighted graphs.

**Complexity:** Time O(V + E), Space O(V).

```javascript
function bfs(graph, start) {
  const visited = new Set([start]);
  const queue   = [start];
  const order   = [];

  while (queue.length > 0) {
    const vertex = queue.shift();
    order.push(vertex);

    // Visit all unvisited neighbors
    for (const { node } of graph.getNeighbors(vertex)) {
      if (!visited.has(node)) {
        visited.add(node);
        queue.push(node);
      }
    }
  }
  return order;
}

// ─── BFS Shortest Path (unweighted) ──────────────
function shortestPath(graph, start, end) {
  if (start === end) return [start];

  const visited  = new Set([start]);
  const queue    = [start];
  const parent   = new Map([[start, null]]);  // track how we got to each node

  while (queue.length > 0) {
    const vertex = queue.shift();

    for (const { node } of graph.getNeighbors(vertex)) {
      if (!visited.has(node)) {
        visited.add(node);
        parent.set(node, vertex);
        queue.push(node);

        if (node === end) {
          // Reconstruct path
          const path = [];
          let current = end;
          while (current !== null) {
            path.unshift(current);
            current = parent.get(current);
          }
          return path;
        }
      }
    }
  }
  return null;  // no path found
}

// ─── BFS on Grid — Shortest Path ─────────────────
function shortestPathGrid(grid, start, end) {
  const [startR, startC] = start;
  const [endR, endC]     = end;
  const rows = grid.length, cols = grid[0].length;
  const dirs = [[0,1],[0,-1],[1,0],[-1,0]];  // right, left, down, up

  const queue    = [[startR, startC, 0]];     // [row, col, distance]
  const visited  = new Set([`${startR},${startC}`]);

  while (queue.length > 0) {
    const [r, c, dist] = queue.shift();

    if (r === endR && c === endC) return dist;

    for (const [dr, dc] of dirs) {
      const nr = r + dr, nc = c + dc;
      const key = `${nr},${nc}`;

      if (nr >= 0 && nr < rows && nc >= 0 && nc < cols
          && grid[nr][nc] !== 1  // 1 = wall
          && !visited.has(key)) {
        visited.add(key);
        queue.push([nr, nc, dist + 1]);
      }
    }
  }
  return -1;  // no path
}
```

---

## 30. DFS — Depth-First Search

Explores as **deep as possible** before backtracking. Uses a stack (or recursion).

**Complexity:** Time O(V + E), Space O(V).

```javascript
// ─── Recursive DFS ───────────────────────────────
function dfsRecursive(graph, start, visited = new Set()) {
  visited.add(start);
  const order = [start];

  for (const { node } of graph.getNeighbors(start)) {
    if (!visited.has(node)) {
      order.push(...dfsRecursive(graph, node, visited));
    }
  }
  return order;
}

// ─── Iterative DFS (using explicit stack) ────────
function dfsIterative(graph, start) {
  const visited = new Set();
  const stack   = [start];
  const order   = [];

  while (stack.length > 0) {
    const vertex = stack.pop();  // ← pop from top (last added)

    if (visited.has(vertex)) continue;
    visited.add(vertex);
    order.push(vertex);

    for (const { node } of graph.getNeighbors(vertex)) {
      if (!visited.has(node)) stack.push(node);
    }
  }
  return order;
}

// ─── DFS on Grid — Island Problems ───────────────
function numIslandsDFS(grid) {
  const rows = grid.length, cols = grid[0].length;
  let islands = 0;

  function dfs(r, c) {
    // Out of bounds or water or already visited
    if (r < 0 || r >= rows || c < 0 || c >= cols || grid[r][c] !== '1') return;

    grid[r][c] = '0';  // mark as visited (sink the island)
    dfs(r+1, c); dfs(r-1, c); dfs(r, c+1); dfs(r, c-1);
  }

  for (let r = 0; r < rows; r++) {
    for (let c = 0; c < cols; c++) {
      if (grid[r][c] === '1') {
        islands++;
        dfs(r, c);  // sink entire connected island
      }
    }
  }
  return islands;
}

// ─── DFS: All Paths from Source to Target ────────
function allPaths(graph, src, dst) {
  const result = [];

  function dfs(node, path) {
    if (node === dst) { result.push([...path]); return; }
    for (const { node: next } of graph.getNeighbors(node)) {
      path.push(next);
      dfs(next, path);
      path.pop();  // backtrack!
    }
  }

  dfs(src, [src]);
  return result;
}

// ─── Cycle Detection in Directed Graph ───────────
function hasCycleDirected(graph) {
  const WHITE = 0, GRAY = 1, BLACK = 2;  // NOT_VISITED, IN_PROGRESS, DONE
  const state = new Map();

  for (const v of graph.getVertices()) state.set(v, WHITE);

  function dfs(v) {
    state.set(v, GRAY);  // currently exploring

    for (const { node } of graph.getNeighbors(v)) {
      if (state.get(node) === GRAY) return true;   // back edge = cycle!
      if (state.get(node) === WHITE && dfs(node)) return true;
    }

    state.set(v, BLACK);  // done exploring
    return false;
  }

  for (const v of graph.getVertices()) {
    if (state.get(v) === WHITE && dfs(v)) return true;
  }
  return false;
}
```

---

## 31. Dijkstra's Shortest Path

Find shortest paths from a source to **all other vertices** in a **weighted graph** (non-negative weights only).

**Complexity:** Time O((V + E) log V) with priority queue. Space O(V).

```javascript
function dijkstra(graph, start) {
  const dist   = new Map();
  const prev   = new Map();
  const pq     = new PriorityQueue();

  // Initialize all distances to Infinity
  for (const v of graph.getVertices()) {
    dist.set(v, Infinity);
    prev.set(v, null);
  }
  dist.set(start, 0);
  pq.push(start, 0);  // {item: start, priority: 0}

  while (!pq.isEmpty()) {
    const u = pq.pop();  // vertex with smallest known distance

    for (const { node: v, weight } of graph.getNeighbors(u)) {
      const newDist = dist.get(u) + weight;

      // Relaxation: found a shorter path to v!
      if (newDist < dist.get(v)) {
        dist.set(v, newDist);
        prev.set(v, u);
        pq.push(v, newDist);
      }
    }
  }

  return { dist, prev };
}

// Reconstruct shortest path from start to end
function getPath(prev, start, end) {
  const path = [];
  let current = end;
  while (current !== null) {
    path.unshift(current);
    current = prev.get(current);
  }
  return path[0] === start ? path : [];
}

// Usage
const g = new Graph(false);
g.addEdge('A', 'B', 4);
g.addEdge('A', 'C', 2);
g.addEdge('C', 'B', 1);
g.addEdge('B', 'D', 5);
g.addEdge('C', 'D', 8);

const { dist, prev } = dijkstra(g, 'A');
console.log(dist.get('D'));           // 8  (A→C→B→D = 2+1+5)
console.log(getPath(prev, 'A', 'D')); // ['A','C','B','D']
```

---

## 32. Bellman-Ford Algorithm

Handles **negative edge weights** (Dijkstra can't). Also detects **negative cycles**.

**Complexity:** Time O(V × E), Space O(V).

```javascript
function bellmanFord(vertices, edges, start) {
  // Initialize distances
  const dist = {};
  for (const v of vertices) dist[v] = Infinity;
  dist[start] = 0;

  // Relax ALL edges V-1 times
  // (shortest path has at most V-1 edges)
  for (let i = 0; i < vertices.length - 1; i++) {
    for (const { from, to, weight } of edges) {
      if (dist[from] !== Infinity && dist[from] + weight < dist[to]) {
        dist[to] = dist[from] + weight;
      }
    }
  }

  // Check for negative cycles (if still relaxing after V-1 rounds, there's a negative cycle)
  for (const { from, to, weight } of edges) {
    if (dist[from] !== Infinity && dist[from] + weight < dist[to]) {
      throw new Error("Graph contains negative cycle!");
    }
  }

  return dist;
}
```

---

## 33. Floyd-Warshall Algorithm

Find **all-pairs shortest paths** — shortest distance between every pair of vertices.

**Complexity:** Time O(V³), Space O(V²).

```javascript
function floydWarshall(n, edges) {
  // Initialize distance matrix
  const dist = Array.from({ length: n }, (_, i) =>
    Array.from({ length: n }, (_, j) => i === j ? 0 : Infinity)
  );

  // Fill in direct edges
  for (const [u, v, w] of edges) {
    dist[u][v] = w;
    dist[v][u] = w;  // undirected
  }

  // Try every vertex as intermediate point
  for (let k = 0; k < n; k++) {          // intermediate vertex
    for (let i = 0; i < n; i++) {        // source
      for (let j = 0; j < n; j++) {      // destination
        // Is going through k shorter?
        if (dist[i][k] + dist[k][j] < dist[i][j]) {
          dist[i][j] = dist[i][k] + dist[k][j];
        }
      }
    }
  }
  return dist;
}

// dist[i][j] = shortest distance from i to j
```

---

## 34. Topological Sort

Order vertices in a **DAG** (Directed Acyclic Graph) such that for every edge u→v, u comes before v. Used for task scheduling, build systems, course prerequisites.

```javascript
// ─── Kahn's Algorithm (BFS-based) ────────────────
function topologicalSortKahn(numCourses, prerequisites) {
  const inDegree = new Array(numCourses).fill(0);
  const adj = Array.from({ length: numCourses }, () => []);

  // Build graph and count in-degrees
  for (const [course, prereq] of prerequisites) {
    adj[prereq].push(course);
    inDegree[course]++;
  }

  // Start with all nodes that have no prerequisites
  const queue  = [];
  const result = [];
  for (let i = 0; i < numCourses; i++) {
    if (inDegree[i] === 0) queue.push(i);
  }

  while (queue.length > 0) {
    const node = queue.shift();
    result.push(node);

    for (const neighbor of adj[node]) {
      inDegree[neighbor]--;
      if (inDegree[neighbor] === 0) queue.push(neighbor);
    }
  }

  // If result has all courses, we can finish; otherwise there's a cycle
  return result.length === numCourses ? result : [];
}

// ─── DFS-based Topological Sort ──────────────────
function topologicalSortDFS(graph) {
  const visited = new Set();
  const stack   = [];

  function dfs(node) {
    visited.add(node);
    for (const { node: next } of graph.getNeighbors(node)) {
      if (!visited.has(next)) dfs(next);
    }
    stack.push(node);  // push AFTER visiting all descendants
  }

  for (const v of graph.getVertices()) {
    if (!visited.has(v)) dfs(v);
  }

  return stack.reverse();  // reverse gives topological order
}

// Course Schedule — can you finish all courses?
topologicalSortKahn(4, [[1,0],[2,0],[3,1],[3,2]]);  // [0,1,2,3] or [0,2,1,3]
```

---

## 35. Minimum Spanning Tree — Kruskal & Prim

A **Minimum Spanning Tree (MST)** connects all vertices with the minimum total edge weight.

```javascript
// ─── Kruskal's Algorithm (greedy, uses Union-Find) ─
// Sort edges by weight, add each if it doesn't create a cycle
function kruskal(n, edges) {
  // Sort edges by weight (ascending)
  edges.sort((a, b) => a.weight - b.weight);

  const uf  = new UnionFind(n);
  const mst = [];
  let   totalWeight = 0;

  for (const edge of edges) {
    const { u, v, weight } = edge;
    // Add edge if it connects two different components (no cycle!)
    if (uf.union(u, v)) {
      mst.push(edge);
      totalWeight += weight;
      if (mst.length === n - 1) break;  // MST is complete
    }
  }
  return { mst, totalWeight };
}

// ─── Prim's Algorithm (greedy, grows from one vertex) ─
// Start from any vertex, always add cheapest edge to unvisited vertex
function prim(graph) {
  const vertices = graph.getVertices();
  const start    = vertices[0];
  const inMST    = new Set([start]);
  const mst      = [];
  let   totalWeight = 0;

  const pq = new PriorityQueue();
  for (const { node, weight } of graph.getNeighbors(start)) {
    pq.push({ from: start, to: node, weight }, weight);
  }

  while (!pq.isEmpty() && inMST.size < vertices.length) {
    const { from, to, weight } = pq.pop();

    if (inMST.has(to)) continue;  // skip if already in MST

    inMST.add(to);
    mst.push({ from, to, weight });
    totalWeight += weight;

    // Add edges from new vertex
    for (const { node, weight: w } of graph.getNeighbors(to)) {
      if (!inMST.has(node)) pq.push({ from: to, to: node, weight: w }, w);
    }
  }
  return { mst, totalWeight };
}
```

---

# PART 7 — ALGORITHM PARADIGMS

---

## 36. Recursion & Backtracking

**Recursion**: function calls itself. **Backtracking**: try a choice, undo it if it doesn't work.

```javascript
// ─── Recursion Fundamentals ───────────────────────
// Every recursive function needs:
// 1. Base case  (when to stop)
// 2. Recursive case (reduce towards base case)

function factorial(n) {
  if (n <= 1) return 1;           // base case
  return n * factorial(n - 1);    // recursive case
}

function power(base, exp) {
  if (exp === 0) return 1;              // base case
  if (exp % 2 === 0) {
    const half = power(base, exp / 2);  // clever: compute half only once
    return half * half;                  // O(log n) instead of O(n)!
  }
  return base * power(base, exp - 1);
}

// ─── Backtracking Template ────────────────────────
/*
function backtrack(choices, current, result) {
  if (isSolution(current)) {
    result.push([...current]);
    return;
  }
  for (const choice of choices) {
    if (isValid(choice, current)) {
      current.push(choice);           // make choice
      backtrack(choices, current, result);  // explore
      current.pop();                  // UNDO choice (backtrack!)
    }
  }
}
*/

// ─── Generate All Subsets ─────────────────────────
function subsets(nums) {
  const result = [];

  function backtrack(start, current) {
    result.push([...current]);  // add current subset (including empty)

    for (let i = start; i < nums.length; i++) {
      current.push(nums[i]);       // include nums[i]
      backtrack(i + 1, current);   // explore with nums[i]
      current.pop();               // exclude nums[i] (backtrack)
    }
  }
  backtrack(0, []);
  return result;
}
subsets([1, 2, 3]);
// [[], [1], [1,2], [1,2,3], [1,3], [2], [2,3], [3]]

// ─── Generate Permutations ───────────────────────
function permutations(nums) {
  const result = [];

  function backtrack(current, used) {
    if (current.length === nums.length) {
      result.push([...current]);
      return;
    }
    for (let i = 0; i < nums.length; i++) {
      if (used[i]) continue;    // skip already used
      used[i] = true;
      current.push(nums[i]);
      backtrack(current, used);
      current.pop();
      used[i] = false;
    }
  }
  backtrack([], new Array(nums.length).fill(false));
  return result;
}
permutations([1, 2, 3]);  // [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]

// ─── N-Queens Problem ────────────────────────────
// Place N queens on N×N board so none attack each other
function solveNQueens(n) {
  const result   = [];
  const board    = Array.from({ length: n }, () => new Array(n).fill('.'));
  const cols     = new Set();
  const diag1    = new Set();  // top-left to bottom-right diagonals
  const diag2    = new Set();  // top-right to bottom-left diagonals

  function backtrack(row) {
    if (row === n) {
      result.push(board.map(row => row.join('')));
      return;
    }
    for (let col = 0; col < n; col++) {
      if (cols.has(col) || diag1.has(row - col) || diag2.has(row + col)) continue;

      // Place queen
      cols.add(col); diag1.add(row - col); diag2.add(row + col);
      board[row][col] = 'Q';

      backtrack(row + 1);

      // Remove queen (backtrack)
      cols.delete(col); diag1.delete(row - col); diag2.delete(row + col);
      board[row][col] = '.';
    }
  }
  backtrack(0);
  return result;
}

// ─── Sudoku Solver ───────────────────────────────
function solveSudoku(board) {
  function isValid(board, row, col, num) {
    const box_row = Math.floor(row / 3) * 3;
    const box_col = Math.floor(col / 3) * 3;

    for (let i = 0; i < 9; i++) {
      if (board[row][i] === num) return false;       // check row
      if (board[i][col] === num) return false;       // check column
      if (board[box_row + Math.floor(i/3)][box_col + i%3] === num) return false; // check 3x3 box
    }
    return true;
  }

  function solve() {
    for (let r = 0; r < 9; r++) {
      for (let c = 0; c < 9; c++) {
        if (board[r][c] !== '.') continue;
        for (let num = 1; num <= 9; num++) {
          const ch = String(num);
          if (isValid(board, r, c, ch)) {
            board[r][c] = ch;
            if (solve()) return true;   // found solution!
            board[r][c] = '.';          // backtrack
          }
        }
        return false;  // no valid number — backtrack
      }
    }
    return true;  // all cells filled
  }
  solve();
}
```

---

## 37. Divide and Conquer

Break problem into **smaller subproblems**, solve them independently, **combine** results.

```javascript
// ─── Merge Sort (already seen) ────────────────────
// ─── Binary Search (already seen) ────────────────

// ─── Maximum Subarray — Kadane's vs D&C ──────────
// Kadane's O(n):
function maxSubarrayKadane(nums) {
  let maxSum     = nums[0];
  let currentSum = nums[0];

  for (let i = 1; i < nums.length; i++) {
    // Either start fresh or extend current subarray
    currentSum = Math.max(nums[i], currentSum + nums[i]);
    maxSum     = Math.max(maxSum, currentSum);
  }
  return maxSum;
}
maxSubarrayKadane([-2,1,-3,4,-1,2,1,-5,4]);  // 6  ([4,-1,2,1])

// Divide and Conquer O(n log n):
function maxSubarrayDC(nums, left = 0, right = nums.length - 1) {
  if (left === right) return nums[left];

  const mid = Math.floor((left + right) / 2);

  const leftMax  = maxSubarrayDC(nums, left, mid);
  const rightMax = maxSubarrayDC(nums, mid + 1, right);
  const crossMax = maxCrossing(nums, left, mid, right);

  return Math.max(leftMax, rightMax, crossMax);
}

function maxCrossing(nums, left, mid, right) {
  let leftSum = -Infinity, sum = 0;
  for (let i = mid; i >= left; i--) {
    sum += nums[i];
    leftSum = Math.max(leftSum, sum);
  }
  let rightSum = -Infinity; sum = 0;
  for (let i = mid + 1; i <= right; i++) {
    sum += nums[i];
    rightSum = Math.max(rightSum, sum);
  }
  return leftSum + rightSum;
}

// ─── Count Inversions ────────────────────────────
// Count pairs (i,j) where i<j but arr[i]>arr[j]
// Piggybacks on merge sort — O(n log n)
function countInversions(arr) {
  let inversions = 0;

  function mergeCount(arr) {
    if (arr.length <= 1) return arr;
    const mid   = Math.floor(arr.length / 2);
    const left  = mergeCount(arr.slice(0, mid));
    const right = mergeCount(arr.slice(mid));
    return mergeAndCount(left, right);
  }

  function mergeAndCount(left, right) {
    const merged = [];
    let i = 0, j = 0;
    while (i < left.length && j < right.length) {
      if (left[i] <= right[j]) {
        merged.push(left[i++]);
      } else {
        inversions += left.length - i;  // all remaining left elements form inversions!
        merged.push(right[j++]);
      }
    }
    return [...merged, ...left.slice(i), ...right.slice(j)];
  }

  mergeCount(arr);
  return inversions;
}
countInversions([8,4,2,1]);  // 6 inversions: (8,4),(8,2),(8,1),(4,2),(4,1),(2,1)
```

---

## 38. Dynamic Programming

DP solves problems by **breaking them into overlapping subproblems** and storing results to avoid recomputation.

Two approaches:
- **Top-Down (Memoization)**: Recursive + cache
- **Bottom-Up (Tabulation)**: Iterative + table

```javascript
// ─── 1. Fibonacci — the classic DP example ───────
// Naive O(2ⁿ) → DP O(n)

// Memoization (top-down)
function fibMemo(n, memo = {}) {
  if (n in memo) return memo[n];    // cache hit!
  if (n <= 1) return n;
  memo[n] = fibMemo(n-1, memo) + fibMemo(n-2, memo);
  return memo[n];
}

// Tabulation (bottom-up)
function fibTab(n) {
  if (n <= 1) return n;
  const dp = [0, 1];
  for (let i = 2; i <= n; i++) dp[i] = dp[i-1] + dp[i-2];
  return dp[n];
}

// Space-optimized (only need last 2 values)
function fibOptimal(n) {
  if (n <= 1) return n;
  let prev2 = 0, prev1 = 1;
  for (let i = 2; i <= n; i++) {
    [prev2, prev1] = [prev1, prev2 + prev1];
  }
  return prev1;
}

// ─── 2. 0/1 Knapsack ─────────────────────────────
// Given items with weights & values, maximize value within weight capacity
function knapsack(weights, values, capacity) {
  const n  = weights.length;
  // dp[i][w] = max value using first i items with capacity w
  const dp = Array.from({ length: n+1 }, () => new Array(capacity+1).fill(0));

  for (let i = 1; i <= n; i++) {
    for (let w = 0; w <= capacity; w++) {
      // Don't include item i-1
      dp[i][w] = dp[i-1][w];
      // Include item i-1 (if it fits)
      if (weights[i-1] <= w) {
        dp[i][w] = Math.max(dp[i][w],
                            dp[i-1][w - weights[i-1]] + values[i-1]);
      }
    }
  }
  return dp[n][capacity];
}
knapsack([2,3,4,5], [3,4,5,6], 5);  // 7  (items 0 and 1)

// ─── 3. Longest Common Subsequence (LCS) ─────────
function lcs(text1, text2) {
  const m = text1.length, n = text2.length;
  const dp = Array.from({ length: m+1 }, () => new Array(n+1).fill(0));

  for (let i = 1; i <= m; i++) {
    for (let j = 1; j <= n; j++) {
      if (text1[i-1] === text2[j-1]) {
        dp[i][j] = dp[i-1][j-1] + 1;         // characters match!
      } else {
        dp[i][j] = Math.max(dp[i-1][j], dp[i][j-1]);  // take best without one char
      }
    }
  }
  return dp[m][n];
}
lcs("abcde", "ace");  // 3  (a,c,e)

// ─── 4. Edit Distance (Levenshtein) ──────────────
// Minimum operations (insert, delete, replace) to convert word1 to word2
function editDistance(word1, word2) {
  const m = word1.length, n = word2.length;
  const dp = Array.from({ length: m+1 }, (_, i) =>
    Array.from({ length: n+1 }, (_, j) => i || j)
  );
  // dp[0][j] = j (j insertions to build word2 from empty string)
  // dp[i][0] = i (i deletions to reach empty string)

  for (let i = 1; i <= m; i++) {
    for (let j = 1; j <= n; j++) {
      if (word1[i-1] === word2[j-1]) {
        dp[i][j] = dp[i-1][j-1];          // no operation needed
      } else {
        dp[i][j] = 1 + Math.min(
          dp[i-1][j],    // delete from word1
          dp[i][j-1],    // insert into word1
          dp[i-1][j-1]   // replace
        );
      }
    }
  }
  return dp[m][n];
}
editDistance("horse", "ros");   // 3

// ─── 5. Coin Change ──────────────────────────────
// Minimum coins to make amount
function coinChange(coins, amount) {
  const dp = new Array(amount + 1).fill(Infinity);
  dp[0] = 0;  // 0 coins needed for amount 0

  for (let i = 1; i <= amount; i++) {
    for (const coin of coins) {
      if (coin <= i && dp[i - coin] + 1 < dp[i]) {
        dp[i] = dp[i - coin] + 1;
      }
    }
  }
  return dp[amount] === Infinity ? -1 : dp[amount];
}
coinChange([1,5,11], 15);  // 3  (5+5+5)

// ─── 6. Longest Increasing Subsequence (LIS) ─────
function lengthOfLIS(nums) {
  const dp = new Array(nums.length).fill(1);  // each element is LIS of length 1

  for (let i = 1; i < nums.length; i++) {
    for (let j = 0; j < i; j++) {
      if (nums[j] < nums[i]) {
        dp[i] = Math.max(dp[i], dp[j] + 1);
      }
    }
  }
  return Math.max(...dp);
}
lengthOfLIS([10,9,2,5,3,7,101,18]);  // 4  ([2,3,7,101] or [2,5,7,101])

// O(n log n) LIS using binary search:
function lisOptimal(nums) {
  const tails = [];  // tails[i] = smallest tail element of increasing subseq of length i+1

  for (const num of nums) {
    let left = 0, right = tails.length;
    while (left < right) {
      const mid = Math.floor((left + right) / 2);
      if (tails[mid] < num) left = mid + 1;
      else right = mid;
    }
    tails[left] = num;
  }
  return tails.length;
}

// ─── 7. Matrix Chain Multiplication ──────────────
function matrixChainOrder(dims) {
  const n  = dims.length - 1;  // number of matrices
  const dp = Array.from({ length: n }, () => new Array(n).fill(0));

  // l = chain length
  for (let l = 2; l <= n; l++) {
    for (let i = 0; i <= n - l; i++) {
      const j = i + l - 1;
      dp[i][j] = Infinity;
      for (let k = i; k < j; k++) {
        const cost = dp[i][k] + dp[k+1][j] + dims[i]*dims[k+1]*dims[j+1];
        dp[i][j] = Math.min(dp[i][j], cost);
      }
    }
  }
  return dp[0][n-1];
}
```

---

## 39. Greedy Algorithms

Make the **locally optimal choice** at each step, hoping to reach the global optimum. Works when problem has **greedy choice property** and **optimal substructure**.

```javascript
// ─── Activity Selection ──────────────────────────
// Select maximum number of non-overlapping activities
function activitySelection(activities) {
  // Sort by end time
  activities.sort((a, b) => a.end - b.end);

  const selected = [activities[0]];
  let lastEnd = activities[0].end;

  for (let i = 1; i < activities.length; i++) {
    // Greedy: always pick activity that ends earliest and doesn't overlap
    if (activities[i].start >= lastEnd) {
      selected.push(activities[i]);
      lastEnd = activities[i].end;
    }
  }
  return selected;
}

// ─── Fractional Knapsack ─────────────────────────
// Unlike 0/1 knapsack, we CAN take fractions of items
function fractionalKnapsack(weights, values, capacity) {
  const items = weights.map((w, i) => ({
    weight: w,
    value:  values[i],
    ratio:  values[i] / w   // value per unit weight
  }));

  // Greedy: take item with highest value/weight ratio first
  items.sort((a, b) => b.ratio - a.ratio);

  let totalValue = 0;
  let remaining  = capacity;

  for (const item of items) {
    if (remaining <= 0) break;
    const take = Math.min(item.weight, remaining);
    totalValue += take * item.ratio;
    remaining  -= take;
  }
  return totalValue;
}

// ─── Jump Game ───────────────────────────────────
// Can you reach the last index? nums[i] = max jump from position i
function canJump(nums) {
  let maxReach = 0;  // furthest position reachable so far

  for (let i = 0; i < nums.length; i++) {
    if (i > maxReach) return false;   // can't reach this position
    maxReach = Math.max(maxReach, i + nums[i]);  // update furthest reach
  }
  return true;
}
canJump([2,3,1,1,4]);  // true
canJump([3,2,1,0,4]);  // false

// ─── Minimum Number of Intervals to Remove ───────
function eraseOverlapIntervals(intervals) {
  intervals.sort((a, b) => a[1] - b[1]);  // sort by end time
  let removed = 0, lastEnd = -Infinity;

  for (const [start, end] of intervals) {
    if (start >= lastEnd) {
      lastEnd = end;     // keep this interval
    } else {
      removed++;         // remove overlapping interval
    }
  }
  return removed;
}

// ─── Huffman Encoding ────────────────────────────
function huffmanEncoding(chars, freqs) {
  const pq = new PriorityQueue();

  // Build initial nodes
  for (let i = 0; i < chars.length; i++) {
    pq.push({ char: chars[i], freq: freqs[i], left: null, right: null }, freqs[i]);
  }

  // Build Huffman tree
  while (pq.size() > 1) {
    const left  = pq.pop();   // smallest frequency
    const right = pq.pop();   // second smallest
    const parent = {
      char:  null,
      freq:  left.freq + right.freq,
      left, right
    };
    pq.push(parent, parent.freq);
  }

  // Generate codes
  const codes = {};
  function buildCodes(node, code) {
    if (!node) return;
    if (node.char !== null) { codes[node.char] = code || '0'; return; }
    buildCodes(node.left,  code + '0');
    buildCodes(node.right, code + '1');
  }
  buildCodes(pq.pop(), '');
  return codes;
}
```

---

## 40. Sliding Window & Two Pointers

Two of the most important interview patterns for array/string problems.

### Sliding Window

```javascript
// ─── Fixed-Size Window ───────────────────────────
// Maximum sum of subarray of size k
function maxSumSubarray(arr, k) {
  let windowSum = arr.slice(0, k).reduce((a, b) => a + b, 0);
  let maxSum    = windowSum;

  for (let i = k; i < arr.length; i++) {
    windowSum += arr[i] - arr[i - k];  // add new, remove old — O(1)!
    maxSum     = Math.max(maxSum, windowSum);
  }
  return maxSum;
}
maxSumSubarray([2,1,5,1,3,2], 3);  // 9  (5+1+3)

// ─── Variable-Size Window ────────────────────────
// Longest substring without repeating characters
function lengthOfLongestSubstring(s) {
  const seen = new Map();  // char → last seen index
  let maxLen = 0, left = 0;

  for (let right = 0; right < s.length; right++) {
    if (seen.has(s[right]) && seen.get(s[right]) >= left) {
      left = seen.get(s[right]) + 1;  // shrink window from left
    }
    seen.set(s[right], right);
    maxLen = Math.max(maxLen, right - left + 1);
  }
  return maxLen;
}
lengthOfLongestSubstring("abcabcbb");  // 3  ("abc")
lengthOfLongestSubstring("pwwkew");    // 3  ("wke")

// Minimum Window Substring
function minWindow(s, t) {
  const need    = new Map();
  const window  = new Map();
  for (const c of t) need.set(c, (need.get(c) || 0) + 1);

  let left = 0, right = 0;
  let valid = 0;  // number of chars with sufficient count
  let minLen = Infinity, minStart = 0;

  while (right < s.length) {
    const c = s[right++];
    if (need.has(c)) {
      window.set(c, (window.get(c) || 0) + 1);
      if (window.get(c) === need.get(c)) valid++;
    }

    // Shrink window from left when all chars are covered
    while (valid === need.size) {
      if (right - left < minLen) {
        minLen = right - left;
        minStart = left;
      }
      const d = s[left++];
      if (need.has(d)) {
        if (window.get(d) === need.get(d)) valid--;
        window.set(d, window.get(d) - 1);
      }
    }
  }
  return minLen === Infinity ? '' : s.substr(minStart, minLen);
}
minWindow("ADOBECODEBANC", "ABC");  // "BANC"
```

### Two Pointers

```javascript
// ─── Two Sum (sorted array) ───────────────────────
function twoSumSorted(nums, target) {
  let left = 0, right = nums.length - 1;

  while (left < right) {
    const sum = nums[left] + nums[right];
    if (sum === target) return [left, right];
    if (sum < target)   left++;
    else                right--;
  }
  return [];
}

// ─── Three Sum ───────────────────────────────────
function threeSum(nums) {
  nums.sort((a, b) => a - b);
  const result = [];

  for (let i = 0; i < nums.length - 2; i++) {
    if (i > 0 && nums[i] === nums[i-1]) continue;  // skip duplicates

    let left = i + 1, right = nums.length - 1;
    while (left < right) {
      const sum = nums[i] + nums[left] + nums[right];
      if (sum === 0) {
        result.push([nums[i], nums[left], nums[right]]);
        while (left < right && nums[left]  === nums[left+1])  left++;
        while (left < right && nums[right] === nums[right-1]) right--;
        left++; right--;
      } else if (sum < 0) {
        left++;
      } else {
        right--;
      }
    }
  }
  return result;
}

// ─── Container With Most Water ───────────────────
function maxWater(height) {
  let left = 0, right = height.length - 1;
  let maxWater = 0;

  while (left < right) {
    const water = Math.min(height[left], height[right]) * (right - left);
    maxWater = Math.max(maxWater, water);

    // Move the pointer at the shorter height (greedy)
    if (height[left] < height[right]) left++;
    else right--;
  }
  return maxWater;
}

// ─── Trapping Rain Water ─────────────────────────
function trap(height) {
  let left = 0, right = height.length - 1;
  let leftMax = 0, rightMax = 0;
  let water = 0;

  while (left < right) {
    if (height[left] < height[right]) {
      leftMax = Math.max(leftMax, height[left]);
      water  += leftMax - height[left];  // water trapped here
      left++;
    } else {
      rightMax = Math.max(rightMax, height[right]);
      water   += rightMax - height[right];
      right--;
    }
  }
  return water;
}
trap([0,1,0,2,1,0,1,3,2,1,2,1]);  // 6
```

---

## 41. Bit Manipulation

Operations on binary representations. Very fast (single CPU instruction).

```javascript
// ─── Basic Bit Operations ────────────────────────
// n = 6 = 0110 in binary

6 & 3      // AND:   0110 & 0011 = 0010 = 2
6 | 3      // OR:    0110 | 0011 = 0111 = 7
6 ^ 3      // XOR:   0110 ^ 0011 = 0101 = 5
~6         // NOT:   ~0110 = ...11111001 = -7
6 << 1     // Left shift:  1100 = 12  (multiply by 2)
6 >> 1     // Right shift: 0011 = 3   (divide by 2)
6 >>> 1    // Unsigned right shift: 3  (for negatives use this)

// ─── Common Bit Tricks ───────────────────────────
const n = 6;  // 0110

// Check if bit i is set
function isBitSet(n, i) { return (n >> i & 1) === 1; }
isBitSet(6, 1);  // true  (bit 1 of 0110 is 1)
isBitSet(6, 0);  // false (bit 0 of 0110 is 0)

// Set bit i
function setBit(n, i) { return n | (1 << i); }
setBit(6, 0);   // 0110 | 0001 = 0111 = 7

// Clear bit i
function clearBit(n, i) { return n & ~(1 << i); }
clearBit(6, 1);  // 0110 & 1101 = 0100 = 4

// Toggle bit i
function toggleBit(n, i) { return n ^ (1 << i); }
toggleBit(6, 0);  // 0110 ^ 0001 = 0111 = 7

// Check if power of 2  (only one bit set)
function isPowerOf2(n) { return n > 0 && (n & (n-1)) === 0; }
isPowerOf2(8);   // true  1000 & 0111 = 0
isPowerOf2(6);   // false 0110 & 0101 = 0100 ≠ 0

// Count set bits (Hamming weight)
function countBits(n) {
  let count = 0;
  while (n) {
    n &= (n - 1);  // remove lowest set bit
    count++;
  }
  return count;
}
countBits(11);  // 3  (1011 has three 1s)

// Get lowest set bit
function lowestSetBit(n) { return n & (-n); }
lowestSetBit(12);  // 1100 & 0100 = 0100 = 4

// ─── XOR Tricks ──────────────────────────────────
// XOR properties: a^a=0, a^0=a, commutative & associative

// Find single number (all others appear twice)
function singleNumber(nums) {
  return nums.reduce((xor, n) => xor ^ n, 0);
  // All pairs cancel out (a^a=0), single remains
}
singleNumber([4,1,2,1,2]);  // 4

// Find two non-duplicate numbers
function singleNumberIII(nums) {
  const xor = nums.reduce((a, b) => a ^ b, 0);  // xor of both singles
  const diff = xor & (-xor);   // any different bit between the two
  let a = 0;
  for (const n of nums) if (n & diff) a ^= n;
  return [a, xor ^ a];
}

// ─── Bitmask DP ──────────────────────────────────
// Traveling Salesman Problem with bitmask DP
function tsp(dist) {
  const n    = dist.length;
  const FULL = (1 << n) - 1;  // all cities visited
  const dp   = Array.from({ length: 1 << n }, () => new Array(n).fill(Infinity));
  dp[1][0] = 0;  // start at city 0

  for (let mask = 1; mask < (1 << n); mask++) {
    for (let u = 0; u < n; u++) {
      if (!(mask & (1 << u))) continue;  // u not in mask
      for (let v = 0; v < n; v++) {
        if (mask & (1 << v)) continue;   // v already visited
        dp[mask | (1 << v)][v] = Math.min(
          dp[mask | (1 << v)][v],
          dp[mask][u] + dist[u][v]
        );
      }
    }
  }
  // Return to start
  return Math.min(...dp[FULL].map((cost, v) => cost + dist[v][0]));
}
```

---

# PART 8 — ADVANCED TOPICS

---

## 42. Advanced String Algorithms — KMP & Rabin-Karp

### KMP — Knuth-Morris-Pratt Pattern Matching

Finds all occurrences of a pattern in text in **O(n + m)** — no backtracking!

```javascript
// KMP precomputes a "failure function" (LPS array):
// LPS[i] = length of longest proper prefix of pattern[0..i] which is also a suffix

function buildLPS(pattern) {
  const lps = new Array(pattern.length).fill(0);
  let len = 0, i = 1;

  while (i < pattern.length) {
    if (pattern[i] === pattern[len]) {
      lps[i++] = ++len;
    } else if (len > 0) {
      len = lps[len - 1];  // don't increment i — try shorter prefix
    } else {
      lps[i++] = 0;
    }
  }
  return lps;
}

function kmpSearch(text, pattern) {
  const n   = text.length;
  const m   = pattern.length;
  const lps = buildLPS(pattern);
  const matches = [];
  let i = 0, j = 0;  // i = text index, j = pattern index

  while (i < n) {
    if (text[i] === pattern[j]) {
      i++; j++;
      if (j === m) {
        matches.push(i - m);  // found at index i-m
        j = lps[j - 1];       // look for next match
      }
    } else if (j > 0) {
      j = lps[j - 1];  // mismatch after j matches — skip already matched
    } else {
      i++;  // no match at all, move text pointer
    }
  }
  return matches;
}

kmpSearch("AABAACAADAABAABA", "AABA");  // [0, 9, 12]

// ─── Rabin-Karp Rolling Hash ──────────────────────
// O(n + m) average using polynomial rolling hash
function rabinKarp(text, pattern) {
  const n = text.length, m = pattern.length;
  const BASE = 31, MOD = 1e9 + 7;
  const matches = [];

  // Compute pattern hash and first window hash
  let patHash = 0, winHash = 0;
  let power = 1;

  for (let i = 0; i < m; i++) {
    patHash = (patHash * BASE + pattern.charCodeAt(i)) % MOD;
    winHash = (winHash * BASE + text.charCodeAt(i)) % MOD;
    if (i > 0) power = power * BASE % MOD;
  }

  // Slide window
  for (let i = 0; i <= n - m; i++) {
    if (winHash === patHash) {
      // Verify actual match (handles hash collisions)
      if (text.substr(i, m) === pattern) matches.push(i);
    }
    if (i < n - m) {
      // Rolling hash: remove first char, add next char
      winHash = (winHash - text.charCodeAt(i) * power % MOD + MOD) % MOD;
      winHash = (winHash * BASE + text.charCodeAt(i + m)) % MOD;
    }
  }
  return matches;
}
```

---

## 43. Advanced Graph — Tarjan's & Kosaraju's SCC

**Strongly Connected Components (SCCs)**: maximal sets of vertices where every vertex is reachable from every other.

```javascript
// ─── Tarjan's SCC Algorithm ───────────────────────
// Single DFS pass, uses a stack — O(V + E)
function tarjanSCC(n, adj) {
  const disc    = new Array(n).fill(-1);   // discovery time
  const low     = new Array(n).fill(-1);   // lowest reachable disc
  const onStack = new Array(n).fill(false);
  const stack   = [];
  const sccs    = [];
  let timer = 0;

  function dfs(u) {
    disc[u] = low[u] = timer++;
    stack.push(u);
    onStack[u] = true;

    for (const v of (adj[u] || [])) {
      if (disc[v] === -1) {
        dfs(v);
        low[u] = Math.min(low[u], low[v]);
      } else if (onStack[v]) {
        low[u] = Math.min(low[u], disc[v]);
      }
    }

    // u is root of SCC if disc[u] == low[u]
    if (low[u] === disc[u]) {
      const scc = [];
      while (true) {
        const v = stack.pop();
        onStack[v] = false;
        scc.push(v);
        if (v === u) break;
      }
      sccs.push(scc);
    }
  }

  for (let i = 0; i < n; i++) {
    if (disc[i] === -1) dfs(i);
  }
  return sccs;
}

// ─── Bridges in Graph ─────────────────────────────
// An edge is a bridge if removing it disconnects the graph
function findBridges(n, adj) {
  const disc = new Array(n).fill(-1);
  const low  = new Array(n).fill(-1);
  const bridges = [];
  let timer = 0;

  function dfs(u, parent) {
    disc[u] = low[u] = timer++;
    for (const v of adj[u]) {
      if (disc[v] === -1) {
        dfs(v, u);
        low[u] = Math.min(low[u], low[v]);
        if (low[v] > disc[u]) bridges.push([u, v]);  // bridge!
      } else if (v !== parent) {
        low[u] = Math.min(low[u], disc[v]);
      }
    }
  }

  for (let i = 0; i < n; i++) if (disc[i] === -1) dfs(i, -1);
  return bridges;
}
```

---

## 44. LRU Cache & LFU Cache

### LRU Cache (Least Recently Used)

Evicts the **least recently used** item when full. Implementation: HashMap + Doubly Linked List.

```javascript
class LRUCache {
  constructor(capacity) {
    this.capacity = capacity;
    this.cache    = new Map();  // key → node

    // Doubly linked list with sentinel nodes
    this.head = { key: null, val: null, prev: null, next: null };  // dummy head (most recent)
    this.tail = { key: null, val: null, prev: null, next: null };  // dummy tail (least recent)
    this.head.next = this.tail;
    this.tail.prev = this.head;
  }

  // Add node right after head (most recently used)
  _addToFront(node) {
    node.next = this.head.next;
    node.prev = this.head;
    this.head.next.prev = node;
    this.head.next = node;
  }

  // Remove any node — O(1) because we have both prev and next pointers
  _remove(node) {
    node.prev.next = node.next;
    node.next.prev = node.prev;
  }

  get(key) {
    if (!this.cache.has(key)) return -1;
    const node = this.cache.get(key);
    this._remove(node);      // remove from current position
    this._addToFront(node);  // move to front (most recently used)
    return node.val;
  }

  put(key, value) {
    if (this.cache.has(key)) {
      const node = this.cache.get(key);
      node.val = value;
      this._remove(node);
      this._addToFront(node);
    } else {
      if (this.cache.size >= this.capacity) {
        // Evict LRU (node just before tail)
        const lru = this.tail.prev;
        this._remove(lru);
        this.cache.delete(lru.key);
      }
      const node = { key, val: value };
      this._addToFront(node);
      this.cache.set(key, node);
    }
  }
}

// Usage
const lru = new LRUCache(2);
lru.put(1, 1);   // cache: {1:1}
lru.put(2, 2);   // cache: {1:1, 2:2}
lru.get(1);      // returns 1, cache: {2:2, 1:1} (1 is now most recent)
lru.put(3, 3);   // evicts 2 (LRU), cache: {1:1, 3:3}
lru.get(2);      // returns -1 (was evicted)

// ─── LFU Cache (Least Frequently Used) ───────────
class LFUCache {
  constructor(capacity) {
    this.capacity = capacity;
    this.minFreq  = 0;
    this.keyToVal = new Map();   // key → value
    this.keyToFreq = new Map();  // key → frequency
    this.freqToKeys = new Map(); // frequency → ordered Set of keys
  }

  _updateFreq(key) {
    const freq = this.keyToFreq.get(key);
    this.keyToFreq.set(key, freq + 1);

    // Remove from current freq bucket
    this.freqToKeys.get(freq).delete(key);
    if (this.freqToKeys.get(freq).size === 0) {
      this.freqToKeys.delete(freq);
      if (this.minFreq === freq) this.minFreq++;
    }

    // Add to new freq bucket
    if (!this.freqToKeys.has(freq + 1)) this.freqToKeys.set(freq + 1, new Set());
    this.freqToKeys.get(freq + 1).add(key);
  }

  get(key) {
    if (!this.keyToVal.has(key)) return -1;
    this._updateFreq(key);
    return this.keyToVal.get(key);
  }

  put(key, value) {
    if (this.capacity <= 0) return;

    if (this.keyToVal.has(key)) {
      this.keyToVal.set(key, value);
      this._updateFreq(key);
      return;
    }

    if (this.keyToVal.size >= this.capacity) {
      // Evict LFU item (first key in minFreq bucket)
      const keys = this.freqToKeys.get(this.minFreq);
      const evictKey = keys.values().next().value;
      keys.delete(evictKey);
      this.keyToVal.delete(evictKey);
      this.keyToFreq.delete(evictKey);
    }

    this.keyToVal.set(key, value);
    this.keyToFreq.set(key, 1);
    if (!this.freqToKeys.has(1)) this.freqToKeys.set(1, new Set());
    this.freqToKeys.get(1).add(key);
    this.minFreq = 1;
  }
}
```

---

## 45. Interview Patterns & Cheat Sheet

### 14 Patterns to Recognize in Interviews

```
1. Sliding Window       → subarray/substring with constraint
2. Two Pointers         → sorted array, linked list, palindrome
3. Fast & Slow Pointers → cycle detection, middle of list
4. Merge Intervals      → overlapping intervals
5. Cyclic Sort          → range [0..n] arrays
6. In-place Reversal    → reverse a linked list / sublist
7. BFS                  → level-order, shortest path (unweighted)
8. DFS                  → path finding, trees, backtracking
9. Two Heaps            → median of a data stream
10. Subsets             → combinations, permutations
11. Binary Search       → sorted array, search space reduction
12. Bitwise XOR         → find single/missing number
13. Top K Elements      → heap-based selection
14. K-way Merge         → merge sorted arrays/lists
```

### Problem Recognition Guide

```javascript
// ── "Subarray of size k" ──────────────────────────
//    → Sliding Window (fixed size)

// ── "Longest/shortest subarray with condition" ────
//    → Sliding Window (variable size)

// ── "Sorted array, pair with sum X" ───────────────
//    → Two Pointers

// ── "Linked list — cycle, middle, nth from end" ───
//    → Fast & Slow Pointers

// ── "Overlapping intervals" ───────────────────────
//    → Sort by start, merge or count

// ── "Top K / Kth largest/smallest" ───────────────
//    → Min-Heap of size K

// ── "All combinations / subsets / permutations" ──
//    → Backtracking (DFS)

// ── "Shortest path in grid / unweighted graph" ───
//    → BFS

// ── "Shortest path in weighted graph" ────────────
//    → Dijkstra (non-negative) / Bellman-Ford (negative)

// ── "Search in sorted array" ─────────────────────
//    → Binary Search (even if rotated!)

// ── "Overlapping subproblems, optimal substructure"
//    → Dynamic Programming

// ── "Task dependencies / ordering" ───────────────
//    → Topological Sort

// ── "Connected components / union queries" ────────
//    → Union-Find

// ── "Prefix matching / autocomplete" ─────────────
//    → Trie

// ── "Find repeated/missing/single in array" ───────
//    → XOR bit tricks
```

### Time Complexity Quick Reference

```
Binary Search          → O(log n)
BFS / DFS              → O(V + E)
Dijkstra               → O((V+E) log V)
Floyd-Warshall         → O(V³)
Sorting                → O(n log n)
Heap push/pop          → O(log n)
Heap build             → O(n)
Trie insert/search     → O(m)  [m = word length]
Union-Find             → O(α(n)) ≈ O(1) amortized
LRU cache get/put      → O(1)
KMP search             → O(n + m)
Segment tree query     → O(log n)
Fenwick tree query     → O(log n)
DP Knapsack            → O(n × W)
DP LCS                 → O(m × n)
Backtracking subsets   → O(2ⁿ)
Backtracking perms     → O(n!)
```

### Space Complexity Quick Reference

```
Array / Hash Map / Set  → O(n)
Binary Tree (balanced)  → O(log n) stack space for DFS
Adjacency List Graph    → O(V + E)
Adjacency Matrix Graph  → O(V²)
DP table                → O(n) to O(n²) depending on problem
Trie                    → O(ALPHABET_SIZE × m × n)
Segment Tree            → O(4n)
Fenwick Tree            → O(n)
```

### JavaScript-Specific Tips for DSA

```javascript
// ── Use Map over {} for hash maps ─────────────────
const map = new Map();  // O(1) guaranteed, ordered, any key type
const obj = {};         // slightly faster for string keys

// ── Avoid array.shift() in queues — O(n) ──────────
// Use a deque or index-based queue instead
let head = 0;
const queue = [1, 2, 3];
const val = queue[head++];  // O(1) "dequeue" with index!

// ── Math.max/min spread can crash for large arrays ─
// WRONG for large arrays (stack overflow):
// Math.max(...largeArray)
// RIGHT:
const max = largeArray.reduce((a, b) => Math.max(a, b), -Infinity);

// ── Sorting numbers (common gotcha!) ──────────────
[10, 2, 21].sort();             // ❌ ['10','2','21'] lexicographic
[10, 2, 21].sort((a,b) => a-b); // ✅ [2, 10, 21] numeric

// ── Infinity for initial comparison values ────────
let min = Infinity;
let max = -Infinity;

// ── Integer operations ────────────────────────────
Math.floor(n / 2)    // integer division
n >> 1               // same, but bitwise (faster, works for non-negative)
n % 2 === 0          // check even
n & 1                // same, but bitwise

// ── Deep clone (simple) ───────────────────────────
const clone = JSON.parse(JSON.stringify(obj));  // only for JSON-safe data
const clone2 = structuredClone(obj);            // modern, handles more types

// ── Array initialization ──────────────────────────
new Array(n).fill(0)                           // [0,0,...,0]
Array.from({length: n}, (_, i) => i)           // [0,1,2,...,n-1]
Array.from({length: n}, () => [])              // n empty arrays (not aliased!)
// ⚠️ new Array(n).fill([]) — ALL point to SAME array!

// ── Frequency counting shorthand ─────────────────
const freq = {};
arr.forEach(x => freq[x] = (freq[x] || 0) + 1);
```

### Most Common Interview Problems by Pattern

```
Arrays & Hashing:   Two Sum, Group Anagrams, Top K Frequent
Two Pointers:       Valid Palindrome, 3Sum, Container With Most Water
Sliding Window:     Best Time to Buy/Sell, Longest Substring, Min Window
Stack:              Valid Parentheses, Min Stack, Daily Temperatures
Binary Search:      Search in Rotated Array, Find Min in Rotated, Koko Bananas
Linked List:        Reverse, Merge Two Sorted, Reorder, Cycle Detection
Trees:              Invert, Max Depth, Same Tree, Subtree, LCA, Serialize
Tries:              Implement Trie, Word Search II
Heap:               Kth Largest, K Closest Points, Merge K Lists
Backtracking:       Subsets, Combinations, Permutations, N-Queens, Sudoku
Graphs:             Islands, Clone Graph, Course Schedule, Pacific Atlantic
Dynamic Programming:Climbing Stairs, House Robber, Coin Change, LCS, Edit Distance
Greedy:             Jump Game, Merge Intervals, Gas Station, Partition Labels
Bit Manipulation:   Single Number, Missing Number, Counting Bits, Reverse Bits
```

---

## Summary: Choosing the Right Data Structure

| Situation | Use |
|-----------|-----|
| Need fast lookup by key | Hash Map (O(1)) |
| Need sorted data with fast search | BST / AVL Tree (O(log n)) |
| Need max/min quickly | Heap (O(log n) insert, O(1) peek) |
| Need LIFO order | Stack |
| Need FIFO order | Queue |
| Need both ends fast | Deque |
| Prefix matching | Trie |
| Range queries + updates | Segment Tree / Fenwick Tree |
| Connectivity queries | Union-Find |
| Graph problems | Adjacency List |
| Dense graph / matrix | Adjacency Matrix |
| Sequential access, fast insert at head | Linked List |
| Random access, cache-friendly | Array |

---

*Data Structures & Algorithms in JavaScript — Beginner to Super Advanced*

*Master these patterns, understand the tradeoffs, and you'll be ready for any technical interview. 🚀*

---
> **Practice Platforms:** LeetCode • HackerRank • CodeSignal • NeetCode.io
