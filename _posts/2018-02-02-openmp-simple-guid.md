---
layout: post
title: OpenCV 간단한 사용법
description: >
  윈도우에서 OpenMP를 사용하는 방법을 기록하고자 한다. 사용해보니 C++에서 thread를 사용하는 것 보다 간편하다.
tags: [c/c++]
---
실험을 하기 위한 프로그램을 빠르게 개발하기 위해 JAVA로 만들었는데 JAVA는 멀티 쓰레드를 사용할 경우 JVM(Java Virtual Machine)에서 멀티코어를 알아서 잘 활용하게 되어있다.

하지만 실험 속도가 너무 느려서 성능 개선을 위해 C++로 다시 만들어야 했는데, C나 C++의 경우는 자원 공유 상황에 따라서 멀티코어를 잘 활용할 수도 있고, 활용을 잘 안할수도 있다고 한다.

그래서 OpenMP를 이용할것을 권장하길래 간단하게 윈도우에서 OpenMP를 사용하는 방법을 알아보고자 한다.
JAVA에서 Thread를 상속받아 만들거나, C#이나 C++처럼 함수를 스레드로 실행하는 것 보다 간편하다.
# 1. 설정
OpenMP는 조건부 컴파일 지시자 **#pragma**를 이용하기 때문에 혹여나 컴파일러에서 OpenMP를 지원하지 않더라도 컴파일 오류가 발생하지 않는다는 장점이 있다.

OpenMP를 따로 설치하지 않아도 Visual Studio에서 기본적으로 지원한다.

하지만 OpenMP 지원의 기본값이 **사용 안함**으로 되어있으므로 OpenMP를 사용하기 위해서는 설정을 해야 한다.

툴바에서 `프로젝트`->`{프로젝트이름}속성`->`구성속성`->`C/C++`->`언어`->`OpenMP 지원` 속성을 **예**로 설정하면 된다.

![](https://skaiblue.github.io/assets/img/posts/c/openmpguid/1.png "Visual Studio Setting")

# 2.사용법
아래는 OpenMP를 이용해 2중 반복문을 병렬로 처리하고 수행 시간을 출력하는 예제이다.

```C
#include <iostream>
#include <time.h>

void doNothing()
{

}

void func(int n, int m)
{
  for(int i = 0 ; i < n ;i +=1 )
  {
    for(int j = 0 ; j < m ; j +=1)
    {
      doNothing();
    }
  }
}

int main()
{
  clock_t start = clock();
  #pragma omp parallel for
  for (int i = 0 ; i < 4 ; i += 1)
  {
    func(100, 1000000);
  }
  std::cout << "run time = " << clock() - start << " milliseconds." << std::endl;
  return 0;
}
```

간단하게 for문 위에 아래의 문장을 작성하면 해당 반복문은 멀티 코어로 병렬 처리된다.
```C
#pragma omp parallel for
```
해당 라인이 있는 경우와 없는 경우에 대한 시간을 실행을 해서 측정 해보면 다음과 같다.

본인의 PC`i3 4세대 2코어 4스레드`에서의 결과는 다음과 같다.
