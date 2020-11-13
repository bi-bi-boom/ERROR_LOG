---
title: Java 对象的浅复制和深复制
date: 2020-11-13 23:56:37
Categories: 
 - Java
tags:
 - "author: zanxinz"
 - Java
---

| 英文 | 名称 |
| :---: | :---: |
| Shallow copy | 浅拷贝|
| Deep copy| 深拷贝 |
| Lazy copy | 延迟拷贝|

***

<!-- More -->

## 浅复制

- 原理

  {% asset_img Java浅复制.png %}

- 类图

  {% asset_img UML浅复制.png %}

### wallet.java

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

### Student.java

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
  }catch(CloneNotSupportedException e) {
   return null;
  }
 }
}
```

### console.java

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

***
