
- =号，在Java里面不是比较，=号叫做赋值符号， =号左边必须是变量. 例子，设x=1

```java
int a = 1;
```

- equals是比较两个对象的值是否相等，而==比较两个值得同时还比较他们的address

Java 里面所有primitive non-primitive data types会保存在同一个address。

Primitive data types - includes byte, short, int, long, float, double, boolean and char ,String,

Non-primitive data types - such as Arrays, list and Classes

```java
public class equalsCompare {
	 public static void main(String[] args) {
			int a = 1;
			int b = 2;
			float c = 1;
			String d = "1";
			String e = "1";
			int[] x = {1,2};
			int[] y = {1,2};
	    }
}

// a == c true, 因为float 赋值为整数时和int 相同, 在同一个地址
// a == d false, 因为类型都不同，地址不同
// d == e true, primitive data type, 在同一个地址
// x == y false, non-primitive data types,地址不同
```java
