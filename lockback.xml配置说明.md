## lockback.xml配置说明

配置文件主要有三个部分appender，logger，root

### appender

appender标识以何种方式输出日志，一般有两种控制台和文件

- 控制台：使用class="ch.qos.logback.core.ConsoleAppender"类来输出
- 文件：使用class="ch.qos.logback.core.rolling.RollingFileAppender"类来输出

### logger

logger可以用来根据某个包下或者某个类名指定输出特定的日志，如：com.thunisoft，jdbc.sqltiming，jdbc.sqlonly，jdbc.resultset等

包含以下几种属性和

- name：用来指定受此logger约束的某一个包或者具体的某一个类
- level：用来设置打印级别，五个常用打印级别从低至高依次为TRACE、DEBUG、INFO、WARN、ERROR，如果未设置此级别，那么当前logger会继承上级的级别
- additivity：是否向上级logger传递打印信息，默认为true；一般设置为false，这样不会重复打印

### **root**

root也是logger元素，但是**它是根logger，只有一个level属性，因为它的name就是ROOT**

这个就是所有的日志都会打印，使用appender-ref来指定看到底打印到控制台还是文件中

### 日志级别

优先级从高到低依次为：OFF、FATAL、ERROR、WARN、INFO、DEBUG、TRACE、 ALL