[toc]

记录学习C++过程中的知识点和疑惑，内容主要来自 **学堂在线-清华大学-郑莉《C++语言程序设计》**和**《C++高级编程》**

# 面向过程

## 数据类型

 C标准中并没有具体给出规定那个基本类型应该是多少字节数，而且这个也与机器、OS、编译器有关，比如同样是在32bits的操作系统，VC++的编译器下int类型为占4个字节；而tuborC下则是2个字节。

所以int，long int，short int的宽度都可能随编译器而异。但有几条铁定的原则（ANSI/ISO制订的）：

sizeof(short int)<=sizeof(int)
sizeof(int)<=sizeof(long int)
short int至少应为16位（2字节）
long int至少应为32位。 

| 类型                                                         | 32位编译器 | 64位编译器 |
| ------------------------------------------------------------ | ---------- | ---------- |
| char                                                         | 1          | 1          |
| char*                                                        | 4          | 8          |
| short int                                                    | 2          | 2          |
| int                                                          | 4          | 4          |
| unsigned int                                                 | 4          | 4          |
| float                                                        | 4          | 4          |
| double                                                       | 8          | 8          |
| long                                                         | 4          | 8          |
| long long                                                    | 8          | 8          |
| unsigned long                                                | 4          | 8          |
| long long                                                    | 8          | 8          |
| unsigned long                                                | 4          | 8          |

==char* ：指针变量，32位的寻址空间是2^32,  即32个bit，也就是4个字节。同理64位编译器==

## 常用I/O流类库操作符

控制输入输出格式

| 操作符             | 含义                               |
| ------------------ | ---------------------------------- |
| dec                | decimal十进制表示                  |
| hex                | hexadecimal十六进制表示            |
| oct                | octonary八进制表示                 |
| ws                 | 提取空白符                         |
| endl               | 插入换行符并刷新流                 |
| setsprecision(int) | 设置浮点数的小数位数（包括小数点） |
| setw(int)          | 设置域宽                           |

我特么终于明白那个冷笑话`oct31==dec25`

## 控制流

### if else

```c++
if(){
	if(){
        pass
    }
    else
        pass
}
else
    pass
```

### switch case

```c++
int main() {
	int day;
	cin >> day;
	switch (day) {
	case 0:cout << "Sunday" << endl; break;
	case 1:cout << "Monday" << endl; break;
	case 2:cout << "Tuesday" << endl; break;
	case 3:cout << "Wednesday" << endl; break;
	case 4:cout << "Thursday" << endl; break;
	case 5:cout << "Friday" << endl; break;
	case 6:cout << "Saturday" << endl; break;
	default:
		cout << "Maybe input error" << endl; break;
	}
	return 0;
}
```

### while

```c++
#include <stdio.h>
#include <iostream>
using namespace std;
//计算x的n次方
double power(double x,int n){
    double val=1.0;
    while(n--)//当n减至0时为false退出循环
        val*=x;
    return val;
}

int main(){
    double pow;
    pow=pow(5,2);
    cout<<"result is"<<pow<<endl;
    return 0;
}
```

#### do-while

```c++
#include <stdio.h>
#include <iostream>
using namespace std;
int main() {
	int n, right_digit, newnum = 0;
	cout << "Enter the number:";
	cin >> n;
	cout << "The number in reverse order is:";
	do {
		right_digit = n % 10;
		cout << right_digit;
		n /= 10;
	} while (n != 0);
	cout << endl;
	return 0;
}
```

上边的这个例子是一个蛮有意思的翻转数字算法，我本来想的是翻转字符串式的方法，还是相形见绌。

**do-while和while的区别是：do-while是先执行的控制体内的语句然后判断条件的，而while先判断条件才执行控制体内的语句。**

### for

```c++

```

输入一系列整数，统计出整数个数i和负整数个数j，读入0则退出

```c++
#include <stdio.h>
#include <iostream>
using namespace std;
int main() {
    int i = 0,j = 0,n;
    cout<<"Enter some integers (please enter 0 to quit):"<<endl;
    cin>>n;
    while(n != 0){
        if(n>0)i+=1;
        if(n<0)j+=1;
        cin>>n;
    }
    cout<<"Count of positive integers:"<<i<<endl;
    cout<<"Count of negative integers:"<<j<<endl;
	return 0;
}
```



## 条件运算符

**表达式1？表达式2：表达式3**

**其中表达式1必须是bool类型**

```c++
	int a, b, x;
	cout << "input vale of a:";
	cin >> a;

	cout << "\n\input vale of b:";
	cin >> b;

	x = (a - b) > 0 ? (a - b) : (b - a);
	cout << "\n\The difference between a and b is:" << x << endl;
```

执行顺序：

- 先计算表达式1；

- 若1为true，则计算出2为最终结果；
- 若1为false，则计算出3为最终结果。

## 自定义类型

`typedef  double Area；`

`using Area = double；`

`auto val = val1 + val2;` 在这里如果val1+val2是int类型，那么val自动成为int类型

`decltype(i) j = 2;` declaration type；表示j以2作为初始值，类型与i一致；感觉像是格式刷

## 枚举enum 

```c++
using namespace std;
enum GameResult{WIN,LOSE,TIE,CANCEL};
int main() {
	GameResult result;
	enum GameResult omit = CANCEL;
	for (int count = WIN; count <= CANCEL; count++) {
		result = GameResult(count);
		if (result == omit)
		{
			cout << "The game was cancelled" << endl;
		}
		else {
			cout << "The game was played";
			if (result == WIN)	cout << " and we won!";
			if (result == LOSE)	cout << "\ and we lost!";
			cout << endl;
		}
	}
	return 0;	
}
```

## 函数

### 定义一个arctan函数求π

求$\pi$的公式
$$
\pi=16 \arctan \left(\frac{1}{5}\right)-4 \arctan \left(\frac{1}{239}\right)
$$

arctan的公式为一个无穷级数
$$
\arctan x=x-\frac{x^{3}}{3}+\frac{x^{5}}{5}-\frac{x^{7}}{7}+\cdots
$$
无穷级数无法计算，在此规定为当某项的绝对值小于$10^{15}$为止

算法实现

```c++
#include <iostream>
using namespace std;

double arctan(double x) {
	double sqr = x * x;
	double e = x;
	double r = 0;
	int i = 1;
	while (e/i>1e-15)
	{
		double f = e / i;
		r = (i % 4 == 1) ? r + f : r - f;
		e = e * sqr;
		i += 2;
	}
	return r;
}
int main() {
	double a = 16.0*arctan(1 / 5.0);//整数相除结果取整
	double b = 4.0*arctan(1 / 239.0);
	cout << "PI =" << a - b << endl;
	return 0;	
}
```

### 递归调用：计算斐波那契数

![](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191127185516072.png)

```c++
#include <iostream>
using namespace std;

long fib(int n){
	//cout << "processing fib(" << n << ")...\n";
	if (n < 3) {
		//cout << "return 1!\n";
		return (1);
	}
	else
	{
		//cout << "call fib(" << n - 2 << ") and fib(" << n - 1 << ").\n";
		return (fib(n - 2) + fib(n - 1));
	}
}

int main() {
	int n;long answer;
	cout << "enter number:" << endl;
	cin >> n;
	cout << "\n\n";
	answer = fib(n);
	cout << answer << " is the " << n << "th fibonacci number.\n" << endl;
   	return 0;
}
```

### 引用类型

值传递是传递参数值，即单向传递；引用传递可以实现双向传递。

定义引用时必须对他进行初始化，使它指向一个已有的对象。例如：

### 综合实例：默认值，重载

```c++
#include <iostream>
#include<cmath>
using namespace std;
int max1(int x, int y);
int max1(int x, int y, int z);
double max1(double x, double y);
double max1(double x, double y,double z);

int max1(int x = 1, int y = 2) {
	if (x == y)return x;
	else if (x >= y)
		return x;
	else
	{
		return y;
	}
}

int max1(int x, int y, int z) {
	return max1(max1(x, y), z);
}

double max1(double x = 1.121, double y = 2.71828) {
	if (abs(x - y) < 1e-10)return x;
	else if (x >= y)
		return x;
	else
		return y;
}

double max1(double x, double y, double z) {
	return max1(max1(x, y), z);
}

int main() {
	int a, b, c; double m, n, l;
	cout << "enter a number:";
	cin >> a;
	cout << "enter a number:";
	cin >> b; 
	cout << "enter a number:";
	cin >> c;
	cout << "enter a number:";
	cin >> m;
	cout << "enter a number:";
	cin >> n;
	cout << "enter a number:";
	cin >> l;
	cout << "\n";
	cout << "Max number of input is " << max1(a, b, c) << endl;
	cout << "Max number of input is " << max1(m, n, l) << endl;
	return 0;
}
```

# 面向对象

设计类就是设计类型

- 此类型的合法值是什么

- 此类型应该有什么样的函数和操作符

- 新类型的对象该如何被创建和销毁

- 如何进行对象的初始化和赋值

- 对象作为函数的参数如何以值传递

- 谁将使用此类型的对象成员

## 构造函数

与类名相同；无返回值，也不用写void；支持多态

其他知识点：

- **委托构造函数：**用默认值初始化构造函数的方式

- **复制构造函数：**引用一个已经存在的对象初始化新对象

  发生复制构造的三种情况

  - 定义一个对象，以本类另一个对象作为初始值；

  - 如果函数的形参是类的对象，调用函数时，将使用实参对象初始化形参对象；

  - 如果函数的返回值是类的对象，函数执行完成返回主调函数时，将使用return语句中的对象初始化一个临时无名对象，传递给主调函数。这种情况也可以通过**移动构造**避免。

  默认复制构造函数：如果没有为类声明时，编译器会自动生成一个默认的复制构造函数。用被复制的对象一一对应生成新对象。**但是这种机械地直接复制只具备最基本的功能**（<a href="#anchor">深拷贝和浅拷贝</a>）

  还可以使用`=delete`指示编译器不生成默认复制构造函数。

- **析构函数：**编译器自动生成的析构函数默认返回为空，是看不到内存被释放的。

```c++
#include <iostream>
using namespace std;
class Clock
{
public:
	Clock(int Hour, int Minute, int Second)://默认构造函数
		hour(Hour), minute(Minute), second(Second) {}//初始化列表：对类的成员变量初始化
	//Clock() = default;//指示编译器提供默认构造函数，用于当无指定值初始化时
	Clock() : Clock(0, 0, 0) {}//委托构造参数

	Clock(const Clock &p){//默认复制构造函数，编译器会生成个一毛一样的
		hour = p.hour;minute = p.minute;second = p.second;
	}

	void setTime(int Hour, int Minute, int Second) {
		hour = Hour;minute = Minute;second = Second;
	}

	void showTime() {
		cout << hour << ":" << minute << ":" << second << endl;
	}

	~Clock()//析构函数
	{
		cout << "No more call!" << endl;
	}

private:
	int hour, minute, second;
};

Clock fun2() {//返回值是类对象
	Clock a;
	return a;
}

void destruct(Clock a) {
	cout << "Clock destructed" << endl;
}

int main() {
	Clock a(2, 30, 50);//指定初值调用构造函数
	Clock b = a; //1复制构造函数，对象通过另外一个对象进行初始化
	b.showTime();
	Clock c;//默认值调用
	c.showTime();
	Clock d = c;//2复制构造函数，函数的参数为类对象
	d.showTime();
	destruct(d);//调用析构函数
	fun2();//3复制构造函数，函数返回值是类对象
	return 0;
}
```

## 类的组合

![image-20191205121510816](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20191205121510816.png)























# Q&A

## 1.记录一个很奇怪的现象

```c++
#include <stdio.h>//库函数
#include <iostream>
using namespace std;
int main() {
    cout<< "the size of an integer is:\t"<<sizeof(int) << "bytes.\n";
	cout << "the size of an long is:\t" << sizeof(long) << "bytes.\n" << endl;
    return 0;
}
```

```
the size of an integer is:      4bytes.
the size of an long is: 4bytes.
```

## 2.无符号整型不能表示负数

```c++
#include <stdio.h>//库函数
#include <iostream>
using namespace std;
int main() {
    unsigned int x, y, z;
	x = y - z;
	cout << "difference is:" << x<<"\n";
	x = z - y;
	cout << "difference is:" << x << endl;
	return 0;
}
```

这里的输出结果第一个是很正常的50，第二个是一个非常奇怪的数字，查查位数总是10位，也可能不一定是10位。总之问题在于unsigned int 是不能表示负数的，他把负数运算出的内容当做正整数来表示了。

如果改成`int x`就没事了。

## 3.<a name="anchor">什么是深拷贝和浅拷贝</a>

如果不显式声明拷贝构造函数的时候，编译器也会生成一个默认的拷贝构造函数，而且在一般的情况下运行的也很好。但是**当数据成员中有指针时**，如果采用简单的浅拷贝，则两类中的两个指针将指向同一个地址，当对象快结束时，会调用两次析构函数，而导致**指针悬挂**现象。因为默认的拷贝构造函数是按成员拷贝构造，这导致了两个不同的指针(如ptr1=ptr2)指向了同一个地址。当一个实例销毁时，调用析构函数 free(ptr1)释放了这段内存，那么剩下的一个实例的指针ptr2就无效了，在被销毁的时候free(ptr2)就会出现错误了, 这相当于重复释放一块内存两次。这种情况必须显式声明并实现自己的拷贝构造函数，来为新的实例的指针分配新的内存。

深拷贝与浅拷贝的区别就在于深拷贝会在堆内存中另外申请空间来储存数据，从而也就解决了指针悬挂的问题。**简而言之，当数据成员中有指针时，必须要用深拷贝**。

1.为什么拷贝构造函数必须是引用传递，不能是值传递？

为了防止递归引用。

当 一个对象需要以值方式传递时，编译器会生成代码调用它的拷贝构造函数以生成一个副本。如果类A的拷贝构造函数是以值方式传递一个类A对象作为参数的话，当需要调用类A的拷贝构造函数时，需要以值方式传进一个A的对象作为实参； 而以值方式传递需要调用类A的拷贝构造函数；结果就是调用类A的拷贝构造函数导致又一次调用类A的拷贝构造函数，这就是一个无限递归。  

2.参数传递过程到底发生了什么？

将地址传递和值传递统一起来，归根结底还是传递的是"值"(地址也是值，只不过通过它可以找到另一个值)！

- 值传递:
  对于内置数据类型的传递时，直接赋值拷贝给形参(注意形参是函数内局部变量)；
  对于类类型的传递时，需要首先调用该类的拷贝构造函数来初始化形参(局部对象)；如`void foo(class_type obj_local){}`, 如果调用`foo(obj)`; 首先`class_type obj_local(obj)` ,这样就定义了局部变量`obj_local`供函数内部使用

- 引用传递:
  无论对内置类型还是类类型，传递引用或指针最终都是传递的地址值！而地址总是指针类型(属于简单类型), 显然参数传递时，按简单类型的赋值拷贝，而不会有拷贝构造函数的调用(对于类类型).

3.拷贝构造函数里能调用private成员变量吗?

**这个问题是在网上见的，当时一下子有点晕。其时从名子我们就知道拷贝构造函数其时就是一个特殊的**构造函数**，操作的还是自己类的成员变量，所以不受private的限制。

## 4.

# 

