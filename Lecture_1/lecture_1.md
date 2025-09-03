# C

## 키워드

- source code
- machine code
- compiler
- GUI(Graphic User Interface)
- CLI(Command-line Interface)
- code, make, ./{machine_code_name}
- ls
- printf
- escape sequence(\n, \t, ...)
- library

## 내용

💡 Source Code

프로그래밍 언어로 작성된 코드를 소스 코드(source code)라고 한다. 하지만 컴퓨터는 이 소스코드를 이해하지 못한다. 왜냐하면 컴퓨터는 0과 1로만 이뤄진 이진 코드 바이너리 시스템이기 때문이다. 그래서 소스 코드를 컴퓨터가 알아볼 수 있도록 머신 코드(machine code) 번역하는 작업이 필요하다.

소스 코드를 머신 코드로 번역해주는 일을 하는 번역기의 이름은 컴파일러(compiler)다.

💡 Visual Studio Code

VSCode에는 GUI(Graphic User Interface)와 CLI(Command-line Interface)가 내장되어 있다.

💡 세 가지 명령

```bash
code hello.c
```

명령으로 VSCode에서 파일을 생성할 수 있다.

```bash
make hello
```

명령으로 컴파일러를 통해 소스 코드를 기계어 코드로 변환한다.

```bash
./hello
```

명령으로 기계어 코드를 실행한다.

💡 'hello, world!'를 출력하는 코드를 작성하고 실행해 보자.

1. 'hello.c'파일 생성

```bash
code hello.c
```

2. 소스 코드 작성

```c
#include <stdio.h>

int main(void)
{
    printf("hello, world!\n");
}
```

3. 컴파일러를 사용해 기계어로 번역

```bash
make hello
```

4. 기계어 코드 실행

```bash
./hello
```

💡 ls 터미널 명령어

list의 약어

💡 printf() 함수

printf() 함수에는 문자열을 입력하는데, 문자열은 큰따옴표쌍(`""`)으로 감싸야 한다.

❗️ hello, world$

printf() 함수에 문자열을 전달할 때 \n 기호를 추가하지 않으면 'hello, world$'라고 출력된다. 일종의 사소한 버그이다. 

💡 이스케이프 시퀀스

'new line'을 의미하는 '\n' 같은 명령을 이스케이프 시퀀스라고 한다. new line 말고도 많은데, 실제로 실무에서 사용할 수 있는 것은 거의 없다. 

- \n: 커서를 다음 라인으로 이동한다.
- \r: 커서를 시작 부분으로 이동한다.
- \t: 탭 이후로 커서를 이동한다.
- \\": 문자열 내에서 "를 표현
- \\': 문자열 내에서 '를 표현
- \\: 문자열 내에서 \를 표현
- ...

예시:
```c
#include <stdio.h>

int main(void)
{
    printf("\"hello, world\"\n");
}
```

💡 헤더 파일

`#include <stdio.h>` 처럼 .h로 끝나는 모든 파일을 헤더 파일이라고 부른다.

만약 헤더 파일을 include 하지 않는다면:

```c
int main(void)
{
    printf("hello, \"world!\"\n");
}
```

```text
cc     hello.c   -o hello
hello.c:3:5: error: call to undeclared library function 'printf' with type 'int (const char *, ...)'; ISO C99 and later do not support implicit function declarations [-Wimplicit-function-declaration]
    3 |     printf("hello, \"world!\"\n");
      |     ^
hello.c:3:5: note: include the header <stdio.h> or explicitly provide a declaration for 'printf'
1 error generated.
make: *** [hello] Error 1
```

이런 에러가 뜬다. 이 에러는 하나하나 뜯어보면 무슨 문제인지 알 수 있다. 

'hello.c:3:5'는 'hello.c 파일:3번째 줄:5번째 문자'를 뜻한다. 그리고 에러 메시지를 보면 작성한 코드의 맨 위에 해당 헤더 파일을 포함하지 않으면 일반적으로 라이브러리(Library)라는 곳에 접근할 수 없다. 

💡 Libraries

라이브러리는 다른 사람이 모두를 위해 작성한 코드 모음이다. 그렇기 때문에 위에서 printf() 함수를 이용해야 하는데 '#include <stdio.h>'를 명시하지 않아서 라이브러리에 접근하지 못해 에러가 발생한 것이다. 참고로, 'stdio.h'는 표준 I/O 헤더 파일이다.

💡 'CS50' 라이브러리를 이용해 입력을 받아보자.



```c
#include <cs50.h>
#include <stdio.h>

int main(void)
{
    string answer = get_string("What's your name? "); // cs50.h 헤더 파일에서 제공하는 'get_string()' 함수
    printf("hello, %s\n", answer);
}
```