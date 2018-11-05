
### Lambda

#### 基本操作
**实例化接口**：
实例化的接口需要满足单方法实现，即一个接口内只能有一个需要实现的方法。在 JDK8 中函数接口提供了 `@FunctionalInterface` 注解来进行编译检查。（单一职责）
```Java
public class lambda {
  @FunctionalInterface
	interface IDemo {
		int getSum(int a, int b);
	}

	public static void main(String[] args) {

		IDemo d1 = (a, b) -> a + b; // 如果是单个参数可以不加括号
		IDemo d2 = (int a, int b) -> a + b;
		IDemo d3 = (a, b) -> {
			System.out.println("多行处理");
			return a + b;
		};

		System.out.println(d1.getSum(1, 2));
		System.out.println(d2.getSum(1, 2));
		System.out.println(d3.getSum(1, 2));

	}
}
```
*****
##### 接口默认实现方法 since JDK1.8
```Java
interface IDemo {
  int getSum(int a, int b);
  default int doubleValue(int i) {
    return i * 2;
  }
}
```
在这个接口中，可以使用 default 来将方法在接口文件内实现，这样做的好处是可以使用 lambda(操作非 default 修饰的方法)，
****
### 函数接口
例：将输入的 int 类型格式化成 String 并输出

旧的写法
```Java
import java.text.DecimalFormat;

public class Functional {

	public static void main(String[] args) {
		Handler h = new Handler(1234);
		h.printInfo(i -> new DecimalFormat("#,###").format(i));
	}

}

interface IChangeType {
	String format(int val);// int转 String
}

class Handler {
	private final int val;

	public Handler(int val) {
		this.val = val;
	}

	public void printInfo(IChangeType changeType) {
		System.out.println("转换后：" + changeType.format(this.val));
	}
}
```
新的写法：
```java
import java.text.DecimalFormat;
import java.util.function.Function;

public class Functional {

	public static void main(String[] args) {
		Handler h = new Handler(1234);
		h.printInfo(i -> new DecimalFormat("#,###").format(i));
	}

}
//去掉了 接口
class Handler {
	private final int val;

	public Handler(int val) {
		this.val = val;
	}

	public void printInfo(Function<Integer,String> changeType) {
		System.out.println("转换后：" + changeType.apply(this.val));//使用 apply进行接收
	}
}
```
lambda 并不关心它实现的是哪个方法，它只关心入参和输出，所以就有了 JDK8 的 Function<args_in,args_out>

lambda 还允许通过函数接口链式操作：
```Java
public static void main(String[] args) {
  Handler h = new Handler(1234);
  Function<Integer, String> changeType = i -> new DecimalFormat("#,###").format(i);
  h.printInfo(changeType.andThen(str -> "价格：￥" + str));//输入一个 String,输出一个 String

}
```
****
### Stream API
Stream 是类似于 Pipeline 的东西，它不属于数据结构之类的，而是像流水线似的堆数据处理的工具。
```Java
    //求和
		int[] nums = {1,2,3};
		int sum = 0;
		for(int num : nums) {
			sum += num;
		}
		System.out.println("外部迭代： " + sum);//外部迭代： 6

		int sum1 = IntStream.of(nums).sum();
		System.out.println("Stream内部迭代： " + sum1);//内部迭代： 6
```
