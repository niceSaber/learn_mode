# 单例模式
## 懒汉式
```Java
public class Test {
	private static Test test;
	private Test(){}
	public static Test getTest(){
		if(test == null){
			test = new Test();
		}
		return test;
	}
}
``` 
以上是最简单的单例模式，但对于多线程而言并不是很安全，因为多线程同时调用getTest()方法时有可能会导致同时创建多个实例。是程序不能工作。
## 懒汉式(多线程)
```Java
public class Test {
	private static Test test;
	private Test(){}
	public static synchronized Test getTest(){
		if(test == null){
			test = new Test();
		}
		return test;
	}
}
```
就是给整个 getTest() 方法设为同步（synchronized）。但是这个方法并不高效,太耗时，每个线程访问getTest()时都会排队，但是对于我们来说只需要这个同步方法执行一次即可，
因此该方法不可取
## 双重检查加锁(多线程且高效)
```Java
public class Test {
	private static Test test;
	private Test(){}
	public static  Test getTest(){
		if(test == null){
			synchronized (Test.class) {
				if(test == null){
					test = new Test();
				}
			}
		}
		return test;
	}
}
```
这个是只给需要的方法添加同步块，在同步块执行前检查一次，执行后再检查一次，就是双重检查，其中**synchronized (Test.class)**代表给Test这个类加锁，只要
第一次执行完之后，就不会再执行这个方法了，因为即使在多线程情况下，第一个线程已经执行了里面的 ，其他线程在这个线程未执行完之前是不会访问这个Test的，因为
Test被加锁了.
但是这段代码看起来很完美，很可惜，它是有问题。主要在于instance = new Singleton()这句，这并非是一个原子操作，事实上在 JVM 中这句话大概做了下面 3 件事情。
1. 给 instance 分配内存
2. 调用 Singleton 的构造函数来初始化成员变量
3. 将instance对象指向分配的内存空间（执行完这步 instance 就为非 null 了) 

JVM 的即时编译器中存在指令重排序的优化。也就是说上面的第二步和第三步的顺序是不能保证的，最终的执行顺序可能是 1-2-3 也可能是 1-3-2。如果是后者，则在 3 执行完毕、2 未执行之前，被线程二抢占了，这时 instance 已经是非 null 了（但却没有初始化），所以线程二会直接返回 instance，然后使用，然后顺理成章地报错。
我们只需要将 instance 变量声明成 volatile 就可以了。
```Java
public class Test {
	private volatile static  Test test ;
	private Test(){}
	public static  Test getTest(){
		if(test == null){
			synchronized (Test.class) {
				if(test == null){
					test = new Test();
				}
			}
		}
		return test;
	}
}

```
## 饿汉式
```Java
public class Test {
	private static Test test =new Test();
	private Test(){}
	public static  Test getTest(){
		return test;
	}
}
```
优点：没有加锁，执行效率会提高。
缺点：类加载时就初始化，浪费内存。

## 枚举
明天再说
