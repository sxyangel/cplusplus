## C++ 日期和时间

c++ 标准库没有提供一个合适的日期类型。c++ 从 C 中继承了针对日期和时间的结构和功能，为了访问与日期和时间相关的功能和结构，需要在 c++ 程序中包括 &lt;ctime&gt; 头文件。
  
这里有四个与时间相关的类型：**clock\_t、time\_t、size\_t** 和 **tm**。clock\_t，size\_t 和 time\_t 类型能够以某种类型的整数表示系统时间和日期。 
  
结构类型 **tm** 以 C 结构体的形式支持日期和时间，有以下元素:

    struct tm {
      int tm_sec;   // seconds of minutes from 0 to 61
      int tm_min;   // minutes of hour from 0 to 59
      int tm_hour;  // hours of day from 0 to 24
      int tm_mday;  // day of month from 1 to 31
      int tm_mon;   // month of year from 0 to 11
      int tm_year;  // year since 1900
      int tm_wday;  // days since sunday
      int tm_yday;  // days since January 1st
      int tm_isdst; // hours of daylight savings time
    }

以下是我们在 C 或 c++ 中处理日期和时间时使用的一些重要的函数。所有这些函数都是标准 C 和 c++ 库的一部分，你可以使用下面给出的 c++ 标准库引用查看它们的使用细节。
<table border = "1">
<tr>
<th>序号</th>
<th>功能与目的</th>
</tr>
<tr>
<td>1</td>
<td><strong>time_t time(time_t *time);</strong></br>这将返回当前系统的日历时间，以自 1970 年 1 月 1 日开始系统运行秒数的形式。如果系统没有时间，返回 1。</td>
</tr>
<tr>
<td>2</td>
<td><strong>char *ctime(const time_t *time);</strong></br>这返回一个指向字符串的指针，字符串形式为 <i>day month year hours:minutes:seconds year\n\0</i>。</td>
</tr>
<tr>
<td>3</td>
<td><strong>struct tm *localtime(const time_t *time);</strong></br>这将返回一个指向 <strong>tm</strong> 结构体的指针，<strong>tm</strong> 结构体代表当地时间。</td>
</tr>
<tr>
<td>4</td>
<td><strong>clock_t clock(void);</strong></br>这将返回一个与被调用程序运行时间的总和接近的值。如果时间无效，返回 1。</td>
</tr>
<tr>
<td>5</td>
<td><strong>char * asctime ( const struct tm * time );</strong></br>这将返回一个指向字符串的指针，该字符串包含的信息以如下结构体存储，结构体形式如下:<i>day month year hours:minutes:seconds year\n\0</i></td>
</tr>
<tr>
<td>6</td>
<td><strong>struct tm *gmtime(const time_t *time);</strong></br>它返回一个指向时间的指针，该时间是 tm 结构的。时间用协调世界时(UTC)表示，在本质上是格林威治标准时间(GMT)。</td>
</tr>
<tr>
<td>7</td>
<td><strong>time_t mktime(struct tm *time);</strong></br>返回日历时间，时间以参数中指出的结构形式表示。</td>
</tr>
<tr>
<td>8</td>
<td><strong>double difftime ( time_t time2, time_t time1 );</strong></br>这个函数计算秒 time1 和 time2 之间的差异。</td>
</tr>
<tr>
<td>9</td>
<td><strong>size_t strftime();</strong></br>这个函数可以用于以一种特定格式来格式化日期和时间。</td>
</tr>
</table>
### 当前的日期和时间：
考虑你想要取得当前系统的日期和时间，作为当地时间或作为一个协调世界时（UTC）。下面是一个实现相同目的的示例：

    #include <iostream>
    #include <ctime>
    
    using namespace std;
    
    int main( )
    {
       // current date/time based on current system
       time_t now = time(0);
       
       // convert now to string form
       char* dt = ctime(&now);
    
       cout << "The local date and time is: " << dt << endl;
    
       // convert now to tm struct for UTC
       tm *gmtm = gmtime(&now);
       dt = asctime(gmtm);
       cout << "The UTC date and time is:"<< dt << endl;
    }

编译和执行上面的代码，执行结果如下：

    The local date and time is: Sat Jan  8 20:07:41 2011
    
    The UTC date and time is:Sun Jan  9 03:07:41 2011

### 使用结构体 tm 格式化时间：

无论是在 C 还是在 C++ 中，**tm** 结构体在处理日期和时间时都是非常重要的。如前所述，该结构以一种 C 语言结构体的形式支持日期和时间。大部分与时间相关的函数使用 tm 结构。下面是一个例子，它使用了各种各样日期和时间的相关函数和 tm 结构： 

在本章中使用结构体，基于一个假设：你已经对 C 语言的结构体有了基本的了解，并且知道如何使用箭头操作符：-> 访问结构体成员。

    #include <iostream>
    #include <ctime>
    
    using namespace std;
    
    int main( )
    {
       // current date/time based on current system
       time_t now = time(0);
    
       cout << "Number of sec since January 1,1970:" << now << endl;
    
       tm *ltm = localtime(&now);
    
       // print various components of tm structure.
       cout << "Year: "<< 1900 + ltm->tm_year << endl;
       cout << "Month: "<< 1 + ltm->tm_mon<< endl;
       cout << "Day: "<<  ltm->tm_mday << endl;
       cout << "Time: "<< 1 + ltm->tm_hour << ":";
       cout << 1 + ltm->tm_min << ":";
       cout << 1 + ltm->tm_sec << endl;
    }
编译和执行上面的代码，执行结果如下：

    Number of sec since January 1, 1970:1294548238
    Year: 2011
    Month: 1
    Day: 8
    Time: 22: 44:59