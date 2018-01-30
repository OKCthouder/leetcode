###  1. Two Sum

**description:**

Given an array of integers, return **indices** of the two numbers such that they add up to a specific target.

You may assume that each input would have **exactly** one solution, and you may not use the *same* element twice.

**Example:**

```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

**solution**

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        for(int i = 0; i < nums.length; i++){
            for(int j = i + 1; j < nums.length; j++){
                if(nums[i] == target - nums[j]){
                    return new int[] {i,j};
                }
            }
        }
        throw new IllegalArgumentException("No two sum solution");
    }
}
```



-----------------------------------------------------------------------------------------------------------------------------------



### 2.  Add Two Numbers

**description:**

You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse order** and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Example:**

```
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.
```

**solution:**

```java
public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
    ListNode dummyHead = new ListNode(0);
    ListNode p = l1, q = l2, curr = dummyHead;
    int carry = 0;
    while (p != null || q != null) {
        int x = (p != null) ? p.val : 0;
        int y = (q != null) ? q.val : 0;
        int sum = carry + x + y;
        carry = sum / 10;
        curr.next = new ListNode(sum % 10);
        curr = curr.next;
        if (p != null) p = p.next;
        if (q != null) q = q.next;
    }
    if (carry > 0) {
        curr.next = new ListNode(carry);
    }
    return dummyHead.next;
}
```



-----------------------------------------------------------------------------------------------------------------------------------



### 3. Reverse Integer

**description:**

Given a 32-bit signed integer, reverse digits of an integer.

**Example 1:**

```
Input: 123
Output:  321

```

**Example 2:**

```
Input: -123
Output: -321

```

**Example 3:**

```
Input: 120
Output: 21

```

**Note:**
Assume we are dealing with an environment which could only hold integers within the 32-bit signed integer range. For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.



**solution:**

```java
class Solution {
    public int reverse(int x) {
        int result = 0;
        
        while (x != 0){
            int tail = x % 10;
            int newResult = result * 10 + tail;
            if ((newResult - tail) / 10 != result){
                return 0;
            }
            result = newResult;
            x = x / 10;
        }
        
        return result;
    }
}
```



----------------------------------------------------------------------------------------------------------------------------------



### 4. Palindrome Number

**description:**

Determine whether an integer is a palindrome. Do this without extra space.

Some hints:

Could negative integers be palindromes? (ie, -1)

If you are thinking of converting the integer to string, note the restriction of using extra space.

You could also try reversing an integer. However, if you have solved the problem "Reverse Integer", you know that the reversed integer might overflow. How would you handle such case?

There is a more generic way of solving this problem.

**solution:**

```java
class Solution {
    public boolean isPalindrome(int x) {
        if(x < 0 || (x % 10 == 0 && x != 0)) {
            return false;
        }
        
        int revertedNumber = 0;
        while(x > revertedNumber) {
            revertedNumber = revertedNumber * 10 + x % 10;
            x /= 10;
        }
        
        return x == revertedNumber || x == revertedNumber / 10;
    }
}
```





------





### 5. Roman to Integer

**description:**

Given a roman numeral, convert it to an integer.

Input is guaranteed to be within the range from 1 to 3999.

**example:**

罗马数字有如下符号：

| 基本字符    | I    | V    | X    | L    | C    | D    | M    |
| ------- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| 对应阿拉伯数字 | 1    | 5    | 10   | 50   | 100  | 500  | 1000 |

计数规则：

1. 相同的数字连写，所表示的数等于这些数字相加得到的数，例如：III = 3
2. 小的数字在大的数字右边，所表示的数等于这些数字相加得到的数，例如：VIII = 8
3. 小的数字，限于（I、X和C）在大的数字左边，所表示的数等于大数减去小数所得的数，例如：IV = 4
4. 正常使用时，连续的数字重复不得超过三次
5. 在一个数的上面画横线，表示这个数扩大1000倍（本题只考虑3999以内的数，所以用不到这条规则）

其次，罗马数字转阿拉伯数字规则（仅限于3999以内）：

从前向后遍历罗马数字，如果某个数比前一个数小，则加上该数。反之，减去前一个数的两倍然后加上该数



**solution:**

```java
class Solution {
    public int romanToInt(String s) {
        int nums[]=new int[s.length()];
    for(int i=0;i<s.length();i++){
        switch (s.charAt(i)){
            case 'M':
                nums[i] = 1000;
                break;
            case 'D':
                nums[i] = 500;
                break;
            case 'C':
                nums[i] = 100;
                break;
            case 'L':
                nums[i] = 50;
                break;
            case 'X' :
                nums[i] = 10;
                break;
            case 'V':
                nums[i] = 5;
                break;
            case 'I':
                nums[i] = 1;
                break;
        }
    }
    int sum = 0;
    for(int i = 0; i < nums.length - 1; i++){
        if(nums[i] < nums[i + 1])
            sum -= nums[i];
        else
            sum += nums[i];
    }
       return sum + nums[nums.length - 1];
    }
}
```

---



### 6. Longest Common Prefix

**description:**

Write a function to find the longest common prefix string amongst an array of strings.

**solution:**

```java
class Solution {
    public String longestCommonPrefix(String[] strs) {
        if(strs.length == 0) return "";
        String prefix = strs[0];
        for (int i = 1; i < strs.length; i++) {
            // while (strs[i].indexOf(prefix) != 0) {
            //     prefix = prefix.substring(0, prefix.length() - 1);
            //     if (prefix.isEmpty()) return "";
            for (; strs[i].indexOf(prefix) != 0;) {
                prefix = prefix.substring(0, prefix.length() - 1);
                if (prefix.isEmpty()) return "";
               }
            }
      //  }
        return prefix;
    }
}
```



---



### 7.Valid Parentheses

**description:**

Given a string containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

The brackets must close in the correct order, `"()"` and `"()[]{}"` are all valid but `"(]"` and `"([)]"` are not.



**solution:**

```java
class Solution {
    public boolean isValid(String s) {
         if(s == null || "".equals(s.trim())){  
            return false;   
        }  
        char array[] = s.toCharArray();  
        int len = s.length();  
        Stack<Character> stack = new Stack<Character>();  
        for(int i = 0; i < len; i++){  
            if(array[i] == '(' || array[i] == '{' || array[i] == '['){  
                stack.push(array[i]);  
            }else if(array[i] == ')' || array[i] == '}' || array[i] == ']'){  
                if(stack.isEmpty()){  
                    return false;  
                }  
                char c = stack.peek();  
                stack.pop();  
                if(array[i] == ')'){  
                    if(c != '('){  
                        return false;  
                    }  
                }  
                if(array[i] == '}'){  
                    if(c != '{'){  
                        return false;  
                    }  
                }  
                if(array[i] == ']'){  
                    if(c != '['){  
                        return false;  
                    }  
                }  
            }  
        }  
        if(!stack.isEmpty()){  
            return false;  
        }  
        return true;  
    }
}
```



---



### 8. Merge Two Sorted Lists

**description:**

Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.



**Example:**

```
Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4
```



**solution:**

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if (l1 == null) {
            return l2;
        }
        
        if (l2 == null) {
            return l1;
        }
        
        ListNode temp;
        if (l1.val < l2.val) {
            temp = l1;
            temp.next = mergeTwoLists(l1.next, l2);
        }
        
        else  {
            temp = l2;
            temp.next = mergeTwoLists(l1, l2.next);
        }
        return temp;
    }
}
```



---



### 9. Remove Duplicates from Sorted Array

**description:**

Given a sorted array, remove the duplicates [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm) such that each element appear only *once* and return the new length.

Do not allocate extra space for another array, you must do this by **modifying the input array in-place** with O(1) extra memory.

**Example:**

```
Given nums = [1,1,2],

Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively.
It doesn't matter what you leave beyond the new length.
```

**solution:**

```java
class Solution {
    public int removeDuplicates(int[] nums) {
        if (nums.length == 0) return 0;
        int i = 0;
        for (int j = 1; j < nums.length; j++) {
            if (nums[j] != nums[i]) {
                i++;
                nums[i] = nums[j];
            }
        }
        return i + 1;
    }
}
```



---



### 10. Maximum Depth of Binary Tree

**description:**

Given a binary tree, find its maximum depth.

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

**solution:**

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public int maxDepth(TreeNode root) {
        if (root == null) return 0;      
        return 1 + Math.max(maxDepth(root.left), maxDepth(root.right));
    }
}
```

---



### 11. Sqrt(x)

**description:**

Implement `int sqrt(int x)`.

Compute and return the square root of *x*.

**x** is guaranteed to be a non-negative integer.

**Example 1:**

```
Input: 4
Output: 2

```

**Example 2:**

```
Input: 8
Output: 2
Explanation: The square root of 8 is 2.82842..., and since we want to return an integer, the decimal part will be trun
```

**solution:**

```java
class Solution {
    public int mySqrt(int x) {
     long i = 0;  
        long j = x / 2 + 1;  
        while (i <= j) {  
            long mid = (i + j) / 2;  
            if (mid * mid == x)  
                return (int)mid;  
            if (mid * mid < x)  
                i = mid + 1;  
            else  
                j = mid - 1;  
        }  
        return (int)j;  
    }
}
```



---



### 12. Implement strStr()

**description:**

Implement strStr().

Return the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.

**Example 1:**

    Input: haystack = "hello", needle = "ll"
    Output: 2

**Example 2:**

    Input: haystack = "aaaaa", needle = "bba"
    Output: -1

**solution:**
```java
class Solution {
   public int strStr(String haystack, String needle) {
    int l1 = haystack.length(), l2 = needle.length();
    if (l1 < l2) {
        return -1;
    } else if (l2 == 0) {
        return 0;
    }
    int threshold = l1 - l2;
    for (int i = 0; i <= threshold; i++) {
        if (haystack.substring(i, i + l2).equals(needle)) {
            return i;
        }
    }
    return -1;
  }
}
```

---



### 13. Count and say

**description:**

The count-and-say sequence is the sequence of integers with the first five terms as following:

```
1.     1
2.     11
3.     21
4.     1211
5.     111221

```

`1` is read off as `"one 1"` or `11`.
`11` is read off as `"two 1s"` or `21`.
`21` is read off as `"one 2`, then `one 1"` or `1211`.

Given an integer *n*, generate the *n*th term of the count-and-say sequence.

Note: Each term of the sequence of integers will be represented as a string.

**Example 1:**

```
Input: 1
Output: "1"

```

**Example 2:**

```
Input: 4
Output: "1211"
```

**solution:**

```java
class Solution {
    public String countAndSay(int n) {
        if (n == 1) {
            return "1";
        }
        String str = countAndSay(n - 1) + "*";
        char[] c = str.toCharArray();
        int count = 1;
        String s = "";
        for (int i = 0; i < c.length - 1; i++) {
            if(c[i] == c[i+1]) {
                count++;
            } else {
                s = s + count + c[i];
                count = 1;
            } 
        }
        return s;
    }
}
```



---



### 14. Symmetric Tree 

**description:**

Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).

For example, this binary tree `[1,2,2,3,4,4,3]` is symmetric:

```
    1
   / \
  2   2
 / \ / \
3  4 4  3

```

But the following `[1,2,2,null,3,null,3]` is not:

```
    1
   / \
  2   2
   \   \
   3    3

```

**Note:**
Bonus points if you could solve it both recursively and iteratively.

**solution:**

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public boolean isSymmetric(TreeNode root) {
        return isMirror(root, root);
    }
    
    public boolean isMirror(TreeNode t1, TreeNode t2) {
        if (t1 == null && t2 == null) {
            return true;
        }
        if (t1 == null || t2 == null) {
            return false;
        }
        return (t1.val == t2.val) 
            && isMirror(t1.right, t2.left) 
            && isMirror(t1.left, t2.right);
    }
}
```



---



### 15. Merge Sorted Array

**description:**

Given two sorted integer arrays *nums1* and *nums2*, merge *nums2* into *nums1* as one sorted array.

**Note:**
You may assume that *nums1* has enough space (size that is greater or equal to *m* + *n*) to hold additional elements from *nums2*. The number of elements initialized in *nums1* and *nums2* are *m* and *n* respectively.

**solution:**

```java
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        while (n > 0) nums1[m+n-1] = (m == 0) || nums2[n - 1] > nums1[m - 1] ? nums2[--n] : nums1[--m];
    }
}
```



---



### 16. Maxium Subarray

**description:**

Find the contiguous subarray within an array (containing at least one number) which has the largest sum.

For example, given the array `[-2,1,-3,4,-1,2,1,-5,4]`,
the contiguous subarray `[4,-1,2,1]` has the largest sum = `6`.

**solution:**

```java
class Solution {
    public int maxSubArray(int[] nums) {
        int maxSoFar = nums[0], maxEndingHere = nums[0];
        for (int i = 1; i < nums.length; ++i) {
            maxEndingHere = Math.max(maxEndingHere + nums[i], nums[i]);
            maxSoFar = Math.max(maxSoFar, maxEndingHere);
        }
        return maxSoFar;
    }
}
```

---



### 17. Plus One

**description:**

Given a non-negative integer represented as a **non-empty** array of digits, plus one to the integer.

You may assume the integer do not contain any leading zero, except the number 0 itself.

The digits are stored such that the most significant digit is at the head of the list.

**solution:**

```java
class Solution {
    public int[] plusOne(int[] digits) {
        int n = digits.length;
        for (int i = n - 1; i >= 0; i--) {
            if (digits[i] < 9) {
                digits[i]++;
                return digits;
            }
            
            digits[i] = 0;
        }
        
        int[] newNumber = new int[n + 1];
        newNumber[0] = 1;
        
        return newNumber;
    }
}
```



---



### 18.Climbing Stairs

**description:**

You are climbing a stair case. It takes *n* steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

**Note:** Given *n* will be a positive integer.

**Example 1:**

```
Input: 2
Output:  2
Explanation:  There are two ways to climb to the top.

1. 1 step + 1 step
2. 2 steps

```

**Example 2:**

```
Input: 3
Output:  3
Explanation:  There are three ways to climb to the top.

1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step
```

**solution:**

```java
class Solution {
    public int climbStairs(int n) {
        if (n == 1) {
            return 1;
        }
        int[] dp = new int[n + 1];
        dp[1] = 1;
        dp[2] = 2;
        for (int i = 3; i <= n; i++) {
            dp[i] = dp[i - 2] + dp[i - 1];
        }
        return dp[n];
    }
}
```

---



### 19. Convert Sorted Array to Binary Search Tree

**description:**

Given an array where elements are sorted in ascending order, convert it to a height balanced BST.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of *every* node never differ by more than 1.

**Example:**

```
Given the sorted array: [-10,-3,0,5,9],

One possible answer is: [0,-3,9,-10,null,5], which represents the following height balanced BST:

      0
     / \
   -3   9
   /   /
 -10  5
```

**solution:**

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def sortedArrayToBST(self, nums):
        """
        :type nums: List[int]
        :rtype: TreeNode
        """
        if not nums:
            return None
    
        mid = len(nums) // 2
        
        root = TreeNode(nums[mid])
        root.left = self.sortedArrayToBST(nums[:mid])
        root.right = self.sortedArrayToBST(nums[mid + 1:])
        
        return root
```



---



### 20.Pascal's Triangle

**description:**

Given *numRows*, generate the first *numRows* of Pascal's triangle.

```

```

For example, given *numRows* = 5,
Return

```
[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]
```

**solution:**

```python
class Solution:
    def generate(self, numRows):
        """
        :type numRows: int
        :rtype: List[List[int]]
        """
        triangle = []
        
        for row_num in range(numRows):
            row = [None for _ in range(row_num + 1)]
           # row = []
		  # for _ in range(row_num + 1):
   		  #  row += [None]
            row[0] = 1
            row[-1] = 1
        
            for j in range(1, len(row) - 1):
                   row[j] = triangle[row_num - 1][j - 1] + triangle[row_num - 1][j]
                   
            triangle.append(row)
                   
        return triangle
```



---



### 21.Valid Palindrome

**description:**

Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

For example,
`"A man, a plan, a canal: Panama"` is a palindrome.
`"race a car"` is *not* a palindrome.

**Note:**
Have you consider that the string might be empty? This is a good question to ask during an interview.

For the purpose of this problem, we define empty string as valid palindrome.

**solution:**

```python
class Solution:
    def isPalindrome(self, s):
        """
        :type s: str
        :rtype: bool
        """
        l, r = 0, len(s) - 1
        while l < r:
            while l < r and not s[l].isalnum():
                l += 1
            while l < r and not s[r].isalnum():
                r -= 1
            if s[l].lower() != s[r].lower():
                return False
            l += 1
            r -= 1
        return True
```

---



### 22. Single Number

**description:**

Given an array of integers, every element appears *twice* except for one. Find that single one.

**Note:**
Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

**solutions:**

```python
class Solution:
    def singleNumber(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        return 2 * sum(set(nums)) - sum(nums)
    
  #  int result = 0;
  #  for (int i = 0; i<n; i++)
  #   {
  #      result ^=A[i];
  #  }
  #  return result;
```



---

### 23. Linked List Cycle

**description:**

Given a linked list, determine if it has a cycle in it.

Follow up:
Can you solve it without using extra space?

**solution:**

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def hasCycle(self, head):
        """
        :type head: ListNode
        :rtype: bool
        """
        try:
            slow = head
            fast = head.next
            while slow is not fast:
                slow = slow.next
                fast = fast.next.next
            return True
        except:
            return False
```

---



### 24. Min Stack

**description:**

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

- push(x) -- Push element x onto stack.
- pop() -- Removes the element on top of the stack.
- top() -- Get the top element.
- getMin() -- Retrieve the minimum element in the stack.

**Example:**

```java
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --> Returns -3.
minStack.pop();
minStack.top();      --> Returns 0.
minStack.getMin();   --> Returns -2.
```

**solution:**

```java
public class MinStack {
    
    Stack<Integer> stackNum = new Stack<Integer>();
    Stack<Integer> stackMin = new Stack<Integer>();
    
    public void push(int x) {
        stackNum.push(x);
        if(stackMin.isEmpty() || stackMin.peek() >= x) {
            stackMin.push(x);
        }
    }

    public void pop() {
        int top = stackNum.pop();
        if(top <= stackMin.peek()) {
            stackMin.pop();
        }
    }

    public int top() {
        return stackNum.peek();
    }

    public int getMin() {
        return stackMin.peek();
    }
}
```



---



###  25. Intersection of Two Linked Lists

**description:**

Write a program to find the node at which the intersection of two singly linked lists begins.

For example, the following two linked lists:

```
A:          a1 → a2
                   ↘
                     c1 → c2 → c3
                   ↗            
B:     b1 → b2 → b3

```

begin to intersect at node c1.

**Notes:**

- If the two linked lists have no intersection at all, return `null`.
- The linked lists must retain their original structure after the function returns.
- You may assume there are no cycles anywhere in the entire linked structure.
- Your code should preferably run in O(n) time and use only O(1) memory.

**solution:**

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        if (headA == null || headB == null) return null;
        
        ListNode a = headA;
        ListNode b = headB;
        
        while (a != b) {
            a = a == null? headB : a.next;
            b = b == null? headA : b.next;
        }
        return a;
    }
}
```



---



### 26. Best Time to Buy and Sell Stock

**description:**

Say you have an array for which the *i*th element is the price of a given stock on day *i*.

If you were only permitted to complete at most one transaction (ie, buy one and sell one share of the stock), design an algorithm to find the maximum profit.

**Example 1:**

```
Input: [7, 1, 5, 3, 6, 4]
Output: 5

max. difference = 6-1 = 5 (not 7-1 = 6, as selling price needs to be larger than buying price)

```

**Example 2:**

```
Input: [7, 6, 4, 3, 1]
Output: 0

In this case, no transaction is done, i.e. max profit = 0.
```

**solution:**

```python
class Solution:
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        min = float('inf')
        profit = 0
        
        for price in prices:
            if min > price:
                min = price
            else:
                if profit < price - min:
                    profit = price - min
        
        return profit
    
  #  def maxProfit(prices):
  #     max_profit, min_price = 0, float('inf')
  #     for price in prices:
  #        min_price = min(min_price, price)
  #        profit = price - min_price
  #        max_profit = max(max_profit, profit)
  #     return max_profit
```



---



### 27. Best Time to Buy and Sell Stock II

**description:**

Say you have an array for which the *i*th element is the price of a given stock on day *i*.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like (ie, buy one and sell one share of the stock multiple times). However, you may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).

**solution:**

```python
class Solution:
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        return sum(max(prices[i + 1] - prices[i], 0) for i in range(len(prices) - 1))
```



----



### 28. Majority Element

**description:**

Given an array of size *n*, find the majority element. The majority element is the element that appears **more than** `⌊ n/2 ⌋` times.

You may assume that the array is non-empty and the majority element always exist in the array.

**Credits:**
Special thanks to [@ts](https://oj.leetcode.com/discuss/user/ts) for adding this problem and creating all test cases.

**solution:**

```python
class Solution:
    def majorityElement(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        nums.sort()
        return nums[len(nums)//2]        
```



---



### 29. Excel Sheet Column Number

**description:**

Related to question [Excel Sheet Column Title](https://leetcode.com/problems/excel-sheet-column-title/)

Given a column title as appear in an Excel sheet, return its corresponding column number.

For example:

```
    A -> 1
    B -> 2
    C -> 3
    ...
    Z -> 26
    AA -> 27
    AB -> 28 
```

**Credits:**
Special thanks to [@ts](https://leetcode.com/discuss/user/ts) for adding this problem and creating all test cases.

**solution:**

```python
class Solution:
    def titleToNumber(self, s):
        """
        :type s: str
        :rtype: int
        """
        s = s[::-1]
        sum = 0
        for exp, char in enumerate(s):
            sum += (ord(char) - 65 + 1) * (26 ** exp)
        return sum
```



---



### 30. Factorial Trailing Zeroes

**description:**

Given an integer *n*, return the number of trailing zeroes in *n*!.

**Note: **Your solution should be in logarithmic time complexity.

**solution:**

```python
class Solution(object):
    def trailingZeroes(self, n):
        """
        :type n: int
        :rtype: int
        """
        r = 0
        while n > 0:
            n /= 5
            r += n
        return r
```



---



### 31. Number of 1 Bits

**description:**

Write a function that takes an unsigned integer and returns the number of ’1' bits it has (also known as the [Hamming weight](http://en.wikipedia.org/wiki/Hamming_weight)).

For example, the 32-bit integer ’11' has binary representation `00000000000000000000000000001011`, so the function should return 3.

```python
class Solution(object):
    def hammingWeight(self, n):
        """
        :type n: int
        :rtype: int
        """
        return bin(n).count('1')

        # c = 0
        # while n:
        #   n &= n - 1
        #   c += 1
        # return c
```



---



### 32. Rotate Array

**description:**

Rotate an array of *n* elements to the right by *k* steps.

For example, with *n* = 7 and *k* = 3, the array `[1,2,3,4,5,6,7]` is rotated to `[5,6,7,1,2,3,4]`.

**Note:**
Try to come up as many solutions as you can, there are at least 3 different ways to solve this problem.

**solution:**

```java
class Solution {
    public void rotate(int[] nums, int k) {
        k = k % nums.length;
        reverse(nums, 0, nums.length - 1);
        reverse(nums, 0, k - 1);
        reverse(nums, k, nums.length - 1);
    }
    
    public void reverse(int[] nums, int start, int end) {
        while (start < end) {
            int temp = nums[start];
            nums[start] = nums[end];
            nums[end] = temp;
            start++;
            end--;
        }
    }
}
```



---



### 33. Reverse Bits

**description:**

Reverse bits of a given 32 bits unsigned integer.

For example, given input 43261596 (represented in binary as **00000010100101000001111010011100**), return 964176192 (represented in binary as **00111001011110000010100101000000**).

**solution:**

```java
public class Solution {
    // you need treat n as an unsigned value
    public int reverseBits(int n) {
        if(n == 0)
            return 0;
        int result = 0;
        for(int i = 0; i < 32; i++) {
            result <<= 1;
            if ((n & 1) == 1) result++;
            n >>= 1;
        }
        return result;
    }
}
```



---



### 34. House Robber

**description:**

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and **it will automatically contact the police if two adjacent houses were broken into on the same night**.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight **without alerting the police**.

**solution:**

```java
class Solution {
    public int rob(int[] nums) {
        if (nums.length == 0) return 0;
        if (nums.length == 1) return nums[0];
        
        int[] mark = new int[nums.length];
        mark[0] = nums[0];
        mark[1] = Math.max(nums[0], nums[1]);
        
        for (int i = 2; i < nums.length; i++) {
            mark[i] = Math.max(nums[i] + mark[i-2], mark[i - 1]);
        }
        return mark[nums.length - 1];
    }
}
```



---



### 35. Happy Number

**description:**

Write an algorithm to determine if a number is "happy".

A happy number is a number defined by the following process: Starting with any positive integer, replace the number by the sum of the squares of its digits, and repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1. Those numbers for which this process ends in 1 are happy numbers.

**Example: **19 is a happy number

- 12 + 92 = 82
- 82 + 22 = 68
- 62 + 82 = 100
- 12 + 02 + 02 = 1

**solution:**

```java
class Solution {
public boolean isHappy(int n) {
        Set<Integer> s = new HashSet<Integer>();
        while (n != 1) {
            int t = 0;
            while (n != 0) {
                t += (n % 10) * (n % 10);
                n /= 10;
            }
            n = t;
            if (s.contains(n)) break;
            else s.add(n);
        }
        return n == 1;
    }
}
```



---



### 36. Count Primes

**description:**

**Description:**

Count the number of prime numbers less than a non-negative number, **n**.

**solution:**

```java
class Solution {
    public int countPrimes(int n) {
        boolean[] notPrime = new boolean[n];
        int count = 0;
        for (int i = 2; i < n; i++) {
            if (notPrime[i] == false) {
                count++;
            }
            for (int j = 2; i * j < n; j++) {
                notPrime[i*j] = true;
            }
        }
        return count;
    }
}
```



---



### 37. Reverse Linked List

**description:**

Reverse a singly linked list.

**solution:**

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode reverseList(ListNode head) {
    // is there something to reverse?
    if (head != null && head.next != null)
    {
        ListNode pivot = head;
        ListNode frontier = null;
        while (pivot != null && pivot.next != null)
        {
            frontier = pivot.next;
            pivot.next = pivot.next.next;
            frontier.next = head;
            head = frontier;
        }
    }
    
    return head;
 }
}
```



---



### 38. Contains Duplicate

**description:**

Given an array of integers, find if the array contains any duplicates. Your function should return true if any value appears at least twice in the array, and it should return false if every element is distinct.

**solution:**

```java
class Solution {
    public boolean containsDuplicate(int[] nums) {
        Set<Integer> set = new HashSet<Integer>();
        for (int i = 0; i < nums.length; i++) {
            if (set.contains(nums[i])) return true;
            set.add(nums[i]);
        }
        return false;
    }
}
```



---



### 39. Delete Node in a Linked List

**description:**

Write a function to delete a node (except the tail) in a singly linked list, given only access to that node.

Supposed the linked list is `1 -> 2 -> 3 -> 4` and you are given the third node with value `3`, the linked list should become `1 -> 2 -> 4` after calling your function.

**solution:**

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public void deleteNode(ListNode node) {
        node.val = node.next.val;
        node.next = node.next.next;
    }
}
```



---



### 40. Valid Anagram

**description:**

Given two strings *s* and *t*, write a function to determine if *t* is an anagram of *s*.

For example,
*s* = "anagram", *t* = "nagaram", return true.
*s* = "rat", *t* = "car", return false.

**Note:**
You may assume the string contains only lowercase alphabets.

**Follow up:**
What if the inputs contain unicode characters? How would you adapt your solution to such case?

**solution:**

```java
class Solution {
    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) {
            return false;
        }
        char[] str1 = s.toCharArray();
        char[] str2 = t.toCharArray();
        Arrays.sort(str1);
        Arrays.sort(str2);
        return Arrays.equals(str1, str2);
    }
}
```



---



### 41. Missing Number

**description:**

Given an array containing *n* distinct numbers taken from `0, 1, 2, ..., n`, find the one that is missing from the array.

**Example 1**

```
Input: [3,0,1]
Output: 2
```

**Example 2**

```
Input: [9,6,4,2,3,5,7,0,1]
Output: 8
```

**Note**:
Your algorithm should run in linear runtime complexity. Could you implement it using only constant extra space complexity?

**solution:**

```java
class Solution {
    public int missingNumber(int[] nums) {
        Set<Integer> numSet = new HashSet<Integer>();
        for (int num : nums) numSet.add(num);
        
        int expectedNumCount = nums.length + 1;
        for (int number = 0; number < expectedNumCount; number++) {
            if (!numSet.contains(number)) {
                return number;
            }
        }
        return -1;
    }
}
```



---



### 42. Move Zeroes

**description:**

Given an array `nums`, write a function to move all `0`'s to the end of it while maintaining the relative order of the non-zero elements.

For example, given `nums = [0, 1, 0, 3, 12]`, after calling your function, `nums` should be `[1, 3, 12, 0, 0]`.

**Note**:

1. You must do this **in-place** without making a copy of the array.
2. Minimize the total number of operations.

**solution:**

```java
class Solution {
    public void moveZeroes(int[] nums) {
        if (nums == null || nums.length ==0) return;
        
        int insertPos = 0;
        for (int num: nums) {
            if(num != 0) nums[insertPos++] = num;
        }
        
        while (insertPos < nums.length) {
            nums[insertPos++] = 0;
        }
    }
}
```



---



### 43. Power of Three

**description:**

Given an integer, write a function to determine if it is a power of three.

**Follow up:**
Could you do it without using any loop / recursion?

**solution:**

```java
class Solution {
    public boolean isPowerOfThree(int n) {
        if (n < 1) return false;
        
        while (n % 3 == 0) {
            n /= 3;
        }
        
        return n == 1;
    }
}
```

