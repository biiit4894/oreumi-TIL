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

[호이스팅에 대한 오해와 진실](https://tecoble.techcourse.co.kr/post/2021-04-25-hoisting/)

**호이스팅**
인터프리터가 JavaScript 코드를 실행하기 전에 함수, 변수, 클래스 또는 임포트(import)의 선언문을 해당 범위의 맨 위로 끌어올리는 것처럼 보이는 현상이다. (출처: MDN)

JavaScript에서 호이스팅(hoisting)이란, 인터프리터가 변수와 함수의 메모리 공간을 선언 전에 미리 할당하는 것을 의미한다. `var`로 선언한 변수의 경우 호이스팅 시 `undefined`로 변수를 초기화한다. 반면 `let`과 `const`로 선언한 변수의 경우 호이스팅 시 변수를 초기화하지 않는다.

- 호이스팅은?
  - 변수, 함수의 선언부가 위치한 인접 스코프의 시작 지점에서 해당 식별자의 관측이 가능한 현상
  - _‘호이스팅은 엔진의 특별한 능력도 아니고 실행 시점에서 발생하는 현상은 더더욱 아니다. 단지 JS의 특성에 따라 코드 실행 전 컴파일을 거치며 자연스럽게 귀결되는 전처리 과정이다.’_
- ‘끌어올린다’?
  - 그러나.. JS 엔진은 특정 변수나 함수만 상단으로 끌어올릴 능력은 없다. **\*어떤 과정**을 거쳐서 변수와 함수에 대한 전체적인 정보를 미리 알고 있을 뿐
  - 그 어떤 과정은…
    - _컴파일러_
    - 컴파일 과정에서 JS 엔진은 모든 스코프를 탐색 → 실행 단계로 넘어가기 전에 **선언된 식별자\*\***(변수명, 함수명, 속성명, 메소드명)\***\*에 대한 정보를 이미 알고 있는 것**
- 호이스팅 규칙 3대장 (함수 호이스팅 + 변수 호이스팅)
  1. 선언문 (`function 함수명 () {}`)으로 작성된 함수는 상단에서 참조, 호출 가능
     1. ‘함수의 선언문은 식별자가 변수 객체에 수집될 때 부가적으로 해당 함수 **참조에 대한 초기화까지 자동으로** 이루어진다. 그래서 선언된 함수는 상단에서 참조, 호출이 가능하다.’
  2. `var` : 상단에서 참조, 할당 가능
  3. `let` , `const` : 상단에서 참조, 할당 불가능
     - ‘선언 → 초기화(메모리 할당, `undefined`) → 값 할당’ 의 과정을 거치는 변수.
     - `var`는 **호이스팅이 발생하면 선언과 초기화가 거의 동시에 이루어짐**. 스코프 최상단에서 메모리가 살아있음.
     - `let`, `const` 는 **호이스팅이 발생하면 선언만 이루어지고 실행 단계에서 선언부에 도달하기 전까지 초기화는 이루어지지 않음.** 그동안 메모리가 존재하지 않음.
     - 이렇게 스코프의 진입지점과 식별자의 선언부 사이를 TDZ(일시적 사각지대, Temporal Dead Zone)라 부름.

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

- DOM(Document Object Model) : HTML 문서 내의 요소들을 객체로 저장해 트리 형태로 만든다
- BOM : 브라우저에서 제공하는 기본적인 기능을 자바스크립트로제어할 수 있다.
  - ex) `prompt()`

![image](https://github.com/biiit4894/ormi-TIL/assets/82032418/40ccc4c9-d9b4-4647-bf2e-828a9493a6bf)

![image](https://github.com/biiit4894/ormi-TIL/assets/82032418/69ea7eb2-0c0a-460e-8a8e-a9d267f1b9c1)

![image](https://github.com/biiit4894/ormi-TIL/assets/82032418/8dc9d79b-5050-4329-bfa5-a534a2956e50)

prompt에 입력하는 값은 String으로 반환된다

**문제풀이**

사용자로부터 입력받은 나이에 따라 다른 인사말을 콘솔로 출력하는 프로그램을 작성하세요.

나이가 18세 이상이면 "안녕하세요!"를 출력하고, 10세 이상이면 "안녕! 반가워 꼬마친구! ” 를 출력하며, 10세 미만이면 “부럽다…” 를 출력합니다.

```jsx
const age = prompt("나이를 입력하세요");
if (age >= 18) {
  console.log("안녕하세요!");
} else if (age >= 10) {
  console.log("안녕! 반가워 꼬마친구!");
} else {
  console.log("부럽다...");
}
```

잘 작동한다. 왜 문자열과 정수형이 비교되고 있을까?

- 📌 **숫자형 문자, 암묵적 형변환**
  - **숫자형 문자**가 존재하는 자바스크립트. 숫자형 문자와 숫자를 비교할 때 문자열이 숫자로 암묵적으로 형변환이 된다.
    ![image](https://github.com/biiit4894/ormi-TIL/assets/82032418/c3a1dc77-de7f-43cd-82ca-575cdc61cdee)

**문제풀이**

사용자로부터 입력받은 성적에 따라 등급을 출력하는 프로그램을 작성하세요.

성적이 90점 이상이면 "A", 80점 이상이면 "B", 70점 이상이면 "C", 60점 이상이면 "D", 그 외에는 “강해져서 돌아와라”를 출력합니다.

```jsx
const score = prompt("성적을 입력하세요");
if (score >= 90) {
  console.log("A");
} else if (score >= 80) {
  console.log("B");
} else if (score >= 70) {
  console.log("C");
} else if (score >= 60) {
  console.log("D");
} else {
  console.log("강해져서 돌아와라");
}
```

삼항연산자로 풀이

```jsx
const score = prompt("성적을 입력하세요");

score >= 90
  ? console.log("A")
  : score >= 80
  ? console.log("B")
  : score >= 70
  ? console.log("C")
  : score >= 60
  ? console.log("D")
  : console.log("강해져서 돌아와라");
```

삼항연산자로 풀이 정답

```jsx
const score = prompt("성적을 입력하세요");

console.log(
  score >= 90
    ? "A"
    : score >= 80
    ? "B"
    : score >= 70
    ? "C"
    : score >= 60
    ? "D"
    : "강해져서 돌아와라"
);
```

**1.3 switch 문**

```jsx
switch (표현식) {
	case 값1:
		break;
	case 값2:
		break;
	...
	default:
		// 모든 case에 해당하지 않을 경우
		break;

}
```

- default 문은 선택사항

```jsx
switch (new Date().getDay()) {
  case 1:
    document.write("월요일입니다.");
    break;
  case 2:
    document.write("화요일입니다.");
    break;
  case 3:
    document.write("수요일입니다.");
    break;
  case 4:
    document.write("목요일입니다.");
    break;
  case 5:
    document.write("금요일입니다.");
    break;
  default:
    document.write("금금요일입니다. 주말이 뭐죠?");
    break;
}
// 목요일입니다.
```

동일 코드에 break문을 일부 적용하지 않을 경우

```jsx
switch (new Date().getDay()) {
  case 1:
    document.write("월요일입니다.");
    break;
  case 2:
    document.write("화요일입니다.");
    break;
  case 3:
    document.write("수요일입니다.");
    break;
  case 4:
    document.write("목요일입니다.");
  // break;
  case 5:
    document.write("금요일입니다.");
  // break;
  default:
    document.write("금금요일입니다. 주말이 뭐죠?");
  // break;
}
```

![image](https://github.com/biiit4894/ormi-TIL/assets/82032418/66870e2f-b3e6-41be-98ae-4e16c23ea479)

- `new Date(`)의 결과는 문자열이 아니고 **객체**
  - **객체 : 데이터와 함수를 갖는다.**
    - 함수가 객체 안에 들어 있으면 **메소드**라고 부른다.

**문제풀이**

사용자로부터 입력받은 성적에 따라 등급을 출력하는 프로그램을 작성하세요. 성적이 90점 이상이면 "A", 80점 이상이면 "B", 70점 이상이면 "C", 60점 이상이면 "D", 그 외에는 “강해져서 돌아와라”를 출력합니다. ⇒ 이 문제를 `switch`문으로 풀어보자.

```jsx
switch (true) {
  case score >= 90:
    console.log("A");
    break;
  case score >= 80:
    console.log("B");
    break;
  case score >= 70:
    console.log("C");
    break;
  case score >= 60:
    console.log("D");
    break;
  default:
    console.log("강해져서 돌아와라");
}
```

switch문에 `true` 대신 `1` 대입 시 case문의 boolean 값과 형이 맞지 않아 default문으로 빠져버림

### 2. 반복문

**2.1 for문의 다양한 예시**

**구구단 5단만 작성해보기**

작성 답안

```jsx
for (let i = 1; i < 10; i++) {
  document.write(`5 X ${i} = ${5 * i}<br>`);
}
```

**JavaScript 템플릿 리터럴**

[Template literals (Template strings) - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals)

` ` 백틱을 이용해 작성한 문자열은 `${}` 내부에 표현식을 쓸 수 있음

```jsx
const txt = "world";

`hello ${txt}`;

`hello ${true ? "world" : "good bye"}`;
```

- 초기화식, 조건식을 생략가능

**2.2 while문**

소괄호 내부에 초기식, 조건식, 증감식을 모두 가지고 있는 for문과 달리 while문은 소괄호 내부에 조건식만을 갖는다.

- **do-while 반복문**

  - 조건식이 거짓이더라도 적어도 한 번은 코드가 실행되도록 하고자 할 때

  ```jsx
  do {
    input = prompt("숫자를 입력하세요.");
  } while (isNaN(input));

  console.log("입력한 숫자는 " + input + "입니다.");
  ```

  - `NaN` : 계산 불가한 숫자. 숫자형은 맞다.

**2.3 반복문의 break & continue**

- `break` : 반복문 탈출
- `continue` : for문 내부 코드에서 continue를 만나면 바로 다음 증감식으로 넘어간다.

**문제풀이**

while 문을 이용해서 1부터 10까지 숫자를 출력하세요. 이때 4와 7은 건너뛰고 출력합니다.

```jsx
let i = 0;
while (i < 10) {
  **i++; // 증감식이 앞에 위치하지 않으면 i === 4 조건에서 무한루프에 빠진다.**

  if ((i === 4) || (i === 7)) {
    continue;
  };
  console.log(i);
}

// 1
// 2
// 3
// 4
// 5
// 6
// 7
// 8
// 9
// 10
```

`i`가 1에서 출발하도록 할 경우, 이런 코드도 동일한 결과를 출력한다.

```jsx
let i = 1;
while (i <= 10) {
  if (i === 4 || i === 7) {
    i++;
    continue;
  }
  console.log(i);
  i++;
}
```

**2.4 label**

## 타입

### Type이란?

### 1. 원시타입 (Primitive Types)

- 값 변경 불가
- 원시 값을 다른 변수에 할당하면 **값의 참조**가 아니라 **값 자체(가리키고 있는 값을 따라가서 실제 메모리에 저장된 주소)**가 복사되어 저장된다
- string, number, bigint, boolean, undefined, symbol, null

```jsx
const me = {
  name: "jaehyun",
  address: "jeju",
  canWalk: function () {
    console.log("재현이가 걷는다.");
  },
};
```

![image](https://github.com/biiit4894/ormi-TIL/assets/82032418/77b33db5-73ff-4797-8c66-babdf2de3cab)

### 2. 객체타입 (Object Types)

- 객체타입의 특징
  1. 객체는 프로퍼티(자바의 필드)로 값과 메서드를 가짐.
  2. 값을 변수에 저장할 때 값 자체가 아니라 **값의 위치**가 저장된다. 객체 값을 다른 변수에 할당할 때 **값의 참조(위치)**가 저장된다.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e8f11927-b70c-4524-9227-a3efac08e7aa/b3121618-2c54-4a42-88b7-cd25e100f864/Untitled.png)

val2, val3는 같은 주소를 가리키고 있다. 그 주소에 담긴 데이터가 [10, 1]로 변경되었기 때문에 가리키는 값이 바뀌어 보이는 것.

![image](https://github.com/biiit4894/ormi-TIL/assets/82032418/1e83bfc4-36cc-44db-95db-bed982ba92ef)

원시타입은 값을 변수에 저장할 때 값 자체를 저장하는 모습이다. 그러나 값은 변경 불가하다.

- 자바스크립트는 autoboxing을 통해 원시타입도 객체타입처럼 사용할 수 있다.

**1 배열 (Array)**

원시타입가 달리 데이터 추가/제거/정렬/검색 등 다양한 작업 가능(메서드)

**배열의 특징**

1. 빈 배열로 생성하거나 요소가 포함된 배열로 생성 가능
2. 인덱싱 가능. 숫자를 이용해 값에 전근하며, 배열 안에 존재하는 값을 원소라 부른다.

   1. 존재하지 않는 원소에도 접근 가능 → undefined 반환

      ![image](https://github.com/biiit4894/ormi-TIL/assets/82032418/2f98203f-cfbc-49d9-b400-fb347fc55538)

3. `length` 프로퍼티를 통해 배열의 길이에 접근
4. 다차원 배열 : 배열 내부에 다른 배열 포함 가능
   1. 2차원 배열 이상의 배열을 사용할 일이 크게 많지는 않음

**배열의 메소드**

- 배열도 결국 **\*\***객체**\*\***이기 때문에 다양한 \***\*\*\*\*\***메소드\***\*\*\*\*\***를 갖는다.

1. push(), pop() : push는 배열의 끝에 요소를 추가하고 길이 반환 / 배열의 마지막 요소를 꺼내 반환 + 꺼낸 요소는 배열에서 제외됨

   ![image](https://github.com/biiit4894/ormi-TIL/assets/82032418/8e2eb460-b253-4ca3-98af-c2911fefc682)

2. shift(), unshif()

   ![image](https://github.com/biiit4894/ormi-TIL/assets/82032418/a781be49-380a-4d43-aaa5-86dd46825752)

   ❓ const 배열 내부의 값이 수정되는 이유?

   배열 데이터의 주소값이 바뀌는 것이 아니기 때문!

3. splice()

   1. `splice(삭제/추가를 시작할 인덱스, 삭제할 요소의 개수, 추가할 요소들)`
   2. 첫 인자로 전달한 **삭제/추가를 시작할 인덱스의 바로 앞 인덱스**에서 **추가**가 이루어진다.
   3. 세번째 인자부터는 추가할 요소들을 쉼표로 전달

   ![image](https://github.com/biiit4894/ormi-TIL/assets/82032418/c3fc931f-a4c4-4fb1-9d76-a7ba67b68bc8)

**splice() 문제**

```jsx
// splice 문제
const fish = ["정어리", "고등어", "돌고래", "참치", "고래상어", "코끼리"];
// 1. splice 를 이용해 코끼리를 제거해보세요
// 2. 참치 다음에 다금바리를 추가해보세요
// 3. 돌고래를 제거하고 옥돔과 갈치를 추가해보세요
```

**splice() 문제 - 작성 답안**

```jsx
const fish = ["정어리", "고등어", "돌고래", "참치", "고래상어", "코끼리"];
fish.splice(5, 1);
fish.splice(4, 0, "다금바리");
fish.splice(2, 1, "옥돔", "갈치");
```

![image](https://github.com/biiit4894/ormi-TIL/assets/82032418/2717721f-9d44-4cec-85eb-4edef3f9f0b6)

**splice() 문제 - 정답**

```jsx
const fish = ["정어리", "고등어", "돌고래", "참치", "고래상어", "코끼리"];
fish.splice(5, 1);
fish.splice(4, 0, "다금바리");
fish.splice(2, 1, "옥돔", "갈치");
```

1. slice()

   1. 배열에서 요소들을 추출해 새로운 배열로 반환한다
   2. `slice(추출을 시작할 인덱스, 추출을 끝낼 인덱스)`
   3. 첫 인자에서 두 번째 인자 바로 직전까지 추출

   ![image](https://github.com/biiit4894/ormi-TIL/assets/82032418/f0d7e35d-5377-4c18-8284-53aed20c2f35)

   `myArray` 배열 내부의 값들은 변하지 않고 있는 모습이다

1. sort()

   1. 배열의 요소를 정렬

      ![image](https://github.com/biiit4894/ormi-TIL/assets/82032418/d33aef7b-c9df-4131-ba25-1bf12d358dc5)

   2. 숫자를 정렬할 때는 원소를 문자열로 전환한 후 유니코드 포인트의 순서대로 변환해 버린다.
   3. **비교 함수**(compareFunction) : 비교 함수의 두 인자(a, b)를 뺄셈으로 비교해서 음수가 나오면 a를 앞으로 위치시킨다. 양수가 나오면 b를 앞으로 위치시킨다. 0이 나오면 인자들의 위치를 바꾸지 않는다.

      함수의 인자로 함수 sort(비교 함수) 전달 ?!

      ![image](https://github.com/biiit4894/ormi-TIL/assets/82032418/85efe4da-95be-41bf-afa8-99549cc86927)

      a: 9 b: 13 → [9, 13, 10]

      a: 10 b: 9 → [9, 13, 10]

      a: 10, b: 13 → [9, 10, 13]

      a: 10, b: 9 → [9, 10, 13]

      - JavaScript sort 메소드는 Time sort 알고리즘에 의해 원소를 정렬한다.

1. forEach()

   1. 배열의 각 요소에 대해 주어진 함수를 실행한다
   2. `forEach(배열 요소, 인덱스)`
   3. 보통 매개변수로 `item`, `index`라는 변수를 설정함.
   4. 매개변수로 콜백함수를 전달한다

      1. 배열 안의 값들을 **‘순환’하면서 배열 안의 원소의 개수만큼 반복한다.**

         ![image](https://github.com/biiit4894/ormi-TIL/assets/82032418/0c94eddb-acdb-4a99-8b8c-961ce2ba2191)

         `arr`를 확인하면 `[0, 1, 2]`로 조회됨

         ![image](https://github.com/biiit4894/ormi-TIL/assets/82032418/9970a517-6ede-445e-a2ca-d23516be27ca)

1. map()

   1. 배열의 각 요소에 대해 주어진 함수를 실행하고 그 결과를 새로운 배열로 반환한다.
   2. `return`이 없으면 `undefined`를 넣어버림.

      ![image](https://github.com/biiit4894/ormi-TIL/assets/82032418/8a6b562b-1cdd-454f-8260-f1b361336b35)

   - 콜백함수는 화살표 함수로 작성하거나 전달할 인자가 하나뿐일때 소괄호까지 생략할 수 있다.
     ![image](https://github.com/biiit4894/ormi-TIL/assets/82032418/4a340bb8-fd77-4ce9-b65c-27528eaf138c)
   - 콜백함수는 실행할 코드가 한 줄일 때 중괄호를 생략할 수도 있는데, 이 경우 `map` 함수의 `return` 이 생략된다.

     ```jsx
     const data = [
       {
         _id: "642ba3980785cecff3f39a8d",
         index: 0,
         age: 28,
         eyeColor: "green",
         name: "Annette Middleton",
         gender: "female",
         company: "KINETICA",
       },
       {
         _id: "642ba398d0fed6e17f2f50c9",
         index: 1,
         age: 37,
         eyeColor: "green",
         name: "Kidd Roman",
         gender: "male",
         company: "AUSTECH",
       },
       {
         _id: "642ba39827d809511d00dd8d",
         index: 2,
         age: 39,
         eyeColor: "brown",
         name: "Best Ratliff",
         gender: "male",
         company: "PRISMATIC",
       },
     ];

     const ages = data.map((item) => item.age);
     ```

❓ `forEach` vs `map`

- map() 은 `break`문을 통해 시행을 멈출 수 있는 반면, forEach()는 `break`를 만나도, `return`을 만나도 멈추지 않는다 ;;

1. filter()

   1. 조건을 만족하는 원소만 추출해 배열을 반환한다.

      ```jsx
      const arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
      const newArr = arr.filter(function (el) {
        if (el % 2 === 0) {
          return el;
        }
      });

      console.log(newArr);

      // filter문을 map문으로 바꾸기
      const arr2 = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
      const newArr2 = arr.map(function (el) {
        if (el % 2 === 0) {
          return el;
        } else {
        }
      });
      ```

1. includes()
   1. 요소가 포함되어있으면 true, 아니면 false 반환

**\*2 객체 (Object)**

자바스크립트의 모든 데이터는 객체처럼 사용할 수 있다.

key-value 쌍으로 구성된다.

**객체의 특징**

1. {}
2. `객체이름.key값` 또는 `객체이름['key값']` 으로 속성에 접근 가능하다
   1. 대괄호로 속성에 접근하기 위해서는 key값의 변수명이 자바스크립트 변수명 선언 규칙을 따라야 함.
3. `객체이름.새로운속성명 = 새로운 값;`으로 객체에 속성을 추가할 수 있다.
   1. `delete 객체이름.속성명;`으로 속성을 삭제할 수 있다.
   2. `in` 연산자로 특정 프로퍼티가 객체 안에 존재하는지 알 수 있다.

**객체의 메소드**

1. hasOwnProperty()
   1. 사실 `in` 연산자가 조금 더 간결하다.
2. for … in

   ```jsx
   const person = {
     name: "재현",
     age: 20,
     gender: "male",
   };

   for (let key in person) {
     console.log(`${key}: ${person[key]}`);
   }

   // name: 재현
   // age: 20
   // gender: male
   ```

   - `for … in` 문 안에서 처리되는 프로퍼티들은 반드시 순서대로 반복되지 않음. 순서가 중요하면 일반적인 for문과 같은 반복문 사용하기! (사실 for … in문 잘 안씀)

3. keys(), values()

   각각 객체의 속성 이름들과 객체의 속성값들을 배열로 반환한다.

   ![image](https://github.com/biiit4894/ormi-TIL/assets/82032418/032db132-9cb8-48d7-9f97-bd1d6487aa5f)

## 6. this

### 6.1 this란?

this는 주소만 가리키고 있는, 객체를 가리키는 참조 변수이다.

![image](https://github.com/biiit4894/ormi-TIL/assets/82032418/1585aeb5-7cec-4682-bb38-3f17287bf8a6)

Window 객체를 가리키기도, myObj 객체를 가리키기도 하고 있는 `this`의 모습

❓ window 객체?

브라우저 환경의 전역공간. Node.js 환경에서의 전역공간은 `global`

```html
<!DOCTYPE html>
<html lang="ko">
  <head>
    <title></title>
  </head>
  <body>
    <button id="btn1">클릭해봐요!</button>
    <button id="btn2">클릭해봐요!</button>
    <script>
      let myObj = {
        val1: 100,
        func1: function () {
          console.log(this);
        },
      };

      let test = myObj.func1;

      let button1 = document.getElementById("btn1");
      button1.addEventListener("click", myObj.func1);
      let button2 = document.getElementById("btn2");
      /*click 이벤트가 발생했을 때 
						myObj의 func1 함수를 실행하라*/
      button2.addEventListener("click", test);
    </script>
  </body>
</html>
```

```jsx
/ * this */;
function sayName() {
  console.log(this.name);
}

var name = "Hero";
// 전역으로 선언한 name 변수의 앞에는 window 가 생략되어 있습니다.
// 때문에 window.name === "Hero" 가 성립합니다.
let peter = {
  name: "Peter Parker",
  sayName: sayName,
};

let bruce = {
  name: "Bruce Wayne",
  sayName: sayName,
};

sayName();
peter.sayName();
bruce.sayName();

/* sayName() 함수를 실행했을 때와 
peter, bruce 객체의 sayName 함수를 호출했을 때의 결과를 비교해 보세요 */
```

- 전역공간 사용을 지양해야하는 이유?
  - 전역공간에 선언된 변수는 프로그램이 종료되기 전까지 계속 메모리를 차지한다.
  - ⇒ 메모리 누수

### 6.2 this의 특징

this는 함수가 만들어질 때 ❌ 실행될 때 ⭕ 그 값이 결정된다.

```jsx
function sayName() {
  console.log(this.name);
}
var name = "Hero";

let peter = {
  name: "Peter Parker",
  sayName: sayName,
};

let bruce = {
  name: "Bruce Wayne",
  sayName: peter.sayName,
};

bruce.sayName();
```

‼ peter의 sayName이 시행되는 곳이 bruce 객체이기 때문에 this는 bruce를 가리키고 있다.

## 7. 객체지향 프로그래밍

- 객체 : 구체적인 사물을 추상적으로 표현한 것
- 객체의 행동 : 메소드 / 객체의 상태 : 프로퍼티

![image](https://github.com/biiit4894/ormi-TIL/assets/82032418/fd5a9d88-13d3-4c8c-bce2-a5f65825fb3e)

me의 teaching 으로 인해 ormi의 level이 올라간 모습이다.

### 7.1 생성자(constructor)

객체를 만들 때 `new` 연산자와 함께 사용하는 함수

```jsx
let myArr = new Array(1, 2, 3);
```

→ 내장 생성자

**7.1.1 생성자를 사용하는 이유**

**7.1.2 커스텀 생성자 만들기**

- 생성자 함수는 new 키워드가 앞에 붙게 되면 실행되었을 때 자동적으로 객체를 생성하고 반환한다.
  - ⇒ 반환되어 만들어진 객체를 **인스턴스(instance)**라고 한다.
  - **\*\*\*\***생성자 함수와 객체의 관계는 `instanceof` 로 확인 가능\*\*
    ![image](https://github.com/biiit4894/ormi-TIL/assets/82032418/afbc5d6c-3c25-4d3f-b748-ae57b1216ce6)
    ![image](https://github.com/biiit4894/ormi-TIL/assets/82032418/3d788c4f-ec65-4348-af50-da926e0582bd)

### 7.2 프로토타입 (prototype)

- 우리는 객체의 메서드를 등록할 때마다 새로운 함수를 생성하고 있다. 객체를 생성할때마다 함수를 매번 새로 만들 수는 없고, 이런 자원 낭비를 방지하기 위해 프로토타입을 사용한다.

![image](https://github.com/biiit4894/ormi-TIL/assets/82032418/c01d15bf-187d-4428-905b-bf55d645b612)

robot2와 robot3의 sayYourName이 같지 않은 것으로 보아 객체를 생성할때마다 함수가 만들어졌던 것을 알 수 있다.

- 객체를 만들때 값은 몰라도 메서드를 공유해서 메모리를 절약할 수 있다.

생성자로 객체를 만드는 방법이나 일일히 객체를 만드는 방법, 두 방법 모두 메모리 사용량이 같다?? ⇒ O

```jsx
this.sayYourName = function () {
  console.log(`삐리비리. 제 이름은 ${this.name}입니다. 주인님.`);
};
```

```jsx
function NewFactory2(name) {
  this.name = name;
}

NewFactory2.prototype.sayYourName = function () {
  console.log(`삐리비리. 제 이름은 ${this.name}입니다. 주인님.`);
};
```

prototype 공간에 sayYourName 함수가 만들어진다.

```jsx
const obj1 = NewFactory2("재현");
const obj2 = NewFactory2("길동");
```

NewFactory2 프로토타입으로 생성한 이 두 변수는 같은 주소값을 참조해 결국 같은 메소드 sayYourName을 가리킨다.

- `__proto__` 프로퍼티는 자신을 만든 생성자 함수의 `prototype`을 참조하는 역할

  ```jsx
  function Test() {}

  const obj = new Test();

  obj.__proto__ === Test.prototype;
  ```

  - 생성자로 인스턴스를 생성하면, 그 인스턴스에는 일종의 프로퍼티(속성)으로 프로토타입에 접근할 수 있는 `__proto__`가 존재

**문제풀이**

객체지향 개념에서 만들었던 ‘나’와 ‘대상’ 객체를 생성자를 통해서 만들어 볼 수 있도록 코드를 수정해보자.

### 7.3 객체의 상속 → 다음주부터!

```jsx
const obj = {
  name: "test",
};

console.log(obj.hasOwnProperty("name")); // true

const arr = [1, 2, 3];

console.log(arr.hasOwnProperty("name")); // false
```

- Array의 `prototype`에 존재하지 않는 Object 객체의 프로퍼티와 메서드를 사용할 수 있는 모습
  - **프로토타입 체이닝:** 자기 자신에게 존재하지 않는 프로퍼티나 메서드를 프로토타입을 통해 추적하는 과정

[JavaScript 핵심 개념 - 프로토타입 체이닝#1 (Prototype Chaining)](https://ji5485.github.io/post/2021-02-05/javascript-core-concept-summary-prototype-chaining-1/)

**프로토타입 체이닝?**

- _자바스크립트에서 모든 객체는_ 자신을 생성한 생성자 함수의 prototype 프로퍼티가 가리키는 *프로토타입 객체를 자신의 부모 객체로 설정하는 [[Prototype]] 링크로 연결한*다.
- 객체를 생성하는 것은 생성자 함수의 몫이지만, 생성된 객체의 실제 부모 역할을 하는 것은 생성자 함수의 prototype 프로퍼티가 가리키는 프로토타입 객체라는 것을 알 수 있습니다.
- **생성자로 만들어진 인스턴스들이 프로토타입을 참조해서 자신에게 없는 속성/메서드를 상속받는다?**

## 8. DOM

### 8.1 DOM API란?

- DOM은 HTML을 트리 형태로 구조화해 웹페이지와 프로그래밍 언어를 연결한다.
- **노드(node) : 각 요소와 속성, 콘텐츠를 표현하는 단위**
  - DOM은 노드들의 집합

### 8.2 DOM 트리에 접근하기

- document.getElementById();
- document.getElementsByTagName();
- document.getElementsByClassName();
- document.querySelector("selector");
  - css 선택자로 접근
- document.querySelectorAll("selector");

### 8.3 DOM 제어 명령어

1. **이벤트 삽입**

   1. `target.addEventListener( type, listener )`

1. **클래스 제어**
   1. `classList` 객체를 통해 요소의 class 속성을 제어
   2. ex) `myBtn.classList.add(”blue”);` → myBtn에게 blue 클래스를 부여한다
1. **요소 제어**

`createElement`, `createTextNode`, `appenㅇchild`, `removeChild` 등의 api들이 있지만..

- `innterHTML`이 강력!
  - 요소 내의 HTML 마크업을 가져오거나 설정함.
    [Element.innerHTML - Web API | MDN](https://developer.mozilla.org/ko/docs/Web/API/Element/innerHTML#security_considerations)
    security considerations 주의하기
  - 마크업 설정 → 편한 건 맞는데 쉽게 더러워질 수 있음..
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e8f11927-b70c-4524-9227-a3efac08e7aa/33eb27b4-ef7f-4c39-b6c5-54f0f00bff78/Untitled.png)

1. element, text 노드를 생성하거나 추가하기

1. 속성 제어하기
   - `style` 객체의 값을 변경하면 inline 스타일과 동일한 가중치(1000)를 가진다. `classList.add` 방식으로 스타일을 제어하는 것을 가장 권장함
   - `getAttribute`, `setAttribte`를 통해 요소의 속성 값에 접근하고 값을 수정할 수 있음

- `toggle` 과 클릭이벤트를 이용해 버튼을 클릭하면 색상이 변하게 하기

```jsx
const myBtn = document.querySelector("button");

myBtn.addEventListener("click", function () {
  // blue 라는 클래스의 속성 값을 지정 할 수 있습니다.
  // myBtn.classList.add("blue");

  // myBtn.classList.remove("blue");     클래스를 제거합니다.
  myBtn.classList.toggle("blue"); // 클래스를 토글합니다.없으면 넣어주고, 있으면 제거합니다.
  // myBtn.classList.contains("blue");   해당하는 클래스가 있는지 확인합니다.
});
```
