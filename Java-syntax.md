# Java Syntax Refresher for DSA 🔄

Smart choice. A shaky Java foundation will slow you down mid-problem. Let's rebuild the exact Java knowledge you *need* for LeetCode — nothing more, nothing less.

---

# The 6 Pillars of Java You Need for DSA

## Pillar 1 — Data Types & Variables

These are the types you'll use in 95% of LeetCode problems:

```java
// The Big 4 primitives
int n = 10;           // whole numbers — your default choice
long big = 10_000_000_000L;  // when int overflows (> 2.1 billion)
double d = 3.14;      // decimals (rare in DSA)
boolean flag = true;  // true/false conditions

// The wrapper — used in Collections (HashMap, ArrayList, etc.)
Integer x = null;     // can be null, unlike int

// Char — crucial for string problems
char c = 'A';
int ascii = (int) 'A';   // → 65  (casting trick you'll use often)
char back = (char) 65;   // → 'A'

// Key trick: character arithmetic
char ch = 'e';
int pos = ch - 'a';   // → 4  (position in alphabet, 0-indexed)
                      // You'll use this constantly in string problems
```

> 🧠 **Mentor tip:** The `ch - 'a'` trick is used in at least 1 out of every 3 string problems on LeetCode. Burn it into memory.

---

## Pillar 2 — Arrays (Your Most-Used Structure)

```java
// Declaration and initialization
int[] arr = new int[5];           // [0, 0, 0, 0, 0] — default zeros
int[] arr2 = {1, 2, 3, 4, 5};    // direct initialization

// 2D array (grids, matrices)
int[][] grid = new int[3][4];     // 3 rows, 4 columns
int[][] grid2 = {{1,2},{3,4}};    // direct init

// Essential operations
int len = arr.length;             // NO parentheses — it's a field, not method
int last = arr[arr.length - 1];   // last element

// Looping — two styles you'll use constantly
for (int i = 0; i < arr.length; i++) {
    System.out.println(arr[i]);   // index-based (use when you need i)
}
for (int val : arr) {
    System.out.println(val);      // enhanced for-each (cleaner, no index)
}

// Sorting — built-in, O(n log n)
Arrays.sort(arr);                 // ascending
// For descending, you need Integer[] not int[]
Integer[] arr3 = {5, 3, 1, 4};
Arrays.sort(arr3, (a, b) -> b - a);   // descending with lambda

// Copying
int[] copy = Arrays.copyOf(arr, arr.length);
int[] partial = Arrays.copyOfRange(arr, 1, 4); // indices 1,2,3

// Filling
Arrays.fill(arr, 0);  // set all elements to 0

// Import needed:
import java.util.Arrays;
```

---

## Pillar 3 — Strings (Tricky in Java)

```java
// The most important thing to know: Strings are IMMUTABLE in Java
// Every modification creates a NEW string — expensive in loops!

String s = "hello";
int len = s.length();           // parentheses here — it IS a method
char c = s.charAt(2);           // → 'l'
String sub = s.substring(1, 4); // → "ell" (start inclusive, end exclusive)
int idx = s.indexOf('l');       // → 2 (first occurrence)
boolean has = s.contains("ell");// → true
String up = s.toUpperCase();
String lo = s.toLowerCase();
char[] chars = s.toCharArray(); // → ['h','e','l','l','o'] ← USE THIS A LOT
String back = new String(chars);// char array back to String

// Comparison — NEVER use == for Strings
s.equals("hello");      // ✅ correct
s == "hello";           // ❌ wrong (compares references, not content)
s.equalsIgnoreCase("HELLO"); // case-insensitive compare

// StringBuilder — use this instead of String concatenation in loops
StringBuilder sb = new StringBuilder();
sb.append("hello");
sb.append(' ');
sb.append("world");
sb.reverse();                   // reverses in-place
sb.deleteCharAt(0);             // remove character at index
String result = sb.toString();  // convert back when done

// Why StringBuilder? 
// String concatenation in a loop = O(n²) time
// StringBuilder in a loop      = O(n) time  ← always prefer this
```

---

## Pillar 4 — The Collections You'll Use (Big 4)

```java
import java.util.*;

// ── 1. ArrayList — dynamic array ──────────────────────────
List<Integer> list = new ArrayList<>();
list.add(5);                    // add to end
list.add(0, 10);                // add at index 0
list.get(1);                    // access by index → 5
list.remove(Integer.valueOf(5));// remove by VALUE
list.remove(0);                 // remove by INDEX
list.size();                    // length
Collections.sort(list);         // sort

// ── 2. HashMap — key-value store ──────────────────────────
Map<String, Integer> map = new HashMap<>();
map.put("apple", 3);
map.get("apple");               // → 3
map.getOrDefault("banana", 0);  // → 0 if key missing ← use this often!
map.containsKey("apple");       // → true
map.remove("apple");
map.size();

// Iterating a map
for (Map.Entry<String, Integer> entry : map.entrySet()) {
    String key = entry.getKey();
    int val = entry.getValue();
}

// ── 3. HashSet — unique values only ───────────────────────
Set<Integer> set = new HashSet<>();
set.add(5);
set.contains(5);                // O(1) lookup ← faster than list!
set.remove(5);
set.size();

// ── 4. Stack / Deque ──────────────────────────────────────
// In Java, use Deque as a Stack (Stack class is legacy/slow)
Deque<Integer> stack = new ArrayDeque<>();
stack.push(1);                  // push to top
stack.pop();                    // remove from top
stack.peek();                   // view top without removing

// As a Queue (FIFO)
Deque<Integer> queue = new ArrayDeque<>();
queue.offer(1);                 // add to back
queue.poll();                   // remove from front
queue.peek();                   // view front

// Priority Queue (Min-Heap by default)
PriorityQueue<Integer> minHeap = new PriorityQueue<>();
PriorityQueue<Integer> maxHeap = new PriorityQueue<>((a, b) -> b - a);
minHeap.offer(5);
minHeap.poll();                 // always removes the SMALLEST
```

---

## Pillar 5 — Control Flow & Java Tricks

```java
// Ternary — clean one-liners
int max = (a > b) ? a : b;

// Integer limits — use these to avoid hardcoding
int max_val = Integer.MAX_VALUE;  // 2,147,483,647
int min_val = Integer.MIN_VALUE;  // -2,147,483,648

// Modulo — useful for circular indexing
int next = (i + 1) % n;          // wraps around

// Math utilities
Math.max(a, b);
Math.min(a, b);
Math.abs(-5);                     // → 5
Math.pow(2, 10);                  // → 1024.0 (returns double)
(int) Math.pow(2, 10);            // → 1024 (cast to int)
Math.sqrt(16);                    // → 4.0

// Null check pattern
if (node != null && node.val > 0) { ... }  // short-circuit evaluation
```

---

## Pillar 6 — Writing Clean LeetCode Methods

Every LeetCode problem gives you a method signature. Here's how they look and how to think about them:

```java
// Typical LeetCode structure — you only write the method body
class Solution {

    // Example: Two Sum problem signature
    public int[] twoSum(int[] nums, int target) {
        // your logic here
        return new int[]{0, 1}; // return format
    }

    // Returning -1 as "not found" sentinel
    public int search(int[] nums, int target) {
        // ...
        return -1; // convention when answer doesn't exist
    }

    // Boolean problems
    public boolean isValid(String s) {
        // ...
        return true;
    }
}

// Inner classes you'll define for Linked List / Tree problems
class ListNode {
    int val;
    ListNode next;
    ListNode(int val) { this.val = val; }
}

class TreeNode {
    int val;
    TreeNode left, right;
    TreeNode(int val) { this.val = val; }
}
```

---

# Quick Self-Check ✅

Before we move to DSA, let me test if the syntax clicked:

**Mental exercise — don't run it, just think:**

```java
String s = "abcde";
char[] chars = s.toCharArray();
chars[0] = 'z';
System.out.println(new String(chars));  // What prints?

int[] arr = {3, 1, 4, 1, 5};
Arrays.sort(arr);
System.out.println(arr[0] + " " + arr[4]);  // What prints?

Map<String, Integer> map = new HashMap<>();
map.put("a", 1);
map.put("b", 2);
System.out.println(map.getOrDefault("c", 99));  // What prints?
```Answer all three — then I'll explain each one and we jump straight into **Phase 1, Lesson 1: Two Pointers**. 🚀