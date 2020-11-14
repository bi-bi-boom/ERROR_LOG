---
title: Java 对象的浅复制和深复制
date: 2020-11-14 00:10:37
Categories: 
 - Java
tags:
 - "author: zanxinz"
 - Java
---

| 英文 | 名称 |
| :---: | :---: |
| Shallow copy | 浅复制|
| Deep copy| 深复制 |
| Lazy copy | 延迟复制|

***

<!-- More -->

## 浅复制

- 原理

  {% asset_img Java浅复制.png %}

- 类图

  {% asset_img UML.png %}

- wallet.java

```java
package smallClass;

public class Wallet {
  private int money;//钱数
  private String rank;
  /**
   * 带初始余额的构造方法
   * @param money 初始余额
   */
  public Wallet(int money,String rank) {
   // TODO Auto-generated constructor stub
   this.setMoney(money);
   this.setRank(rank);
  }
  /**
   * 设置钱包的余额
   * @param money 钱包的余额
   * @return 设置余额是否成功
  */
  public void setMoney(int money) {
    this.money=money;
   }
  /**
   * 设置钱包的称号
   * @param rank 钱包的称号
   */
  public void setRank(String rank) {
    this.rank=rank;
  }
  /**
   * 获取钱包的余额
   * @return 钱包的余额
   */
  public int getMoney() {
   return money;
  }
  /**
   * 获取钱包称号
   * @return rank 钱包的称号
   */
  public String getRank() {
    return this.rank;
  }
}

```

- Student.java

```java
package smallClass;
/**
 * 学生类
 * @author Zanxin
 *
 */
public class Student implements Cloneable {
  private String name;
  private Wallet wallet;
  public Student() {
   // TODO Auto-generated constructor stub
  }
  public Student(String name,int money,String rank) {
    setName(name);
    wallet=new Wallet(money,rank);
  }
  /**
  * 获取学生姓名
  * @return name 学生姓名
  */
  public String getName(){
    return this.name;
  }
  /**
  * 获取钱包余额
  * @return Wallet.money 钱包的余额
  */
  public int getMoney() {
    return wallet.getMoney();
  }
  /**
   * 获取钱包称号
   * @return Wallet.rank 钱包的称号
   */
  public String getWalletRank() {
    return this.wallet.getRank();
  }
  /**
   * 设置姓名
   * @param name 学生姓名
  */
  public void setName(String name) {
    this.name=name;
  }
  /**
   * 设置钱包余额
   * @param money 钱包余额
   */
  public void setWalletMoney(int money) {
    this.wallet.setMoney(money);
  }
  /**
   * 设置钱包称号
   * @param rank 钱包的称号
   */
  public void setWalletRank(String rank) {
    this.wallet.setRank(rank);
  }
  @Override
  protected Object clone() {
   // TODO Auto-generated method stub
   try{
     return super.clone();
     }catch(CloneNotSupportedException e){
       return null;
      }
  }
}
```

- console.java

```java
package smallClass;

public class Console {
 public static void main(String[] args) {
   Student stu=new Student("维多利亚", 50,"菜鸟");
   Student stu2=(Student) stu.clone();
  
   System.out.println(stu.getName()+stu.getMoney()+stu.getWalletRank());
   System.out.println(stu2.getName()+stu2.getMoney()+stu2.getWalletRank());
  
   stu2.setName("朱丽叶");
   stu2.setWalletMoney(20);//只是改了stu2 而stu却跟着一起变（这个money是money里面的，而整个wallet是共享的）
   stu2.setWalletRank("青铜");
  
   System.out.println("----------------");
   System.out.println("修改后：");
   System.out.println(stu.getName()+stu.getMoney()+stu.getWalletRank());//stu的wallet很无辜地被改变
   System.out.println(stu2.getName()+stu2.getMoney()+stu2.getWalletRank());
   System.out.println("----------------");
  }
}

```

- 运行结果
   {% asset_image 浅复制结果.png %}

***

## 深复制

- 原理
  {% asset_image Java深复制.png %}
- 类图
  {% asset_img UML.png %}

- wallet.java

```java
package smallClass;

public class Wallet {
  private int money;//钱数
  private String rank;
  /**
   * 带初始余额的构造方法
   * @param money 初始余额
   */
  public Wallet(int money,String rank) {
   // TODO Auto-generated constructor stub
   this.setMoney(money);
   this.setRank(rank);
  }
  /**
   * 设置钱包的余额
   * @param money 钱包的余额
   * @return 设置余额是否成功
  */
  public void setMoney(int money) {
    this.money=money;
   }
  /**
   * 设置钱包的称号
   * @param rank 钱包的称号
   */
  public void setRank(String rank) {
    this.rank=rank;
  }
  /**
   * 获取钱包的余额
   * @return 钱包的余额
   */
  public int getMoney() {
   return money;
  }
  /**
   * 获取钱包称号
   * @return rank 钱包的称号
   */
  public String getRank() {
    return this.rank;
  }
}
```

- Student.java
  
```java
package smallClass;
/**
 * 学生类
 * @author Zanxin
 *
 */
public class Student implements Cloneable {
  private String name;
  private Wallet wallet;
  public Student() {
   // TODO Auto-generated constructor stub
  }
  public Student(String name,int money,String rank) {
    setName(name);
    wallet=new Wallet(money,rank);
  }
  /**
  * 获取学生姓名
  * @return name 学生姓名
  */
  public String getName(){
    return this.name;
  }
  /**
  * 获取钱包余额
  * @return Wallet.money 钱包的余额
  */
  public int getMoney() {
    return wallet.getMoney();
  }
  /**
   * 获取钱包称号
   * @return Wallet.rank 钱包的称号
   */
  public String getWalletRank() {
    return this.wallet.getRank();
  }
  /**
   * 设置姓名
   * @param name 学生姓名
  */
  public void setName(String name) {
    this.name=name;
  }
  /**
   * 设置钱包余额
   * @param money 钱包余额
   */
  public void setWalletMoney(int money) {
    this.wallet.setMoney(money);
  }
  /**
   * 设置钱包称号
   * @param rank 钱包的称号
   */
  public void setWalletRank(String rank) {
    this.wallet.setRank(rank);
  }
  @Override
  protected Object clone() {
    // TODO Auto-generated method stub
    return new Student(name,wallet.getMoney(),wallet.getRank());//生成新对象
  }
}
```

- Console.java
  
```java
package smallClass;

public class Console {
 public static void main(String[] args) {
   Student stu=new Student("维多利亚", 50,"菜鸟");
   Student stu2=(Student) stu.clone();
  
   System.out.println(stu.getName()+stu.getMoney()+stu.getWalletRank());
   System.out.println(stu2.getName()+stu2.getMoney()+stu2.getWalletRank());
  
   stu2.setName("朱丽叶");
   stu2.setWalletMoney(20);//只是改了stu2 而stu却跟着一起变（这个money是money里面的，而整个wallet是共享的）
   stu2.setWalletRank("青铜");
  
   System.out.println("----------------");
   System.out.println("修改后：");
   System.out.println(stu.getName()+stu.getMoney()+stu.getWalletRank());//stu的wallet很无辜地被改变
   System.out.println(stu2.getName()+stu2.getMoney()+stu2.getWalletRank());
   System.out.println("----------------");
  }
}
```

- 运行结果
  {% asset_image 深复制结果.png %}

***

### 浅复制和深复制的具体差异

- 本示例中
  - **实现Cloneable接口时重写了clone方法的方式不一样**
  - 而用到的各个类之间的关系是一样的（只有重写 clone 方法不同，其他地方一模一样）

- 浅复制重写clone
  - 这时候 stu 的 wallet 和 stu2 的 wallet 会指向同一个 wallet 对象

  ```java
  @Override

  protected Object clone() {
  // TODO Auto-generated method stub
  try{
    return super.clone();//父类clone方法默认是浅复制
  }catch(CloneNotSupportedException e) {
    return null;
    }
  }
  ```

- 深复制重写clone
  - 这时候 stu 的 wallet 和 stu2 的 wallet 指向不同的 wallet 对象

  ```java
  @Override

  protected Object clone() {
    return new Student(name,wallet.getMoney(),wallet.getRank());
  }
  
  ```

## 延迟复制

- 像是浅复制，又像是深复制
- 多个引用共享一个对象，当通过某个引用要改变对象的内容时，会生成一个新对象给这个引用使用，所以也叫做[写时拷贝]。
- 提高了深复制的性能，避开了浅复制的“改一个，影响大家”的问题。

## 复制的默认形式

- 基础类型对象：直接复制。因为基础类型没有对象，不存在深复制问题。（Integer Double String）
- 数组、集合都是浅复制
- Cloneable 接口的 clone ：浅复制
- String str2 = new String(“ABC”);**至少创建一个对象，也可能两个**。因为用到new关键字，肯定会在heap中创建一个str2的String对象，它的value是“ABC”。同时如果 "ABC" 这个字符串在java String池里不存在，会在java池里创建这个String对象 "ABC"
- 浅复制 复制了引用
- 深复制 复制了引用和它所引用的内容，一层一层进去复制

## 序列化

- 如果把一个对象序列化，再反序列化给一个新对象，就可以实现复制功能。
- 优势
  - 操作简便
- 缺陷
  - 不能序列化 transient 变量。
  - 效率低，它比通过实现Clonable接口这种方式来进行深复制几乎多花100倍的时间。
  