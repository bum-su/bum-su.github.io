---
layout: post
title: C++ 동적 할당
date: 2023-05-20 22:00:00 +0900
categories: C++ DynamicAllocation
tags: DynamicAllocation Pointer MemoryLeak
---

# 동적 할당이란?
---------

런타임에서 메모리의 크기를 결정하는 프로세스를 말합니다. 

이는 프로그램이 실행되는 동안 필요한 메모리를 할당하고, <br/>더 이상 필요하지 않을 때 메모리를 반환하는 것을 가능하게 합니다.

## malloc 과 free 함수
--------------

C 프로그래밍 언어에서 동적 메모리 할당과 해제를 위해 사용되는 함수입니다. <br/><stdlib.h> 헤더 파일에 정의되어 있습니다.

### malloc 함수

주어진 크기의 바이트를 할당하고, 할당된 메모리 블록의 첫 번째 바이트에 대한 포인터를 반환합니다. 

이 함수는 프로그램의 힙 영역에 메모리를 할당합니다.<br/>
다음은 malloc 함수의 정의입니다.

```cpp
void* malloc(size_t size);
```
size는 할당하려는 메모리의 크기(바이트 단위)입니다. 

메모리가 성공적으로 할당되면, 함수는 할당된 메모리 블록의 첫 바이트에 대한 포인터를 반환합니다. 

만약 메모리 할당에 실패하면 NULL을 반환합니다.

예를 들어, int의 동적 배열을 생성하려면 다음과 같이 할 수 있습니다.

```cpp
int* array = (int*)malloc(10 * sizeof(int));  // Allocates memory for an array of 10 integers.
```

(int*)는 C 언어에서 캐스팅 연산자입니다. <br/>
(int*)는 malloc이 반환하는 void*를 (int*)로 변환해서 void* 대신 int*로 반환합니다. <br/>

int*는 malloc이 할당한 첫번째 주소를 가리키고,<br/>
포인터 변수 array에 malloc이 할당한 첫번째 주소가 저장된다. <br/>
그래서 *array는 malloc이 할당한 주소의 값을 참조할 수 있게 된다.

### free 함수

malloc, calloc, 또는 realloc에 의해 할당된 메모리 블록을 해제합니다. 사용법은 다음과 같습니다:

```cpp
void free(void* ptr);
```
void* ptr는 해제하려는 메모리 블록의 포인터입니다. free 함수는 해당 메모리 블록을 해제하고, 그 메모리를 시스템에 반환합니다. 

이렇게 해야만 그 메모리는 다시 malloc, calloc 또는 realloc에 의해 재사용될 수 있습니다.

free 함수를 사용한 예는 다음과 같습니다:
```cpp
free(array);  // Frees the memory previously allocated for the array.
```


## new 와 delete 연산자
-------------

C++에서 new와 delete는 동적 메모리 할당과 해제를 위한 연산자입니다. 

### new 연산자
new 연산자는 메모리를 할당하고, 해당 타입의 객체를 그 메모리에 생성하는 역할을 합니다. 

그리고 할당된 메모리의 주소를 반환합니다. 예를 들어,
```cpp
int* p = new int;  // Allocates memory for an integer and returns a pointer to it
```
또한, new 연산자는 동적 배열 할당에도 사용될 수 있습니다:
```cpp
int* arr = new int[10];  // Allocates memory for an array of 10 integers
```
### delete 연산자
delete 연산자는 new에 의해 할당된 메모리를 해제하는 역할을 합니다. 

delete는 해당 메모리에 있는 객체를 소멸시키고, 그 메모리를 시스템에 반환합니다. 예를 들어,
```cpp
delete p;  // Deallocates the memory previously allocated by new
```
배열에 대한 메모리 해제는 delete[]를 사용하여 수행됩니다:
```cpp
delete[] arr;  // Deallocates the memory for the array
```

# new, delete 와 malloc, free의 차이
-----------
## Constructor and Destructor
new와 delete는 생성자와 소멸자를 자동으로 호출합니다. 이는 new를 사용하여 객체를 생성할 때 해당 객체의 생성자가 호출되고, delete를 사용하여 객체를 해제할 때 해당 객체의 소멸자가 호출된다는 것을 의미합니다. 

반면에, malloc과 free는 단순히 메모리를 할당하고 해제합니다. 이들은 생성자나 소멸자를 호출하지 않습니다.

## Type Safety
new는 타입 안전(type safe)을 보장합니다. 즉, new를 사용하여 메모리를 할당하면 해당 타입의 포인터가 반환됩니다. 

반면에, malloc은 void*를 반환하므로 프로그래머가 적절한 타입으로 캐스팅해야 합니다.

## Memory Allocation
new와 delete는 연산자이며, malloc과 free는 함수입니다. 

이는 new와 delete가 C++의 일부이고, malloc과 free가 C 라이브러리의 일부라는 점에서 중요합니다. 이로 인해 두 쌍 사이에는 메모리 할당 방식에서 차이가 있을 수 있습니다.

## Error Handling
new 연산자는 메모리 할당에 실패하면 예외를 던집니다. 

반면에, malloc은 메모리 할당에 실패하면 NULL을 반환합니다.

## Overloading
new와 delete 연산자는 C++에서 오버로딩(overloading)할 수 있습니다. 즉, 프로그래머는 이들 연산자의 동작을 자신의 요구 사항에 맞게 변경할 수 있습니다. 

반면에, malloc과 free는 오버로딩할 수 없습니다.