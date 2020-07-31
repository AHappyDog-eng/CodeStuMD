### JIN Java interface Native（eg： UnSafe）



### JAVA 序列化和反序列化

通过实体类继承io.Serializable 就是java序列化操作

序列化不用调用原有类的constructor（反射构造方法对象） 构造方法

```
1 通过一个超类
ReflectionFactory factory = ReflectionFactory.getReflectionFactory 获取反射对象
factory.newContructorSerialization(“需要反射的类”，“构造的方法”)
```

