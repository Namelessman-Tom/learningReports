# 221105学习报告

## C语言 结构体

### 声明语法

```c

struct 结构体名 {
    字段表
}变量表;
```
### 例

```c

struct Book{
    int ISBN;
    char name[30];
    double prise;
}book1;
```

### 访问结构体

- 用指针访问
    
    - `结构体 -> 字段名`
    - `*(结构体).字段名`

- 用值访问

    - `结构体.字段名`

### 应用

```c

#include "stdio.h"
struct vector {
    double x;
    double y;
};

int main() {
    struct vector v1, v2,v3;
    scanf("%lf %lf %lf %lf", &v1.x, &v1.y, &v2.x, &v2.y);
    v3.x = v1.x+v2.x;
    v3.y = v1.y+v2.y;
    printf("(%.1lf, %.1lf)", v3.x, v3.y);
}
```

### 位域
 
 - C语言的一大使用领域--单片机。其内存不像个人计算机那么充裕，可谓是寸土寸金，在使用内存的时候应该做到能省就省。

 - 一个保存学生信息的结构，需要包含一下字段
    
    - 姓名
    - 学号
    - 座号
    - 电话号码
    - 性别
- 若座号，性别都用一个int来存，这两个字段就需要占用`2*sizeof(int)`个字节的空间。

- 但保存一个二位数学号顶多只需要`7bit`，保存一个姓名只需要0和1，也就是`1bit`，如果能指定以上两个字段占用多少空间，原本`2*sizeof(int)`就减少成了`8bit`。

- #### 实现方法

    - 原始方法

        ```c

        struct Student1{
            char name[4];
            char id[10];
            unsigned int number;
            char phone[10];
            unsigned int gender;
        };
        ```
    - 改进方法

        ```c

        struct Student2 {
            char name[4];
            char id[10];
            unsigned int number : 7; 
            char phone[10];
            unsigned int gender : 1;
        };
        ```

    - 对比
    
        ![20221105211425](https://raw.githubusercontent.com/Namelessman-Tom/Pics/main/20221105211425.png)


---

撰写：`Namelessman`
日期：`2022.11.5`
