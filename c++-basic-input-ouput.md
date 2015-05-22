## C++ 基本输入输出

c++ 标准库提供了一组广泛的的输入/输出功能，我们将在随后的章节中展开。本章将讨论 c++ 编程所需的最基本和最常见的 I/O 操作。   

C++ I/O发生在流中，流是一种字节序列。如果字节流从一个设备（如键盘、磁盘驱动器,或网络连接等）到主内存，这称为输入操作（**input operation**）。如果字节从主内存流向一个设备（如显示屏，打印机，磁盘驱动器，或网络连接等），这就是所谓的输出操作（**output operation**）。

### I/O 库头文件：

下边列出对于 c++ 程序重要的头文件：

<table>
<tr>
<th>头文件</th>
<th>功能和描述</th>
</tr>
<tr>
<td>&lt;iostream&gt;</td>
<td>这个文件定义了 <strong>cin、cout、cerr</strong> 和 <strong>clog</strong> 对象，它们分别对应与标准输入流，标准输出流，无缓冲标准错误流和有缓冲标准错误流。</td>
</tr>
<tr>
<td>&lt;iomanip&gt;</td>
<td>这个文件声明的服务用于执行格式化的 I/O，即所谓的参数化流操纵者，如 <strong>setw</strong> 和 <strong>setprecision</strong>。</td>
</tr>
<tr>
<td>&lt;fstream&gt;</td>
<td>这个文件声明的服务用于用户控制文件处理。我们将在文件和流相关的章节更详细讨论关于它的内容。</td>
</tr>
</table>

### 标准输出流(cout):

预定义的对象 **cout** 是 **ostream** 类的一个实例。cout 对象通常连接到标准输出设备，一般是显示屏。**cout** 和流插入运算符联合使用，流插入运算符写为 <<，即两个表示小于的符号，如以下示例所示。   

    #include <iostream>
     
    using namespace std;
     
    int main( )
    {
       char str[] = "Hello C++";
     
       cout << "Value of str is : " << str << endl;
    }

编译和执行上面的代码，产生以下结果：

	Value of str is : Hello C++

c++ 编译器也决定了输出的变量数据类型并选择适当的流插入运算符来显示值。<< 操作符重载了多种输出数据项（包括各种内置类型：整数、浮点数、双精度浮点数、字符串和指针类型的值）。   

插入运算符 << 在一个语句中可能不止一次被使用，如上所示，**endl** 写在结束的时候用于添加一个新行。

### 标准输入流(cin):

预定义对象 **cin** 是 **istream** 类的一个实例。cin 对象通常用于标准输入设备，一般是键盘。**cin** 和流提取运算符联合使用，流提取符号写为 >> 即两个表示大于的符号，如以下示例所示。  

    #include <iostream>
     
    using namespace std;
     
    int main( )
    {
       char name[50];
     
       cout << "Please enter your name: ";
       cin >> name;
       cout << "Your name is: " << name << endl;
     
    }

编译和执行上面的代码，它会提示输入一个名称。输入一个值，然后回车，显示的结果如下：

    Please enter your name: cplusplus
    Your name is: cplusplus

c++编译器也决定输入值的数据类型和选择适当的流提取运算符提取值并将其存储在给定的变量。  

流提取操作符 >> 可以在一个声明中不止一次使用。请求多个数据您可以以下使用：

	cin >> name >> age;

这将是相当于两个语句如下：

	cin >> name;
	cin >> age;

### 标准错误流(cerr):

预定义对象 **cerr** 是 **ostream** 类的一个实例。cerr 对象通常附加到标准错误设备，这一般也是一个显示屏，但对象 **cerr** 是无缓存的，每当有流插入到 cerr 会导致其输出立即出现。

**cerr** 也与流插入操作符一起使用，如以下示例所示。

    #include <iostream>
     
    using namespace std;
     
    int main( )
    {
       char str[] = "Unable to read....";
     
       cerr << "Error message : " << str << endl;
    }

编译和执行上面的代码，产生以下结果：

	Error message : Unable to read....

### 标准日志流(clog)：

预定义对象 **clog** 是 **ostream** 类的一个实例。clog 对象通常附加到标准错误设备，这一般也是一个显示屏，但对象 **clog** 是有缓冲的。这意味着每个插入的 clog 会暂存在缓冲区中，直到缓冲区满或者缓冲区刷新才会导致一次输出。

**clog** 也与流插入操作符一起使用，如以下示例所示。

    #include <iostream>
     
    using namespace std;
     
    int main( )
    {
       char str[] = "Unable to read....";
     
       clog << "Error message : " << str << endl;
    }

编译和执行上面的代码，它产生以下结果：

	Error message : Unable to read....

在这些小例子中，你无法看到 cout，cerr，clog 的任何差异，但在写和执行大项目是，差异就变得显而易见了。所以这是很好的实践：使用 cerr 流显示错误消息，而使用 clog 显示其他日志信息。