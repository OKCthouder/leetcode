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