# C

## 1. **소스 코드와 머신 코드**
- **소스 코드 (Source Code)**: 프로그래밍 언어(C 등)로 작성된 코드.
- **머신 코드 (Machine Code)**: 컴퓨터가 이해할 수 있는 0과 1로 이루어진 이진 코드.
- **컴파일러 (Compiler)**: 소스 코드를 머신 코드로 번역.
  - 예: `make hello`는 소스 코드를 컴파일하여 머신 코드 생성.
  - 실행: `./hello`로 컴파일된 프로그램 실행.

---

## 2. **Visual Studio Code (VSCode)**
- **GUI (Graphic User Interface)**: 그래픽 기반 인터페이스.
- **CLI (Command-line Interface)**: 터미널 명령어로 파일 관리 및 코드 실행.
- **기본 명령어**:
  - `code hello.c`: VSCode에서 `hello.c` 파일 생성/열기.
  - `make hello`: 소스 코드를 컴파일.
  - `./hello`: 컴파일된 프로그램 실행.

---

## 3. **기본 예제: Hello, World!**
1. 파일 생성:
   ```bash
   code hello.c
   ```
2. 소스 코드 작성:
   ```c
   #include <stdio.h>
   int main(void)
   {
       printf("hello, world!\n");
   }
   ```
3. 컴파일:
   ```bash
   make hello
   ```
4. 실행:
   ```bash
   ./hello
   ```
   - 출력: `hello, world!`

---

## 4. **printf() 함수와 이스케이프 시퀀스**
- **printf()**: 문자열을 출력하는 함수. 문자열은 큰따옴표(`""`)로 감싸야 함.
  - 예: `printf("hello, world!\n");`
  - `\n` 없이 출력 시 커서가 다음 줄로 이동하지 않음 (예: `hello, world$`) → 사소한 버그.
- **이스케이프 시퀀스 (Escape Sequence)**:
  - `\n`: 새 줄로 이동.
  - `\r`: 커서를 줄의 시작으로 이동.
  - `\t`: 탭 간격.
  - `\"`, `\'`, `\\`: 각각 `"`, `'`, `\` 문자 출력.
  - 예:
    ```c
    #include <stdio.h>
    int main(void)
    {
        printf("\"hello, world\"\n"); // 출력: "hello, world"
    }
    ```

---

## 5. **헤더 파일과 라이브러리**
- **헤더 파일**: `.h`로 끝나는 파일 (예: `stdio.h`).
  - `#include <stdio.h>`: 표준 입출력 라이브러리 포함.
  - 포함하지 않으면 `printf` 같은 함수 사용 시 에러:
    ```text
    cc     hello.c   -o hello
    hello.c:3:5: error: call to undeclared library function 'printf'...
    note: include the header <stdio.h> or explicitly provide a declaration for 'printf'
    ```
  - 에러 해석: `hello.c:3:5`는 `hello.c` 파일의 3번째 줄, 5번째 문자에서 문제 발생.
- **라이브러리 (Library)**: 다른 개발자가 작성한 코드 모음.
  - `stdio.h`: 표준 I/O 함수(`printf`, `scanf` 등) 제공.

---

## 6. **CS50 라이브러리**
- **CS50 헤더 파일**: `<cs50.h>`는 사용자 입력을 쉽게 받는 함수 제공 (예: `get_string`, `get_int`).
- **문제점 예시**:
  ```c
  #include <cs50.h>
  #include <stdio.h>
  int main(void)
  {
      string answer = get_string("What's your name? ");
      printf("hello, answer\n"); // 잘못된 출력: "hello, answer"
  }
  ```
  - **해결**: 플레이스홀더(`%s`) 사용.
    ```c
    printf("hello, %s\n", answer); // 올바른 출력: "hello, 사용자입력"
    ```

---

## 7. **터미널 명령어**
- **파일 및 디렉토리 관리**:
  - `cd`: 디렉토리 이동.
  - `cp`: 파일 복사 (예: `cp hello.c backup.c`).
  - `ls`: 디렉토리 내 파일 목록.
  - `mkdir`: 디렉토리 생성 (예: `mkdir hello`).
  - `mv`: 파일 이동/이름 변경 (예: `mv hello.c hello/old.c`).
  - `rm`: 파일 삭제 (예: `rm hello`).
  - `rmdir`: 빈 디렉토리 삭제 (예: `rmdir hello`).
- **예제**: `hello.c`를 `hello/` 디렉토리로 이동 및 복구:
  ```bash
  rm hello           # 머신 코드 삭제
  mkdir hello        # 디렉토리 생성
  mv hello.c hello   # 파일 이동
  cd hello           # 디렉토리로 이동
  mv hello.c old.c   # 파일 이름 변경
  mv old.c hello.c   # 이름 복구
  cp hello.c backup.c # 파일 복사
  rm backup.c        # 복사본 삭제
  mv hello.c ..      # 상위 디렉토리로 이동
  cd ..              # 상위 디렉토리로 이동
  rmdir hello        # 디렉토리 삭제
  ```

---

## 8. **데이터 타입**
- `bool`: 참/거짓.
- `char`: 단일 문자.
- `double`: 고정밀 부동소수점.
- `float`: 부동소수점.
- `int`: 정수.
- `long`: 더 큰 정수.
- `string`: 문자열 (CS50 라이브러리 제공).

---

## 9. **포맷 코드**
- `%c`: 문자.
- `%f`: 부동소수점.
- `%i`: 정수.
- `%li`: 긴 정수 (`long`).
- `%s`: 문자열.

---

## 10. **조건문**
- **if, else if, else**:
  ```c
  if (x < y) {
      printf("x is less than y\n");
  } else if (x > y) {
      printf("x is greater than y\n");
  } else {
      printf("x is equal to y\n");
  }
  ```
  - **효율성**: `else if`를 사용하면 조건이 참일 때 나머지 조건 검사 생략.
  - 단일 `if`만 사용 시 모든 조건 순차 검사 → 비효율적.
- **논리 연산자**:
  - `||` (OR): 하나라도 참이면 참.
  - `&&` (AND): 모두 참이어야 참.
  - 예:
    ```c
    if (c == 'y' || c == 'Y') {
        printf("Agreed.\n");
    }
    ```

---

## 11. **반복문**
- **while**:
  ```c
  int i = 3;
  while (i > 0) {
      printf("meow\n");
      i--;
  }
  ```
- **for**:
  ```c
  for (int i = 0; i < 3; i++) {
      printf("meow\n");
  }
  ```
- **무한 루프**:
  ```c
  while (true) {
      // 무한 반복
  }
  ```
  - 종료: `Ctrl+C` (control-c).
- **do-while**:
  ```c
  int n;
  do {
      n = get_int("Number: ");
  } while (n < 1);
  ```

---

## 12. **함수**
- **함수 선언 및 호출**:
  ```c
  #include <stdio.h>
  void meow(void);
  int main(void) {
      for (int i = 0; i < 3; i++) {
          meow();
      }
  }
  void meow(void) {
      printf("meow\n");
  }
  ```
- **매개변수**:
  ```c
  void meow(int n) {
      for (int i = 0; i < n; i++) {
          printf("meow\n");
      }
  }
  int main(void) {
      meow(3);
  }
  ```
- **반환값**:
  ```c
  int get_positive_int(void) {
      int n;
      do {
          n = get_int("Number: ");
      } while (n < 1);
      return n;
  }
  ```

---

## 13. **마리오 게임 예제**
- **가로 3개 물음표 박스**:
  ```c
  for (int i = 0; i < 3; i++) {
      printf("?");
  }
  printf("\n"); // 출력: ???
  ```
- **세로 4개 블록**:
  ```c
  for (int i = 0; i < 4; i++) {
      printf("#\n");
  }
  // 출력:
  // #
  // #
  // #
  // #
  ```
- **3x3 블록**:
  ```c
  for (int row = 0; row < 3; row++) {
      for (int col = 0; col < 3; col++) {
          printf("#");
      }
      printf("\n");
  }
  // 출력:
  // ###
  // ###
  // ###
  ```

---

## 14. **상수 (Constants)**
- **`const` 키워드**: 변수 값 변경 불가.
  ```c
  const int n = 3; // n은 변경 불가
  ```

---

## 15. **연산**
- **기본 연산자**: `+`, `-`, `*`, `/`, `%`, `=`, `<`, `<=`, `>`, `>=`, `==`, `!=`.
- **변수 증가**:
  ```c
  counter = counter + 1; // counter += 1; 또는 counter++;
  ```
- **가독성 좋은 코드**:
  ```c
  int x = get_int("x: ");
  int y = get_int("y: ");
  printf("%i\n", x + y);
  ```
- **정수 오버플로우**:
  - `int` (32비트)로 큰 값 계속 증가 시 오버플로우 발생 → `long` (64비트) 사용.
  - 예:
    ```c
    long dollars = 1;
    while (true) {
        char c = get_char("Here's %li. Double it? ", dollars);
        if (c == 'y') {
            dollars *= 2;
        } else {
            break;
        }
    }
    printf("Here's $%li.\n", dollars);
    ```

---

## 16. **절삭 (Truncation)**
- 정수 나눗셈은 소수점 이하 절삭:
  ```c
  int x = get_int("x: ");
  int y = get_int("y: ");
  printf("%i\n", x / y); // 예: 1/3 → 0
  ```
- **해결**: 부동소수점으로 캐스팅.
  ```c
  printf("%f\n", (float) x / y); // 예: 1/3 → 0.333333
  ```
- **소수점 자릿수 지정**:
  ```c
  printf("%.5f\n", (float) x / y); // 소수점 5자리 출력
  printf("%.50f\n", (float) x / y); // 소수점 50자리 출력
  ```

---

## 17. **부동소수점 정밀도 문제 (Floating-point Imprecision)**
- 부동소수점 숫자는 컴퓨터의 한계로 인해 정확하지 않을 수 있음.
- 이유: 컴퓨터는 유한한 비트로 부동소수점을 표현 → 근사값 저장.
- 예: `0.1 + 0.2`는 정확히 `0.3`이 아닌 근사값 출력 가능.

---

## 18. **중요 원칙**
- **정확성 (Correctness)**: 코드가 의도대로 동작.
- **디자인 (Design)**: 코드 구조가 명확하고 효율적.
- **스타일 (Style)**: 가독성 높고 유지보수 쉬움.

---

## 19. **추가 코드 예제**
- **동의 여부 확인**:
  ```c
  char c = get_char("Do you agree? ");
  if (c == 'y' || c == 'Y') {
      printf("Agreed.\n");
  } else if (c == 'n' || c == 'N') {
      printf("Not agreed.\n");
  }
  ```
