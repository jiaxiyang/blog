---
title: Cpp to c interface
date: 2020-07-27 22:43:02
categories:
- Program
- Cpp
tags:
- Cpp
---


## method.hpp

``` c++
#pragma once

namespace jia {
Class Method {
 public:
    static std::unique_ptr<Method> create(std::string name);

    virtual const std::string get_name() const = 0;
}
}
```
## method_imp.hpp

``` c++
#pragma once
#include "method.hpp"

namespace jia {
Class MethodImp : public Method {
 public:
    MethodImp(std::string name);
    const std::string get_name() const override;

 private:
    int name_;
    int value_;
    friend class c_api;
}
}

```

## method.cpp

``` c++
#include "method.hpp"
#include "method_imp.hpp"

namespace jia {

std::unique_ptr<Method> Method::create(std::string name) {
    return std::unique_ptr<Method>{static_cast<Method*>(new Method{name})};
}

}

```

## method_imp.cpp

``` c++
#include "method_imp.hpp"
#include "c.h"

namespace jia {

MethodImp::MethodImp(std::string name)
    : name_{name},
      value_{1}{};

const std::string MethodImp::get_name() const {
    return name_;
}

}  // namespace jia

/* C API implementations */
#include "c.h"

namespace jia {

class c_api {
 public:
    static int get_value(c_method_t method) {
        auto self = static_cast<jia::Method*>(method);
        return self->value_;  // to get value_; c_api need to be friend class of MethodImp
    }
}

extern "C" c_method_t c_create(const char* name) {
    auto m = jia::Method::create(std::string(name));
    return static_cast<c_method_t>(m.realse());  // release will move unique_ptr ownership
}

extern "C" int c_destroyed(c_method_t method) {
    auto m = static_cast<jia::Method*>(method);
    delete m;
    return 0;
}

extern "C" const char* c_get_name(c_method_t method) {
    auto self = static_cast<jia::Method*>(method);
    return self->get_name().cstr();
}

extern "C" int c_get_value(c_method_t method) {
    return jia::c_api::get_value(method);
}

}

```

## c.h

``` c++
#pragma once

#ifdef __cplusplus  // c++ will use and c not use
extern "C" {
#endif

typedef void* c_method_t;

c_method_t c_create(const char* name);  // create an instance

int c_destroyed(c_method_t);            // destroy the instance

const char* c_get_name(c_method_t method);

int c_get_value(c_method_t method);

#ifdef __cplusplus
}
#endif
```

## test.c

``` c++
#include "c.h"

int main() {
    c_method_t m = c_create("c_test");
    printf("name:  %s", m->c_get_name());
    printf("value: %d", m->get_value());
    c_destroyed(m);
}
```
