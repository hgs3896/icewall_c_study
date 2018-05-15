# 8 주차

8주차 : 구조체, 지금까지 내용 복습, 복합 과제 \(기한 일주일\)

**구조체란?**

복잡한 객체들은 일반적으로 같은 데이터 타입으로만 되어 있지 않다.

배열이 타입이 같은 데이터의 모임이라면, 구조체는 타입이 다를 수 있는 데이터를 묶는 방법이다.

c언어 에서는 구조체를 struct를 사용하여 표현한다.

```
struct person{
    char *name;
    int age;
    float height;
};
```

위와 같이 구조체의 형식이 정의한 다음 구조체 변수는 다음과 같이 생성한다.

sturct 구조체명 변수명;

**struct person p;**

와 같이 a 구조체 변수를 만들고 나면,

p.name = "yurim";

p.age = 20;

p.height = 180.5; 이런 식으로 이용할 수 있다.

매번 구조체를 선언 할 때, struct 구조체명 변수명;와 같은 형식으로 선언하는게 번거로울 때는 typedef라는 것을 이용하면 편리하다.

typedef\(type define\) : 형을 정의한다는 것을 의미한다.

예를 들어 typedef int element;라고 정의한다면, int 를 element라고 정의해서 int 대신 element 를 써도 되는 것이다.

```
typedef struct person{        
    char *name;            
    int age;
    float height;
}person;
```

이렇게 typedef로 정의하고 난 뒤에는

person p; 이런식으로 구조체 변수를 선언할 수 있다.

간단한 예제를 실행해보자.

```
#include <stdio.h>

typedef struct student {
  int id;
  char *name;
  float percentage;
}student; // 구조체 뒤에 세미콜론이 와야함

int main() {
  student s;
  s.id=1;
  s.name = "김철수";
  s.percentage = 90.5;
  printf("아이디: %d \n", s.id);
  printf("이름: %s \n", s.name);
  printf("백분율: %f \n", s.percentage);
  return 0;
}
```

위의 코드는 구조체를 만든후 구조체 변수 s를 초기화 한 뒤 출력한 예제이다.

만약 구조체 내의 각 변수들을 한 번에 초기화 하고 싶다면,

```
student s = {1,"김철수",90.5};
```

이렇게 간단하게 해도 된다.

###### 

그렇다면 이번에는 구조체 포인터를 이용해 구조체에 접근해보자.

```
#include <stdio.h>

typedef struct student {
  int id;
  char *name;
  float percentage;
}student; // 구조체 뒤에 세미콜론이 와야함

int main() {

  student employee, *stptr;
  stptr = &employee;
  stptr->id = 1;
  stptr->name = "홍길동";
  stptr->percentage =90.5;
  printf("직원 안내: 아이디=%d\n%s\n%f\n", stptr->id, stptr->name,
  stptr->percentage);
  return 0;
}
```

구조체를 가리키는 포인터로 구조체 변수에 접근하고 싶을 때는**.**대신에**-&gt;**를 이용해 접근한다.

만약 내가 해당하는 구조체 변수에 대해 여러 함수에서 접근해 값을 변경하고 싶다면, 구조체 포인터를 이용하는것이 좋다!

# 

# C 언어 수업 끝!!!! {#c-언어-수업-끝}

###### 

### 지금 까지 수업8 주동안 배운 것 중 어려웠던 개념들 지금 추가로 물어봐주세요! {#지금-까지-수업8-주동안-배운-것-중-어려웠던-개념들-지금-추가로-물어봐주세요}

###### 

_**마지막 복합형 과제!**_

character라는 구조체를 만들고 x,y 값을 입력 받으면 character 구조체에 서 c\_pos\_x, c\_pos\_y에 각각 저장한다. 그리고 이차원 배열\(4x4\)을 통해 캐 릭터의 좌표가 움직임을 보여준다.\(x,y 초기 값은 0으로\)

무한 루프로 계속 입력을 받으면서 캐릭터의 움직임을 보여주고, x나 y값에 에 음수가 입력되면, 프로그램을 종료한다. 이 같은 프로그램을 작성하시오. \(구조체 포인터로 구현해주세요!\)

###### ![](https://newrim.gitbooks.io/c-study_icewall/content/assets/스크린샷 2017-05-29 오후 5.02.25.png)

-&gt; 이 과제는 필수이니 모두 저한테 개인적으로 제출하시기 바랍니다!



http://blog.llvm.org/2011/05/what-every-c-programmer-should-know.html

http://blog.llvm.org/2011/05/what-every-c-programmer-should-know\_14.html

http://blog.llvm.org/2011/05/what-every-c-programmer-should-know\_21.html

