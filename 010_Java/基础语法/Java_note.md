# Java

## 包装类

### 基本数据类型和包装类之间的转换

 **装箱**和**拆箱** 

```markdown
将“基本数据类型转换成包装类”的过程叫做装箱，将“包装类转换成基本数据类型”的过程叫做拆箱。
```

![11.jpg](https://cdn.acwing.com/media/article/image/2022/04/17/186034_9a6f502abe-11.jpg) 

![5.jpg](https://cdn.acwing.com/media/article/image/2022/04/17/186034_73f9bb62be-5.jpg) 

### 包装类转换成其他数据类型

无论包装类是什么样的类型，转换时加想要转换的类型即可  

```java
Integer i = new Integer(1024);
int a = i.intValue(); 
double b = i.doubleValue();
char c = i.charValue();
```

```java
Integer i = new Integer(100);  
//转换成double类型  
double d = i.doubleValue();  
System.out.println("d的值：" + d);
//转换成float类型  
float f = i.floatValue();  
System.out.println("f的值" + f);  
```

### 包装类与字符串之间的转换

* 将基本数据类型转换成字符串

  ![12.jpg](https://cdn.acwing.com/media/article/image/2022/04/17/186034_745b3282be-12.jpg) 

* 将字符串转换成基本数据类型

  parse : 作语法分析

  ![13.jpg](https://cdn.acwing.com/media/article/image/2022/04/17/186034_95650c9dbe-13.jpg) 

## 异常处理

### ID检测

`Java`定义了一个异常类的层次结构，以`Throwable`开始，扩展出`Error`和`Exception`，而`Exception`又扩展出`IOException`类和`RuntimeException`类.

1. `Error`：由`Java`虚拟机生成并抛出，`Java`程序不做处理。
2. `Exception`(程序中的问题,可预知的)：`Java`编译器要求`Java`程序必须捕获或声明所有的非运行时异常。
3. `Runtime Exception`(被`0`除等系统错误,数组下标超范围)：由系统检测，用户的`Java`程序可不做处理，系统将它们交给缺省的异常处理程序。
4. ` IOException`：流异常，通常用于文件读取中。

![14.jpg](https://cdn.acwing.com/media/article/image/2022/04/17/186034_a9f58938be-14.jpg) 

```java
public class ThrowException {
	public static void function(String id) {  //利用throws关键字声明该方法可能出现异常IllegalArgumentException
		if (id.length() == 7) {  //输出ID合法时的语句
			System.out.println("ID格式正确：" + id);
		}
	    else {  //利用throw关键字抛出异常IllegalArgumentException			
			throw new IllegalArgumentException();
		}
	}
    
	public static void main(String[] args) {
		Scanner sc=new Scanner(System.in);
		String id=sc.nextLine();
		try {
	        function(id);
	    }
	    catch (IllegalArgumentException e) {  //输出ID不合法时的语句	 
			System.err.println("ID长度应为7");
	    }
	}
}
```

### 异常的捕获与处理 - 文本统计

使用`try`和`catch`关键字可以捕获异常。`try/catch`代码块放在异常可能发生的地方。`try/catch`代码块中的代码称为保护代码，使用`try/catch`的语法如下： 

```java
try  {  
   //接受监视的程序块,在此区域内发生的异常,由catch中指定的程序处理;  
}  
catch(要处理的异常种类和标识符) {  
   //处理异常;  
}  
catch(要处理的异常种类和标识符) {  // 可能发生多个不同的异常
   //处理异常;  
}  
```

```java
// 包装类的方法
isLetter(char ch);  // 判断是否是字母
isSpaceChar(char ch);  // 判断是否是空格
isDigit(char ch);  // 判断是否是数字
Character.isLetter(str.charAt(i));
```

### 自定义异常 - 正负数

```markdown
用户定义的异常同样要用try{} catch{}捕获，但必须由用户自己抛出 throw new MyException。
异常是一个类,用户定义的异常必须继承自Throwable或Exception类，建议用Exception类。
```

```java
class MyException extends Exception {  
    public MyException(String m) {  
        super(m);  
    }  
}  
```

## IO流

```markdown
字符 = 字节 + 编码
字节 = 字符 + 解码 
```