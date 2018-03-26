# 7 주차

7주차 : argv, argc 이해하기, 동적 메모리 할당 & 스택프레임 그리기, use after free 취약

##### 

##### 오늘은 이 C 스터디의 첫 시간에 배웠던_argv, argc_에 대해 다시 짚고 넘어가보자. {#오늘은-이-c-스터디의-첫-시간에-배웠던-argv-argc에-대해-다시-짚고-넘어가보자}

그 때는 그 내용이 너무 생소해서 아마 잘 이해가 안 갔을 것이다.

이번 수업을 들으면서, 아 그 때 그런 의미였구나!! 라고 깨닫기를 바란다.

```
#include <stdio.h>
int main(int argc, char * argv[])
{
    printf("parameter 개수 : %d\n",argc);
    for(int i=0 ; i<argc; i++)
        printf("%s\n",argv[i]);
    return 0;
}
```

이 코드를 분석해보자.

지금까지 수업을 하면서, 함수라는 개념에 대해서 알게 되었을 것이다.

함수는 return\_type func\_Name\(parameter\) 이런형식이다.

return과 parameter 모두 있어도 되고 없어도 된다.

main은 프로그램의 시작점이 되는 함수이다. 그렇다면, main에 parameter를 어떻게 줘야 할까?

```
gcc -o w word.c
```

위의 명령문을 linux의 terminal 창에서 실행하면, w라는 실행파일 이 생긴다. 이 word.c라는 파일을 gcc라는 컴파일러로 컴파일 해서 w라는 실행파일\(exe\)를 만든다는 의미이다.

###### 

실행 화면을 보면서 이해해보자.

![](https://newrim.gitbooks.io/c-study_icewall/content/assets/스크린샷 2017-05-22 오전 11.26.57.png)

**./라는 명령어**는 실행파일을 실행시키는 명령어이다.

./w라는 명령문으로 w라는 실행파일을 실행시킨다. 이때 실행과 동시에 main 함수에 hi hello라는 문자열을 전달한다.

main에 parameter\(인자\)를 전달할 때는**./실행파일명**쓰면 된다.

위의 실행화면 처럼 여러개를 전달할 수 있고, 전달되는 인자는 모두_문자열_형태로 전달된다. 그리고**실행파일명까지 함께 전달**이 된

전달된 문자열들은 argv라는 문자열의 배열 안에 차례차례 담긴다.

argc는 넘어오는 인자의 개수이다.

# 

---

# 

## 동적 메모리 할당 {#동적-메모리-할당}

동적 메모리 할당이란 프로그램이 실행 도중에 동적으로 메모리를 할당 받는 것을 말한다. 보통 프로그램이 메모리를 할당받는 방법에는 정적과 동적 두 가지가 있다. 정적 메모리 할당은

int buffer\[100\]; 와 같이 프로그램이 시작되기 전에 미리 그 크기를 아는 경우이다.

동적 메모리 할당은 프로그램의 실행 도중에 메모리를 할당 받는 것이다. 프로그램에서는 필요한 만큼의 메모리를 시스템으로부터 동적으로 할당받아서 사용하고, 사용이 끝나면 시스템에 메모리를 반납한다.

필요한 만큼만 할당을 받고 또**필요한 때에 사용하고 반납할 수 있기 때문에 메모리를 효율적**으로 사용할 수 있다.

C언어에서는 malloc이라는 함수를 지원하여 동적메모리를 할당할 수 있으며, Memory Allocation\(메모리 할당\)을 줄여서 함수 명을 지은 것으로 보인다. 이 함수는 stdlib.h 헤더파일을 인클루드해야 사용할 수 있다. 사용법은 다음과 같다.

![](https://newrim.gitbooks.io/c-study_icewall/content/assets/malloc.png)

###### 

malloc 함수는 인자로 들어온 메모리 크기값 만큼 메모리를 할당하여 void\* 자료형으로 반환한다. 따라서 자신이 원하는 자료형으로 형변환을 시켜줄 필요가 있다.

이렇게 형변환을 해주는 가장 큰 이유는 나중에 메모리에 접근할 때 얼마만큼의 메모리를 읽을 것인지를 판단하기 위해서이다. 예를 들어 int\*의 경우 메모리 참조를 할 떄 메모리 영역을 4byte만큼만 읽을 것이다

###### 

그렇다면, 사용한 메모리의 반납은 어떻게 할까?

```
    free(iptr);
    free(cptr);
    free(dptr);
```

이런 식으로 free라는 함수를 통해 메모리를 해제한다.

동적할당된 메모리를 해제하는 것은 매우 중요한 일이다. 프로그램이 실행되는 동안에는 할당된 메모리가 사용되지 않는 중에도 계속 남아있기 때문이다. 예를 들어 게임에서 맵을 로딩하고 다른 맵으로 넘어갈 때 해제하지 않는다면? RAM이 버티질 못해서 컴퓨터가 꺼질 것이다. 프로그램에 필요한 최소한의 메모리를 사용하는 것은 운영체제나 다른 프로그램을**조화롭게 사용**하기 위해서 매우 중요한 일이다.

###### 

이번에는 배열을 동적으로 할당해보자.

```
int* ptr = (int*)malloc(sizeof(int) * 10);
```

위 코드는 sizeof\(int\)에 10을 곱한 크기 만큼, 즉 길이가 10인 정수형 배열을 동적할당 한 것이다. 단순히 malloc의 인자로 들어가는 값을 곱한 것이다.

![](https://newrim.gitbooks.io/c-study_icewall/content/assets/2.png)

세로 8, 가로 6의 배열을 동적할당한다고 할 때, 위 같이 코드를 작성할 수 있다.

위에서 우리가 다루었던 내용들을 생각해보면 일단 가로 6의 배열을 8개를 만들면 된다는 것을 떠올려볼 수 있다. 역순으로 생각하면 길이 6의 배열을 할당할 길이 8의 포인터 배열을 동적할당하고, 순차적으로 길이 6의 배열을 할당하면 세로 8, 가로 6의 배열을 만들 수 있는 것이다. 그래서 소스코드 1번 라인에서 우선 포인터 배열을 동적할당하기 위해 2차 포인터를 만들고 malloc으로 동적할당 했다. 그리고 for문으로 할당된 포인터 배열을 돌면서 길이 6의 정수형 배열을 모두 할당했다.

###### 

이렇게 만들어진 2차원 배열은 2가지 방식으로 사용할 수 있다.

int arr\[8\]\[6\]의 array

1. 포인터를 사용하는 방식!

arr\[1\]\[2\];

int \*\* pptr = arr;

\*\(\*\(pptr+1\)+2\) ==arr\[1\]\[2\]

![](https://newrim.gitbooks.io/c-study_icewall/content/assets/ptr.png)

1. 배열 형식으로 참조하는 방식

![](https://newrim.gitbooks.io/c-study_icewall/content/assets/arr.png)

###### 

_**2차원 배열 메모리 해제하는 법**_

```
for(int y = 0; y < 8; y++) {
            free(*(pptr + y));
 }
 free(pptr);
```

먼저 각각의 여러 행에 할당된 메모리를 해제하고

전체 pptr을 해제한다.

1차원 하나의 행으로만 이루어진 것이기 때문에 free를 한번만 하면 된다.

###### 

이러한 동적 메모리는 메모리의 heap이라는 영역에 할당된다.

![](https://newrim.gitbooks.io/c-study_icewall/content/assets/스크린샷 2017-05-23 오전 10.32.42.png)

데이터 영역: 전역 변수와 static 변수가 할당되는 영역

* 프로그램의 시작과 동시에 할당되고, 프로그램이 종료되어야 메모리에서 소멸됨

스택 영역 : 함수 호출 시 생성되는 지역 변수와 매개 변수가 저장되는 영역

* 함수 호출이 완료되면 사라짐

스택 영역에 함수와 변수들이 어떻게 쌓였다가 리턴되는지 파악할 수 있는 그림을 stack frame이라고 한다._**fibonacci 함수를 구현하는 코드로 간단한 스택프레임**_을 그려보자.

```
#include <stdio.h>

int fibonacci( int n )
{
    if( n == 1 || n == 2 )
    {
        return 1;
    }

    return fibonacci( n - 1 ) + fibonacci( n - 2 );
}

int main()
{
    int input;
    int i;

    printf( "input number : " );
    scanf( "%d", &input );

    for( i = 1; i <= input; i++ )
    {
        printf( "%d ", fibonacci( i ) );
    }
    printf( "\n" );

    return 0;
}
```

### fibo\(4\)의 stack frame {#fibo4의-stack-frame}

##### ![](https://newrim.gitbooks.io/c-study_icewall/content/assets/스택프레임.png)

##### 

##### _heap영역에서도 5주 수업 때 얘기 했던 overflow\(stack에서 일어나\) 취약점이 비슷한 형식으로 발생할 수 있다._ {#heap영역에서도-5주-수업-때-얘기-했던-overflowstack에서-일어나-취약점이-비슷한-형식으로-발생할-수-있다}

##### ![](https://newrim.gitbooks.io/c-study_icewall/content/assets/스크린샷 2017-05-23 오전 10.44.03.png)

그리고 free라는 함수로 인해 생기는 Use After Free 라는 취약점도 발생합니다.

```
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
    int* heap1;
    int* heap2;
    int* heap3;

    heap1 = (int*)malloc(256);
    heap2 = (int*)malloc(256);

    printf("heap1 : %p\n",heap1);
    printf("heap2 : %p\n",heap2);

    *heap2 = 1234;
    printf("heap2 number : %d\n",*heap2);

    free(heap2);
    printf("free heap2\n");

    heap3 = (int*)malloc(256);
    printf("new heap : %p\n",heap3);
    printf("new heap number: %d\n",*heap3);

    return 0;
}
```

##### 

---

_**오늘의 과제!!**_

![](https://newrim.gitbooks.io/c-study_icewall/content/assets/snail.png)  
숫자 n을 입력 받은 후 그림과 같이\(달팽이 배열\) n\*n배열을 출력하는 프로그램을 작성하시오.

-&gt; 동적 메모리 할당 이용

###### \*달팽이가 어렵다면 그냥 쭉 1~n\*n까지 출력해도 됩니다. {#달팽이가-어렵다면-그냥-쭉-1nn까지-출력해도-됩니다}



