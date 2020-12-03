---
title: C语言 const 关键字的使用场景
date: 2020-12-03 13:03:26
categories: 
- C
tags: 
- "author: zanxinz"
- C
---


## const 限定的变量

- 被 const 声明的变量，在定义时赋值，然后后面就不能修改变量的值了。

  ```c
  const int num = 25;//定义 int 类型的 num 并且赋值
  //num = 20;//num 为被 const 限定，不能再修改
  ```

## 补充一下：指针——也称为**指针变量**

- 指针的使用
  
  ```c
  int number = 10;
  int *p = &number ;   //定义一个 int 类型的【指针变量】p  (* 号作为一个标识符，代表这是一个指针),然后 p 指向 number
  ```

## const 和指针变量的结合

- 指向 【常量】的【指针变量】

    写成const int *p = &a ;

    或者int const *p = &a ;

    都可以

    ```c
    int a = 25;
    const int *p = &a ;//定义 int 类型的指针变量， 指向 a//也可以

    //*p = 20;//尝试通过指针p修改 a 的值，不能的，因为 p 指向的 a 被 const 限定了。

    int dog = 50;
    p = &a;//修改 p 的指向，可以的，因为 p 是一个指针变量，是一个可变的值。
    ```

- 指针常量，也称为const类型指针。
  
  const 写在 * 后面

  >int * const ptr = &n;

  ```c
  int n = 30;
  int  * const ptr = &n;//指针不能变，但指向的内容（n）可以变
  *ptr = 20;            //可以实现。
  ```

- 指向【常量】的【指针常量】
  
  ```c
  int n = 30;
  
  //【非常量】的地址给指向【常量】的【指针变量】是安全的
  const int * const ptr = &n;//指针不能变，指向的内容(n)也不能变
  //*ptr = 20;               //第一个 const 限定了 ptr 指向的内容不能被修改，所以这里会编译不通过。
  ```

## const 的坑

常量：被 const 限定
  
变量：未被 const 限定

- 常量（被 const 限定）的地址，赋给不带 const 的指针是不安全的。
  
  ```c
  const int a = 20;
  int *p = &a;//很不安全
  *p=20;      //不安全的操作(Visual studio 不能编译，但 gcc 可以，只是 会有警告，最后可以运行，并且 a 的值会被改变)
  ```

- （常量或者变量）的地址，可以赋给带 const 的 int 指针

  比如，下列函数只需要读取 a 的值用作显示，那么不需要修改 a，使用const可以防止 a 在函数体内被修改。而在调用时，给函数传递的 int 类型参数的地址,可以是 const 或者非 const 都可以。
  
  函数拿到地址之后，只做读取而不修改

  ```c
  void display(const int *a);
  ```

## 二级指针不安全

- 例子

  ```c
  const int n = 8;//本意是 n 的值不能改变
  const int * p1;
  p1 = &n;
  int ** pp2;
  pp2 = &p1;     //不安全，不能使用 const int **，初始化 int **pp2

  **pp2 = 10;    //通过pp2修改到了n的值，违背本意。
  printf("n:%d\n",n);
  ```

  (Visual studio会自动检测这种情况从而不让编译通过，但是C语言本身是可以编译通过的,只是会有下面的警告)
  
  ```c
  new.c: 在函数‘main’中:
  new.c:11:8: 警告：从不兼容的指针类型赋值 [-Wincompatible-pointer-types]
    pp2 = &p1;
        ^
  new.c:15:4: 警告：隐式声明函数‘system’ [-Wimplicit-function-declaration]
    system("pause");
  
  ```

  gcc编译之后运行程序，结果n可以打印出来就是10

  小结：**n 被 const 限定了，但是却可以通过二级指针绕过这个限定**，所以二级指针在误用的情况下很不安全。
