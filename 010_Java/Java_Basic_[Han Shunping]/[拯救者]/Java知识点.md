* Java文档注释 /**......\*/

* 命名 字母 数字 下划线 $
* 字符型数据采用的是Unicode编码
  * 每个Unicode占用2个字节
* Java 的数据类型占用字节数和平台无关保证了很好的移植性
* 类变量会被默认初始化 先初始化为默认值 再进行初始赋值
* 局部变量不会自动初始化
* java允许继承， 单不允许循环继承
* 构造一个外部类的内部类
  * Outer outer = new Outer();
  * Outer.Inner in = outer.new Inner();

* 写源文件 javac编译源文件得到字节码文件 解释器运行源文件
  * 源文件.java 
  * 字节码文件 .class
* byte char short int long float double
  * float常量必须用F或f为后缀。
    double常量用D或d为后缀，但允许省略后缀。
*  char型字符在Unicode表中的位置范围是0至65535
* /u后边为16进制位