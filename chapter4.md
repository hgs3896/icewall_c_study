# 4 주차

4주차 : 조건문 + 반복문, 함수, 재귀호출식, 반복문 활용 : 별찍기

지난 주에 **if 문, switch 문 **을 배웠으니 복습을 위해 이를 활용 해보자!

만약 숫자를 입력 받고, 입력 받은 숫자가 3의 배수인지 확인하려면 어떻게 해야할까?

```
#include <stdio.h>

int main(int argc, char * argv[]) {
    int number;
    scanf("%d", &number);

    if (number % 3 == 0) {
        printf("3의 배수다.\n");
    }
    else {
        printf("3의 배수가 아니다.\n");
    }
}
```

###### 

위와 같은 코드로 입력받은 수 number가 3의 배수인지를 확인할 수 있다.

그렇다면, 내가 이 작업을 5번 반복하고 싶다면?..

1번의 Ctrl + C, 5번의 Ctrl + V를 시전하면 된다.

```
#include <stdio.h>

int main(int argc, char * argv[]) {
    int number;
    scanf("%d", &number);
    if (number % 3 == 0) {
        printf("3의 배수다.\n");
    }
    else {
        printf("3의 배수가 아니다.\n");
    }

    scanf("%d", &number);
    if (number % 3 == 0) {
        printf("3의 배수다.\n");
    }
    else {
        printf("3의 배수가 아니다.\n");
    }

    scanf("%d", &number);
    if (number % 3 == 0) {
        printf("3의 배수다.\n");
    }
    else {
        printf("3의 배수가 아니다.\n");
    }

    scanf("%d", &number);
    if (number % 3 == 0) {
        printf("3의 배수다.\n");
    }
    else {
        printf("3의 배수가 아니다.\n");
    }

    scanf("%d", &number);
    if (number % 3 == 0) {
        printf("3의 배수다.\n");
    }
    else {
        printf("3의 배수가 아니다.\n");
    }
}
```

하지만 반복되는 코드들을 계속 복사해서 쓴다면, 코드 라인이 늘어날수록 읽기 힘든 코드가 되어 가독성이 떨어지고,

반복되는 코드의 내용을 수정하기 위해 다시 복사와 반복을 해야겠죠?.

이 문제는 반복문과 함수를 통해 해결할 수 있습니다.

###### 

우선 반복문의 문법부터 살펴봅시다.

init-expression : 초기화 수식

condition-expression : 조건 수식

loop-expression : 반복을 위한 수식\(주로 증감식\)

```
for(init-expression; condition-expression; loop-expression)
    statement
```

###### 

statement는 하나의 문장이지만 중괄호로 묶은 { statement } 는 여러 문장을 하나의 문장으로 묶어주기에 여러 문장의 내용을 반복할 수도 있다.

실행순서는

1. init - expression \(initialize expression, 말 그대로 반복문에 필요한 변수를 맨 처음에 초기화 해주는 부분이다.\)
2. conditon-expression\(어떠한 조건에서 반복문을 실행할지 결정하는 부분이다.\)
3. statement\(반복할 실행문\)
4. loop-expression \(statement를 거친 다음 2번으로 돌아가기 전에 실행되는 부분, 주로 초기화된 변수에 대한 증감식이 들어감.\)

```
#include <stdio.h>

int main(int argc, char * argv[]) {
    int number;
    int i;
    for (i = 0; i < 5; i = i + 1) {
        scanf("%d", &number);
        if (number % 3 == 0) {
            printf("3의 배수다.\n");
        }
        else {
            printf("3의 배수가 아니다.\n");
        }
    }
    return 0;
}
```

제일 처음에 i를 0으로 초기화 한 후에, i는 5보다 작으므로 {}안에 있는 코드들을 실행하게 된다. number에 값을 입력 받고, 3의 배수인지 아닌지 판별하여 출력한 후에, i = i + 1을 실행한다.

그러면 i는 1이 되고, i는 5보다 작으므로 다시 입력받고, 3의 배수인지 판별한다.

이걸 5번 반복하면 i는 5이상이 되게 되어 i &lt; 5의 결과가 거짓이 되므로 for문 밖으로 빠져나와 return 0; 이 실행되게 된다.

for문을 쓰지 않을 때보다 훨씬 간결하지 않은가? 반복적으로 해야되는 작업들이 또 무엇이 있을까? 구구단을 예로 들어보자.

아래는 7단을 출력하는 예제이다.

```
#include <stdio.h>

int main(int argc, char * argv[]) {
    int number = 7;
    int i;
    for (i = 1; i <= 9; i = i + 1) {
        printf("%d x %d = %d\n", number, i, number*i);
    }
}
```

그렇다면 2단부터 19단까지 출력하려면 어떻게 해야할까? 위 반복문을 9번 반복하기 위해 9번 복사 붙여넣기를 할 것인가?

for문 안에 for문을 넣을 수 있다. 이런걸**이중 for문**이라고 한다. 예제를 보자.

```
#include <stdio.h>

int main(int argc, char * argv[]) {
    int dan, i;
    for (dan = 2; dan <= 19; dan++) {
        for (i = 1; i <= 9; i = i + 1) {
            printf("%d x %d = %d\n", dan, i, dan*i);
        }
    }
}
```

for문이 2개가 되었다. i를 기준으로 도는 for문이 있고, dan을 기준으로 도는 for문이 있다. 실행 순서는

1. dan을 2로 초기화한다.

2. dan &lt;= 9가 참인지 아닌지 판별한다.

3. {} 안에 있는 코드\(for문\)를 실행한다.

4. i를 1로 초기화한다.

5. i &lt;= 9가 참인지 아닌지 판별한다.

6. {} 안에 있는 코드\(printf\)를 실행한다.

7. i++을 실행한다.

8. i &lt;= 9가 거짓이 될 때까지 5-7을 반복한다.

9. dan++을 실행한다.

10. dan &lt;= 9가 거짓이 될 때까지 2-9를 반복한다.

###### 

for문을 중첩해서 쓰는 경우는 흔하지만, 너무 많이 중첩할 경우 역시 코드 읽기가 어려워지고 실행시간이 많이 소비되므로 주의해야한다.

###### 추가로 while문에 대해 알아보자. {#추가로-while문에-대해-알아보자}

```
int i=0;
while (condition-expression){ // 종결조건

    statement!

    i++;               // loop-expression, i 값을 1 증가시킨다.

}
```

for문과 다르게,변수의 초기화와,증감식이 괄호안에 따로 없다.

그렇기 때문에초기화는 while문 밖에서 증감식은 while문 안인 {}안에서 한다.

###### 

```
do
    statement
while(condition-expression);
```

do while문은 조건을 while문의 파생버전이다. while문은 조건 확인 후 {}안의 statement를 실행한다. 하지만, do while문은 먼저 do 뒤의 statement를 실행한 후, 조건식을 계산해서 0이 아니면 반복하고 아니면 반복을 끝내는 반복문이다.

while문의 차이?과 do-while문

while문은 조건에 부합하지 않으면 반복되는 statement를 실행하지 않지만, do-while문은 조건이 맞지 않더라도 적어도 한 번은 실행된다!

###### 

##### 이번에는 이를 함수 사용하여 더욱 간결하게 표현하는 법에 대해 알아보자. {#이번에는-함수를-어떻게-사용하는지에-대해-알아보자}

###### 

모든 작업을 전부 main 함수에 다 때려넣게 되면 인간이 보기에 적힌 코드를 한 눈에 보고 무슨 일을 하는지 알기 어렵다. 이를 위한 방법에는 함수라는 것이 존재한다. 우리가 자주 봤던 main도 함수이다.

함수의 표현 방법은

```
return_type function_name(parameters) {
    definition
}
```

이다. 위의 형식에서 definition이 빠진

return\_type function\_name\(parameters\);

위와 같은 형태를**선언**이라 하고,

return\_type function\_name\(parameters\) { definition }

위와 같은 형태는**정의**라고 한다. 함수를 쓰기 위해서는 선언이 먼저 되어있어야 하고, 선언된 함수는 반드시 후에 정의되어야 한다.

역시 그냥 보면 이해하기 힘드니 예제를 보자.

```
#include <stdio.h>
void gugudan(int dan);
int isThreeMultiple(int number) {
    if (number % 3 == 0) {
        return 1;
    } else {
        return 0;
    }
}

int main(int argc, char * argv[]) {
    int dan;

    for (dan = 2; dan <= 9; dan++) {
        if (isThreeMultiple(dan)) {
            gugudan(dan);
        }
    }
}

void gugudan(int dan) {
    int i;

    for (i = 1; i <= 9; i++) {
        printf("%d x %d = %d\n", dan, i, dan * i);
    }
}
```

3, 6, 9단만 출력하는 예제이다. return\_type은 함수가 종료된 후, 함수가 불러진 위치로 값을 전달하게 되는데 이때 전달되는 값의 type을 의미한다. void의 경우 return하는 값이 없고, int의 경우 int형의 값을 return한다.

function\_name은 함수 이름이다. 말 그대로 이름을 지어주면 된다.

\(\)안에 들어있는 것들은 파라미터이다. 함수가 호출된 곳에서 쓰던 지역 변수들을 함수 내에서 쓰려면 파라미터로 전달해주어야 한다. 함수의 호출이란 위의 코드에서 gugudan\(dan\);과 같이 만들어진 함수를 부르는 것을 의미한다.

뜬금 없이 지역변수 이야기가 나와서 당황했는가? 잠시 보고 넘어가자.

지역 변수는 가장 가까운 {} 안에 있는 변수들을 의미한다.

전역 변수는 모든 {} 밖에 있는 변수들을 의미한다.

예를 들어보자.

```
#include <stdio.h>

int thisIsGlobal = 2;

void function(int parameter) {
    int thisIsLocal2 = 20;

    printf("%d is global variable\n", thisIsGlobal);

    printf("%d is parameter\n", parameter);

    printf("%d is local variable\n", thisIsLocal2);

    // printf("%d is local variable\n", thisIsLocal);
}

int main(int argc, char * argv[]) {
    int thisIsLocal = 10;

    function(thisIsLocal);

    return 0;
}
```

모든 {} 밖에 있는 변수들은 전역변수라고 불리고, 같은 이름의 지역변수가 있지 않은 한, 모든 함수 내에서 사용할 수 있다. 위의 예제에서 thisIsGlobal이라는 이름의 전역변수가 있고, 이 전역변수는 function이라는 이름을 가진 함수 내에서 사용이 가능하다. {} 내부에 있는 변수들은 지역변수라고 불리고, 선언된 함수 내부에서만 쓸 수 있다. thisIsLocal은 main함수 에서 선언이 되었기 때문에 function에서 thisIsLocal 변수를 출력하려고 하면 에러가 나게 된다. 실험해 보고 싶다면 주석처리\(//\)를 지우고 컴파일 해보면 된다.

다시 함수 설명으로 돌아와 보자. 각 함수에서 선언된 지역변수는 선언된 함수 내에서만 사용이 가능하다. 따라서 선언된 곳과 다른 함수에서 쓰고 싶다면 파라미터로 넘겨주어야 한다. 파라미터로 넘겨주는 방법은 함수를 호출 할 때 \(\) 안에 , 로 구분하여 써주면 된다. 각자 두 개의 int형의 파라미터를 받아서 덧셈을 하는 함수를 만들어 보면서 연습해보도록 하자.

함수에 대해 이해했다면 재귀에 대해서 이해하는 것도 필요하다. 재귀란 자기 자신을 호출하는 것을 말한다. 따라서 재귀 함수는 자기 자신을 호출하는 함수를 의미한다. 간단한 예시를 들어보면 이해가 빠를 것이다.

```
#include <stdio.h>
int factorial(int n) {
    if (n == 0) {
        return 1;
    }
    else {
        return n * factorial(n - 1);
    }
}
int main(int argc, char * argv[]) {
    int number;

    scanf("%d", &number);

    printf("factorial result of %d : %d\n", number, factorial(number));

    return 0;
}
```

고등학교 때 배웠던 팩토리얼 연산을 코드로 옮겨 본 것이다.\(재귀 함수를 설명할 때 자주 등장하는 예시이다.\) 만약 4를 입력한다면 factorial\(4\)가 호출될 것이고, factorial\(4\)에서는 n이 0이 아니기 때문에 n \* factorial\(3\)을 연산하기 위해 factorial\(3\)을 호출할 것이다. 이 과정이 반복되는 것을 나타내 보면

return 4 \* factorial\(3\)

return 4 \* 3 \* factorial\(2\)

return 4 \* 3 \* 2 \* factorial\(1\)

return 4 \* 3 \* 2 \* 1 \* factorial\(0\)

return 4 \* 3 \* 2 \* 1 \* 1

과 같이 될 것이다.

재귀 함수에서는 종결 조건을 잘 설정해주는 것이 중요하다. 위의 예제 코드에서는

If\(n == 0\) return 1; 과 같은 종결조건을 설정해주었다. 재귀 함수를 조금 더 연습해 보고 싶다면 피보나치 수열을 계산하는 함수를 만들어 보면 될 것이다.

재귀 함수는 반복문으로 대체 가능하다. for, while에 비해 오버헤드도 많다. 그러나 프로그래밍에서 사용되는 개념이기 때문에 알고 넘어가야 한다. 재귀함수가 활용되는 곳은 함수형 프로그래밍, DFS와 같은 알고리즘 등이 있다.

여담으로 몇 가지를 더 설명하자면, static, 스택 프레임, call by value, call by reference가 있지만.. 포인터를 설명한 후에 듣는 것이 이해가 편하니 다음 주차에서 듣도록 하자. 먼저 궁금하다면 스터디를 진행하는 강사 혹은 조교에게 설명을 해 달라고 하면 된다.

## ※ ~~\(컴공이면 이맘때 쯤 만들어보는\)~~ 별찍기

1\) 삼각형의 높이를 입력받아 아래와 같은 직각 삼각형 만들기

5

\*

\*\*

\*\*\*

\*\*\*\*

\*\*\*\*\*

```
#include <stdio.h>

int main(void){
    int n, i, j;
    scanf("%d", &n);
    for(i=1;i<=n;i=i+1){
        /* i번 째 줄에는 별 i개 출력 */
        for(j=1;j<=i;j=j+1){
            /* 별 하나 출력 */
            printf("*");
            /* 문자 하나만 출력을 하는 경우에 한해 사용가능한 함수 putchar 를 이용해도 됩니다.
             * printf 대신 하나의 char를 출력할 수 있는 putchar함수를 이용해도 됩니다.
             * ex) putchar('*');
             * 단, 이 때는 쌍 따옴표가 아니라 따옴표를 써서 단일한 문자 하나임을 명시해야해요.
             */
        }
        /* 한 줄 출력이 끝나면 엔터를 치기 */
        printf("\n"); // putchar('\n');을 해도 돼요.
    }
}
```

만약, 위와 같은 중첩된 for 반복문을 사용하기가 싫다면, printf의 서식 기능을 이용해도 돼요.

```
#include <stdio.h>

int main(void){
    int n, i;
    scanf("%d", &n);
    for(i=1;i<=n;i=i+1)
        /* i번 째 줄에는 적절히 i개 별 출력 후 엔터 */
        printf("%-*.*s\n", n, i, "**********************************************************************");
        /*
         * 서식 문자에 대한 설명
         * - : 왼쪽 정렬
         * *.* : 점(.) 기준으로 왼쪽 *은 printf함수의 두번 째 인자에서 받아오고, 오른쪽 *은 세번 째 인자에서 받아오고, 마지막 s는 서식이 필요한 문자열인 * 70개짜리 문자열을 의미해요.
         * 그래서 n = 5, i = 3이라면 -*.*s는 '왼쪽 정렬을 하되, 일단 최소한 5칸을 출력하도록 하는데, 서식이 필요한 문자열에서 받아올 수 있는 가장 긴 문자열의 길이는 3칸이다'라는 의미에요.
         * 이에 맞는 출력 결과는 "***  \n"(*문자(3개) + 띄어쓰기(2개) + 엔터문자[\n] (1개) + 널문자[\0] (1개) = 7자)가 되는 것이죠.
         */
}
```

printf의 서식 기능을 이용하면 \* 찍기와 같은 일들은 매우 간단하게 해결할 수 있어요.

2\) 오른쪽으로 정렬된 별찍기

5

\_\_\_\_\*

\_\_\_\*\*

\_\_\*\*\*

\_\*\*\*\*

\*\*\*\*\*

```
#include <stdio.h>

int main(void){
    int n, i;
    scanf("%d", &n);
    for(i=1;i<=n;i=i+1)
        /* i번 째 줄에는 오른쪽으로 정렬된 i개 별 출력 후 엔터 */
        printf("%*.*s\n", n, i, "**********************************************************************");
}
```

3\) 이등변 삼각형 모양의 별 찍기

```
#include <stdio.h>

int main(void){
    int n, i;
    scanf("%d", &n);
    for(i=1;i<=n;i=i+1)
        /* i번 째 줄에는 최소 n + i개의 칸에 2i-1개의 별이 출력된 후 엔터 */
        printf("%*.*s\n", n + i, 2*i-1, "**********************************************************************");
}
```

4\) 다이아몬드 모양의 별 찍기

```
#include <stdio.h>

int main(void){
    int n, i;
    scanf("%d", &n);
    for(i=1;i<=n;i=i+1)
        printf("%*.*s\n", n + i, 2*i-1, "**********************************************************************");
    // 재활용
    for(i=n-1;i>=1;i=i-1)
        printf("%*.*s\n", n + i, 2*i-1, "**********************************************************************");
}
```



