---
title: Dangling pointer
date: 2020-07-26 09:18:37
categories:
- Program
- C++
tags:
- C++
---

## Sample1

``` c++
int main() {
    auto Name = input();
    cout << "Hello " << Name << '\n';
    return 0;
}

const char* input() {
    string Line;
    getline(cin, Line);
    return Line.c_str();  // Line is destroyed
}

```

## Sample2

``` c++
#include <iostream>
using namespace std;

void test() {
    int* p = nullptr;
    {
        int x = 0;
        p = &x;
        cout << *p;
    }  // x is destroyed

    cout << *p;
}
```

## Sample3

``` c++
#include <iostream>
using namespace std;

string_view {
    size_t len;
    const char* str;
}

void test() {
    string_view s;
    {
        char a[100];
        s = a;
        cout << s[0];
    }  // a is destroyed and a.str become a dangling pointer

    cout << s[0];
}

```

## Sample4

``` c++
void swap(Object* a, Object* b){
    Object* tmp;
    tmp = a;  //tmp point to a
    a = b;
    b = tmp;
}  // tmp was destroyed and b will be a dangling pointer

```

## Sample5

``` c++
int* a = new int(100);

for (size_t i = 0; i < 100; i++) {
    *(a++) = i;  // a has been changed and a not point array[0] now
}

std::cout << a[0] << std::endl;
delete a;

```

## Links
[zhihu example](https://zhuanlan.zhihu.com/p/85200304)
