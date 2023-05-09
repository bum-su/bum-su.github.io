---
layout: post
title: C++ 함수 호출 규약(Calling Convention)
date: 2023-05-09 15:00:00 +0900
categories: C++ Calling_Convention
tags: Calling_Convention
---

# 함수 호출 규약이란?
-----------
함수 호출 규약은 컴파일러가 함수를 호출하고 결과를 반환하는 방법을 정의하는 규칙이다. 

이는 호출자와 피호출자 간의 인터페이스를 제공하며, 이 인터페이스는 스택 정리, 매개변수 전달 순서, 반환 값 처리 등을 명시한다.

C++에서는 주로 네 가지 함수 호출 규약이 사용된다: __cdecl, __stdcall, __fastcall, 그리고 __thiscall.

<br>

# 이걸 왜 사용하는 가?
-----------
첫째, 이 규약을 통해 컴파일러가 함수 호출을 어떻게 처리할지 알 수 있다. 

둘째, 이 규약은 프로그램의 실행 시간과 메모리 사용량을 최적화하는 데 도움이 된다.

## __cdecl
----------------
C와 C++에서 가장 일반적으로 사용되는 기본 함수 호출 규약입니다. cdecl은 "C declaration"의 약자로, C언어 선언 방식을 따르는 것을 의미합니다.

1. 매개변수 전달: cdecl 규약은 매개변수를 오른쪽에서 왼쪽으로 스택에 푸시합니다. 이 방식은 가변 인수 함수(variadic function)에 적합합니다.
2. 스택 정리: 호출자가 함수 호출 후 스택 정리를 담당합니다. 이는 함수 호출이 끝난 후 스택에서 매개변수를 제거하는 작업을 의미합니다.
3. 이름 장식: cdecl 규약은 함수 이름 앞에 밑줄(_)을 추가하여 이름을 장식합니다.

```cpp
#include <iostream>

void __cdecl Add(int a, int b) {
    std::cout << "두 정수의 합: " << (a + b) << std::endl;
}

int main() {
    Add(3, 5);
    return 0;
}
```

## __stdcall
-------------
Win32 API에서 주로 사용되는 함수 호출 규약입니다. __stdcall은 "Standard Calling"의 약자로, 표준 호출 방식을 따르는 것을 의미한다.

1. 매개변수 전달: __stdcall 규약도 cdecl 규약과 같이 매개변수를 오른쪽에서 왼쪽으로 스택에 푸시합니다.
2. 스택 정리: __stdcall 규약은 피호출자가 함수 호출 후 스택 정리를 담당합니다. 이는 함수가 반환될 때 함수 자체에서 스택을 정리하여 스택 메모리를 관리합니다.
3. 이름 장식: __stdcall 규약은 함수 이름에 밑줄(_)을 추가하고, 매개변수의 크기를 16진수로 표시하여 이름을 장식합니다. 예를 들어, void Add(int a, int b) 함수는 _Add@8로 장식됩니다.

```cpp
#include <iostream>

void __stdcall Add(int a, int b) {
    std::cout << "두 정수의 합: " << (a + b) << std::endl;
}

int main() {
    Add(3, 5);
    return
}
```

## __fastcall
------------
__fastcall 규약은 함수 호출의 속도를 최적화하기 위해 설계된 함수 호출 규약입니다.

1. 매개변수 전달: __fastcall 규약은 가능한 한 많은 매개변수를 CPU 레지스터를 통해 전달하려고 합니다. 일반적으로 첫 번째와 두 번째 매개변수가 레지스터(ECX, EDX)에 할당되며, 나머지 매개변수는 스택에 푸시됩니다.
2. 스택 정리: __fastcall 규약에서도 피호출자가 스택을 정리합니다.
3. 이름 장식: __fastcall 규약은 함수 이름 앞에 @ 기호를 붙여 이름을 장식합니다. 또한 매개변수의 총 크기를 16진수로 표시합니다. 예를 들어, void Add(int a, int b) 함수는 @Add@8로 장식됩니다.

```cpp
#include <iostream>

void __fastcall Add(int a, int b) {
    std::cout << "두 정수의 합: " << (a + b) << std::endl;
}

int main() {
    Add(3, 5);
    return 0;
}
```

__fastcall 규약은 함수 호출 속도를 최적화하는데 초점을 맞추고 있지만, 모든 매개변수를 레지스터에 할당할 수 없을 때는 스택을 사용해야 하므로 주의가 필요합니다.

## __thiscall
---------------
__thiscall 규약은 클래스의 멤버 함수를 호출할 때 사용되는 함수 호출 규약입니다.

1. 매개변수 전달: __thiscall 규약은 객체의 포인터(this 포인터)를 첫 번째 매개변수로 전달합니다. 이 포인터는 ECX 레지스터를 통해 전달되며, 다른 매개변수는 오른쪽에서 왼쪽으로 스택에 푸시됩니다.
2. 스택 정리: __thiscall 규약에서도 피호출자가 스택을 정리합니다.
3. 이름 장식: __thiscall 규약은 멤버 함수를 표현할 때 클래스 이름과 함께 함수 이름을 표시하며, 매개변수의 크기를 16진수로 표시합니다.

```cpp
#include <iostream>

class MyClass {
public:
    void __thiscall Add(int a, int b) {
        std::cout << "두 정수의 합: " << (a + b) << std::endl;
    }
};

int main() {
    MyClass myObj;
    myObj.Add(3, 5);
    return 0;
}
```