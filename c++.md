# C++

# C++入门
## 1.第一个C++程序
```c++
#include<iostream>
using namespace std;
int main()
{
    cout<<"Hello World"<<endl;
    return 0;
}
```
>文件包含`include<iostream>`,其中包含了iostream的标准库   
第二行，声明使用了一个叫std的命名空间   
第三行~七行，只含有一个主函数体main，`cout<< "Hello World" >>endl;`是c++的标准输出语句


## 2.解读命名空间
```c++
using namespace std;
```
>这是C++新引入的一个机制，主要是为了解决多个`模块`间命名冲突的问题，就像现实生活中两个人重名一个道理。C++把相同的名字都放到不同的空间里，来防止名字的冲突   
例如标准C++库提供的对象都存放在std这个标准名字空间中，比如cin、cout、endl,所以我们会看到在C++程序中都会有using namespace std;这句话了

如程序:
```c++
#include<iostream>
using namespace std;
int main()
{
    cout<<"Nice to meet you!"<<endl;
    return 0;
}
```
程序用到cout和endl则必须提前告知使用std这个命名空间，除此以外，还有另外两种写法:
- 用域限定符::来逐个制定，刚才的代码还可以写成:    
```c++
#include<iostream>
int main()
{
    std::cout<<"Nice to meet you!<<endl;
    return 0;
}
```
- 用using和域限定符一起制定用哪些名字，如代码:
```c++
#include<iostream>
using std::cout;
using std::endl;
int main()
{
    cout<<"Nice to meet you!<<endl;
    return 0;
}
```
先用using对具体的名字进行声明

## 3.C++中的输入输出
>c++兼容c的写法，即使用printf和scanf函数来实现，但不推荐  
采用c++自己的一套输入输出流：cin和cout来表示，使用之前需要以来标准库iostream,即也要`include<iostream>`

- cout输出流的使用    
```c++

cout<<"Hello"; //即可输出Hello

//本质上，是将字符串"Hello"插入到cout对象里面，并以cout对象作为返回值返回，因此还可以用<<在后面连续输出多个内容，如：
cout<<"Hello"<<"World";

//至于前面采用到的endl操作符，可以直接将它插入到cout里，起输出换行的效果
cout<<"Hello"<<endl<<"World"<<endl;
/*
Hello
World
*/
```

- cin输入流的使用
```c++
// 接收一个数据之前,都要先定义一个与之类型一致的变量,用来存放这个数据,然后利用cin搭配>>输入操作符，来接收用户从键盘的输入，如代码：
#include<iostream>
using namespace std;
int main()
{
    int a;
    cout<<"input number:"<<endl;
    cin>>a;
    cout<<"Get "<<a<<endl;
    return 0;
}
// 程序运行结果如下:
// input number:
// 22
// Get 22

// 同样的，cin也可以连续接受多个变量
int a,b;
cin>>a>>b;

```

## 3.C++的数据类型
>与C语言基本一致，int\char\double\.....   
相比于C语言，还有额外的一种类型，叫做布尔类型:bool,内存上一般只占一个字节，用于表达真假逻辑结果的值
```c++
int a = 0, b = 1;
bool r;
r = a>b;
cout<<r;
// false
```

# C++的选择、循环、顺序结构、运算符、表达式
与C语言基本一致！

不展开
、
# C++函数调用传参内联重载模板

## 1.C++中函数调用的用法

## 2.

## 3.

## 4.


# C++类和对象
## 1.类的定义
>什么是类？什么是对象？   
对于面向对象的C++语言学习，类和对象的理解是整个语言学习中核心的基础。通俗的理解，类其实就是一个模子，是一个变量类型，对象就是这个类型定义出来的具体的变量，就像int a;这句话，int对应类，a就对应对象。大家应该就好理解了，但需要注意的是int是C++的内置类型，并不是真正的类。
>总的来说：类是对象的抽象和概括，而对象是类的具体和实例。

C++中的类，可以看作C中的结构体，但相比于结构体，在类中还能定义函数即（类的方法）,并且类中的变量叫做属性，函数叫做方法
```c++
// 关键字用class类定义，比如下面定义一个C++的类，学生类：
class Student
{
public:
    int num;
    char name[100];
    int score;
    int print()
    {
        cout<<num<<" "<<name<<" "<<score;
        return 0;
    }
};
//其中public是控制成员访问权限的一个存取控制属性，除了public以外，还有privare、protected一共三种
//private:表示私有，被它声明的成员，仅仅能被该类里的成员访问，外界不能访问，是最封闭的一种权限；
//protected比private稍微公开一些，除了类内自己的成员可以访问外，它的子类也可以访问（关于子类的概念我们会在后面详细展开）
//public声明的成员，则可以被该类的任何对象访问，是完全公开的数据
```
>，在认识了类的基本样子以后，下面我们再给大家看另一种写法，我们刚才看的这种写法，成员函数是写在类里的，如果类里的成员函数很多的话，阅读起来就会乱很多，故此，C++还支持另外一种写法，就是成员函数仅在类内声明函数原型，在类外定义函数体，这样在类里可以看到所有成员函数的列表，像目录一样一目了然，规范很多。

```c++
//在类中声明函数原型的方法与一般C语言的函数原型声明一样，而在类外定义函数的方法，则需要类名加：：作用域限定符表示，
class Student
{
public:
    int num;
    char name[100];
    int score;
    int print();
};
int Student::print()
{
    cout<<num<<" "<<score;
    return 0;
}
//函数头部分在返回值和函数名之间用类名加：：的方式指明这个函数是属于哪个类的。
```

## 2.对象的建立和使用
- 对象的创建
>类就是包含函数的结构体，是一种自定义数据类型，用它定义出来变量，就是对象，这就是所谓的“对象是类的具体和实例”，定义了一个这个类的对象，也可以说实例化了一个对象，就是这个意思！ 而对象的使用，和结构体的使用也一样，都是主要访问里面的成员，也都是用.的方式来访问，如：
```c++
Student A;
A.num = 101;
strcpy(A.name,"dotcpp");
A.score = 100;
A.print();
```
>需要注意的是，这里类的成员变量都是声明为public类型的，允许外部访问，但如果声明为private类型，则在主函数中不能通过对象.变量的方式直接访问，因为不能直接访问私有变量，要通过定义一个public类型的专门赋值的方法，通过内部成员访问private声明的变量，就可以在外部通过这个public的方法来间接控制这些私有成员，来起到封装、保护的效果，而这个public类型的方法，也称之为这个类的一个外部接口！

- 对象的指针
> 与普通变量一样，对象也是一片连续的内存空间，因此也可以创建一个指向对象的指针，即对象指针，存储这个对象的地址。   
那么创建方法与使用一般类型的指针类似，定义方法如下：   
类名 *指针名;     
如定义Student *p;     
定义一个Clock类型的指针p，需要清楚的是，这里并没有建立对象，当然也不会调用构造函数。      
接下来就可以将一个同类型的类对象地址赋值给这个指针，然后通过->来访问对象中的成员。
```c++
Student *p;
Student A;
p = &A;
p->print();
//除了在赋值和访问成员的时候用以外，在传参的时候也建议用指针来传递，因为其传递的为地址，不会进行对象之间的副本赋值，从而减少内存的开销，提高效率。
```