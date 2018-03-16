# 6 주차

6주차 : 포인터, 동적 할당 & 스택프레임 그리기

![](https://newrim.gitbooks.io/c-study_icewall/content/assets/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202017-05-16%20%EC%98%A4%EC%A0%84%2010.10.44.png)

포인터\(Pointer\)란 메모리의 주소 값을 담고있는 변수 혹은 상수이다. 비슷하게는 데이터의 위치를 가리키는 녀석이라고 할 수도 있다. 의외로 간단해 보일지도 모르겠지만 주소 값과 관련이 있어 메모리의 주소체계를 이해하지 못하면 포인터를 정확히 이해할 수 없다. 여기서 주소란 그 메모리의 저장장소의 위치를 나타내는 값으로 하나의 주소값은 1바이트 크기의 메모리 공간을 표현한다.

포인터 변수란 메모리 주소를 저장하는 변수이며 데이터 타입과 식별자\(=변수명\) 사이에 그저 \* 하나만 넣어주면 포인터 변수가 된다. 기본적인 데이터 타입과 구조체, 배열, 공용체에 대해서도 포인터형을 만들수가 있다. 그리고 & 연산자를 변수명 앞에다 가져오면 그 변수의 주소값을 반환하게 된다.

예제를 보며 좀 더 이해를 도와보자!

```
#
include
<
stdio.h
>
int
main
()
{
    
int
 num, num1, num2;

    num=
50
;
    num1=
72
;
    num2=
94
;
    
printf
(
"num의 저장 위치: %#x\n"
, 
&
num);
    
printf
(
"num1의 저장 위치: %#x\n"
, 
&
num1);
    
printf
(
"num2의 저장 위치: %#x\n"
, 
&
num2);
    
return
0
;
}

```

![](https://newrim.gitbooks.io/c-study_icewall/content/assets/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202017-05-16%20%EC%98%A4%EC%A0%84%2010.23.58.png)

위의 예제는 &연산자를 이용하여 각 변수의 저장 위치,즉 주솟값을 출력해 본 것이다.

이번에는_포인터_를 이용해 접근 해 보자.

```
#
include
<
stdio.h
>
int
main
()
{
    
int
 Number;
    
int
 *pNumber;

    Number=
50
;
    pNumber=
&
Number;

    
printf
(
"변수 Number의 값: %d\n"
, Number);
    
printf
(
"변수 Number의 주소값: %#x\n\n"
, pNumber);

    *pNumber=
60
;
    
printf
(
"변수 Number의 값: %d\n"
, Number);
    
return
0
;
}

```

![](https://newrim.gitbooks.io/c-study_icewall/content/assets/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202017-05-16%20%EC%98%A4%EC%A0%84%2010.25.59.png)

pNumber라는 int형 포인터를 만들고 그 포인터 변수가 Number를 가리키게 만들었다.\(pNumber=&Number\)

그리고나서 pNumber를 출력해보면, Number의 주솟값이 출력되는 것을 확인할 수 있다.

pNumber라는 포인터를 이용해서 Number의 값에 접근을 하고 싶다면 어떻게 해야할까?

pNumber라는 변수를 사용할 때\(포인터변수 선언할때 말고\)변수 이름앞에 \*을 붙이면,포인터가 가리키는 주소에 가서 그 값에 접근할 수 있게 된다.

#### 이번에는이중포인터에 대해 배우자. {#이번에는이중포인터에-대해-배우자}

이중 포인터는 \*을 두개를 붙여서 이중 포인터 변수를 선언한다.

```
#
include
<
stdio.h
>
int
main
()
{
    
int
 Num1=
50
, Num2=
100
;
    
int
 *pNum1=
&
Num1;
    
int
 **dpNum1=
&
pNum1;

    
printf
(
"정수형 변수 Num1의 값: %d\n"
, Num1);
    
printf
(
"pNum1이 가리키는 변수의 값: %d\n"
, *pNum1);
    
printf
(
"dpNum1이 가리키는 변수의 값: %d\n\n"
, **dpNum1);

    *dpNum1=
&
Num2; 
// pNum1=
&
Num2
printf
(
"정수형 변수 Num2의 값: %d\n"
, Num2);
    
printf
(
"pNum1이 가리키는 변수의 값: %d\n"
, *pNum1);
    
printf
(
"dpNum1이 가리키는 변수의 값: %d\n\n"
, **dpNum1);

    **dpNum1+=
150
;
    
printf
(
"정수형 변수 Num2의 값: %d\n"
, Num2);
    
printf
(
"pNum1이 가리키는 변수의 값: %d\n"
, *pNum1);
    
printf
(
"dpNum1이 가리키는 변수의 값: %d\n"
, **dpNum1);

    
return
0
;
}

```

예를 들면,\*이 하나있는 int형 포인터 변수는 int형 변수를 가리키게 된다.그렇다면 \*\*이 두개인 int형 이중 포인터 변수는 int형 포인터 변수를 가리키는 포인터의 포인터가 되는 것이다.

![](https://newrim.gitbooks.io/c-study_icewall/content/assets/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202017-05-16%20%EC%98%A4%EC%A0%84%2010.41.58.png)

포인터의 주소값을 저장하기 위해 포인터 형이 int \*\*인 변수에 저장하였다. 포인터 변수 dpNum1에서 \*를 한번만 사용하면 dpNum1이 가리키는 포인터 pNum1의 주소값을 참고한다. \*\*를 두번 사용하면 dpNum1이 가리키는 변수를 의미한다. 이런 녀석을 이중 포인터라고 부르며, 포인터 변수를 가리키는 포인터라고 한다.

###### 

###### _그렇다면,이러한 포인터들로 기본적인 연산을 할수 있을까?_ {#그렇다면이러한-포인터들로-기본적인-연산을-할수-있을까}

예제를통해 확인해보자!

```
#
include
<
stdio.h
>
int
main
()
{
    
char
 *pc;
    
int
 *pi;
    
double
 *pd;

    pc=(
char
 *)
100
;
    pi=(
int
 *)
100
;
    pd=(
double
 *)
100
;

    
printf
(
"pc 증가 전: %d\n"
, pc);
    
printf
(
"pi 증가 전: %d\n"
, pi);
    
printf
(
"pd 증가 전: %d\n\n"
, pd);
    pc++;
    pi++;
    pd++;
    
printf
(
"pc 증가 후: %d\n"
, pc);
    
printf
(
"pi 증가 후: %d\n"
, pi);
    
printf
(
"pd 증가 후: %d\n"
, pd);
    
return
0
;
}

```

각각의 char, int, double형 포인터들을 ++하면, 1씩 증가할까?

결과를 보자.

![](https://newrim.gitbooks.io/c-study_icewall/content/assets/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202017-05-16%20%EC%98%A4%EC%A0%84%2010.49.24.png)

결과를 보시면 포인터의 자료형의 크기만큼 증가한다는 것을 알수 있습니다. char는 1, short는 2, int는 4, float는 4, double는 8로 말입니다. 만약에 2 이상의 수를 더한다면 '포인터가 가리키는 변수 데이터 타입의 크기 \* 정수' 만큼 증가가 되는걸 보실수 있습니다. 뺄셈도 이와 마찬가지입니다.

![](https://newrim.gitbooks.io/c-study_icewall/content/assets/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202017-05-16%20%EC%98%A4%ED%9B%84%2012.51.17.png)

```
int
 *arr2; 
// 포인터를 배열 처럼도 사용 가능.
for
(
int
 i=
0
 ; i
<
2
 ;i++) {
    (arr2+i)=i; 
//arr[0]=0, arr[1]=1, arr[2]=2 이런식으로포인터를 배열처럼도쓸수있다

}

```

```
#
include
<
stdio.h
>
int
main
(
void
)
{


int
 arr[
5
] = {
1
, 
2
, 
3
, 
4
, 
5
};

int
 *ptr = arr;

for
(
int
 i=
0
 ; i
<
5
 ; i++){

    
printf
(
"%d\n"
,*(ptr+i)); 
// 포인터를 이용해 배열 접근. *(ptr+i)==arr[i].

}


return
0
;
}

```

![](https://newrim.gitbooks.io/c-study_icewall/content/assets/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202017-05-16%20%EC%98%A4%ED%9B%84%2012.51.33.png)![](https://newrim.gitbooks.io/c-study_icewall/content/assets/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202017-05-16%20%EC%98%A4%ED%9B%84%2012.55.20.png)

```
#
include
<
stdio.h
>
void
swap_value
(
int
 a, 
int
 b)
{

int
 temp = a;
a=b;
b=temp;
}


void
swap
(
int
 *n1, 
int
 *n2)
{

int
 temp = *n1;
*n1=*n2;
*n2=temp;
}


int
main
(
void
)
{

int
 n1,n2;
n1=
10
;
n2=
20
;
swap_value(n1, n2);

printf
(
"%d %d\n"
,n1,n2);
swap(
&
n1,
&
n2);

printf
(
"%d %d\n"
,n1,n2);

return
0
;

}

```

연습 해보기!

```
#
include
<
stdio.h
>
int
main
(
int
 argc, 
char
* argv[])
{
   
int
 arr[
5
];
   
for
 (
int
 i = 
0
; i 
<
5
; ++i) {
      arr[i] = i;
   }

   
int
* pNum = 
&
arr[
0
];
   
int
* pNum2 = 
&
arr[
3
];

   
int
** ppNum = 
&
pNum;

   *pNum += 
2
;
   arr[
0
] += 
10
;
   arr[
2
] -= 
2
;
   *pNum2 -= 
3
;

   (pNum)++;


   *pNum = 
103
;


   ppNum = 
&
pNum2;

   **ppNum = 
100
;

   (*ppNum)++;

   
for
 (
int
 i = 
0
; i 
<
5
; ++i) {
      
printf
(
"arr[%d] : %d\n"
, i, arr[i]);
   }


   
printf
(
"*pNum : %d\n"
, *pNum);
   
printf
(
"*pNum2 : %d\n"
, *pNum2);
   pNum2--;
   
printf
(
"**ppNum: %d\n"
, **ppNum);


   
return
0
;
}
```



