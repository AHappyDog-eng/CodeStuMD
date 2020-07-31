

### 在注释中出现以@开头东东被称之为Javadoc文档标记，是JDK定义好的，如@author、@version、@since、@see、@link、@code、@param、@return、@exception、@throws等。



```
单行
/**
* Miscellaneous {@link String} utility methods.
*
*/

多行

/**
 * Class {@code Object} is the root of the class hierarchy.
 * Every class has {@code Object} as a superclass. All objects,
 * including arrays, implement the methods of this class.
 */
```

### @link：

@link的使用语法`{@link 包名.类名#方法名(参数类型)}`，其中当包名在当前类中已经导入了包名可以省略，可以只是一个类名，也可以是仅仅是一个方法名，也可以是类名.方法名，使用此文档标记的类或者方法

```
// 完全限定的类名
{@link java.lang.Character}

// 省略包名
{@link String}

// 省略类名，表示指向当前的某个方法
{@link #length()}

// 包名.类名.方法名(参数类型)
{@link java.lang.String#charAt(int)}
```

#### @code： {@code  text} 将文本标记为code

```
一般在Javadoc中只要涉及到类名或者方法名，都需要使用@code进行标记。
```

#### p <p> 作用

一般段落都用p标签来标记，凡涉及到类名和方法名都用@code标记，凡涉及到组织的，一般用a标签提供出来链接地址

#### @see 

```
@see 一般用于标记该类相关联的类,@see即可以用在类上，也可以用在方法上。
/**
 * @see IntStream
 * @see LongStream
 * @see DoubleStream
 * @see <a href="package-summary.html">java.util.stream</a>
 * /
```

#### @since 从以下版本开始

```
@since 一般用于标记文件创建时项目当时对应的版本，一般后面跟版本号，也可以跟是一个时间，表示文件当前创建的时间
/**
* @since 1.8
*/
public interface Stream<T> extends BaseStream<T, Stream<T>> {}
```

#### @value

```
/** 默认数量 {@value} */
private static final Integer QUANTITY = 1;
```

####  @exception

```
描述 方法上跑出的异常
/**
* @exception IllegalArgumentException if <code>key</code> is null.
*/
public static Object get(String key) throws IllegalArgumentException {}
```

#### @throws

```
描述内部 可能会出现的异常
/**
* @throws IllegalArgumentException when the given source contains invalid encoded sequences
*/
public static String uriDecode(String source, Charset charset){}
```

