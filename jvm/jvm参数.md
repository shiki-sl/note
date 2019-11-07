jvm参数固定值:-XX(+/-)\<option>表示开启或者关闭option选项
+true -false jvm有部分默认开启的功能
-XX:\<option>=\<value>表示将option的值设置为value
1. 追踪类的加载信息并打印出来:-XX:+TraceClassLoading
2. 追踪类的卸载信息并打印出来:-XX:+TraceClassUnloading
3. 改变系统类加载器: -Djava.system.class.loader=x.class 系统类加载器是由appclassloader进行加载的