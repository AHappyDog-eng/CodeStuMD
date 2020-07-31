## java反射

通过反射可以直接获任何任意对象的成员变量，成员方法，成员参数等，并且可以通过java反射的机制来进行对对象的创建等基本的操作

并且可以调用任何类的类成员方法，并且调用任何类的类成员变量 包括成员方法，并且包含成员私有参数，并且可以直接更改对象参数等基本操作

### 获取 java Class的对象方法

```
大分三种 比如有一个测试类 TestA 为测试类

TestA.class

Class.forName("TestA"); 通过类的全限定类名来获取他们的反射对象

classLoader.classloader("类的全限定类名") eg： com.anheng.demo.testA

```

