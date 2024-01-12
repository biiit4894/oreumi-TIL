- reference : 이스트소프트 오르미 백엔드 개발자 양성과정 4기 - 위니브 소속 강사님 교안

# JavaScript 기본

## 1. JavaScript란 무엇인가?

### 1.1 JavaScript의 탄생 배경

- 1995 넷스케이프 브랜든 아이크 주도로 만들어진 언어
- HTML/CSS를 프로그래밍적으로 제어
  - ex) JS 변수에 HTML 태그를 담을 수 있음
- 브라우저에서 타 언어를 해석하게 해주는 웹어셈블리도 있기는 하지만, 웹 브라우저가 해석해서 실행할 수 있는 유일한 프로그래밍 언어.
- JS 런타임환경 : Node.js
  - 런타임: 특정한 언어가 실행시킬 수 있는 공간.

### 1.2 정적인 웹에서 동적인 웹으로

- JS 표준 명세서가 ECMA에 등록되어있기 때문에 표준명칭은 ECMAScript

### 1.3 동적인 웹을 위해 자바스크립트가 할 수 있는 것들

1. 데이터 저장
2. 값 계산
3. 결과 반영
   1. DOM & BOM API
   2. 연산 결과를 브라우저/HTML 문서에 보여줄 수 있다
4. 다른 컴퓨터와 통신
   1. Ajax
   2. 서버, 클라이언트 컴퓨터가 서로 데이터를 주고받을 수 있도록 함

### 1.4 JavaScript를 사용하는 여러가지 방법들

- HTML 파일 내부에 삽입하기
  - HTML 태그 내에 삽입 → 잘 사용 X
  - script 태그로 삽입
- HTML 파일 외부에 있는 스크립트 파일을 로드하기 → 가장 추천
  ```markdown
  <!DOCTYPE html>
  <html lang="ko">
  <head>
  </head>
  <body>
      <script src="test.js"></script>
  </body>
  </html>
  ```
- 브라우저 콘솔창 `about:blank` 페이지에서 간단히 JS 연습 가능

## 2. 변수

### 2.1 변수란?

**변수의 특징**

- `var`, `let`, `const`

- 변수 선언 후 초기화를 통해 변수에 저장되는 데이터 형식이 무엇인지를 다른 개발자들이 예상할 수 있다.

  ```jsx
  let 변수;
  변수 = 10;
  ```

  변수 선언 후 10을 할당해 초기화함으로써 정수형 변수임을 예측 가능

- `var` : 변수
  - 초기화: 불필요
    ![Untitled (9)](https://github.com/biiit4894/ormi-TIL/assets/82032418/487571b0-49d0-40b3-87be-7272327048e9)
  - 재할당: 가능
  - 생략: 가능 → 권장 X
  - 사장
- `let` : 블록 레벨 변수
  - 재정의: 불가
- `const` : 블록 레벨 상수

  - 초기화: 필수
    ![Untitled (10)](https://github.com/biiit4894/ormi-TIL/assets/82032418/383a4432-b4a1-41a2-918f-c705e0950157)

- `let` vs `const`
  - `const` 우선 사용
    1. `const`는 의도하지 않은 값의 변경을 방지할 수 있음
    2. 가독성, 유지보수성
       1. `const`는 반드시 초기화해야 하기 때문에 변수에 어떤 데이터가 사용되는지 빠르게 확인할 수 있음

## 3. 함수

### 3.1 함수 구조

```jsx
function 함수이름(parameter1, parameter2 ...) { // 함수의 선언부
	// 실행코드
	return 반환값
}

함수이름(argument1, argument2 ...) // 함수의 호출
```

### 3.2 함수의 활용 - 매개변수와 전달인자

- parameter : 매개변수, 파라미터
  - 함수와 메서드에 입력하는 변수의 이름
- argument : 인자, 인수, 아규먼트
  - 매개변수로 넘겨지는 값
  - 함수와 메서드에 실제로 입력되는 값
- return 구문을 만나면 해당 함수는 종료된다
- ❓`undefined` vs `null`
  - `undefined` : 값을 담을 공간은 생성되었지만 아직 아무 값도 할당되지 않은 경우
  - `null` : 값을 담을 공간을 생성하고 빈 값을 할당한 상태
- 메소드 vs 함수
  - 메소드 : 클래스(객체) 내부에 선언
  - 함수 :

```jsx
// 함수
// 읽어볼만한 문헌 : https://ko.javascript.info/function-basics

// 1번
function 안녕(파라미터){
    console.log(파라미터);
    console.log('hello');
    return 100;
}

let 아규먼트 = 1000;
안녕(아규먼트);
console.log(안녕(아규먼트) + 안녕(아규먼트));

// 2번
function 안녕(){
    console.log('hello');
}

안녕();
console.log(String(안녕()) + String(안녕()));
**// undefined를 반환하는 안녕 함수. return 값이 없다. -> String 변환 후 concat**

// 3번
function 안녕(){
    console.log('hello')
    return 10
}

안녕()
console.log(String(안녕()) + String(안녕()))
**// 10(정수형)을 반환하는 안녕 함수. -> String 변환 후 concat**

// 4번
function 안녕(){
    console.log('hello')
    console.log('hello')
    console.log('hello')
    return
    console.log('hello')
    console.log('hello')
    console.log('hello')
}

안녕()
```

**3.2.1 함수의 활용 - 함수의 아규먼트에 따른 반환값**

- 아규먼트(인자)는 매개변수보다 적거나 많아도 에러가 발생하지 않음
  - 매개변수보다 많은 인자를 전달하면,
    - 개수를 초과해 전달된 인자는 메모리에서 사라질 것.
    - 콘솔 출력 가능
  - 매개변수보다 적은 인자(ex. int)를 전달하면
    - 콘솔에 `NaN` 출력

### 3.3 함수를 선언하는 여러가지 방법

- 함수는 선언문이자 표현식이다.

1. 함수 선언문과 함수 표현식

   ```jsx
   // 함수 선언문
   function sum(x, y) {
     return x + y;
   }

   // 함수 표현식
   let sumXY = function (x, y) {
     return x + y;
   };
   console.log(sum(10, 20));
   console.log(sumXY(10, 20));
   ```

   - 왜 함수 표현식을 더 많이 사용할까?
   - ❗ 호이스팅
     - 인터프리터가 변수와 함수의 메모리 공간을 선언 전에 미리 할당하는 것
     - 함수를 선언하기에 앞서 함수를 호출해도 오류가 발생하지 않는다
     ```jsx
     console.log(myFunction);

     function myFunction() {
       return null;
     }
     // 함수 선언문
     ```
   - ❓ JS는 왜 이런 장치를?
     - 상대적으로 에러 발생 가능성이 큰 JS. 인터프리터 언어의 특성상 오류 발생을 방지하는 다양한 장치가 있는 것이 아닐까?
   - ❓ 구문(Statement) Vs 표현식(Expression)
     - 구문: 명령문. 작업 수행을 위한 코드 블록. (ex. if, switch, for문)
     - 표현식 : 값으로 평가될(표현할) 수 있는 것. 함수를 값처럼 사용하기 때문에 ‘함수 표현식’이라고 쓰는 것
     ```jsx
     function myFunc() {
       return;
     } // 선언식
     myFunc(); // 표현식
     ```

**호이스팅**

인터프리터가 JavaScript 코드를 실행하기 전에 함수, 변수, 클래스 또는 임포트(import)의 선언문을 해당 범위의 맨 위로 끌어올리는 것처럼 보이는 현상이다. (출처: MDN)

JavaScript에서 호이스팅(hoisting)이란, 인터프리터가 변수와 함수의 메모리 공간을 선언 전에 미리 할당하는 것을 의미한다. `var`로 선언한 변수의 경우 호이스팅 시 `undefined`로 변수를 초기화한다. 반면 `let`과 `const`로 선언한 변수의 경우 호이스팅 시 변수를 초기화하지 않는다.

1. 화살표 함수 (자바의 lambda식)

   ```jsx
   function add(x, y) {
     return x + y;
   }

   let add1 = (x, y) => x + y; // 한 줄의 코드는 중괄호 생략 가능

   let add2 = (x) => x + 10; // 매개변수가 1개일 경우 소괄호 생략 가능
   ```

## 4. 조건문과 반복문

### 1. 조건문

- JS는 모든 값에 대해 참인지 거짓인지에 대한 판단 기준을 가지고 있다
- `Truthy` :
- `Falsy`
- `!null` : `true` → `null`은 `Falsy`한 값이다.

```jsx
!null;
```

**1.1 if문**

```jsx
if (조건식) {
}
```

- if문의 조건식에는 표현식으로 나타낼 수 있는 모든 것들이 들어갈 수 있음
  - ex) `if(1 < 5) { console.log("true"};` // true
- if-else 문
  ```jsx
  if() {

  } else {

  };
  ```
- else if 문
  - 참을 반환하는 조건식을 만나면 해당 블록의 코드를 실행하고 조건문을 나간다.
  ```jsx
  if() {

  } else if () {

  } else if () {
  		...
  };
  ```

**1.2 삼항연산자**

<img width="432" alt="스크린샷 2022-02-24 오후 8 49 33" src="https://github.com/biiit4894/ormi-TIL/assets/82032418/420e61e3-ae6f-4ddd-ad2a-30c778ca5d4e">

- `console.log`는 반환값이 없어서(`undefined`) `item`에 `undefined`가 할당된다. 이후 `item`을 콘솔로 출력하려고 하면 `undefined`가 출력된다.

- 삼항 연산자도 `else if`처럼 쓸 수 있다.
  ```jsx
  let age = 50;

  let message = age > 60 ? "노년" : age > 40 ? "중년" : "청년";

  console.log(message);

  // 중년
  ```
