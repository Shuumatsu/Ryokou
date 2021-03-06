---
title: Dynamic Dispatch
---

CPP 的 virtual function 以及 Java 的方法采用动态分发的方式，方法的 receiver 在运行时才能确定
例如下面的程序，输出为

```
FOO: print
FOO: print
FOO: virtual_print
Bar: virtual_print
```


```
#include <iostream>

using namespace std;

class Foo {
   public:
    void call_print() const { print(); }
    void print() const { cout << "FOO: print" << endl; }
    void call_virtual_print() const { virtual_print(); }
    virtual void virtual_print() const { cout << "FOO: virtual_print" << endl; }
};

class Bar : public Foo {
   public:
    void print() const { cout << "Bar: print" << endl; }
    virtual void virtual_print() const { cout << "Bar: virtual_print" << endl; }
};

int main() {
    Foo foo;
    Bar bar;
    foo.call_print();
    bar.call_print();

    foo.call_virtual_print();
    bar.call_virtual_print();

    return 0;
}
```