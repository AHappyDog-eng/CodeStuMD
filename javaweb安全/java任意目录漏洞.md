### java 任意目录漏洞

通过漏洞可以遍历服务器中所有的文件目录导致可以遍历出系统后台文件导致危险发生

### java文件空字节字节漏洞

2013年9月10日发布的`Java SE 7 Update 40`修复了空字节截断这个历史遗留问题。此次更新在`java.io.File`类中添加了一个`isInvalid`方法，专门检测文件名中是否包含了空字节。

```
Java空字节截断利用场景最常见的利用场景就是文件上传时后端获取文件名后使用了endWith、
正则使用如:.(jpg|png|gif)
$验证文件名后缀合法性且文件名最终原样保存,同理文件删除(delete)、获取文件路径(getCanonicalPath)、
创建文件(createNewFile)、文件重命名(renameTo)等方法也可适用
```

### Apache Commons Collections反序列化漏洞



