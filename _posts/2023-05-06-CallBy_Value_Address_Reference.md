---
layout: post
title: "Callby_value_address_reference"
date: 2023-05-06 14:00:00 +0900
categories: C++ Variable
tags: Callby_value_address_reference Pointer
---

# 서론
Call by value, call by address, 그리고 call by reference는 함수 호출 시 매개변수에 인자를 전달하는 방식에 대한 개념이다. <br/><br/>
그럼 **araboza**

## call by value
-----------
- 함수가 호출될 때 인자로 전달되는 변수의 값을 복사하여 전달한다. 
- 이 방식은 원본 변수에 영향을 주지 않으며, 함수 내에서의 변경이 원본 변수에 영향을 미치지 않는다.

```cpp
#include <iostream.h>

using namespace std;

void changeValue(int num) {
    num = 20;
}

int main() {
    int num1 = 10;
    cout << "Before " << num1 << '\n';

    changeValue(num1);

    cout << "After " << num1;

    return 0;
}
```
**output:** <br/><br/>
Before: 10 <br/>
After: 10 <br/><br/>
함수 changeValue에서 num의 값을 변경하더라도 main 함수의 num1 값은 변하지 않는다. 이는 call by value 방식으로 값이 복사되어 전달되기 때문

## call by address
--------------
- 포인터를 사용하여 변수의 주소를 전달한다.
- 이를 통해 함수 내에서 원본 변수의 값을 변경할 수 있다. 
- 주소를 통한 값 변경이 가능하므로 원본 변수에 영향을 줄 수 있다.

```cpp
#include <iostream.h>

using namespace std;

void changeValue(int *num) {
    *num = 20;
}

int main() {
    int num1 = 10;
    cout << "Before " << num1 << '\n';

    changeValue(&num1);

    cout << "After " << num1;
    return 0;
}
```
**output:** <br/><br/>
Before: 10<br/>
After: 20<br/><br/>
함수 changeValue에서 포인터를 통해 변수 num1의 주소를 전달하고, 원본 값을 변경된 결과값이 나왔다.

## call by reference
----------
- 참조자(reference)를 사용하여 인자를 전달하는 방식. 
- 참조자는 원본 변수의 별칭(alias)이며, 함수 내에서 참조자를 통해 원본 변수를 수정할 수 있다. 
- 이 방식 역시 원본 변수에 영향을 줄 수 있습니다.

```cpp
#include <iostream>

using namespace std;

void changeValue(int &num) {
    num = 20;
}

int main() {
    int num1 = 10;
    cout << "Before: " << num1 << std::endl;
    changeValue(num1);
    cout << "After: " << num1 << std::endl;
    return 0;
}
```
**output:** <br/><br/>
Before: 10<br/>
After: 20<br/><br/>
함수 changeValue에서 참조자를 사용하여 원본 변수 num1을 전달하고 수정된 결과가 나왔다.

# 정리
----------------
1. **call by value**
    - 함수에 인자로 전달되는 변수의 값을 **복사하여 전달하는 방식**. 원본 변수에 영향을 주지 않는다.

2. **call by address**
    - 함수에 인자로 전달되는 변수의 **주소를 전달하는 방식**. 함수 내에서 원본 변수를 변경할 수 있다.

3. **call by reference**
    - 함수에 인자로 전달되는 변수의 **참조자(별칭)를 전달하는 방식**. 함수 내에서 원본 변수를 변경할 수 있다.