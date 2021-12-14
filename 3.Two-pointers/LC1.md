1. Two Sum

Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.

Example 1:

Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Output: Because nums[0] + nums[1] == 9, we return [0, 1].

## 思路

双指针，时间复杂度是n^2
HashMap time complexity 是n



代码如下：

```java

class Solution {
  public int[] twoSum(int[] nums, int target) {

      for (int i = 0; i <= nums.length, i++) {
          for (int j = i + 1; j < nums.length; j++)
          // if (nums[i] = tartget - nums[j]) 这里必须要双等号。
              if (nums[i] ==  target - nums[j]) {
              return new int[] {i,j};
          }
      }
      return null;
      // java 在最外层一定要有一行return
  }
}
```



## 总结Conclusion

- =号，在Java里面不是比较，=号叫做赋值符号， =号左边必须是变量
- equals是比较两个对象的值是否相等，而==比较两个值得同时还比较他们的address

Java 里面所有primitive non-primitive data types会保存在同一个address。

Primitive data types - includes byte, short, int, long, float, double, boolean and char ,String,

Non-primitive data types - such as Arrays, list and Classes
```
public class equalsCompare {
	 public static void main(String[] args) {
			int a = 1;
			int b = 2;
			float c = 1;
			String d = "1";
			String e = "cv1";
			int[] x = {1,2};
			int[] y = {1,2};
	    }
}

// a == c true, 因为float 赋值为整数时和int 相同, 在同一个地址
// a == d false, 因为类型都不同，地址不同
// d == e true, primitive data type, 在同一个地址
// x == y false, non-primitive data types,地址不同
```java
