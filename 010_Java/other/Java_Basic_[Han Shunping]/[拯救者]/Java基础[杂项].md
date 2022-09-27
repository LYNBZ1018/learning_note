## 常用类 String

charAt 返回第i个字符

concat 在尾部添加字符串

equals 比较两个字符串是否一样

indexOf 返回一个字符第一次出现的位置

startsWith 是否以某个字符串为前缀开始

toCharArray() 转换为一个数组

trim() 清除前后的空格



```java
public static void main(String[] args) {
        String str = new String("HelloWorld");
        System.out.println(str.charAt(1));
        System.out.println(str.concat("nihao"));
        System.out.println(str.equals("nihao"));
        System.out.println(str.indexOf('l', 5));
        System.out.println(str.startsWith("Hel"));
        char[] ch = str.toCharArray();
        System.out.println(ch[0]);
        str = "  Hello   ";
        System.out.println(str);
        System.out.println(str.trim());
    }
```



#### StringBuffer

![image-20220615103405307](C:\Users\lyn95\AppData\Roaming\Typora\typora-user-images\image-20220615103405307.png)

#### Math 和 Random

![image-20220615103530369](C:\Users\lyn95\AppData\Roaming\Typora\typora-user-images\image-20220615103530369.png)

```java
Random random = new Random();
for (int i = 0; i < 10; i ++ ) {
    System.out.println(random.nextInt(11)); // [0, 10]  
}
```

#### 包装类

![image-20220615104006135](C:\Users\lyn95\AppData\Roaming\Typora\typora-user-images\image-20220615104006135.png)

![image-20220615104129718](C:\Users\lyn95\AppData\Roaming\Typora\typora-user-images\image-20220615104129718.png)

## 集合

![image-20220615110500459](C:\Users\lyn95\AppData\Roaming\Typora\typora-user-images\image-20220615110500459.png)

![image-20220615111359082](C:\Users\lyn95\AppData\Roaming\Typora\typora-user-images\image-20220615111359082.png)



## 多线程

![image-20220615112353993](C:\Users\lyn95\AppData\Roaming\Typora\typora-user-images\image-20220615112353993.png)

```java
public class Testing {
    public static void main(String[] args) {
        Thread1 thread1 = new Thread1();
        Thread2 thread2 = new Thread2();
        Thread thread = new Thread(thread2);
        thread1.start();
        thread.start();
        for (int i = 0; i < 10; i ++ ) {
            System.out.println("main_thread" + " i=" + i);
        }
    }
}

class Thread1 extends Thread {
    @Override
    public void run() {
        try {
            Thread1.sleep(5000);
        } catch(InterruptedException e) {
            e.printStackTrace();
        }

        for (int i = 0; i < 10; i ++ ) {
            System.out.println(Thread.currentThread().getName() + " i=" + i);
        }
    }
}

class Thread2 implements Runnable {
    @Override
    public void run() {
        for (int i = 0; i < 10; i ++ ) {
            System.out.println(Thread.currentThread().getName() + " i=" + i);
        }
    }
}

```



## IO输入输出



![image-20220615163519504](C:\Users\lyn95\AppData\Roaming\Typora\typora-user-images\image-20220615163519504.png)

![image-20220615163557992](C:\Users\lyn95\AppData\Roaming\Typora\typora-user-images\image-20220615163557992.png)

![image-20220615163713389](C:\Users\lyn95\AppData\Roaming\Typora\typora-user-images\image-20220615163713389.png)

```java
import java.io.*;

public static void main(String[] args) throws IOException {
        Reader reader = new FileReader("D:\\document\\text1.txt");
        Writer writer = new FileWriter("D:\\document\\text2.txt", true);  // 这个true是append
        char[] cpy = new char[1024];
        int len = 0;
        while ((len = reader.read(cpy)) != -1) {
            writer.write(cpy, 0, len);
            writer.flush();
        }

        reader.close();
        writer.close();
    }
```

字节流读取

FileInputStream read

FileOutputStream write

```java
InputStream is = new FileInputStream("D:\\document\\text1.txt");
        OutputStream os = new FileOutputStream("D:\\document\\text2.txt", true);
        byte[] bytes = new byte[1024];
        int len = 0;
        while ((len = is.read(bytes)) != -1) {
            os.write(bytes, 0, len);
            os.flush();
        }

        is.close();
        os.close();
```



![image-20220615171318799](C:\Users\lyn95\AppData\Roaming\Typora\typora-user-images\image-20220615171318799.png)

```java
File file = new File("D:\\document\\text3.txt");
        System.out.println(file.exists());
        System.out.println(file.getName());
        System.out.println(file.mkdir());
        System.out.println(file.isDirectory());
```



## JDBC

![image-20220615172627512](C:\Users\lyn95\AppData\Roaming\Typora\typora-user-images\image-20220615172627512.png)