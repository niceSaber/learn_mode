
## Class类
### 认识Class
```Java
public Class Test{
  Test test = new Test();
}
```
上面这段代码中**test**就是Test这个类的实例对象,Class类是所有类的实例

而Test则是Class的实例对象，有三种表示方式
### 第一种
```Java
Class class = Test.Class
```
### 第二种
```Java
Class class = test.getClass()
```
### 第三种
```Java
Class class = Class.forName("类的路径")   
```
当然这些class是相等的

我们既然可以根据Test获取Class的实例对象，那么也可以反过来,class是那个类的ClassType，

也可以由class推出来这个类不过需要做强制类型转换,如下:
```Java
Test test = (Test)class.newInstance();
```
