## C++ 结构

C/C++ 可以将相同类型的数据组合成一个数组并将该数组定义为一个变量，但结构（**structure**）是一种用户定义的数据类型，允许你将不同类型的数据项放在一起。   

结构用来表示一条记录。假设你想在图书馆中找一本书，您可能需要查找每本书的以下属性：

- Title
- Author
- Subject
- Book ID 

### 定义一个结构体

定义一个结构，您必须使用结构体声明。结构语句为您的程序定义了一个新的数据类型，拥有一个以上的成员。结构体声明的格式是这样的:

    struct [structure tag]
    {
       member definition;
       member definition;
       ...
       member definition;
    } [one or more structure variables];  

**structure tag** 是可选的，每个成员的定义都是一个正常的变量定义，如 int i；或者 float f；或者任何其他有效的变量定义。在结构的定义结束时，在结构体定义结尾处的（“；”）符号之前可以指定一个或多个结构变量，但它是可选的。这是声明书结构体的方式:

    struct Books
    {
       char  title[50];
       char  author[50];
       char  subject[100];
       int   book_id;
    }book;  

### 访问结构成员:

访问一个结构的任何成员，我们使用 **member access operator**（成员访问操作符）：**(.)** 来访问结构体成员。成员访问操作符编码为结构变量名和我们要访问结构成员之间的一个点符号。使用关键字 **struct** 来定义结构类型的变量。下面是例子解释怎样使用结构体：

    #include <iostream>
    #include <cstring>
     
    using namespace std;
     
    struct Books
    {
       char  title[50];
       char  author[50];
       char  subject[100];
       int   book_id;
    };
     
    int main( )
    {
       struct Books Book1;// Declare Book1 of type Book
       struct Books Book2;// Declare Book2 of type Book
     
       // book 1 specification
       strcpy( Book1.title, "Learn C++ Programming");
       strcpy( Book1.author, "Chand Miyan"); 
       strcpy( Book1.subject, "C++ Programming");
       Book1.book_id = 6495407;
    
       // book 2 specification
       strcpy( Book2.title, "Telecom Billing");
       strcpy( Book2.author, "Yakit Singha");
       strcpy( Book2.subject, "Telecom");
       Book2.book_id = 6495700;
     
       // Print Book1 info
       cout << "Book 1 title : " << Book1.title <<endl;
       cout << "Book 1 author : " << Book1.author <<endl;
       cout << "Book 1 subject : " << Book1.subject <<endl;
       cout << "Book 1 id : " << Book1.book_id <<endl;
    
       // Print Book2 info
       cout << "Book 2 title : " << Book2.title <<endl;
       cout << "Book 2 author : " << Book2.author <<endl;
       cout << "Book 2 subject : " << Book2.subject <<endl;
       cout << "Book 2 id : " << Book2.book_id <<endl;
    
       return 0;
    }

编译和执行上面的代码，执行结果如下：

    Book 1 title : Learn C++ Programming
    Book 1 author : Chand Miyan
    Book 1 subject : C++ Programming
    Book 1 id : 6495407
    Book 2 title : Telecom Billing
    Book 2 author : Yakit Singha
    Book 2 subject : Telecom
    Book 2 id : 6495700

### 结构作为函数参数:

你可以将结构作为函数参数传递，其使用方式和将其他任何变量或指针作为参数传递非常相似。你可以以同样的方式访问结构变量，就如在上面的例子中显示的一样：

    #include <iostream>
    #include <cstring>
     
    using namespace std;
    void printBook( struct Books book );
    
    struct Books
    {
       char  title[50];
       char  author[50];
       char  subject[100];
       int   book_id;
    };
     
    int main( )
    {
       struct Books Book1;// Declare Book1 of type Book
       struct Books Book2;// Declare Book2 of type Book
     
       // book 1 specification
       strcpy( Book1.title, "Learn C++ Programming");
       strcpy( Book1.author, "Chand Miyan"); 
       strcpy( Book1.subject, "C++ Programming");
       Book1.book_id = 6495407;
    
       // book 2 specification
       strcpy( Book2.title, "Telecom Billing");
       strcpy( Book2.author, "Yakit Singha");
       strcpy( Book2.subject, "Telecom");
       Book2.book_id = 6495700;
     
       // Print Book1 info
       printBook( Book1 );
    
       // Print Book2 info
       printBook( Book2 );
    
       return 0;
    }
    void printBook( struct Books book )
    {
       cout << "Book title : " << book.title <<endl;
       cout << "Book author : " << book.author <<endl;
       cout << "Book subject : " << book.subject <<endl;
       cout << "Book id : " << book.book_id <<endl;
    }

编译和执行上面的代码，执行结果如下：

    Book title : Learn C++ Programming
    Book author : Chand Miyan
    Book subject : C++ Programming
    Book id : 6495407
    Book title : Telecom Billing
    Book author : Yakit Singha
    Book subject : Telecom
    Book id : 6495700

### 结构体指针:

您可以定义结构体指针，以一种定义指向其他变量的指针非常相似的方式，如下所示：

	struct Books *struct_pointer;

现在，您可以用上面定义的指针变量存储一个结构变量的地址。找到一个结构变量的地址，把操作符 & 置于结构体名称的前面，如下所示：

	struct_pointer = &Book1;

为了通过一个指向结构的指针访问结构体成员，必须使用 -> 操作符，如下所示：

	struct_pointer->title;

让我们使用结构指针重写上面的例子，希望这将帮助你更容易理解这个概念：

    #include <iostream>
    #include <cstring>
     
    using namespace std;
    void printBook( struct Books *book );
    
    struct Books
    {
       char  title[50];
       char  author[50];
       char  subject[100];
       int   book_id;
    };
     
    int main( )
    {
       struct Books Book1;// Declare Book1 of type Book
       struct Books Book2;// Declare Book2 of type Book
     
       // Book 1 specification
       strcpy( Book1.title, "Learn C++ Programming");
       strcpy( Book1.author, "Chand Miyan"); 
       strcpy( Book1.subject, "C++ Programming");
       Book1.book_id = 6495407;
    
       // Book 2 specification
       strcpy( Book2.title, "Telecom Billing");
       strcpy( Book2.author, "Yakit Singha");
       strcpy( Book2.subject, "Telecom");
       Book2.book_id = 6495700;
     
       // Print Book1 info, passing address of structure
       printBook( &Book1 );
    
       // Print Book1 info, passing address of structure
       printBook( &Book2 );
    
       return 0;
    }
    // This function accept pointer to structure as parameter.
    void printBook( struct Books *book )
    {
       cout << "Book title : " << book->title <<endl;
       cout << "Book author : " << book->author <<endl;
       cout << "Book subject : " << book->subject <<endl;
       cout << "Book id : " << book->book_id <<endl;
    }

编译和执行上面的代码，执行结果如下：
    
    Book title : Learn C++ Programming
    Book author : Chand Miyan
    Book subject : C++ Programming
    Book id : 6495407
    Book title : Telecom Billing
    Book author : Yakit Singha
    Book subject : Telecom
    Book id : 6495700

### typedef关键字

有一个更简单的方法来定义结构体，你可以给你创建的类型起一个别名，例如：

    typedef struct
    {
       char  title[50];
       char  author[50];
       char  subject[100];
       int   book_id;
    }Books;

现在，可以直接使用 Books 来定义书籍类型的变量，而不使用struct 关键字。下面是示例：

	Books Book1, Book2;

你也可以在非结构体（non-structs）中使用 typedef 关键字，如下所示：

    typedef long int *pint32;
     
    pint32 x, y, z;

x,y,z是指向长整数类型的指针。