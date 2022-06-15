JFrame

```java
public static void main(String[] args) {
        JFrame jf = new JFrame();
        jf.setTitle("Tesing");
        jf.setSize(400, 300);
        jf.setLocation(400, 300);
        jf.setVisible(true);
        jf.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);

    }
```



JDialog

```java
public static void main(String[] args) {
        JFrame jf = new JFrame();
        jf.setTitle("Tesing");
        jf.setSize(400, 300);
        jf.setLocation(400, 300);
        jf.setVisible(true);
        jf.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);

        JDialog jd = new JDialog(jf);
        jd.setTitle("test");
        jd.setBounds(400, 300, 150, 200);
        jd.setVisible(true);
        jd.setDefaultCloseOperation(WindowConstants.DISPOSE_ON_CLOSE);

    }
```



JPanel

```java
		JButton jb1 = new JButton("btn1");
        JButton jb2 = new JButton("btn2");
        JPanel jp = new JPanel();
        jp.add(jb1);
        jp.add(jb2);
        jf.add(jp);
```



JButton

```java
public static void main(String[] args) {
        JFrame jf = new JFrame();
        jf.setTitle("test");
        jf.setLayout(new FlowLayout());
        jf.setBounds(400, 300, 300, 400);

        JRadioButton jrb1 = new JRadioButton("T");
        JRadioButton jrb2 = new JRadioButton("F");
        ButtonGroup brg = new ButtonGroup();
        brg.add(jrb1);
        brg.add(jrb2);

        jf.add(jrb1);
        jf.add(jrb2);

        jf.setVisible(true);
        jf.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
    }
```

JCheckBox

```java
 public static void main(String[] args) {
        JFrame jf = new JFrame();
        jf.setTitle("test");
        jf.setLayout(new FlowLayout());
        jf.setBounds(400, 300, 300, 400);

        JCheckBox box1 = new JCheckBox("Sleeping", true);
        JCheckBox box2 = new JCheckBox("Sleeping", false);
        JCheckBox box3 = new JCheckBox("Sleeping", false);
        jf.add(box1);
        jf.add(box2);
        jf.add(box3);

        jf.setVisible(true);
        jf.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
    }
```

JComboBox

```java
 public static void main(String[] args) {
        JFrame jf = new JFrame();
        jf.setTitle("test");
        jf.setLayout(new FlowLayout());
        jf.setBounds(400, 300, 1000, 1000);

        JComboBox box = new JComboBox();
        box.addItem("---select your educational background");
        box.addItem("university");
        box.addItem("high school");
        box.addItem("junior high school");

        jf.add(box);

        jf.setVisible(true);
        jf.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
    }
```





JMune

```java
public static void main(String[] args) {
        JFrame jf = new JFrame();
        jf.setTitle("test");
        jf.setBounds(400, 300, 300, 400);
        jf.setLayout(new FlowLayout(FlowLayout.CENTER));

        JMenuBar jmb = new JMenuBar();
        JMenu menu1 = new JMenu("menu1");
        JMenu menu2 = new JMenu("menu2");
        JMenu menu3 = new JMenu("menu3");
        JMenuItem item1 = new JMenuItem("item1");
        JMenuItem item2 = new JMenuItem("item2");
        JMenuItem item3 = new JMenuItem("item3");
        JMenuItem item4 = new JMenuItem("item4");
        JMenuItem item5 = new JMenuItem("item5");
        JMenuItem item6 = new JMenuItem("item6");
        menu1.add(item1);
        menu1.add(item2);
        menu1.add(item3);
        menu2.add(item4);
        menu3.add(item5);
        menu3.add(item6);
        jmb.add(menu1);
        jmb.add(menu2);
        jmb.add(menu3);
        jf.add(jmb);


        jf.setVisible(true);
        jf.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
    }
```



JTextField && JPasswordField

```java
public static void main(String[] args) {
        JFrame jf = new JFrame();
        jf.setTitle("test");
        jf.setBounds(400, 300, 300, 400);
        jf.setLayout(new FlowLayout(FlowLayout.LEFT));

        JTextField text = new JTextField("input name", 10);
        JLabel jl1 = new JLabel("Account");
        jf.add(jl1);
        jf.add(text);

        JPasswordField pwd = new JPasswordField("input", 10);
        pwd.setEchoChar('*');
        JLabel jl2 = new JLabel("password");
        jf.add(jl2);
        jf.add(pwd);

        jf.setVisible(true);
        jf.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
    }
```



JTextArea

```java
public static void main(String[] args) {
        JFrame jf = new JFrame();
        jf.setTitle("test");
        jf.setBounds(400, 300, 300, 400);
        jf.setLayout(new FlowLayout(FlowLayout.LEFT));

        JTextArea area = new JTextArea(10, 10);
        area.setLineWrap(true);
        jf.add(area);

        jf.setVisible(true);
        jf.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
    }
```



FlowLayout

BorderLayout

GridLayout

```java
 jf.setLayout(new BorderLayout());

        JButton btn1 = new JButton("btn1");
        JButton btn2 = new JButton("btn2");
        JButton btn3 = new JButton("btn3");
        JButton btn4 = new JButton("btn4");
        JButton btn5 = new JButton("btn5");

        jf.add(btn1, BorderLayout.NORTH);
        jf.add(btn2, BorderLayout.SOUTH);
        jf.add(btn3, BorderLayout.WEST);
        jf.add(btn4, BorderLayout.EAST);
        jf.add(btn5, BorderLayout.CENTER);
```



事件监听

![image-20220614231816225](C:\Users\lyn95\AppData\Roaming\Typora\typora-user-images\image-20220614231816225.png)

```java
public static void main(String[] args) {
        JFrame jf = new JFrame();
        jf.setTitle("Listener");
        jf.setBounds(400, 300, 300, 400);
        jf.setLayout(new FlowLayout(FlowLayout.CENTER));

        JTextArea area = new JTextArea(10, 18);
        area.setLineWrap(true);
        jf.add(area);
        JButton btn = new JButton("hit house");
        jf.add(btn);
        btn.addActionListener(new AbstractAction() {
            @Override
            public void actionPerformed(ActionEvent e) {
                area.append("conduct oneself well");
            }
        });

        jf.setVisible(true);
        jf.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
    }
```



![image-20220614233935425](C:\Users\lyn95\AppData\Roaming\Typora\typora-user-images\image-20220614233935425.png)





![image-20220614234133170](C:\Users\lyn95\AppData\Roaming\Typora\typora-user-images\image-20220614234133170.png)

```java
public static void main(String[] args) {
        JFrame jf = new JFrame();
        jf.setTitle("Test");
        jf.setBounds(400, 300, 300, 200);
        jf.setLayout(new FlowLayout(FlowLayout.LEFT));

        JLabel jl1 = new JLabel("count");
        JTextField usernameText = new JTextField("", 22);
        JLabel jl2 = new JLabel("password");
        JPasswordField passwordText = new JPasswordField("", 20);
        JTextField out_ = new JTextField("log status", 26);
        JButton btn = new JButton("Login");

        jf.add(jl1);
        jf.add(usernameText);
        jf.add(jl2);
        jf.add(passwordText);
        jf.add(out_);
        jf.add(btn);


        jf.setVisible(true);
        jf.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
    }
```

