

# 一.开始学习C++

## 1.1进入C++

* out生成字符输出
* 用//表示注释
* C++是大小写敏感的语言
* 函数头int main()
* 结束main()函数的return语句
* 所有的语句都要以分号结束

```C++
# include<iostream>
int main()
{
	using namespace std;
	cout << "Hello World!" << endl;
	return 0;
}
```

* 头文件名
  * C++旧式风格：.h结尾
  * C旧式风格：.h结尾
  * C++新式风格：没有拓展名：iostream
  * 转化后的C：加上前缀c，没有拓展名：cmath

## 1.2C++语句

```C++
# include<iostream>
int main()
{
	using namespace std;
	int carrots=25;
	cout << "I have " << carrots << " carrots." << endl;
	carrots -= 1;
	cout << "I have " << carrots << " carrots." << endl;
	return 0;
}
```

* cout打印字符串和变量

## 1.3其他C++语句

* cin

```C++
# include<iostream>
int main()
{
	using namespace std;

	int carrots;
	cout << "请输入:";
	cin >> carrots;
	cout << "I have " << carrots << " carrots." << endl;
	return 0;
}
```

## 1.4函数

* 使用库函数

```C++
# include<iostream>
# include<cmath>

int main()
{
	using namespace std;

	double area;
	cout << "请输入一个数：";
	cin >> area;
	double side = sqrt(area);
	cout << area << "'s side is " << side << endl;
	return 0;
}
```

* 用户自定义函数

```C++
# include<iostream>
void own_function();


int main()
{
	own_function();
	return 0;
}

void own_function()
{
	using namespace std;
	cout << "You call the function successfully!" << endl;
}
```

# 二.处理数据

* 当你的变量类型不能够存储数值时（缩窄），在不同编译器上得到的结果可能会不同。

* 强制类型转换(两种方法都行)

  ```C++
  int stone;
  (long) stone; # C语言风格
  long (stone);  # C++语言风格, 使强制类型转换像函数一样调用
  ```

# 三.复合类型

## 3.1数组

数组被称为复合类型，是因为它是使用其他类型来创建的。

```C++
short months[12];  # typeName arrayName[arraySize];
```

```C++
# include<iostream>

int main()
{
	using namespace std;
    // 声明数组
	int yams[3] = {7, 8, 6};  //列表初始化
	cout << "Total Yams:" << yams[0] + yams[1] + yams[2] << endl;
	cout << "Array Size is:" << sizeof(yams) << endl;  //获取数组size：12bytes
	cout << "Element Size is:" << sizeof(yams[0])  << endl;  //获取变量size：4bytes
	return 0;
}
```

* 不能将数组赋值给另一个数组
* 只要将显示地为数组赋值一个0，则整个数组的值均为0；也可以对数组的一部分进行赋值
* 若初始化时方括号内为空，则C++编译器会自动计算元素个数（这种方式并不好，不过在初始化字符串的时候很好用）
* 列表初始化禁止缩窄

## 3.2字符串

* C++处理字符串的方式有两种

  * C风格字符串

    * 特性：以空字符（\0）结尾，空字符被用来标记字符串的结尾

    * 字符串常量：隐式地包括结尾的空字符（空字符也要占该字符串的长度）

    * 字符串用""表示, 单个字符(字符常量)用‘’表示

      ```C++
      char fish[] = "Bubbles";
      ```

      

  * string类库

    * include<string>

    * 同样使用名称空间std

      ```C++
      # include<string>
      string fish = "Bubbles";
      ```

      

### 3.2.1在数组中使用字符串

* 将字符串存储到数组中的两种方法

  * 将数组初始化为字符串常量

  * 将键盘或文件输入到数组中

```C++
# include<iostream>

const int arraySize = 15;  //字符串长度常量
int main()
{
	using namespace std;
	char name1[arraySize] = "ChengZhuoLu"; // 数组初始化构建字符串
	char name2[arraySize];
	cout << "I'm " << name1 << " What's your name?" << endl;
	cin >> name2;  //键盘输入读入数组
	cout << "Nice to meet you, " << name2 << endl;
	return 0;
}
```

* strlen与sizeof的区别
  * strlen只会返回字符串的长度(不含空字符): strlen(abcd)=4
  * sizeof会返回数组的长度(也就是声明数组时的长度)
* cin的机制：每次只能读取一个单词
  * cin使用空白（空格、制表符和换行符）来确定字符串的结束位置=>这意味着cin在获取字符串数组输入时只能读取一个单词
    * cin读取单词后会自动在结尾添加空字符

* 每次读取一行字符串输入:getline()和get()

  * getline()

    * cin.getline()=>通过回车键输入的换行符来确定输入结尾，但是getline()不保存换行符，在存储时将换行符替换为空字符

    * 参数1：存储输入行的数组的名称

    * 参数2：读取的字符串数（含空字符）

    * 参数3：在第17章讨论

      ```C++
      # include<iostream>
      
      const int arraySize = 20;
      
      int main()
      {
      	using namespace std;
      	char name[arraySize];
      	char dessert[arraySize];
      	cout << "Name:";
      	cin.getline(name, arraySize);
      	cout << "dessert:";
      	cin.getline(dessert, arraySize);
      	cout << "So, " << name << "'s favorite dessert is " << dessert;
      	return 0;
      }
      ```

  * get()

    * cin.get()=>原理与getline()相似，但是get不再读取并丢弃换行符
    * get()特性：不带任何参数可以读取下一个字符，因此可以用来处理换行符，例如cin.get(variable, arraySize).get()，其中第二个get是用来处理换行符的

  * get的使用场景比getline更多

    * 老式实现没有getline()
    * get()可以查看下一个输入字符，检查错误更简单

  * 当get遇到空行时会发生问题，将在后续章节探讨如何避免这些问题

* 混合输入字符串和数字

  主要需要防备因为读取数字留下的未处理换行符影响后续数据输入。

```C++
# include<iostream>

int main()
{
	using namespace std;
	int number;
	char name[20];
	cout << "Number:";
	(cin >> number).get();  //cin可能会留下换行符, 影响后续数据读取
	cout << "Name:";
	cin.get(name, 20).get();
	cout << name << " puts a number: " << number << "." << endl;
	return 0;
}
```

### 3.2.2string类字符串

* 在很多方面，string对象的使用方式与字符数组的使用方式相同
* string对象可以声明为简单变量，而不是数组
* string类的设计可以让程序自动处理string的大小，使用string对象更方便，也更安全

* string类字符串的常见操作

  * 初始化

    ```C++
    string test_string = {"The Bread Bowl"};
    ```

  * 赋值(对标strcpy)

    不能将数组赋值给另一个数组（静态），但是可以将一个string对象赋值给另一个string对象（此时被赋值对象原本指向的字符串会消失）

  * 拼接（对标strcat）

    可以使用+运算来将两个string对象合并起来。也能用+=这样的形式将一个string对象拼接在原始string对象的后面。

  * 获取字符串长度(对标strlen)：stringObject.size()
  * 使用getline从键盘读取输入并赋值给string对象：getline(cin, stringObject); //现在cin作为参数，不需要再额外指定最大读取长度

## 3.3结构

```C++
struct inflatable  //结构声明
{
	char name[20];
	float volume;
	double price;
};
inflatable test_object = {"ChengzhuoLu", 20.1, 33,73}; //结构初始化
cout << test_object.price << endl; //结构对象的属性调用
```

## 4.指针与自由存储空间

* 地址运算符&

* 解除引用运算符*

* 声明和初始化指针

  ```C++
  int higgens = 5;
  int* pr = &higgens; //声明并初始化指针
  ```

* 一定要在使用解除运算符*之前为指针初始化一个适当的、确定的地址，这是关于使用指针的金科玉律

* 虽然指针所指向的地址是整数，但是不能将整数直接赋值给指针

### 4.1使用new来分配内存

```C++
int* pn = new int;  //typeName* pointer_name = new typeName;
```

* new int告诉程序，需要适合存储int的内存，然后new就会去寻找满足要求的内存，并返回其地址

* 使用delete释放内存
  * 只能使用delete来释放new分配的内存
  * 不要对已经释放的内存使用delete
  * 对空内存使用delete是安全的

```C++
int* pn = new int;  //typeName* pointer_name = new typeName;
//some statement
delete pn;  // 释放内存
```

* 动态联编（Dynamic binding）=>在程序运行时选择数组的长度，这种数组叫做动态数组
  * 使用new来创建动态数组
    * ps本质上保存的是数组中第一个元素的地址
    * 使用new[]为数组分配内存，则应使用delete[]来释放
  * 使用动态数组
    * 可以直接使用索引的方式使用动态数组

```C++
int* ps = new int[10]; //new运算符会返回第一个元素的地址  typeName* pointer_name = new type_name[num_elements];
cout << ps[5] << end; //使用索引的方式使用动态数组
ps = ps + 1; //该式子对指针试用, d但是不能对数组名使用
// some statements
delete[] ps;  //释放空间
```

### 4.2指针、数组和指针运算

* 对指针变量+1后，增加的量等于它指向的类型的字节数
* 指针与字符串常量
  * 在这个示例中，"wren"实际是表示的是字符串的地址，因此这条语句将”wren“的地址献给了test_string指针
  * 字符串字面值视为只读常量，不能对其进行修改
  * C++不能保证字符串字面值被唯一地存储，编译器可能存储多个"wren"的副本
  * strcpy(desnation_pointer, source_pointer)：将源指针的字符串复制给目标指针

```C++
const char* test_string = "wren";
```

## 5.数组的替代品

### 5.1模板类vector

* 需要包含头文件vector=>#include <vector>
  * 使用名称空间std

```c++
vector<int> vi(10); //声明int类型vector
```

### 5.2模板类array

* 需要包含头文件array=>#include <array>
  * 使用名称空间std

```C++
array<int, 5>ai; //创建长度为5的array
```

# 四.循环与关系表达式

## 1.for循环

* for循环的基本要素
  * 设置初始值
  * 执行测试，看看循环是否应当继续进行
  * 执行循环操作
  * 更新用于测试的值

```C++
for(initialization;test-expression;update-expression) {statement body}
```

* 自增运算符（++）
  * 前缀递增、前缀递减、解除引用运算符的优先级相同，按照从右往左的方式进行结合:++*pt=>先获取pt指向的值，再自增
  * 后缀自增运算符的优先级更高：*pt++=>先指针自增，然后解除引用
* 逗号运算符
  * 将声明中相邻的变量名称分开
  * 在for循环初始化时提供更多样的初始化

* 比较两个字符串是否相同：strcmp(string_1, string_2)
  * 两个字符串相同返回0，不同返回1

## 2.while循环

```C++
while(test-condition) {statement body}
```

* 如果测试条件为真则执行循环中的雨具
* for循环和while循环本质是一样的

## 3.do while循环

```C++
do
{statement body}
while(test-condition)
```

* 先执行循环体，直到不满足条件（false）退出循环
* 特点是出口条件循环，会先执行一次循环体

## 4.基于范围的for循环（C++11）

* 本质上是遍历

```C++
double prices[5] = {4.99, 10.99, 6.87, 7.99, 8.49};
for (double x:prices) {
    cout << x << endl;
}
```

* 这种循环主要用于后续讨论的模板容器类

## 5.循环和文本输入

* 使用原始的cin进行读取
  * cin将会忽略空格和换行符
  * 对于cin，只有按下换行符后输入才被传输给程序，这意味着在#后面还可以进行一系列输入，虽然它们并不会被处理

```C++
# include<iostream>
# include<string>

int main()
{
	using namespace std;
	char ch;
	string input_text = "";  //初始化一个空字符
	cout << "请输入字符串:";
	bool out = false;
	while (!out)
	{
		cin >> ch;  // 读取单个字符
		if (ch == '#') {  //读取到预设好的结束字符
			out = true;
		}
		else {
			input_text += ch;  //拼接字符串
		}
	}
	cout << "Your input text is: " + input_text + '.' << endl;
	cout << "And its length is " << input_text.size();
	return 0;
}
```

* 使用cin.get(char)进行补救
  * cin.get(ch)读取输入中的下一个字符（即使它是空格），并将其赋值给变量ch
  * 使用这个方法可以有效解决上面提到的问题

```C++
# include<iostream>
# include<string>

int main()
{
	using namespace std;
	char ch;
	string input_text = "";  //初始化一个空字符
	cout << "请输入字符串:";
	bool out = false;
	while (!out)
	{
		cin.get(ch);  //使用cin.get代替cin>>
		if (ch == '#') {  //读取到预设好的结束字符
			out = true;
		}
		else {
			input_text += ch;  //拼接字符串
		}
	}
	cout << "Your input text is: " + input_text + '.' << endl;
	cout << "And its length is " << input_text.size();
	return 0;
}
```

* 文件尾条件（EOF）

```C++
cin.fail() == false;  //检测文件尾, 到达文件尾时cin.fail()返回True
```

# 五.分支语句与逻辑运算符

## 1.if语句

* if语句
* if else语句
* if else if语句
* 错误方法：程序员们选择使用value==variable来表达式variable==value，一次来捕获将相等运算符误写为辅助运算符的错误

```C++
if(test-condition) {  //如果条件为真则执行代码块
	statements
}
```

## 2.逻辑运算符

* 逻辑运算符的优先级低于关系运算符
* 逻辑OR运算符：||=>当条件满足时（一个条件为真），则不会去做后面的运算了
* 逻辑AND运算符：&&=>当条件不满足时（一个条件为假），则不会去做后面的运算了，&&的优先级高于||
* 逻辑NOT：！=>！运算符的优先级高于所有的逻辑运算符和算术运算符，但是低于关系运算符

## 3.?:运算符

```C++
expression1?expression2:expression3
```

* 如果expression的值为真，则整个条件表达式的值为expression2的值
* 如果expression的值为假，则整个条件表达式的值为expression3的值
* 从可读性来讲，?:适用于简单关系和简单表达式的值

```C++
# include<iostream>

int main()
{
	using namespace std;
	int a = 0, b = 0;
	cout << "2 nums:";
	cin >> a >> b;

	int result = a > b ?100:200;
	cout << result << endl;
	return 0;
}
```

## 4.switch

```C++
switch (integer-expression)  //switch条件是整数表达式
{
	case label1: statements;
	case label2: statements;
	case label3: statements;
	...
}
```

* switch跳跃到对应标签的那一行，然后按顺序执行后面的代码，可以使用break跳出switch

## 5.break和continue语句

* break会使程序跳过switch和循环后面的语句
* continue应用于循环，会跳过本次循环中余下的代码，开启新一轮的循环

# 六.函数

## 1.函数的基本知识

* 每个函数都是用一条using编译指令
  * 在每个函数开头写using namespace
  * 在函数定义前（外部）放一条using编译指令
* 使用函数的三个步骤
  * 定义函数
    * 没有返回值用void定义，然后return;
    * 有返回值用typeName定义，然后返回typeName(具体的值必须是这一类的或可以类型转化成这一类的);
  * 函数原型
    * 函数原型描述了函数到编译器的接口，它将函数的返回类型和参数的类型、数量都告诉了编译器。
    * 函数原型可以提高效率，因为C++的编程风格是将main()放在最前面，因为它通常提供了程序的整体结构
    * 函数原型是一条语句，因此必须以分号结束
    * 函数原型不要求提供变量名，有类型列表就够了；原型中的变量名是占位符，不必与函数定义中的变量名相同
    * 函数原型能降低程序出错的几率
  * 函数调用
    * 函数参数
      * C++将数值参数传递给函数，而后将其赋给一个新的变量；这样函数使用的是一个副本，不会影响原来的数据（这就是为什么C++的函数不会改变数据的值）
      * 用来接收传递值的变量被称为形参（parameter），传递给函数的值被称为实参（argument）
      * 函数内部的变量称为局部变量，在函数调用时创建，在函数结束时释放
      * 函数可以有多个参数，在调用函数时，使用逗号将这些参数分开即可

```C++
void cheers(int);
double cube(double x);
```

```C++
#include<iostream>
using namespace std;

void n_chars(char c, int n); // 函数原型
int main() 
{
	int epoch;
	char ch;
	cout << "epoch:";
	(cin >> epoch).get();
	cout << "letter:";
	cin.get(ch);  
	n_chars(ch, epoch);
}


//函数定义
void n_chars(char c, int n)
{
	while (n-- > 0) {
		cout << c << endl;
	}
	return;
}
```

## 2.函数与数组

* 在C++中，当且仅当用于函数头或函数原型是, int *arr和int arr[]的含义是相同的，都以为着arr是一个int指针
* 在C++中，必须显式的传递数组长度，因为在函数中，传入的仅是一个指针，无法再获取数组的长度

```C++
#include<iostream>
using namespace std;

int sum_arr(int arr[], int length);
void main()
{
	int cookies[] = { 1, 2, 4, 8, 16, 32, 64, 128 };
	cout << "cookies:" << sum_arr(cookies, sizeof(cookies)/sizeof(int)) << endl;
	return;
}

int sum_arr(int arr[], int length) {  //本质上给定了数组的起始位置和结束位置
	int result = 0;
	for (int i = 0; i < length; i++) {
		result += *(arr + i);
	}
	return result;
}
```

* 函数与二维数组
  * 在下面的例子中，指针类型指出该指针指向由4个int组成的数组
  * 指针类型指定了列数，所以不需要再将列数作为独立的函数参数进行传递(在使用时就可以直接用这个列数了)
  * 对于二维数组：arr\[r][c]=*(\*(arr+r)+c)

```C++
int data[3]][4] = {{1,2,3,4},{5,6,7,8},{9,10,11,12}};
int sum(int arr[][4], int size); //函数原型等效于int sum(int (*arr)[4])
```

## 3.函数与C风格字符串

* 将字符串作为参数来传递，实际上传递的是字符串第一个字符的地址
* 字符串都是以空字符结尾（没有空字符的只是数组，不是字符串），因此在传递参数时不再需要传递长度，只需要找到空字符即可

```C++
# include<iostream>
int count_char(const char* str, char target);
int main()
{
	using namespace std;
	const char *text = "hello";
	char ch;
	cout << "char:";
	cin.get(ch).get();
	cout << "count:" << count_char(text, ch) << endl;
	return 0;
}

int count_char(const char *str, char target)
{
	int count = 0;
	while (*str)  //当*str=='\0'时(遇到空字符)退出 
	{
		if (*str == target)
		{
			count++;
		}
		str++;
	}
	return count;
}
```

* 返回C风格字符串

```C++
#include<iostream>
char* buildstr(char c, int n);
int main()
{
	char* output = buildstr('c', 10);
	std::cout << output << std::endl;
	return 0;
}

char* buildstr(char c, int n)
{
	char* result = new char[n + 1];
	result[n] = '\0';  //字符串以空字符结尾
	while (n-- > 0)  //先有n>0，然后n-1
	{
		result[n] = c;
	}
	return result;
}
```

## 4.函数指针

* 函数的地址是存储器机器语言代码的内存的开始地址
  * 将一个函数A的地址传递给函数B，这样函数B就能够调用函数A并运行它

* 函数的地址：也就是函数名（带上括号就是函数调用，不带括号就是函数名）
  * process(think)：process能够调用think函数
  * thought(think())：thought会调用think函数的返回值

# 七.函数探幽

## 1.内联函数

* 内联函数是C++为提高程序运行速度的一项改进。主要区别在于C++编译器将其组合到程序中的方式与常规函数不同
  * 对于内联代码，程序无需跳到另一个位置处执行代码，再调回来=>速度更快，但是需要更多内存
* 内联函数的使用
  * 两个方法（选一个）
    * 在函数声明前加上关键字inline
    * 在函数定义前加上关键字inline
  * 通常的做法是省略原型，将整个定义（函数头和所有函数代码）放在本应提供原型的地方（也就是把函数写在前面）
  * 内联函数不应该过大，且内联函数不能递归
  * 内联函数的使用方法与常规函数一致，都是按值传递

```C++
#include<iostream>

inline double square(double x) { return x * x; }

int main()
{
	using namespace std;
	double a = 10.;
	cout << square(a) << endl;
	return 0;
}
```

## 2.引用变量

* 引用是已定义的变量的别名
* 引用变量的主要用途是用作函数的形参，通过将引用变量用作参数，函数将使用原始数据，而不是副本

* C++中使用&来创建引用
  * 变量和对应引用的值和地址都是一样的，并且同步变化
  * 必须在声明引用时将其初始化，而不能像指针一样先声明，再赋值
  * 引用更接近const指针，必须在创建时进行初始化，一旦与某个变量关联起来，就一致对它负责。不要想着用赋值将一个引用用在另一个变量上

```C++
int a = 0;  //创建变量
int& b = a;  //创建变量的引用
```

* 将引用作为函数的参数
  * 这种传递参数的方法被称为按引用传递
  * 这使得函数中的变量名称为调用程序中的变量的别名，这样就可以直接在函数中对变量进行修改

```C++
#include<iostream>
using namespace std;
void swap(int& a, int& b);
int main()
{
	int x = 10, y = 20;
	int& rx = x, & ry = y;
	swap(rx, ry);
	cout << x << endl << y << endl;
	return 0;
}


void swap(int& a, int& b)  //按引用传递
{
	int temp = a;
	a = b;
	b = temp;
}
```

* 临时变量、引用参数和const（尽可能使用const）=>主要是针对不希望改变值的函数，但是实际上不改变值可以不用引用
  * 使用const可以避免无意中修改数据的编程错误（因为引用虽然能变化，但是赋值可能会导致错误，一般用作形参）
  * 使用const可以是函数能够处理const和非const实参，否则将只能接受非const数据
  * 使用const引用是函数能够正确生成并使用临时变量

* 引用非常适合用于结构和类，实际上引用主要是为了用于这些类型的，而不是基本数据类型
* 返回引用
  * 常规函数返回值，从概念上来说，这个值被复制到一个临时位置，而调用程序将使用这个值
  * 在返回值为引用是，直接将返回值赋值给左值，效率更高
  * 返回引用时应注意的问题
    * 应避免返回函数终止时不再存在的内存单元引用（也就是临时变量）
      * 最简单的方法是返回一个作为参数传递给函数的引用（就是把变量改变后返回）
      * 另一种方法是使用new来分配新的存储空间(该代码会返回结构的引用)，缺陷是常常忘记使用delete来释放内存

```C++
const free_throws &clone(free_throws &ft)
{
    free_throws *pt;
    *pt = ft;
    return *pt;
}
```

* 对象、继承和引用
  * 派生类继承了积累的方法，派生类对象可以使用基类的特性
  * 基类引用可以指向派生类对象，而无需进行强制类型转换
* 何时使用引用参数
  * 程序员能够修改调用函数中的数据对象
  * 通过传递引用而不是整个数据对象，可以提高程序的运行速度
  * 如果数据对象是数据，则只能使用指针

## 3.默认参数

* 默认参数指的是当函数调用中省略了实参时自动使用的一个值
  * 极大地提高了函数使用的灵活性
  * 默认参数支持使用不同数目的参数调用同一个函数

* 通过函数原型设置默认值（将值赋给原型中的参数）
  * 只有函数原型指定了默认值，函数定义域没有默认参数时完全相同
* 必须从右向左传递默认值

## 4.函数重载

* 函数多态（函数重载）支持使用多个重名的函数
* 可以通过函数重载来设计一系列函数——它们完成相同的工作，但使用不同的参数列表
* 重载函数的关键是函数的参数列表——函数特征标
  * C++允许定义名称相同的函数，条件是它们的特征标不同
  * 特征标不同：参数数目或参数类型不同、是否有const限制等（函数的返回类型不是特征标）
  * 编译器将类型引用和类型本社视为同一个特征标

## 5.函数模板

* 函数模板——使用泛型来定义函数，其中泛型可用具体的类型替换
  * 通过将类型作为参数传递给模板，可是编译器产生该类型的函数
  * typename是C++98天假的关键字，C++也可以使用class关键字来创建模板
  * 函数模板本身不会生成函数定义，只是一个用于生成函数定义的方式

```C++
template <typename AnyType>  //声明模板
void Swap(AnyType &a, AnyType &b)
{
	AnyType temp;
	a = temp;
	a = b;
	b = temp;
}
```

### 5.1重载的模板

```C++
#include<iostream>
template <typename T>  //使用模板
void Swap(T &a, T &b);

template <typename T>  //每次对一个函数使用模板时都要标注
void Swap(T a[], T b[], int n);

const int arrSize = 3;

int main()
{
	using namespace std;
	int a = 10, b = 20;
	int& x = a, & y = b;
	cout << "a: " << a << endl << "b: " << b << endl;
	Swap(x, y);
	cout << "a: " << a << endl << "b: " << b << endl;

	int a_array[arrSize] = { 1, 2, 3 }, b_array[arrSize] = { 4, 5, 6 };
	cout << "a: " << *a_array << endl << "b: " << *b_array << endl;
	Swap(a_array, b_array, arrSize);
	cout << "a: " << *a_array << endl << "b: " << *b_array << endl;
	return 0;
}


template <typename T>
void Swap(T &a, T &b)
{
	T temp;
	temp = a;
	a = b;
	b = temp;
}

template <typename T>
void Swap(T a[], T b[], int n)  //重载的模板
{
	T temp;
	for (int i = 0; i < n; i++)
	{
		temp = a[i];
		a[i] = b[i];
		b[i] = temp;
	}
}

```

* 模板的局限性
  * 编写的模板函数可能无法处理某些类型
    * 数组不支持赋值
    * 结构不支持逻辑运算
  * 解决方法
    * 重载运算符
    * 为特定类型提供具体化的模板定义

### 5.2模板具体化

* 当编译器找到与函数调用匹配的具体化定义时，将使用该定义，而不再寻找模板
* 第三代具体化（ISO/ANSI C++标准）
  * 对于给定的函数名，可以有非模板函数、模板函数和显式具体化模板函数以及它们的重载版本
  * 显式具体化的原型和定义应以template<>打头，并通过名称来指出类型
  * 具体化优先于常规模板，而非模板函数优先于具体化和常规模板

```C++
void Swap(int a, int b; //非模板函数

template<typename T>
void Swap(T a, T b); //模板函数

template<> void Swap(int a, int b); //具体化模板
```

```C++
#include<iostream>
struct job
{
	char name[40];
	double salary;
	int floor;
};

template<typename T>  //常规模板
void Swap(T& a, T& b);
template<> void Swap(job& a, job& b); //模板具体化
void show(job j);



int main()
{
	job j1 = { "111", 111.11, 11 };
	job j2 = { "222", 222.22, 22 };
	Swap(j1, j2);
	show(j1);
	return 0;
}

template<typename T>  //常规模板
void Swap(T& a, T& b)
{
	T temp = a;
	a = b;
	b = temp;
}

template<> void Swap(job& a, job& b) //模板具体化
{
	double temp_salary;
	int temp_floor;

	//开始交换
	temp_salary = a.salary;
	a.salary = b.salary;
	b.salary = temp_salary;

	temp_floor = a.floor;
	a.floor = b.floor;
	b.floor = temp_floor;
}

void show(job j)
{
	using namespace std;
	cout << j.name << "  salary:" << j.salary << "  floor:" << j.floor;
}
```

# 八.内存模型和名称空间

## 1.单独编译

* 程序构成
  * 头文件：包含结构声明和使用这些结构的函数的原型
    * 函数原型
    * 使用#define或const定义的符号常量
    * 结构声明
    * 类声明
    * 模板声明
    * 内联函数
    * 不要讲函数定义和变量声明放在头文件中
  * 源代码文件：包含与结构有关的函数的代码
  * 源代码文件：包含调用与结构相关的函数的代码
* 不要讲头文件加入项目列表，也不要在源代码文件中使用#include来包含其他的源代码文件（应该包含对应的头文件）

* 在同一个文件中只能将一个头文件包含一次
  * 虽然记起来很简单，但是很可能在不知情的情况下将头文件包含多次。例如使用包含了另一个头文件的头文件
  * 使用预处理编译器指令#ifndef

```C++
#ifndef head
#define head
... //在这里面防止include的文件内容
#endif
```

## 2.存储持续性、作用域和链接性

* C++11的不同存储数据方案（4种）
  * 自动存储持续性：在所属函数或代码块执行时创建，结束时释放
  * 静态存储持续性：static定义的变量，在整个代码运行期间都会存在
  * 动态存储持续性：new运算符分配的变量，一直存在，直到使用delete释放
  * 线程存储持续性：thread_local声明的变量，其生命周期与所属的线程一样长

* 作用域和链接
  * 作用域（Scope）描述了名称在文件（翻译单元）的多大范围内可见
  * 链接性描述了名称如何在不同单元间共享
    * 链接性为外部的名称可在文件间共享
    * 链接性为内部的名称只能由一个文件中的函数共享
    * 自动变量的名称没有链接性，因为它们不能共享

### 2.1自动存储持续性

* 对于代码块中的自动变量，当执行到代码块时为变量分配内存，但是它作用域的起点是它的声明位置
* 如果在代码块内外出现了同名的自动变量，则在运行代码块时会隐藏外部变量，代码块运行结束后由重新可见
* 编译器先预留出 一段内存，并将其视为栈（后进先出），来完成对自动变量的管理
* 寄存器变量，使用关键字register来声明变量，它建议编译器使用CPU寄存器来存储自动变量，旨在提高访问变量的速度(在C++11中已经不怎么使用)

```C++
register int count_fast;
```

### 2.2静态持续变量

* 静态存储持续性变量的三种链接性
  * 外部链接性（全局变量）=>可在其他文件中访问=>代码块外面声明
  * 内部链接性=>只能在当前文件中访问=>代码块外面声明，并使用static修饰
  * 无链接性=>只能在当前函数或代码块中访问=>代码块内部声明，并使用static修饰
* 这三种链接性在整个程序执行期间存在，与自动变量相比，它们的寿命更长
* 静态变量的数目是固定的，编译器将分配固定的内存块来存储所有的静态变量

#### 2.2.1静态持续性+外部链接性

* 每个使用外部变量的文件中，都必须声明它
* 单定义规则
  * 变量只能有一次定义
  * 定义：给变量分配存储空间
  * 声明：不给变量分配存储空间，使用关键字extern，且不进行初始化
* 如果要使用外部变量，只需要在一个文件中包含该变量的定义（单定义规则），但在其他文件中必须使用extern声明它
* 仍然可能有多个变量的名称相同，并且局部变量会隐藏同名的全局变量

#### 2.2.2说明符和限定符

* 说明符
  * register
  * static
  * extern
  * thread_local
  * mutable
* cv限定符
  * const
  * volatile
    * mutable：指出即使结构（或类）变量为const，其某个成员也可以被修改
* 再谈const
  * 默认情况下全局变量的链接性是外部的，但是const全局变量的链接性是内部的（就像使用了static修饰一样）
  * 这是为了简化程序员的操作，因为如果是const全局变量是外部的话，必须额外使用extern修饰；但是视作内部链接就可以直接在其他文件中使用定义

### 2.3函数与链接性

* C++不允许在函数内部定义另一个函数=>所有函数的存储持续性都是静态的
* 可以使用static修饰使得函数仅能在对应文件中使用（函数和定义都必须使用static修饰）
* 对于链接性为外部的函数，只能有一个文件包含该函数的定义，但使用该函数的文件都应包含函数原型

### 2.4存储方案与动态分配

* 动态内存由new和delete来控制

* new运算符初始化（C++11）

```C++
int *arr = new int[4] {1, 2, 3 ,4};  //初始化列表
```

## 3.名称空间

### 3.1传统的名称空间

* 相关概念
  * 声明区域
  * 潜在作用域

### 3.2新的名称空间特性

* 创建名称空间
  * 名称空间可以是全局的，也可以位于另一个名称空间之中，但是不能位于代码块中。因此在默认情况下，在名称空间中声明的名称的链接性为外部的（除非它引用了常量）

```C++
namespace test
{
	double pail;
	void fetch();
	int pal;
	struct Well{};
}
```

* 名称空间是开放的，可以吧名称加入已有的名称空间中
  * 也可以对已经提供了原型的函数提供定义

```C++
namespace test
{
	char *goose(const char*); //添加函数原型
}

namespace test
{
    void fetch()  //添加函数定义
    {
      ...  
    };
}
```

* 作用域解析符::

```C++
test::pail = 1.23;  //访问命名空间中的名称
test::pal = 10;
```

#### 3.2.1using声明和using编译指令

* 使用

```C++
using test::pal;  //using声明，在作用域中使用的pal为名称空间test中的pal
using namespace test; //using编译指令，在名称空间中的所有名称都可以使用
```

* 对比
  * using声明更像是声明了相应的名称，如果某个名称已经在函数中声明了，就不能使用using声明了
  * using编译指令将对名称解析，如果已经被声明了名称，则局部名称将隐藏名称空间内的名称。不过仍然可以使用作用域解析运算符::

# 九.对象和类

## 1.抽象和类

```C++
#ifndef STOCK00_H_
#define STOCK0_H_
#include <string>
using namespace std;
class Stock //类声明
{
private:
	string company;
	long shares;
	double share_val;
	double total_val;
	void set_tot()
	{
		total_val = shares * share_val;
	}
public:
	void acquire(const string& co, long n, double pr);
    void buy(long num, double price);
    void sell(long num, double price);
    void update(double price);
    void show();
};
#endif
```

* C++使用class定义类设计
  * 此处的class和typename不同义了（之前在函数模板处二者都可以使用）
  * 访问控制
    * private：只能通过共有函数或友元函数访问对象的私有成员
    * public：使用类对象的程序都可以直接访问共有部分
    * protected：后续介绍
  * 封装
    * 将实现细节放在一起并将它们与抽象分开
    * 将类函数定义和类声明放在不同的文件
    * 数据隐藏不仅可以防止直接访问数据，还可以让开发者无需了解数据是如何被表示的
* 控制对成员的访问：共有还是私有
  * 数据常常放在私有部分，而组成类接口的成员函数放在共有部分
  * private是类对象的默认访问控制，在类声明的时候可以省略
* 实现类成员函数
  * 定义成员函数时，使用作用域解析运算符::来指出函数所属的类
  * 类方法可以访问类的private组件
  * 其定义位于类声明中的函数都将自动成为内联函数，因此Stock::set_tot()是一个内联函数
    * 也可以在类声明之外定义内联成员函数，只需在定义函数时使用inline限定符即可

```C++
#include<iostream>
#include"Stock00.h"

void Stock::acquire(const string& co, long n, double pr)
{
	company = co;
	shares = n;
	share_val = pr;
	set_tot();
}
void Stock::buy(long num, double price)
{
	shares += num;
	share_val = price;
	set_tot();
}
void Stock::sell(long num, double price)
{
	shares -= num;
	share_val = price;
	set_tot();
}
void Stock::update(double price)
{
	share_val = price;
	set_tot();
}
void Stock::show()
{
	cout << "Company: " << company << endl;
	cout << "Shares: " << shares << endl;
	cout << "Share Price:  $" << share_val << endl;
	cout << "Total Worth:  $" << total_val << endl;
}
```

* 方法使用哪个对象
  * 所创建的每个对象都有自己的存储空间，用于存储其内部变量和类成员
  * 但同一个类的所有对象共享一组类方法，即每种方法只有一个副本

```c++
kate.show();  //kate和joe都是Stock类的对象
joe.show();
```

* 使用类

```C++
#include "Stock00.h"

int main()
{
	Stock test;
	test.acquire("NanoSmart", 20, 12.50);
	test.show();
	test.buy(15, 18.125);
	test.show();
	test.sell(4, 20.00);
	test.show();
	test.buy(30000, 40.125);
	test.show();
	test.sell(30000, 0.125);
	test.show();
	return 0;
}
```

## 2.类的构造函数和析构函数

### 2.1构造函数

* 构造函数的定义
  * 构造函数的函数名就是类名
  * 但是不要用类成员变量名当做构造函数的参数名，这将会导致错误
    * 为了避免这种混乱，一种常见的做法是在数据成员名中使用m_前缀

```C++
Stock::Stock(const string &co, long n, double pr)
{	
	company = co;
    shares = n;
    share_val = pr;
    set_tot();
}
```

* 使用构造函数
  * 构造函数是用来创建对象的，而不能通过对象来调用

```C++
Stock test = Stock("World Cabbage", 250, 1.25); //显示调用构造函数
Stock test1("Furry Nason", 50, 2.5); //隐式调用构造函数
Stock *pstock = new Stock("Electroshock Games", 18, 19.0); //使用new动态分配内存，必须使用delete的析构函数
```

* 默认构造函数
  * 未提供显式初始值时，用来创建对象的构造函数
  * 当且仅当没有定义任何构造函数时，编译器才会提供默认构造函数
  * 为类定义了构造函数后，程序员就必须为它提供默认构造函数（
    * 使用默认参数
    * 通过重载来定义另一个构造函数——一个没有参数的构造函数
  * 在设计类时，通常应提供对所有类成员做隐式初始化的默认构造函数

```C++
Stock::Stock()
{
	company = "no name";
    shares = 0;
    share_val = 0.0;
    total_val = 0.0;
}
```

* 使用C++11的列表初始化

```c++
Stock test = {"World Cabbage", 250, 1.25}; //显示调用构造函数
Stock test1   {"Furry Nason", 50, 2.5}; //隐式调用构造函数
```

* const成员函数
  * 括号后的const表示该方法不会改变被隐式访问的对象

```C++
void show() const
{
	...
}
```



### 2.2析构函数

* 对象过期后，程序将自动调用析构函数，完成相应的清理工作
* 析构函数的名称：在类名前加上~

```C++
~Stock(); //析构函数原型
Stock::~Stock()
{
    cout << "Bye, " << company << endl;  //析构函数可以不承担任何工作，也就是不编写执行操作的代码
}
```

* 通常不应在代码中显式地调用析构函数

### 2.3改进Stock类

* 头文件

```C++
#pragma once
#ifndef STOCK10_H_
#define STOCK10_H_
#include <string>

using namespace std;
class Stock //类声明
{
private:
	string company;
	long shares;
	double share_val;
	double total_val;
	void set_tot()
	{
		total_val = shares * share_val;
	}
public:
	Stock();  //默认构造函数
	Stock(const string& co, long n, double pr);  //构造函数和析构函数都不需要用返回类型修饰
	~Stock(); //析构函数用~修饰
	void buy(long num, double price);
	void sell(long num, double price);
	void update(double price);
	void show();
};
#endif
```

* 实现文件

```C++
#include<iostream>
#include"Stock10.h"

Stock::Stock()  //默认构造函数
{
	std::cout << "Default Constructor Called." << std::endl;
	company = "No name";
	shares = 0;
	share_val = 0;
	set_tot();
}
Stock::Stock(const string& co, long n, double pr)
{
	std::cout << "Constructor Called." << std::endl;
	company = co;
	shares = n;
	share_val = pr;
	set_tot();
}
Stock::~Stock()  // 析构函数定义
{
	std::cout << "Bye, " << company << std::endl;
}
void Stock::buy(long num, double price)
{
	shares += num;
	share_val = price;
	set_tot();
}
void Stock::sell(long num, double price)
{
	shares -= num;
	share_val = price;
	set_tot();
}
void Stock::update(double price)
{
	share_val = price;
	set_tot();
}
void Stock::show()
{
	cout << "Company: " << company << endl;
	cout << "Shares: " << shares << endl;
	cout << "Share Price:  $" << share_val << endl;
	cout << "Total Worth:  $" << total_val << endl;
}
```

* 客户文件

```C++
#include"Stock10.h"

int main()
{
	Stock stock1("NanoSmart", 20, 20.0);
	stock1.show();
	Stock stock2 = Stock("Boffo Objects", 2, 2.0);
	stock2.show();
	stock2 = stock1;
	stock1.show();
	stock2.show();
	return 0;
}
```

## 3.this指针

* 虽然C++类中的成员变量无法直接访问，但是可以通过内联函数使用方法获取返回值

```C++
public:
	doubule total() const {return total_avl};
```

* 示例
  * 第三个const表示不会改变被隐式访问的对象
  * 第二个const表示不会改变被显式访问的对象
  * 因为将返回两个const Stock& 之一，所以用const修饰方法

```C++
const Stock& topval(const Stock& s) const;

top = stock1.topval(stock2);  //显式地访问Stock2，隐式地访问stock1，此时this指向stock1
top = stock2.topval(stock1);  //此时this指向stock2
```

* this指针：指向被用来调用成员函数的对象
  * this被称为隐藏参数传递给方法
  * this是一个指针，使用this调用方法是应该为：this->方法名

* 头文件

```C++
#pragma once
#ifndef STOCK10_H_
#define STOCK10_H_
#include <string>

using namespace std;
class Stock //类声明
{
private:
	string company;
	long shares;
	double share_val;
	double total_val;
	void set_tot()
	{
		total_val = shares * share_val;
	}
public:
	Stock();  //默认构造函数
	Stock(const string& co, long n, double pr);  //构造函数和析构函数都不需要用返回类型修饰
	~Stock();
	void buy(long num, double price);
	void sell(long num, double price);
	void update(double price);
	void show();
	const Stock& topval(const Stock& s) const;  //三个const含义各不相同
};
#endif
```

* 实现文件

```C++
#include<iostream>
#include"Stock10.h"

Stock::Stock()  //默认构造函数
{
	std::cout << "Default Constructor Called." << std::endl;
	company = "No name";
	shares = 0;
	share_val = 0;
	set_tot();
}
Stock::Stock(const string& co, long n, double pr)
{
	std::cout << "Constructor Called." << std::endl;
	company = co;
	shares = n;
	share_val = pr;
	set_tot();
}
Stock::~Stock()  // 析构函数定义
{
	std::cout << "Bye, " << company << std::endl;
}
void Stock::buy(long num, double price)
{
	shares += num;
	share_val = price;
	set_tot();
}
void Stock::sell(long num, double price)
{
	shares -= num;
	share_val = price;
	set_tot();
}
void Stock::update(double price)
{
	share_val = price;
	set_tot();
}
void Stock::show()
{
	cout << "Company: " << company << endl;
	cout << "Shares: " << shares << endl;
	cout << "Share Price:  $" << share_val << endl;
	cout << "Total Worth:  $" << total_val << endl;
}

const Stock& Stock::topval(const Stock& s) const
{
	return s.total_val > total_val ? s : *this;
}
```

## 4.对象数组

* 声明对象数组的方法与声明标准类型数组相同

```C++
Stock mystuff[4];
```

* 对象数组的初始化
  * 使用列表初始化
  * 但是必须为每个元素调用构造函数

```C++
Stock mystuff[2] = 
{
	Stock("test1", 10, 20.0);  //构造函数
	Stock();  //默认构造函数
}
```

## 5.类作用域

* 不能直接使用const来创建类作用域的常量

  * 因为声明类只是描述了对象的形式，没有创建对象，因此在创建对象前，声明的const int这类无意义，用于数组将报错

* 解决方法

  * 枚举
    * 在类声明中的枚举的作用域为整个类

  ```C++
  class Bakery
  {
  	private:
      	enum{Months = 12};
      	double costs[Months];
  }
  ```

  * 使用关键字static
    * 这将创建对应的常量，并与其他的静态变量存储在一起，而不是存储在对象中
    * 在类声明中创建的目的是让这个静态变量的作用域为类作用域

```C++
class Bakery
{
	private:
    	static const int Months = 12;
    	double costs[Months];
}
```

# 十.使用类

## 1.运算符重载

* C++多态
  * 函数重载（函数多态）
  * 运算符重载
    * C++根据操作数的数目和类型决定使用那种操作（例如*可以是解除引用，也可以是乘积）
* 运算符函数的特殊函数形式
  * 不能虚构新的运算符符号
  * 重载运算符后，编译器后续会使用相应的运算符函数替换运算符
    * result = object1 + object2 => result = object1.operator +(object2);
    * 对于连续的加法：t = t1+t2+t3=>t = t1.operator+(t2.operator+(t3))；可以发现仍然成立，这正是我们期望的

```C++
operatorop(argument-list);  //例如operator +()  operator *()
```

* 计算时间：一个运算符重载实例

  * 头文件

  ```C++
  #pragma once
  class Time
  {
  private:
  	int hours;
  	int minutes;
  public:
  	Time();
  	Time(int h, int m = 0);
  	void addMin(int m);
  	void addHr(int h);
  	void Reset(int h = 0, int m = 0);
  	Time operator +(const Time& t) const;  //重载加法运算符
  	void show() const;
  };
  ```

  * 实现文件

  ```C++
  #include"head.h"
  #include<iostream>
  
  Time::Time()
  {
  	hours = minutes = 0;
  }
  Time::Time(int h, int m = 0)
  {
  	hours = h;
  	minutes = m;
  }
  void Time::addMin(int m)
  {
  	minutes += m;
  	hours += minutes / 60;
  	minutes %= 60;
  }
  void Time::addHr(int h)
  {
  	hours += h;
  }
  void Time::Reset(int h = 0, int m = 0)
  {
  	hours = h;
  	minutes = m;
  }
  Time Time::operator +(const Time& t) const  //重载加法运算符
  {
  	int temp_h = 0, temp_m = 0;
  	temp_m = minutes + t.minutes;
  	temp_h = hours + t.hours + temp_m / 60;
  	temp_m %= 60;
  	Time temp = Time(temp_h, temp_m);
  	return temp;
  }
  void Time::show() const
  {
  	using std::cout;
  	cout << hours << " hours, " << minutes << " minutes.\n";
  }
  ```

  * 使用文件

```C++
# include "head.h"

int main()
{
	Time t1 = Time(2, 40);
	Time t2(5, 55);
	t1.show();
	t2.show();
	t1 = t1 + t2;  //使用重载运算符
	t1.show();
	return 0;
}
```

* 重载的限制
  * 重载后的运算符必须至少有一个操作数是用户定义的类型，这将防止用户为标准类型重载运算符
  * 使用重载运算符时不能违反运算符原来的句法规则，不能修改运算符的优先级
  * 不能创建新的运算符
  * 部分运算符不能重载，例如sizeof
  * =，()，，[]，->只能通过成员函数进行重载

## 2.友元

* 友元有三类
  * 友元函数
  * 友元类
  * 友元成员函数
* 友元函数：通过让函数成为类的友元，可以赋予该函数与类成员函数相同的访问权限（也就是可以访问到private的数据和方法了）
* 为什么需要友元
  * 问题：在上述重载二元运算符时，如果重载Time和double的乘法，那么t*2.7是合理的，但是2.7\*t则会报错，因为2.7不是Time类型
  * 成员函数总是会认为第一个参数是自身，因此可以使用非成员函数解决：Time operator *(double m, const Time &t);
  * 常规的非成员函数无法访问类的私有成员，但是有一类特殊的非成员函数可以，它们被称为友元函数
* 创建友元
  * 第一步：将原型放在类声明中，并在原型声明前加上关键在friend
    * 该原型意味着
      * 虽然operator*()函数实在类声明中声明的，但它不是成员函数，因此不能使用成员运算符来调用
      * 虽然operator*()函数不是成员函数，但它与成员函数的访问权限相同
  * 第二步：编写函数定义
    * 它不是成员函数，隐藏不使用Time::限定符
    * 在定义时不需要使用关键字friend
* 只有类声明可以决定哪一些函数是友元，因此类声明仍然控制了哪些函数可以访问私有变量
* 可以使用友元函数来反转操作数的顺序，然后就可以直接调用成员函数中的重载运算符函数了

```C++
friend Time operator*(double m, const Time &t);
```

### 2.1常用的友元：重载<<运算符

假设trip是一个Time对象

* <<的第一个重载版本
  * 考虑到一般的语法是cout << trip;显然我们需要一个友元函数，因为第一个参数是ostream类对象cout

```C++
void operator<<(ostream & os, const Time&t)
{
	os << t.hours << " hours, " << t.minutes << " minutes.";
}
```

* <<的第二个重载版本
  * 上述重载版本仅允许使用一个<<运算符
  * 输出代码为从左向右计算，为了能多次使用<<运算符，应当让重载后的运算符函数返回ostream对象

```C++
ostream & operator<<(ostream & os, const Time&t)
{
	os << t.hours << " hours, " << t.minutes << " minutes.";
    return os;
}
```

## 3.再谈重载：一个矢量类

* 使用状态成员
  * 这种成员描述的是对象所处的状态（可以用枚举来实现）enum 枚举名 {枚举可能的值};
  * 如果友元函数想使用枚举的状态变量，需要使用  类名::枚举值
    * 友元函数不再类作用域中，所以必须使用类名::限定符
    * 友元函数在名称空间中，所以不需要再用名称空间修饰
* 如果方法通过计算得到一个新的类对象，则应考虑是否可以使用类构造函数来完成这种工作。这样做不仅可以避免麻烦，而且可以确保新的对象是按照正确的方式创建的。
* 一元运算符和二元运算符
* 随机方法
  * 使用标准库cstdlib:  #include \<cstdlib>
    * rand()：返回0到某个值（取决于实现）的随机整数=>伪随机（10次调用将会生成10次相同的随机数），随机值用作下一次的随机种子
    * srand()：允许覆盖默认的种子值，重新启动另一个随机数序列
  * 使用标准库ctime：#include\<ctime>
    * time(0)：返回当前时间，可以当做随机种子

## 4.类的自动转换和强制类型转换

* 隐式转换
  * 条件：接受一个参数的构造函数
  * 方法：该构造函数会将于它参数类型相同的值转换为类（一个值->一个类对象）
  * 限制：只有接受一个参数的构造函数才能作为转换函数。如果一个接受多参数的构造函数有多个默认参数，只留下一个未知参数，那么它也可以作为构造函数。
  * 缺陷：这种隐式转换并非总是合乎需要的，偶尔会导致意外的类型转换。C++新增了explicit，可以使用explicit来修饰构造函数来关闭这种特性。

```C++
Stonewt(double lbs); //只有一个参数的构造函数
Stonewt myCat; //声明一个对象
myCat = 19.6;  //程序将构造函数Stonewt(double lbs)来创建一个临时的Stonewt对象，然后逐成员赋值=>隐式转换
explicit Stonewt(double lbs); //explicit关闭隐式转换
```

* 显示转换（显示强制转换）
  * explicit关闭了隐式转换，但是仍然支持显示转换
  * 同样只有接受一个参数的构造函数才能作为转换函数

```C++
explicit Stonewt(double lbs); //explicit关闭隐式转换
Stonewt myCat; //声明一个对象
myCat = Stonewt(19.6);  //显式转换，仍然是逐成员赋值
```

* 二步转换
  * 当且仅当转换不存在二义性时，才会进行二步转换（例如int->double，double->对象）

* 构造函数只用于从某种类型到类类型的转换，要进行相反的转换，必须使用特殊的C++运算符函数——转换函数。
  * 转换函数是用户自定义的强制类型转换，可以像强制类型转换那样使用它们。
  * 转换函数的注意点：
    * 转换函数必须是类方法
    * 转换函数不能指定返回类型（不能指定，不是void）
    * 转换函数不能有参数
  * 可以使用explicit来修饰转换函数，这就使得使用对应的转换函数时必须是显式的，这将会避免错误

```C++
operator typeName();  //声明转换函数，实例：operator double();
operator double()  //实现转换函数
{
    return pounds;
}
double test_double = double (test_object);  //使用自定义的强制类型转换
```

* 自动类型转换
  * 如果只有一种可行的转换，那么编译器会进行自动类型转换
  * 如果有多种可行的转换（也就是有二义性），那么编译器将会拒绝自动类型转换

# 十一.类和动态内存分配

## 1.动态内存和类

* 静态类成员
  * 无论创建了多少对象，程序都只创建一个静态类变量副本
  * 可以帮助类对象共享类私有数据
  * 可以在实现代码文件中对静态类成员进行初始化，但不能再类声明中初始化静态变量成员。这是因为类声明描述了如何分配内存，但并不分配内存。
  * 初始化语句不需要再使用static修饰
  * 对于不需要再进行修改的静态类成员，可以使用const或枚举创建 

```C++
static int test; //静态类成员变量
int ClassName::test = 10; //有变量类型, 有作用域限定符, 但是没有static修饰
```

* 动态内存
  * 在构造函数中使用new来分配内存，必须在相应的析构函数中使用delete来释放内存
  * 如果使用new[]来分配内存，必须使用delete[]来释放内存
* 特殊成员函数（C++自动定义的成员函数）
  * 默认构造函数：不进行任何操作，此时对象的值在初始化时是未知的
    * 如果定义了构造函数，C++将不会定义默认构造函数
    * 用户也能显式定义默认构造函数：这种构造函数没有任何参数，但是可以用来设置特定的值
    * 用于在定义默认构造函数时，应确保没有二义性，也就是如果没有参数，编译器只会执行一个构造函数
  * 默认析构函数：不进行任何操作
  * 复制构造函数：用于将一个对象复制到新创建的对象中
    * 它被用于初始化过程中（包括按值传递），而不是常规的赋值过程
    * 类的赋值构造函数原型通常如下：CLass_name(const Class_name &);
    * 何时调用复制构造函数：新建一个对象并将其初始化为同类现有对象时
      * 最常见的是将新对象显式地初始化为现有的对象
      * 每当程序生成了对象副本是，编译器都将使用复制构造函数（例如函数按值传递或函数返回对象时）=>使用函数时应该按引用传递对象，可以节省调用构造函数的时间以及存储新对象的空间
    * 默认复制构造函数的功能
      * 默认的复制构造函数逐个复制非静态成员（成员复制也成为浅复制），复制的是成员的值
        * 如果这个成员本身就是类对象，则使用这个类的复制构造函数来复制成员对象（也是复制非静态成员的值）
  * 赋值运算符
  * 地址运算符：默认返回this指针的值，影响不大

### 1.1复制构造函数存在的问题

* 复制构造函数的问题

  * 在创建对象副本时会使用复制构造函数，但是复制构造函数并没有说明相关的行为，可能导致其与自定义的构造函数、析构函数出现不匹配的问题

  * 复制构造函数是按值复制，如果遇到了字符串这种指针数据，创建副本时会将指针所指向的地址复制过来，在副本消失时又释放了指针指向的地址，这将会导致其他指向改地址的指针也无法使用，造成更大的问题

* 定义一个显式复制构造函数以解决问题

  * 通过自定义复制构造函数以解决复制构造函数与一般构造函数和析构函数行为不匹配的问题
  * 对于类设计中释放内存会导致的问题，可以采取的方法是深度复制。也就是说，复制构造函数应当复制字符串并将副本的地址传递给类成员。这样每个对象都有自己的字符串，而不是引用另一个对象的字符串。调用析构函数时都将释放不同的字符串。

* 什么时候需要显式定义复制构造函数

  * 在构造函数和析构函数中有一些相对应的操作，默认复制构造函数无法表现
  * 类中包含了使用new初始化的成员，需要使用深度复制，避免不同对象之间引用的释放冲突

* 复制构造函数的声明和定义

```C++
Class_name (const Class_name & st);  //复制构造函数的声明
Class_name::Class_name (const Class_name & st)  //复制构造函数的定义
{
    //描述复制构造函数
}
```

### 1.2赋值运算符

* C++允许类对象赋值，这是通过自动重载赋值运算符(=)实现的
  * 函数原型如下，它接受并返回一个指向类对象的引用
  * 将已有的对象赋值给另一个对象，可以使用重载的赋值运算符
  * 赋值运算符的隐式实现也是使用逐个复制（浅复制）来完成的

```
Class_name & Class_name::operator=(const Class_name &);
```

* 显然，赋值运算符存在的问题和复制构造函数存在的问题类似
  * 创造对象副本，析构函数和默认复制构造函数不匹配
  * 浅层复制，导致不同对象可以指向同一个地址，释放空间时出错
* 解决方法：提供赋值运算符（进行深度复制）定义
  * 注意点：
    * 由于目标对象可能引用了以前分配的内存，所以应使用delete[]来释放这些数据
    * 函数应当避免将对象付给自身；否则，给对象重新赋值前，释放内存操作可能删除对象的内容（因为你删除了内容，这个时候你后续再赋值也没用了）
    * 函数返回一个指向调用对象的引用（复制构造函数因为是构造函数，所以什么都不会返回）

## 2.改进后的string类

* 比较字符串#inlcude\<ctring>
  * strcmp(str1, str2)
    * 按字母排序（或者说按机器排序列），第一个字符串在第二个字符串之前，则返回一个负值
    * 如果字符串相同，则返回0
    * 第一个字符串在第二个字符串之后（>），则返回一个正值
* 重载中括号运算符
  * 中括号运算符是二元C++运算符，接受两个操作数
    * 第一个操作数位于中括号前面，也就是调用中括号的对象
    * 第二个操作数位于中括号中间，也就是需要访问数据的索引值

```C++
typeName &operator[](int i);
```

* 静态成员函数
  * 使用static修饰函数
  * 静态成员函数不能使用this指针，也不能通过对象调用静态成员函数
  * 如果静态成员函数是公有的，则可以通过类名和作用域解析符::来调用它
  * 静态成员函数只能使用静态数据成员

* 头文件

```C++
#include<iostream>

using std::ostream;
using std::istream;

class String
{
private:
	char* str;  //指向字符串的指针
	int len;  //字符串长度(不含空字符)
	
	static int num_strings;  //静态成员变量, 表示生成的对象的个数
	static const int CINLIM = 80;  //最大输入限制

public:
	//构造函数
	String();  //默认构造函数
	String(const char*);  //一般构造函数
	String(const String& s);  //复制构造函数, 特点是参数为对象本身的引用
	~String();  //析构函数

	//返回字符串长度
	int length() const { return len; }  //这种直接返回值的函数, 可以使用内联函数

	//重载赋值运算符(赋值运算符默认为浅复制)
	String& operator=(const String&);
	String& operator=(const char*);
	//重载中括号运算符
	char & operator[](int i);
	const char& operator[](int i) const;  //用于处理指向字符串常量时候的String

	//重载关系运算符
	friend bool operator<(const String& st1, const String& st2);
	friend bool operator>(const String& st1, const String& st2);
	friend bool operator==(const String& st1, const String& st2);

	//重载输入输出运算符
	friend ostream& operator<< (ostream & os, const String & st);
	friend istream& operator>>(istream& is, String& st);

	//静态成员方法, 只能访问静态成员变量
	static int HowMany();
};
```

* 实现文件

```C++
#include"head.h"
#include <cstring>

using std::cin;
using std::cout;

//初始化静态成员变量
int String::num_strings = 0;


//定义静态成员函数
int String::HowMany()
{
	return num_strings;
}

//定义构造函数
String::String()  //默认构造函数
{
	using std::strcpy;
	len = 4;
	str = new char[1];  //为了与析构函数中delete[]匹配, 需要在这里用new[]创建数组
	str[0] = '\0';
	num_strings++;
}

String::String(const char* s)  //一般构造函数
{
	len = std::strlen(s);
	str = new char[len + 1];  //+1是给空字符留位置
	std::strcpy(str, s);  //复制一个副本，并将指针指向副本的位置
	num_strings++;
}

String::String(const String& s)  //复制构造函数
{
	len = s.len;
	str = new char[len + 1];
	std::strcpy(str, s.str);  //深复制, 先复制一个副本, 再用指针指过去
	num_strings++;
}

String::~String()  //析构函数
{
	num_strings--;  //静态变量-1
	delete[] str;  //释放数组空间
}

//定义赋值运算符函数
String& String::operator=(const String& s)
{
	if (this == &s) return *this;  //赋值运算符函数需要避免将对象赋值给自身
	delete[]str;  //先释放原本指向的字符串空间
	len = s.len;
	str = new char[len + 1];
	std::strcpy(str, s.str);  //深复制, 先复制一个副本, 再用指针指过去
	num_strings++;
	return *this;
}

String& String::operator=(const char* s)
{
	delete[]str;
	len = std::strlen(s);
	str = new char[len + 1];
	std::strcpy(str, s);
	num_strings++;
	return *this;
}

//定义中括号运算符
char& String::operator[](int i)
{
	return str[i];
}

const char& String::operator[](int i) const
{
	return str[i];
}

//定义关系运算符(友元函数)
bool operator<(const String& s1, const String& s2)
{
	return (std::strcmp(s1.str, s2.str) < 0);
}

bool operator>(const String& s1, const String& s2)
{
	return (std::strcmp(s1.str, s2.str) > 0);
}

bool operator==(const String& s1, const String& s2)
{
	return (std::strcmp(s1.str, s2.str) == 0);
}

//重载输入输出
ostream& operator<<(ostream& os, const String& s)
{
	os << s.str;
	return os;
}

istream& operator>>(istream& is, String& s)
{
	char temp[String::CINLIM];
	is.get(temp, String::CINLIM);
	if (is) s = temp;  //这里使用了构造函数来进行隐式地数据转换
	while (is && is.get() != '\n')
		continue;
	return is;
}
```

## 3.在构造函数中使用new时应注意的事项

* 使用new初始化对象的指针成员时要特别小心
  * 构造函数中使用new，则应在析构函数中使用delete
  * new和delete必须兼容。new对应delete，new[]对应delete[]
  * 如果有多个构造函数，则应该以相同的方式使用new，要么都带中括号，要么都不带。因为只有一个析构函数，所有的构造函数都必须与它兼容。然而，可以在一个构造函数中使用new或new[]，而在另一个构造函数中将指针初始化为空，因为delete和delete[]都可以用于空指针
  * 应该定义一个复制构造函数，通过深度复制将一个对象复制给另一个对象（而不仅仅是复制地址）
  * 应该定义一个赋值运算符，通过深度复制将一个对象复制给另一个对象（需要返回引用，且避免将对象赋值给自身）

## 4.有关返回对象的说明

* 当成员函数或独立函数返回对象时，有3中返回方式可供选择
  * 返回指向对象的引用
  * 返回指向对象的const引用
  * 返回const对象

### 4.1返回指向const对象的引用

* 如果函数返回传递给它的对象，可以通过返回引用提高效率（传入啥，返回啥）=>例如对象比较
* 返回对象将调用复制构造函数（在返回时先创建一个副本，然后复制给外面的变量），而返回引用则不会调用复制构造函数（引用是对象的别名，不会额外创建临时对象，不过需要注意的是该引用的对象在外部也必须有效=>不是函数内部创建的引用）

### 4.2返回指向非const对象的引用 

* 两种常见的返回非const对象的情形：
  * 重载赋值运算符=>提高效率
    * operator=()的返回值用于连续赋值：s3=s2=s1;
    * s2.operator=()的返回值被赋值给s3，为此，返回String对象或String对象的引用都是可行的，但是返回引用可以避免函数调用复制构造函数来创建一个新的String对象
    * 根据上面的代码，重载后的赋值运算符实际上是进行了深度复制，然后返回自己的引用
  * 重载与cout一起使用的<<运算符=>必须这样做
    * 在operator<<()方法中，需要返回ostream&,因为如果返回ostream将会调用复制构造函数，但是ostream没有共有的复制构造函数

### 4.3返回对象

* 如果被返回的对象是被调用函数中的局部变量，则不应按引用的方式返回它，因为被调用函数执行完毕时，局部对象将调用析构函数。因此当控制权回到调用函数时，引用指向的对象将不再存在。在这种情况下，应返回对象而不是引用。
  * 通常被重载的算术运算符属于这一类（可以翻阅以前重载的算术运算，它们都在内部创建了新的对象，来避免额外的其他操作）

# 十二.类继承

* 类继承：从已有的类中派生出新的类，而派生类继承了原有类（成为基类）的特征，包括方法

## 1.一个简单的基类

* 从一个类派生出另一个类时，原始类成为基类，继承类称为派生类

* 基类头文件

```C++
#pragma once
//基类的头文件
#ifndef Table_H_
#define Table_H_

#include <string>
using std::string;

class TableTennisPlayer
{
private:
	string firstname;
	string lastname;
	bool hasTable;
public:
	TableTennisPlayer(const string& fn = "none",
		const string& ln = "none", bool ht = false);
	void Name() const;
	bool HasTable() const { return hasTable; };
	void ResetTable(bool v) { hasTable = v; };
};
#endif
```

* 基类实现文件

```C++
//基类的实现文件
#include "base.h"

#include <iostream>

TableTennisPlayer::TableTennisPlayer(const string& fn,
	const string& ln, bool ht) 
{
	firstname = fn;  //将会自动调用string类的赋值运算符进行深复制
	lastname = ln;
	hasTable = ht;
}

void TableTennisPlayer::Name() const
{
	std::cout << lastname << ", " << firstname;
}
```

### 1.1派生一个类

```C++
class RatedPlayer : public TableTennisPlayer
{
	...
}
```

* 上面的代码表示RatedPlayer类是从TableTennisPlayer类中派生来的
  * 冒号指出RatedPlayer类的基类是TableTennisPlayer类
  * public声明头表明TableTennisPlayer是一个公有基类，这被称为公有派生
  * 派生类对象包含基类对象，使用共有派生，基类的共有成员将成为派生类的共有成员
  * 基类的私有部分也将成为派生类的一部分，但是只能通过基类的共有和保护方法访问

* 派生类

  * 关于基类
    * 派生类继承了基类的数据成员（派生类继承了基类的实现）
    * 派生类对象可以使用基类的方法（派生类继承了基类的接口）
  * 还需要添加什么
    * 派生类自己的构造函数
    * 派生类可以根据需要添加额外的数据成员和成员函数

* 构造函数：访问权限的考虑

  * 派生类不能直接访问基类的私有成员，而必须通过基类方法进行访问=>具体的说，派生类构造函数必须使用基类构造函数

    ```C++
    derived::derived(type1 x, type 2 y): base(x, y)  //derived表示派生类, 使用初始化列表调用基类构造函数
    {
        ...
    }
    ```

  * 派生类构造函数的要点：

    * 首先创建基类对象
    * 派生类构造函数应通过成员初始化列表将基类信息传递给基类构造函数
    * 派生类构造函数应初始化派生类新增的数据成员

  * 在调用析构函数时，先调用派生类的析构函数，再调用基类的析构函数

* 加上派生类后的头文件

```C++
#ifndef Table_H_
#define Table_H_

#include <string>
using std::string;

//基类
class TableTennisPlayer
{
private:
	string firstname;
	string lastname;
	bool hasTable;
public:
	TableTennisPlayer(const string& fn = "none",
		const string& ln = "none", bool ht = false);
	void Name() const;
	bool HasTable() const { return hasTable; };
	void ResetTable(bool v) { hasTable = v; };
};

//派生类
class RatedPlayer : public TableTennisPlayer
{
private:
	unsigned int rating;  //新增数据成员
public:
	RatedPlayer(unsigned int r, const string& fn = "none",
		const string& ln = "none", bool ht = false);  //派生类的构造函数
	RatedPlayer(unsigned int r, TableTennisPlayer& tp);
	unsigned int Rating() const { return rating; };
	void ResetRating(unsigned int r) { rating = r; };
};
#endif
```

* 加上派生类后的实现文件

```C++
//基类的实现文件
#include "base.h"

#include <iostream>

TableTennisPlayer::TableTennisPlayer(const string& fn,
	const string& ln, bool ht) 
{
	firstname = fn;  //将会自动调用string类的赋值运算符进行深复制
	lastname = ln;
	hasTable = ht;
}

void TableTennisPlayer::Name() const
{
	std::cout << lastname << ", " << firstname;
}

RatedPlayer::RatedPlayer(unsigned int r, const string& fn,
	const string& ln, bool ht) : TableTennisPlayer(fn, ln, ht)
{
	rating = r;
}

RatedPlayer::RatedPlayer(unsigned int r, TableTennisPlayer& tp) : TableTennisPlayer(tp)
{
	rating = r;
}
```

* 派生类和基类之间的特殊关系
  * 派生类可以使用基类非私有的方法
  * 基类指针可以再不进行显式类型转换的情况下指向派生类对象
  * 基类引用可以再不进行显式类型转换的情况下引用派生类对象
  * 对应的，基类指针或引用只能调用基类方法

## 2.多态公有继承

* 多态：多种形态，即同一个方法的行为随上下文而异
* 用于实现多态公有继承的两种重要机制
  * 在派生类中重新定义基类的方法
  * 使用虚方法

* 头文件
  * 使用virtual修饰。程序将根据引用或指针指向的对象的类型来选择方法
    * 对于非虚方法，程序将运行其指针所表示的类的方法
    * 对于虚方法，程序将运行引用或指针所指向的具体的类的方法
  * 虚方法的特性使用起来非常方便，因此常常在基类中将派生类会重新定义的方法声明为虚方法
    * 方法在积累中被声明为虚后，它在派生类中将自动成为虚方法（当然，在派生类中使用virtual指出那些函数是虚函数也不失为一个好方法）
  * 在基类中声明虚析构函数是为了确保释放派生对象时，按正确的顺序调用析构函数
    * 如果派生类的有一个执行某些操作的析构函数，则基类必须有一个虚析构函数（即使这个析构函数什么也不做），这将保证正确的析构函数序列被调用
  * virtual仅用在类声明的方法原型中，实现时不再需要（和友元函数的friend相同）

```C++
#ifndef BRASS_H_
#define BRASS_H_
#include <string>

class Brass  //基类
{
private:
	std::string name;  //客户姓名
	long acctNum;  //账号
	double balance;  //当前结余
public:
	Brass(const std::string& s = "Nullbody", long an = -1, double bal = 0.0);  //构造函数
	void Deposit(double amt);  //存款
	virtual void Withdraw(double amy);  //取款，虚方法
	double Balance() const { return balance; };
	virtual void ViewAcct() const;  //虚方法
	virtual ~Brass();  //虚析构函数
};


class BrassPlus:public Brass  //派生类
{
private:
	double maxLoan;  //透支上限
	double rate;  //透支贷款利率
	double owesBank;  //当前的透支总额
public:
	BrassPlus(const std::string& s = "Nullbody", long an = -1, double bal = 0.0,
		double ml = 500, double r = 0.11125);
	BrassPlus(Brass& ba, double ml = 500, double r = 0.11125);
	virtual void ViewAcct() const;
	virtual void Withdraw(double amt);
	void ResetMax(double m) { maxLoan = m; };
	void ResetRate(double r) { rate = r; };
	void ResetOwes() { owesBank = 0; }
};
#endif
```

* 实现文件

```C++
#include "base.h"
#include <iostream>

using std::cout;
using std::endl;
using std::string;

//格式化
typedef std::ios_base::fmtflags format;
typedef std::streamsize precis;
format setFormat();
void restore(format f, precis p);

//Brass的方法实现
Brass::Brass(const std::string& s, long an, double bal)
{
	name = s;
	acctNum = an;
	balance = bal;
}

void Brass::Deposit(double amt)
{
	if (amt < 0) cout << "Error, the value of deposit is negative.";
	else
	{
		balance += amt;
	}
}

void Brass::Withdraw(double amt)
{
	format initialState = setFormat();
	precis prec = cout.precision(2);  //保留两位小数？
	if (amt < 0) cout << "Error, the value of withdraw is negative.";
	else if (amt <= balance) balance -= amt;
	else cout << "Error, the value of withdraw is bigger than your balance.";
	restore(initialState, prec);
}

void Brass::ViewAcct() const
{
	format initialState = setFormat();
	precis prec = cout.precision(2);  //保留两位小数？
	cout << "Client: " << name << endl;
	cout << "Account Number: " << acctNum << endl;
	cout << "Balance: $" << balance << endl;
	restore(initialState, prec);
}

//BrassPlus方法实现
BrassPlus::BrassPlus(const std::string& s, long an, double bal,
	double ml, double r): Brass(s, an, bal)
{
	maxLoan = ml;
	rate = r;
	owesBank = 0.0;
}

BrassPlus::BrassPlus(Brass& ba, double ml, double r): Brass(ba)  //这里会自动调用 string 自己的复制构造函数
{
	maxLoan = ml;
	rate = r;
	owesBank = 0.0;
}

void BrassPlus::ViewAcct() const
{
	format initialState = setFormat();
	precis prec = cout.precision(2);  //保留两位小数？

	Brass::ViewAcct(); //先调用基类的同名函数
	cout << "Maximum Loan: $" << maxLoan << endl;
	cout << "Owed to bank: $" << owesBank << endl;
	cout.precision(3);
	cout << "Loan Rate: " << 100*rate << "%" << endl;
	restore(initialState, prec);
}

void BrassPlus::Withdraw(double amt)
{
	format initialState = setFormat();
	precis prec = cout.precision(2);

	double bal = Balance();  //派生类没有对这个方法进行重定义，所以可以不用作用域解析符
	if (amt <= bal) Brass::Withdraw(amt);
	else if (amt <= bal + maxLoan - owesBank)
	{
		double advance = amt - bal;
		owesBank += advance * (1.0 + rate);
		Deposit(advance);
		Brass::Withdraw(amt);
	}
	else cout << "Exceeded！" << endl;

	restore(initialState, prec);
}

format setFormat()
{
	return cout.setf(std::ios_base::fixed, std::ios_base::floatfield);
}

void restore(format f, precis p)
{
	cout.setf(f, std::ios_base::floatfield);
	cout.precision(p);
}
```

## 3.静态联编和动态联编

* 函数名联编（binding）：将源代码中的函数调用解释为执行特定的函数代码块
  * 静态联编（早期联编）：在编译过程中进行联编
  * 动态联编（晚期联编）：编译器必须生成能够在程序运行时选择正确的虚方法的代码

* 指针和引用类型的兼容性
  * 一般的，C++不允许将一种类型的指针或引用赋给另一种类型的指针或引用
  * 然而指向基类的引用或指针可以引用派生类对象，而不必进行显式类型转换，称为**向上强制转换**=>该规则是is-a关系的一部分
    * 相反的过程，将基类指针或引用转换为派生类指针或引用（称为**向下强制转换**），如果不使用显式类型转换，则向下类型转换是不允许的

* 动态联编分析
  * 为什么有两种类型的联编以及为什么默认为静态联编
    * 虽然动态联编能够重新定义类方法，而静态联编在这方面很差，但是动态联编在效率和概念模型部分有不足
      * 效率：为了是程序在运行阶段进行决策，必须采取一些方法来跟踪基类指针或引用指向的对象类型，增加了额外的处理开销
        * 静态联编效率更高，因此被设置为C++的默认选择
      * 概念模型：在设计类时，可能包含一些不在派生类重新定义的成员函数（仅将那些预期被重写定义的方法声明为虚的）
  * 虚方法的工作原理
    * 给每个对象添加一个隐藏成员，隐藏成员保存了一个指向函数地址数组（虚函数表）的指针。虚函数表中存储了为表对象进行声明的虚函数的地址
    * 如果派生类提供了虚函数的新定义，该虚函数表将会保存新的地址；否则保存原始版本的地址。
    * 总之，使用虚函数在内存和执行速度方面有一定的成本，包括
      * 每个对象都将增大，增大量为存储地址的空间
      * 对于每个类，编译器都创建一个虚函数地址表（数组）
      * 对于每个函数调用，都需要执行一项额外操作，即到表中查找地址
* 虚函数的构造事项
  * 构造函数不应该是虚的（有顺序要求：先执行基类的构造函数，再执行派生类的部分）；析构函数应该是虚的（确保执行顺利）
    * 通常给基类提供一个虚析构函数，即使它不需要析构函数
  * 友元不能是虚函数，因为友元不是类成员。如果因为这个引起了问题，可以让友元函数使用虚成员函数来解决
  * 重新定义将隐藏方法：重新定义继承的方法并不是重载，无论参数列表是否相同，该操作将隐藏所有的同名基类方法
    * 经验规则一：如果重新定义继承的方法，应确保与原来的原型完全相同，但如果返回类型是基类引用或指针，则可以修改为指向派生类的引用或指针（返回类型协变）。
    * 经验规则二：如果基类声明被重载了，则应在派生类中重新定义所有的基类版本（如果只定义一个版本，则另外的版本将被隐藏，派生类对象将无法使用它们）。如果不需要修改，则新定义可只调用基类版本。

## 4.访问控制：protected

* 派生类可以直接访问基类的protected成员，但不能直接访问基类的private成员
  * 最好对类数据成员采用私有访问控制，不要使用保护访问控制；同时通过基类方法是派生类能够访问基类数据。

## 5.抽象基类（abstract base class, ABC）

* 纯虚函数：C++使用纯虚函数（pure virtual function）提供未实现的函数，纯虚函数声明的结尾处=0

```C++
virtual double Area() const =0;  //一个纯虚函数的声明
```

* 当类声明中包含纯虚函数时，则不能创建该类的对象=>包含纯虚函数的类只能用作基类
  * 要成为ABC，必须至少包含一个纯虚函数
  * 纯虚函数在ABC中可以定义，也可以不定义（在派生类中定义）

## 6.继承与动态内存分配

### 6.1情况一：派生类不使用new

* 不需要在派生类中定义析构函数、复制构造函数和赋值运算符

### 6.2情况二：派生类使用new

* 必须为派生类定义显式析构函数、复制构造函数和赋值运算符

* 头文件

```c++
#ifndef DMA_H_
#define DMA_H_

#include <iostream>

//基类
class baseDMA
{
private:
	char* label;
	int rating;
public:
	baseDMA(const char* l = "null", int r = 0);  //构造函数(含默认构造函数)
	baseDMA(const baseDMA& r); //复制构造函数
	virtual ~baseDMA();  //虚析构函数
	baseDMA& operator=(const baseDMA& r); //重载赋值运算符
	virtual friend std::ostream& operator<<(std::ostream& os, const baseDMA& r);  //重载<<便于输出
};

//不使用new的派生类，不需要自定义析构函数、复制构造函数和重载赋值运算符
class lacksDMA :public baseDMA
{
private:
	static const int COL_LEN = 40;
	char color[COL_LEN];
public:
	lacksDMA(const char* c = "blank", const char* l = "null", int r = 0);
	lacksDMA(const char* c = "blank", const baseDMA& r);
	virtual friend std::ostream& operator<<(std::ostream& os, const baseDMA& r);
};

//使用new的派生类，需要自定义析构函数、复制构造函数和重载赋值运算符
class hasDMA : public baseDMA
{
private:
	char* style;
public:
	hasDMA(const char* c = "none", const char* l = "null", int r = 0);
	hasDMA(const char* c = "none", const baseDMA& r);
	hasDMA(const hasDMA& h);
	hasDMA& operator=(const hasDMA& h);
	virtual ~hasDMA();
	virtual friend std::ostream& operator<<(std::ostream& os, const baseDMA& r);
};
#endif
```

* 实现文件

```C++
#include "base.h"
#include <cstring>

//基类方法实现
baseDMA::baseDMA(const char* l, int r)
{
	label = new char[std::strlen(l) + 1];
	std::strcpy(label, l);
	rating = r;
}

baseDMA::baseDMA(const baseDMA& r)
{
	label = new char[std::strlen(r.label) + 1];
	std::strcpy(label, r.label);
	rating = r.rating;
}

baseDMA::~baseDMA()
{
	delete[] label;
}

baseDMA& baseDMA::operator=(const baseDMA& r)
{
	if (this == &r)
	{
		return *this;  //赋值运算符应避免将对象赋值给自身
	}
	delete[] label;  //否则在释放内存后会导致后续流程无法顺利进行
	label = new char[std::strlen(r.label) + 1];
	std::strcpy(label, r.label);
	rating = r.rating;
	return *this;
}

std::ostream& operator<<(std::ostream& os, const baseDMA& r)
{
	os << "Label: " << r.label << std::endl;
	os << "Rating: " << r.rating << std::endl;
	return os;
}

//lacksDMA方法实现
lacksDMA::lacksDMA(const char* c, const char* l, int r)
{
	baseDMA(l, r);  //调用基类构造函数
	std::strncpy(color, c, 39);
	color[39] = '\0';
}

lacksDMA::lacksDMA(const baseDMA& r, const char* c)
{
	baseDMA(r);
	std::strncpy(color, c, 39);
	color[39] = '\0';
}

std::ostream& operator<<(std::ostream& os, const lacksDMA& r)
{
	os << (const baseDMA&) r;  //根据指针类型, 调用baseDMA的<<方法
	os << "Color: " << r.color << std::endl;
	return os;
}

//hasDMA方法实现
hasDMA::hasDMA(const char* c, const char* l, int r)
{
	baseDMA(l, r);
	style = new char[std::strlen(c) + 1];
	std::strcpy(style, c);
}

hasDMA::hasDMA(const baseDMA& r, const char* c)
{
	baseDMA(r);
	style = new char[std::strlen(c) + 1];
	std::strcpy(style, c);
}

hasDMA::hasDMA(const hasDMA& r)
{
	baseDMA(r);  //只会传入baseDMA的部分=>隐式向上转换
	style = new char[std::strlen(r.style) + 1];
	std::strcpy(style, r.style);
}

hasDMA::~hasDMA()
{
	delete[] style;
}

hasDMA& hasDMA::operator=(const hasDMA& r)
{
	if (this == &r)
	{
		return *this;
	}
	delete[] style;
	baseDMA(r);  //只会传入baseDMA的部分=>隐式向上转换
	style = new char[std::strlen(r.style) + 1];
	std::strcpy(style, r.style);
	return *this;
}

std::ostream& operator<<(std::ostream& os, const hasDMA& r)
{
	os << (const baseDMA&)r;
	os << "Style: " << r.style << std::endl;
	return os;
}
```

# 十三.C++中的代码重用

## 1.包含对象成员的类

### 1.1valarray类简介

* valarray类是由头文件valarray支持的

```C++
valarray<int> q_values;
valarray<double> weights;

//特殊的构造函数
valarray<int> v (10, 8); //包含8个元素的数组, 每个值设置为8
```

* valarray中的常用方法
  * operator\[]()：访问个元素
  * size():返回元素数
  * sum():返回所有元素之和
  * max()：返回最大值
  * min()：返回最小值

### 1.2Student类的设计

* Student使用string保存学生姓名和valarray保存成绩，Student类的成员函数可以使用string和valarray类的公有接口来访问和修改name和scores对象，但在类的外面不允许这样做
  * 这被称为Student类获得了其成员对象的实现，但没有继承接口（获得接口是is-a关系的组成部分）
  * 使用组合，类可以获得实现，但是不能获得接口（has-a的组成部分）
* 在has-a关系中，各成员对象可以分别使用 成员名(参数列表)的方式完成初始化，并使用逗号分割（初始化列表）
  * 初始化顺序为变量声明的顺序，在需要使用一个成员变量去初始化另一个成员变量的时候尤其需要注意
* 被包含的对象的接口不是公有的，但可以在类方法中使用它（但在外面不能使用了，直接原因是因为一般类的成员变量是私有的，无法访问）

## 2.私有继承

* C++还有另一种实现has-a关系的途径——私有继承
  * 私有继承同样是获得实现，但不获得接口
  * 进行私有继承时，使用关键字private
  * 私有继承隐式地继承组件，因此很多时候不能再使用具体的变量名来描述对象了。相对的，可以直接使用类名来调用构造函数完成初始化
  * 访问基类方法：在私有继承中，可以使用类名和作用域解析符来调用基类方法
  * 访问基类对象：由于派生类是由基类派生而来的，因此可以使用强制类型转换，将派生类对象转换为基类对象
  * 访问基类友元函数：同样，利用显式转换，将派生类对象转换为基类对象，这时就可以自动访问基类友元函数了
* 多重继承（multiple inheritance，MI）：使用多个基类的继承
* 使用包含还是私有继承
  * 大多数情况下使用包含=>易于理解
  * 继承会使关系更抽象，也会引起很多问题，尤其从多个基类继承时
  * 私有继承具备更多的特性：可以再派生类中使用protected数据；可以重新定义虚函数
* 保护继承：私有继承的变体，将基类的公有成员和保护成员变为派生类的保护成员

## 3.多重继承

* 多重继承描述的是由多个直接基类的类，公有MI表示的也是is-a关系
  * 必须使用public来限定每一个基类，否则，编译器默认使用私有派生
  * 多重继承会带来更多的问题，因此应当谨慎、适度地使用多重继承

```
class SingingWaiter : public Waiter, public Singer{...};
```

* 虚基类

  * 虚基类使得从多个类（它们的基类相同）派生出的对象只继承一个基类对象
  * 通过在类声明中使用关键字virtual，可以使基类成为虚基类（virtual 和 public的次序无关紧要）

  ```C++
  class Singer: virtual public Worker{};  //虚基类
  class Waiter: virtual public Worker{};
  class SingingWaiter: public Singer, public Waiter{};  //使用一个Worker对象, 而不是引入自己的Worker对象副本
  ```

  * 新的构造函数：
    * 对于非虚基类，唯一可以出现在初始化列表中的构造函数即是基类构造函数
    * 对于虚基类，C++禁止信息通过中间类自动传递给基类，需要显式地调用虚基类的构造函数，再使用基类的构造函数完成对其他成员变量的初始化

```C++
SingerWaiter(const Worker &wk, int p=0, int v = Singer::other) :Worker(wk), Waiter(wk, p), Singer(wk, v){}
//对于虚基类必须显式地调用Worker(const Worker&wk)
//对于非虚基类，这样是违法的
//显然，在各个间接基类中需要实现类名(虚基类&, 额外的成员变量参数列表)方法
```

* 哪个方法？
  * 多重继承可能会导致函数调用的二义性：不重新定义方法，且对应的方法名在多个基类中都有实现
  * 解决方法
    * 可以使用作用域解析符来澄清编程者的意图
    * 更好的方法是在派生类中重新定义重名方法
* 更多问题
  * 混合使用虚基类和非虚基类：当类通过多条虚途径和非虚途径继承某个特定的基类时，该类将包含一个表示所有的虚途径的基类子对象和分别表示各条非虚途径的基类子对象

## 4.类模块

* 同样使用template\<Class Type>来完成类模板的定义
  * class并不意味着Type必须是一个类；而是表明Type是一个通用的类型说明符
  * 较新的C++实现允许在这种情况下使用不太容易混淆的关键字啊typename取代class，也就是template\<typename Type>
* 由于模板不是函数，不能单独进行编译。模板必须与特定的模板实例化请求一起使用
  * 最简单的方法是将所有模板信息放在一个头文件中，并在要使用这些模板的文件中包含该头文件

```C++
//创建类模板
template<typename Type>  //模板声明
class Stack
{
private:
	static const int MAX = 10;  //类静态常量
	Type items[MAX];  //保存数据
	int top; //保存栈顶
public:
	Stack();  //构造函数
	bool isEmpty();
	bool isFull();
	bool push(const Type& item);
	bool pop(Type& item);  //弹出栈顶给item
};

//模板类实现
//由于模板不是函数，不能单独进行编译。模板必须与特定的模板实例化请求一起使用
//最简单的方法是将所有模板信息放在一个头文件中，并在要使用这些模板的文件中包含该头文件

template<typename Type>
Stack<Type>::Stack()
{
	top = 0；
}

template<typename Type>
bool Stack<Type>::isEmpty()
{
	return (top == 0);
}

template<typename Type>
bool Stack<Type>::isFull()
{
	return (top == MAX);
}

template<typename Type>
bool Stack<typename Type>::push(const Type& item)
{
	if (isFull()) return false;
	items[top] = item;
	top += 1;
	return true;
}

template<typename Type>
bool Stack<Type>::pop(Type& item)
{
	if (isEmpty()) return false;
	item = items[--top];
	return true;
}
```

* 使用模板类
  * 仅在程序中包含模板并不能生成模板类，而必须请求实例化
    * 程序将对应地生成类声明和独立的类方法

```C++
Stack<int> kernels;
Stack<string> colonels;
```

* 指针栈
  * 正确使用指针栈的方法：让调用程序提供一个指针数组，其中每个指针都指向不同的字符串。这样就可以把指针放入栈中。
  * 栈是什么，就把什么存进去，可能需要注意特定的实现
  * 在模板类的实现过程中，可以再赋值运算符函数的返回类型声明为对应的引用（例如Stack&），这实际上是Stack\<Type>的缩写，只能在类中使用。
* 数组模板示例和非类型参数
  * 非类型（表达式）参数的缺陷
    * 只能是整形、枚举、引用或指针
    * 模板代码不能修改该参数的值，也不能使用参数的地址
    * 实例化模板时，用作表达式参数的值必须是常量表达式（和创建数组时类似，因为在模板代码中就是用的数组来管理数据）
  * 优点：表达式参数方法使用的是为自动变量维护的内存站，执行速度更快
  * 缺点：每种数组大小都将生成自己的模板

```C++
template<typaname T, int n>  //该模板包含一个类型参数T和一个非类型参数n
```

### 4.1模板多功能性

#### 4.1.1常规类技术应用于模板类

* 技术汇总
  * 模板类可用作基类
  * 模板类可用作组件类
  * 模板类可用作其他模板的类型参数

#### 4.1.2递归使用模板

```C++
ArrayTP<ArrayTP<int, 5>, 10> twodee; //twodee是包含10个元素，每个元素是长度为5的int类型数组，等效于int twodee[10][5];
//注意在模板语法中，为的顺序与等价的二维数组相反
```

#### 4.1.3使用多个类型参数

```C++
template<typename T1, typename T2>;  //有两个类型参数
```

#### 4.1.4默认类型模板参数

```C++
template<typename T1, typename T2=int>;  //有两个类型参数, 其中T2默认为int
```

### 4.2模板的具体化

* 类模板与函数模板很相似

  * 具体化

    * 隐式实例化：在声明一个或多个对象时，指出所需的类型，编译器使用通用模板提供的处方生产具体的类定义

      ```C++
      ArrayTP<int 10> stuff;  //这种一般的方法就是隐式实例化
      ```

    * 显式实例化：使用关键字template并指出所需类型来声明类时，编译器将生成类声明的显式实例化。声明必须位于模板定义的名称空间中

      ```C++
      template class ArrayTP<string, 10>;
      ```

    * 显式具体化：特定类型的定义，在为特殊类型实例化时，对模板进行修改，使其行为不同

      ```C++
      template<> class Classname<特定的类型名称> {};
      ```

### 4.3成员模板

* 模板可用作结构、类或模板类的成员
  * 要完全实现STL的设计，必须使用这项特性

```C++
#include <iostream>
using std::cout;
using std::endl;

template<typename T>  //使用模板声明
class beta
{
private:
	template<typename V>  //使用模板类作为模板类的成员
	class hold
	{
	private:
		V val;
	public:
		hold(V v = 0) { val = v; }
		void show() const { cout << val << endl; }
		V Value() { return val; }
	};

	hold<T> q;  //基于模板类的对象作为类成员
	hold<int> n;
public:
	beat(T t, int i) : q(t), n(i) {}
	template<typename U>  //使用模板函数作为成员方法
	U blab(U u, T t) { return (n.Value() + q.Value() * u / t; }
	void show const{ q.show(); n.show(); }
};
```

* 还可以将模板类当作参数

### 4.4模板类和友元

* 模板类声明可以有友元。模板的友元分为3类
  * 非模板友元
  * 约束模板友元，即友元的类型取决于类被实例化时的类型
  * 非约束模板友元，即友元的所有具体化都是类的每一个具体化的友元

* 非模板友元

  * 在模板类中将一个常规函数声明为友元

    ```C++
    template<typename T>
    class HasFriend
    {
    public:
    	friend void counts();  //所有HasFriend实例的友元
    }
    ```

  * 上述声明使counts()函数称为模板所有实例化的友元，例如HasFriend\<int>和HasFriend\<string>

    * counts不是通过对象该调用的，也没有对象参数
    * 可以访问全局变量；也可以使用全局指针访问非全局对象；可以访问对立与对象的模板类的静态数据成员

  * 进一步为友元函数提供模板类参数：friend void counts(HasFriend\<T> &)

    * 注意上述参数不能写HasFriend &，因为这并不是一个确定的类，而是一个模板

    * 带HasFriend\<int>参数的counts会变成HasFriend\<int>的友元

    * 带HasFriend\<double>参数的counts会是counts的重载——它是HasFriend\<double>的友元

    * 注意，此时counts并不是模板函数，而只是使用一个模板作参数。这意味着必须为要使用的友元定义显式具体化

      ```C++
      void counts(HasFriend<int> &) {};
      void counts(HasFriend<double> &) {};
      ```

* 约束模板友元

  * 两次声明

    * 首先，在类定义的前面声明每个模板函数

    * 然后，在类中再次将模板函数声明为友元

      ```C++
      //在类定义的前面声明每个模板函数=>作用：然友元函数变成模板函数
      template<typename T> void counts();
      template<typename T> void report(T &);
      
      //在类中再次将模板函数声明为友元=>作用：使用友元函数
      template <typename TT>
      class HasFriend
      {
      public：
          friend void counts<TT>();
          friend void report<TT>(HasFriend<TT> &);
      }
      ```

* 非约束模板友元

  * 可以在类内部声明模板，创建非约束友元函数。每个函数具体化都是每个类具体化的友元

    ```C++
    template<typename T>  //模板类
    class HasFriend
    {
    public:
    	template<typename C, typename D> friend void show2(C &, D&);  //非约束模板友元
    }
    ```

# 十四.友元、异常和其他

## 1.友元

* 友元类声明可以位于公有、私有或保护部分，其所在的位置无关紧要

  * 友元类声明

    ```C++
    friend class Remote;
    ```

* 友元成员函数

  * 可以选择让特定的类成员成为另一个类的友元，而不必让整个类成员友元

    * 这样做比较麻烦，要编译下面的语句，需要将Remote的定义放在Tv前面。但是由于该方法需要使用Tv，又需要将Tv定义位于Remote前面
    * 避开这种循环依赖的方法是：前向声明（forward declaration）

    ```C++
    friend void Remote::set_chan(Tv &t, int c);  //Remote是另一个类, 该声明让Remote类中的set_chan方法成为友元
    ```

    ```C++
    class Tv;  //前向声明
    class Remote {};
    class Tv {};
    ```

    * 对于那些在友元类中提前使用到的私有数据，由于现在Tv类的定义在Remote类之后了，Tv类的成员变量和成员方法第一时间无法知道，无法使用内联函数实现

      * 解决方法是在友元类中只包含方法声明，并将实际的定义放在Tv类后面

        ```C++
        class Tv;  //前置声明
        class Remote {};
        class Tv {};
        //将Remote方法的定义放在class Tv的声明后面
        ```

* 互为友元
  * 两个互为友元的类在声明时有前后关系，注意到前面的类在使用**后面的类的方法**时，在类中只能先声明原型，具体的实现必须等后面的你的类声明后才能定义
* 共同友元：
  * 一个类或者方法是两个或更多的类的友元

## 2.嵌套类

* 在另一个类中声明的类被称为嵌套类，它通过提供新的类型类作用域来避免名称混乱
  * 包含类的成员函数可以创建和使用被嵌套的类的对象
  * 仅当声明位于公有部分，才能在包含类的外面使用嵌套类，而且必须使用作用域解析运算符
  * 对类进行嵌套是为了帮助实现另一个类，并避免名称冲突
* 对类进行嵌套与包含并不同
  * 包含意味着将类对象作为另一个类的成员
  * 对类嵌套不创建类成员，而是定义一种类型，该类型仅在包含嵌套类声明的类中有效

## 3.异常

* 调用abort()
  * abort()函数的原型位于头文件cstdlib中
  * abort()会返回一个随实现而异的值

```C++
#include<iostream>
#include<cstdlib>

double hmean(double a, double b);

int main()
{
	double x, y, z;
	x = 1.0;
	y = 2.0;
	z = -1.0;
	std::cout << "the result of x and y is " << hmean(x, y) << std::endl;
	std::cout << "the result of x and z is " << hmean(x, z) << std::endl;
	return 0;
}

double hmean(double a, double b)
{
	if (a == -b)
	{
		std::cout << "Error!" << std::endl;
		std::abort();
	}
	return 2.0 * a * b / (a + b);
}
```

* 使用错误码
  * 一种比异常终止更灵活的方法，使用函数的返回值来指出问题
  * 可以使用指针参数或引用参数将值返回给程序，并使用函数的返回值来指出成功还是失败

```C++
#include<iostream>
#include<cstdlib>

bool hmean(double a, double b, double & ans);

int main()
{
	double x, y, z;
	double answer;
	x = 1.0;
	y = 2.0;
	z = -1.0;
	std::cout << "the result of x and y is " << hmean(x, y, answer) << std::endl;
	std::cout << "the result of x and z is " << hmean(x, z, answer) << std::endl;
	return 0;
}

bool hmean(double a, double b, double & ans)
{
	if (a == -b)
	{
		ans = 0;
		return false;
	}
	ans = 2.0 * a * b / (a + b);
	return true;
}
```

* 异常机制
  * 异常机制是对程序运行过程中发生异常情况的一种响应。异常提供了将控制权从程序的一部分传递给另一个部分的途径。
  * 对异常的处理有3个组成部分
    * 引发异常：throw
    * 使用处理程序捕获异常：catch
    * 使用try块：try
  * throw关键字表示引发一场，紧随其后的值（例如字符串或对象）指出了异常的特征
    * 异常类型可以是字符串，通常是类
    * throw
    * throw不是将控制权返回给调用程序，而是导致程序延函数调用序列后退，直到找到包含try块的函数
  * catch关键字表示捕获异常
    * 随后是位于括号中的类型声明，它指出了一场处理程序要响应的异常类型
    * 然后是一个用花括号括起的代码块，指出要采取的措施
    * 如果try块中没有异常，就跳过try块后面的catch块，直接执行程序后面的第一条语句
  * try块表示其中特定的异常可能被激活的代码块，它后面跟一个或多个catch块
    * try块是由关键字try指示的
    * 关键字try的后面是一个由花括号括起的代码块，表明需要注意这些代码引发的异常

```C++
#include<iostream>
#include<cstdlib>

double hmean(double a, double b);

int main()
{
	double nums[3] = { 1.0, 2.0, -2.0 };
	for (int i = 0; i < 2; i++)
	{
		try //引起try块
		{
			std::cout << hmean(nums[i], nums[i + 1]) << std::endl;
		}
		catch (const char* s)  //catch引起异常处理程序
		{
			std::cout << s << std::endl;  //处理异常信息
			std::cout << "Error!" << std::endl;
		}
		
	}
	return 0;
}

double hmean(double a, double b)
{
	if (a == -b) throw "bad hmean() arguments: a=-b not allowed";
	return 2.0 * a * b / (a + b);
}
```

* 将对象用作异常类型
  * 通常，引发对象的函数将传递一个对象
    * 可以使用不同的异常类型来区分不同的函数在不同情况下引发的异常
    * catch块可以根据这些信息来决定采取什么样的措施

```C++
//异常类
class bad_hmean
{
private:
    int v1;
    int v2;
public:
    bad_hmean(int a = 0, b= 0): v1(a), v2(b) {}
    void mesg();
};

inline void bad_hmean::mesg()
{
    std::cout << "error!" << std::endl;
}

//捕获异常类
try 
{
   ... 
}
catch (bad_hmean & hg)
{
    ...
}
```

* throw部分是异常规范，在C++11中摒弃它
* 栈解退：当程序由于函数出现异常时，程序将释放栈中的内存，但不会在释放站的第一个返回位置停止，而是会继续释放栈，直到找到第一个位于try块的返回地址（并且对应的catch能正确捕获对应的异常），随后将控制权转到块尾的异常处理程序。

### 3.1exception类

* exception头文件中定义了exception类，C++可以把它用作其他类的基类

```C++
#include<exception>
class bad_hmean : public std::exception
{
public:
    const char* what() {return "bad arguments to hemean()";}
    ...
}
```

## 4.RTTI

* RTTI是运行阶段类型识别（Runtime Type Identification）
  * 只能将RTTI用于包含虚函数的类层次结构，因为只有对于这种类层次结构，才应该将派生对象的地址赋给基类指针

### 4.1dynamic_cast运算符

* dynamic_cast运算符是最常用的RTTI组件，回答“是否可以安全地将对象的地址赋给特定类型的指针”

```C++
Superb *pm = dynamic_cast<Superb *>pg;
//指针pg的类型是否可以安全地转换为Superb*
//如果可以，运算符将返回对象的地址
//否则返回一个空指针
```

# 十五.string类和标准模板库

## 1.string类

* 由头文件string支持
* string的输入：
  * cin>>string：读取一个字符
  * getline(cin, stuff)：读取一行, 并无视换行符
    * 自动调整大小的功能让string版本的getline()不需要指定读取多少个字符的数值参数
