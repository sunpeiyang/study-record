摘在《c++标准库》

## c++ 11新特性

#### 1、template 表达式内的空格

 在两个template表达式的闭符之间放一个空格 的要求已经过时了。

```
vector<list<list> >;  所有版本支持
vector<list<int>>;   c++ 11 开始支持
```

#### 2、新增类型 nullptr 类型

nullptr --&gt; void \*

```
void f(int);
void f(void*);
f(0);  //call f(int)
f(NULL); //call f(int)
f(nullptr) // call f(void*)
```

#### 3、 以auto 完成类型自动推导

```
double f();
auto d = f(); // d  is double
auto i; //error 推导失败
```

4、一致性初始化与初始化列

对任何初始化动作，都可使用相同语法，使用大括号初始化。

```
int  values[] {1, 2, 3};
vecter<int> vi { 2, 3, 4, 5};
vector<string> vs {"zhangsan", "lisi" };

int i; // i has undefined value
int j{} // j is init by 0
int* p; //p has undefined value
int* q{}; //q is init by nullptr

//窄化narrowing 是不成立的
int x1(5.3);  //x1 = 5
int x2 = 5.3; // x2 = 5
int x3{5.0};   //error narrowing
int x4 = {5.3}; //error narrowing

char c2{7}; //ok
char c3{9999} //error narrowing
```

5、Range-Based for 循环

一种新的for循环，类似用其他语言的foreach

```
for ( decl : coll)
{
    statement
}

for (int i : {1, 2, 3})
{
    cout << i << endl;
}

vector<int> vi;
...
for (auto& elem : vi)
{
    elem *= 3;  //数组每个元素*3
}
```



