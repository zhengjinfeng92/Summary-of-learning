## Java注解

[引用](https://blog.csdn.net/ajianyingxiaoqinghan/article/details/81436118)

### 什么是注解

就是给类，接口，属性等添加标签 如：@service，@param等

### 元注解

元注解是可以注解到注解上的注解，或者说元注解是一种基本注解，但是它能够应用到其它的注解上面。或者可以理解为：元注解也是一张标签，但是它是一张特殊的标签，它的作用和目的就是给其他普通的标签进行解释说明的。

基本的元标签有 @Retention, @Documented, @Target, @Inherited 四种（后来到了 Java 8 又加入了 @Repeatable）


#### @Retention  

定义了该注解的生命周期。当 @Retention 应用到一个注解上的时候，作用就是说明这个注解的存活时间。

- RetentionPolicy.SOURCE: 注解只在源码阶段保留，在编译器完整编译之后，它将被丢弃忽视；
  例：@Override, @SuppressWarnings
- RetentionPolicy.CLASS: 注解只被保留到编译进行的时候，它并不会被加载到 JVM 中；
- RetentionPolicy.RUNTIME: 注解可以保留到程序运行的时候，它会被加载进入到 JVM 中，所以在程序运行时可以获取到它们；笔者接触到大部分的注解都是 RUNTIME 的生命周期。

#### @Target

@Target 表示该注解用于什么地方，可以理解为：当一个注解被 @Target 注解时，这个注解就被限定了运用的场景。可以使用的 ElementType 参数：

- ElementType.CONSTRUCTOR: 对构造方法进行注解；
- ElementType.ANNOTATION_TYPE: 对注解进行注解；
- ElementType.FIELD: 对属性、成员变量、成员对象（包括 enum 实例）进行注解；
- ElementType.LOCAL_VARIABLE: 对局部变量进行注解；
- ElementType.METHOD: 对方法进行注解；
- ElementType.PACKAGE: 对包进行注解；
- ElementType.PARAMETER: 对描述参数进行注解；
- ElementType.TYPE: 对类、接口、枚举进行注解；2.3 @Documented

#### @Documented 

@Documented 是一个简单的标记注解，表示是否将注解信息添加在 Java 文档，即 Javadoc 中。

#### @Inherited

Inherited 是指可以被继承，@Inherited 定义了一个注释与子类的关系。如果一个超类带有 @Inherited 注解，那么对于该超类，它的子类如果没有被任何注解应用的话，那么这个子类就继承了超类的注解。

#### @Repeatable

@Repeatable 是 Java 8 中加入的，是指可重复的意思。通常使用 @Repeatable 的时候指**注解的值可以同时取多个**

###  注解的属性

注解的属性也叫做成员变量。**注解只有成员变量，没有方法**。注解的成员变量在注解的定义中以**无形参的方法**形式来声明，其方法名定义了该成员变量的名字，其返回值定义了该成员变量的类型

```java
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
public @interface Coder {
    int id();
    String name();
    String language();
    String company();
}
```

