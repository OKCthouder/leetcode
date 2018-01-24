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



### 15. Merge Sorted Array

**description:**

Given two sorted integer arrays *nums1* and *nums2*, merge *nums2* into *nums1* as one sorted array.

**Note:**
You may assume that *nums1* has enough space (size that is greater or equal to *m* + *n*) to hold additional elements from *nums2*. The number of elements initialized in *nums1* and *nums2* are *m* and *n* respectively.

**solution:**

