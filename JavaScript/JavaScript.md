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

**배열(Array)**

**객체(Object)**
