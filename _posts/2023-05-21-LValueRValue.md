---
layout: post
title: C++ r-value l-value
date: 2023-05-21 16:00:00 +0900
categories: C++ r-value_l-value
tags: r-value_l-value
---

# r-value l-value
--------
C++에서 r-value와 l-value는 변수나 표현식의 속성을 나타내며, <br/>
할당 연산자의 왼쪽이나 오른쪽에 올 수 있는지를 결정합니다.

## r-value
-----------
r-value는 이름이 없는 임시 값이며, 할당 연산자(=)의 오른쪽에만 올 수 있습니다.<br/> 
r-value는 값을 가질 수 있지만 변경할 수는 없습니다.

예를 들어,
```cpp
int x = 10; // '10'은 r-value입니다.
x = x + 5; // 'x + 5'는 r-value입니다.
```
여기서 '10'과 'x + 5'는 r-value로, 값이 있지만 변경할 수 없습니다. 이들은 임시 값이므로 이름이 없습니다.

## l-value
-----------
l-value는 메모리 위치를 참조하며, 할당 연산자(=)의 왼쪽이나 오른쪽에 올 수 있습니다.

즉, l-value는 값을 가질 수도 있고, 변경할 수도 있습니다.

l-value가 왼쪽인 경우의 예
```cpp
int x = 10; // 'x'는 l-value입니다.
x = 20; // 'x'는 값을 가질 수 있고 변경할 수도 있습니다.
```

l-value가 오른쪽인 경우의 예
```cpp
int a = 5;
int b = a;
```
a는 l-value로서 b에 값을 할당 했고, b도 l-value이기 때문에 a의 값을 할당 받은 코드입니다.