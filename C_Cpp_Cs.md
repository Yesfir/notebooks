# Cpp

#### 小知识点

```cpp
int INF = Integer.MAX_VALUE;
INT_MAX, INT_MIN.
g++ main.cpp -W -Wall // add W & Wall not to ignore warning
-g // debug版本 vs. release版本
-O2    // release开个优化
```

#### BASIC KNOWLEDGE

```cpp
1. stdin & stdout;
In C++, you can read a single whitespace-separated token of input using cin, and print output to stdout using cout;
2. basic data types;
Int ("%d"): 32 Bit integer
Long ("%ld"): 64 bit integer
Char ("%c"): Character type
Float ("%f"): 32 bit real value
Double ("%lf"): 64 bit real value

To read a data type, use the following syntax:
scanf("`format_specifier`", &val);

char ch;
double d;
scanf("%c %lf", &ch, &d);

To print a data type, use the following syntax:
printf("`format_specifier`", val);

can use cin and cout but will be faster using scanf and printf especially for large numbers;

cout precison: cout << fixed << setprecision(6) << ans[i] << endl;
```

- auto
  
  The **`auto`** keyword is a simple way to declare a variable that has a complicated type. The **`auto`** keyword is a placeholder for a type, but it is not itself a type.

- inline
  
  节省调用开销，便于编译器和上下文配合做优化

- const
  
  修饰类成员函数，其目的是防止成员函数修改被调用对象的值，如果我们不想修改一个调用对象的值，所有的成员函数都应当声明为 const 成员函数。

## Classes

- OOP: Object-Oriented Programming

- a class is a template for objects, and an object is an instance of a class.

- class members: variables and functions

```cpp
// crete a class
class MyClass {       // The class
  public:             // Access specifier
    int myNum;        // Attribute (int variable)
    void myMethod() {  // Method/function defined inside the class
      cout << "Hello World!";
    }
};
// create obj and access
int main() {
  MyClass myObj;  // Create an object of MyClass
  myObj.myNum = 15; // Access attribute and set value
  myObj.myMethod();  // Call the method
  return 0;
}

//outsie example, declare inside and define with scope resolution :: operator
class MyClass {        // The class
  public:              // Access specifier
    void myMethod();   // Method/function declaration
};
// Method/function definition outside the class
void MyClass::myMethod() {
  cout << "Hello World!";
}

// Constructors, a special method automatically called when an object iscreated.
// use the same name as class followed by parentheses ()
class MyClass {     // The class
  public:           // Access specifier
    int year;
    MyClass(int z) {     // Constructor
      year = z;
      cout << "Hello World!";
    }
};
int main() {
  MyClass myObj(1999);    // Create an object of MyClass (this will call the constructor)
  return 0;
}
```

- `public` - members are accessible from outside the class

- `private` - members cannot be accessed (or viewed) from outside the class

- `protected` - members cannot be accessed from outside the class, however, they can be accessed in inherited classes. 
  
  **Note:** By default, all members of a class are `private` if you don't specify an access specifier. Good practice to keep variables private, and make set & get methods.

```cpp
// static in .h
class Vector3 {
public:
    static double Dot(Vector3 x, Vector3 y);
}
// static in .cpp
double Vector3::Dot(Vector3 x, Vector3 y) {
    return x._x * y._x + x._y * y._y + x._z * y._z;
}
// use in .cpp
auto a = Vector3::Dot(x, y);

//operator in .h
Vector3 operator - (Vector3 &second) {
    Vector3 res;
    res.set(_x - second.x(), _y - second.y(), _z - second.z());
    return res;
}
```

### Inheritance

group the "inheritance concept" into two categories:

- **derived class** (child) - the class that inherits from another class
- **base class** (parent) - the class being inherited from

To inherit from a class, use the `:` symbol.

```cpp
// Base class
class Vehicle {
  public:
    string brand = "Ford";
    void honk() {
      cout << "Tuut, tuut! \n" ;
    }
};

// Derived class
class Car: public Vehicle {
  public:
    string model = "Mustang";
};

int main() {
  Car myCar;
  myCar.honk();
  cout << myCar.brand + " " + myCar.model;
  return 0;
}

// Derived class
class MyChildClass: public MyClass, public MyOtherClass {
};
```

- virtual function (虚函数)

```cpp
class Parent  {      
public:  
    char data[20];  
    void Function1();     
    virtual void Function2();   // 这里声明Function2是虚函数  
}parent;  

void Parent::Function1()  {  
    printf("This is parent,function1\n");  
}  

void Parent::Function2()  {  
    printf("This is parent,function2\n");  
}  

class Child:public Parent  {  
    void Function1();  
    void Function2();  
} child;  

void Child::Function1()  {  
    printf("This is child,function1\n");  
}  

void Child::Function2()  {  
    printf("This is child,function2\n");  
}  

int main(int argc, char* argv[])  {  
    Parent *p;  // 定义一个基类指针  
    if(_getch()=='c')     // 如果输入一个小写字母c      
        p=&child;         // 指向继承类对象  
    else      
        p=&parent;       // 否则指向基类对象  
    p->Function1();   // 这里在编译时会直接给出Parent::Function1()的入口地址。      
    p->Function2();    // 注意这里，执行的是哪一个Function2？  
    return 0;  
}  
/*
c: parent function1, child function2
!c: parent function1, parent function2
*/
```

### iostream

In C++ input and output are performed in the form of a sequence of bytes or more commonly known as **streams**.

- **Input Stream:** If the direction of flow of bytes is from the device(for example, Keyboard) to the main memory then this process is called input.
- **Output Stream:** If the direction of flow of bytes is opposite, i.e. from main memory to device( display screen ) then this process is called output.

iostream stands for standard input-output stream. This header file contains definitions of objects like cin, cout, cerr, etc.

- **Standard output stream (cout)**: Usually the standard output device is the display screen. The C++ **cout** statement is the instance of the ostream class. The data needed to be displayed on the screen is inserted in the standard output stream (cout) using the insertion operator(**<<**).
- **standard input stream (cin)**: Usually the input device in a computer is the keyboard. C++ cin statement is the instance of the class **istream**.
  The extraction operator(**>>**) is used along with the object **cin** for reading inputs. The extraction operator extracts the data from the object **cin** which is entered using the keyboard.

```cpp
void write_color(std::ostream &out, Vector3 pixel_color) {
    out << static_cast<int>(255.999 * pixel_color.x()) << ' '
        << static_cast<int>(255.999 * pixel_color.y()) << ' '
        << static_cast<int>(255.999 * pixel_color.z()) << '\n';
}

write_color(std::cout, pixel_color);
```

### header file

Consider the following program:

```cpp
#include <iostream>
int main()
{
    std::cout << "Hello, world!";
    return 0;
}
```

This program prints to the console using *std::cout*. how does the compiler know what *std::cout* is? has been forward declared in the “iostream” header file. When we `#include <iostream>`, we’re requesting that the **preprocessor** copy all of the content (including forward declarations for std::cout) from the file named “iostream” into the file doing the #include.

#### Header guards

Duplicate definitions and a compile error.

Header guards are conditional compilation directives that take the following form:

```cpp
#ifndef SOME_UNIQUE_NAME_HERE
#define SOME_UNIQUE_NAME_HERE

// your declarations (and certain types of definitions) here

#endif
```

For class: put declaration in .h and definition in .cpp (outside with `#include "MyClass.h"` and scope ::)

#### 

#### 二分

```c++
// 本质： 两段性质的划分（两个边界点）
** 如果用到left = mid， 则mid需要加一！！
```

#### 排序

```C++
// 1. 冒泡排序
// 2. 快速排序——分治, 确定pivot是O(n), T(n)=2*T(n/2)+O(n), O(nlogn), 要求左右比较均匀; 最坏O(n^2)

// 3. 归并排序
```

#### operator 运算符

```c++
a=++i；    //i=i+1; a=i;
b=j++;    //b=j; j=j+1;
a[index--]='0';    //1. 赋0 2. index--

//magic code
static const auto __=[](){
  std::ios::sync_with_stdio(false);
  std::cin.tie(nullptr);
  return nullptr;
}();
```

#### class

```c++
class MyLinkedList {
public:
    // 定义链表节点结构体
    struct LinkedNode {
        int val;
        LinkedNode* next;
        LinkedNode(int val):val(val), next(nullptr){}
    };

    // 初始化链表
    MyLinkedList() {
        _dummyHead = new LinkedNode(0); // 这里定义的头结点 是一个虚拟头结点，而不是真正的链表头结点
        _size = 0;
    }
    // 在链表最前面插入一个节点，插入完成后，新插入的节点为链表的新的头结点
    void addAtHead(int val) {
        LinkedNode* newNode = new LinkedNode(val);
        newNode->next = _dummyHead->next;
        _dummyHead->next = newNode;
        _size++;
    }
private:
    int _size;
    LinkedNode* _dummyHead;
};

// 带值初始化
NumArray(vector<int>& nums){}
NumArray* obj=new NumArray(nums);
obj->update(index, val);
```

## Data structure

### shared_ptr

`shared_ptr<type>` is a pointer to some allocated type, with reference-counting semantics. Every time you assign its value to another shared pointer (usually with a simple assignment), the reference count is incremented. As shared pointers go out of scope (like at the end of a block or function), the reference count is decremented. Once the count goes to zero, the object is deleted.

Typically, a shared pointer is first initialized with a newly-allocated object, something like this:

```cpp
#include <memory>
shared_ptr<double> double_ptr = make_shared<double>(0.37);
shared_ptr<vec3>   vec3_ptr   = make_shared<vec3>(1.414214, 2.718281, 1.618034);
shared_ptr<sphere> sphere_ptr = make_shared<sphere>(point3(0,0,0), 1.0);
// or simplified
auto double_ptr = make_shared<double>(0.37);
```

### queue

```cpp
queue<TreeNode*> que;
while (!que.empty())
int num = que.size();
q.push(i);
int u=q.front();
q.pop();

//priority_queue 优先队列 703. topK
class KthLargest {
public:
    priority_queue<int, vector<int>, greater<int>> pq;
    int k;
    KthLargest(int k, vector<int>& nums) {
        this->k = k;
        for (auto& x: nums) {
            add(x);
        }
    }
    int add(int val) {
        q.push(val);
        if (q.size() > k) {
            q.pop();
        }
        return q.top();
    }
};
```

#### vector

```cpp
vec.push_back(i);    //在表尾添加元素
// O(1)操作，但触发扩容就是O(N)
vec.pop_back();    //在表尾删除元素
vec.erase(vec.begin() + 1); //index = 1
vector<bool> vec(x, false);    //初始化x个元素的bool向量
vector<int> vec={x1,x2,x3};    //初始化vector数组
vector<vector<int>> ans(r, vector<int>(c)); //初始化r*c二维数组
sums.resize(m + 1, vector<int>(n + 1));        //resize二维数组
fill(visited.begin(), visited.end(), false); //重新赋值
res.push_back(vector<int>(i+1,1));    //也可以直接用
ret.insert(ret.end(),temp.begin(),temp.end());    //数组后面插入数组
sort(nums.begin(), nums.end());    //排序
int x=nums.back(); //最后一个

// 迭代器插入, begin()是0号元素, begin()+2, 插在第3位
vector<int> ivec;
auto it=ivec.begin()+2;
ivec.insert(it, 100);

bool comp(const int &a, const int &b){return a>b;}
sort(v.begin(), v.end(), comp);        //条件排序
sort(v.begin(), v.end(), [](vector<int> a, vector<int> b){
  return a[1]>b[1];
});    //lambda表达式

for (int e:nums) sum+=e;    //一个快速的求和

//另一种访问方式, 区别是越界会抛出异常
int x = ivec.at(0);

vector<char> v(s.begin(), s.end());    //vector to set

// lower_bound & upper_bound
std::vector <int> v = {10, 10, 10, 20, 20, 20, 20, 30, 30};
std::vector<int>::iterator low,up;
low=std::lower_bound (v.begin(), v.end(), 20);
up= std::upper_bound (v.begin(), v.end(), 20);

std::cout << "lower_bound at position " << (low- v.begin()) << '\n';// 3
std::cout << "upper_bound at position " << (up - v.begin()) << '\n';// 7

// min index
int minPosition = min_element(v.begin(),v.end()) - v.begin();
```

#### string

```c++
string str=bitset<32>(n).to_string();    //把n转换成32位字符串
int x=stoi(s);    //string_to_integer
string s = to_string(int/long/...);

if (n[0]=='0') {n=n.substr(1);}    //去掉先导0
n.substr(1,5);    //从1开始截取5位
n.insert(0,1,'1');    //在第0位插入一个'1'
reverse(s.begin(), s.end());            //反转字符串

for (char ch : s){}    //遍历

//string 的stack用法
string stk;
stk.empty();
(char)stk.back();    // end char
stk.pop_back();
stk.push_back(ch);

// 删去末尾空格
while (res.size() and res.back() == ' '){
    res.pop_back();
}
```

#### stack

```c++
stack<char> stk;
stk.size();
stk.top();
stk.pop();
stk.push();
stk.empty();
```

#### Tree

```c++
//层次遍历分层思路：外循环层次+内循环节点
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

// height-balanced tree: a binary tree in which the left and right subtrees of every node differ in height by no more than 1.
```

#### unordered_set

```cpp
//哈希集合
unordered_set<char> ooc;
occ.erase(s[i]);
occ.insert(s[i]);
occ.find('a');    //查找元素，返回对应元素或/occ.end()
occ.count('a');    //查找元素个数（0/1）
//存路径常用
vector<unordered_set<int>> g(n);    //n是点数
g[u].insert(v);
if (g[i].count(j)){}    //有直接相连的边
```

#### map & unordered_map

```cpp
// map: 内部实现红黑树，自动排序(by key)，空间占用率高, map中存的是pair: first, second(key->value)
1. mp.size();
2. mp.insert(pair);
3. mp.find(key);   m.count(key); ?==1;
4. mp.erase(key);
5**. mp[key] = value;
for (auto it = mp.begin(); it != mp.end(); it++) {
  cout << it->first << " " << it->second<<endl;
}

map.rbegin();  // reverse begin in C++ STL, throws a reverse iterator

//哈希表：key->value, O(1), 5 ops as above
unordered_map<string,int>mem;
mem.size();        //key的数量
if (mem.find(n)!=mem.end){return mem[n]}    //已经计算过
if (hash.count(t)){}    //不加可能会超时
//一个思路：边找边加入而非全部加入再找

//key->set 实现存储多个变量
unordered_map<int, vector<int>> mp;
//遍历哈希表
for (auto& [_, vec] : mp){}
```

#### Topological Sort

```c++
//拓扑排序
//有向图的拓扑排序是其顶点的线性排序，使得对于从顶点u到顶点v的每个有向边uv，u在排序中都在v之前
//有向无环图（DAG）=》拓扑排序
//eg. 是否能排课
//1. BFS
//用数组记录先修课程，入度为0加入队列，时空O(m+n)
```

#### cmath

```C++
//下面都是弧度要*180/M_PI
double atan2(double y, double x);    //涉及角度相关，值域为[-PI,PI]
double atan(double x);
```

#### Gray Code (格雷码)

在一组数的编码中，若任意两个相邻的代码只有一位二进制数不同，则称这种编码为格雷码(Gray Code). 另外,格雷码的最大数与最小数之间也仅一位数不同，即“首尾相连”，因此又称循环码或反射码.

#### 并发问题

```c++
//信号量
# include <semaphore.h>
sem_t x;
sem_init(&x, 0, 0);
sem_post(&x);
sem_wait(&x);
```

#### 动态规划(Dynamic Programming)

```c++
/*
e.g. 玩家拿数
dp[i][j] 表示nums的[i,j]子序列时，先手最多分数
最终答案: dp[0][n-1]*2>=SUM
状态转移方程：
dp[i][j]=max(
nums[i]+sum(i+1,j)-dp[i+1][j]
nums[j]+sum(i,j-1)-dp[i][j-1]
)
*/
// 动规要谨记：循环顺序！
1. 确定状态：（最优策略的）最后一步->子问题
2. 转移方程
3. 初始条件和边界情况
4. 计算顺序

dp的状态函数中间，一个重要的下标是target
dp的第二个下标一般是状态，分情况讨论转移

  1. 背包问题: 2 variables = weight and values, so to get max(dp[N][0-V])
```

#### 并查集：三个操作

```c++
// 初始化
int *p=new int[n];
for (int i=0; i<n; i++){
  p[i]=i;
}
// find
int getf(vector<int>& f, int x) {
    if (f[x] == x) {return x;}
    int newf = getf(f, f[x]);
  f[x] = newf;
  return newf;
}
// union
void add(vector<int>& f, int x, int y) {
  int fx = getf(f, x);
  int fy = getf(f, y);
  f[fx] = fy;
}
// eg. 连通分量: how many p[x]==x;
```

#### 堆

```c++
// 从vector生成最大堆
make_heap(piles.begin(), piles.end());
for (int i = 0; i < k; ++i){
    // 单次操作：记录并弹出最大值，修改后重新添加进堆
    pop_heap(piles.begin(), piles.end());
    piles.back() -= piles.back() / 2;
    push_heap(piles.begin(), piles.end());
}
return accumulate(piles.begin(), piles.end(), 0);
时间复杂度：O(n+klogn)，其中 n 为 piles 的长度。建堆与计算结果的复杂度为 O(n)；每次弹出最大值与添加新值的时间复杂度为 O(logn)，共需进行 k 次。
```

#### 位运算

```c++
A[i]^=1;    //异或（翻转）
int u = (bs[bucket] | (1 << loc));    //或者，移位
```

#### 线段树

```C++
// 对数时间从数组中找到max、min、sum、最大公约数、最小公倍数
```

#### 多线程多进程

```c
// 进程：分配系统资源的实体，struct task_struct结构体描述，即进程控制块PCB——标识符，状态，优先级，程序计数器（PC，下条指令地址），内存指针，上下文数据（Reg），I/O状态信息，记账信息，其他
// linux创建子进程：子进程拷贝父进程PCB以及页表等结构，创建完成后具有自己的进程虚地址空间和页表结构，返回0子进程，>0父进程
#include <unistd.h>
pid_t fork(void);
// 线程：轻量级进程
#include <pthread.h>
int pthread_create(pthread_t *thread, const pthread_attr_t *attr, void* (*start_routine)(void *), void *arg);
```

## Eigen

```c++

```

## C

```c
// typedef is a language construct that associates a name to a type
typedef int myinteger;
typedef char *mystring;
// a function pointer stores the address of a function
typedef void (*myfunc)();
myinteger i;   // is equivalent to    int i;
mystring s;    // is the same as      char *s;
myfunc f;      // compile equally as  void (*f)();
```
