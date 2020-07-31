### 重写equals 和 hashcode

##### 自反性原则

自身调用equals 方法一定要返回true

x.equals(x) 返回true

##### 对称性原则

x.equals(y) y.equals(x) 都要返回true

##### 传递性

x.equals（y） y.equals（z）  那么 x.equals（z） 返回true

##### 一致性

对于任意的引用值x和y，如果用于equals比较的对象没有被修改的话，那么，对此调用x.equals(y)要么一致地返回true，要么一致的返回false

##### 非空性

对于任意的非空引用值x，x.equals(null)一定返回false。