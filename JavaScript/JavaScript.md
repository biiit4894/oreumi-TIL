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

# 변수

## 2.1 변수란?

- 언제든지 변할 수 있는 수/정보
- 변수명 결정 시 예약어 사용하지 않도록 주의
- `var`, `let`, `const`

  ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e8f11927-b70c-4524-9227-a3efac08e7aa/9fd0f423-a286-4b43-b87b-4eb74f7b1a3d/Untitled.png)

- 변수 선언 후 초기화를 통해 변수에 저장되는 데이터 형식이 무엇인지를 다른 개발자들이 예상할 수 있다.

  ```jsx
  let 변수;
  변수 = 10;
  ```

  변수 선언 후 10을 할당해 초기화함으로써 정수형 변수임을 예측 가능

- `var` : 변수
  - 초기화: 불필요
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e8f11927-b70c-4524-9227-a3efac08e7aa/705fc4cb-f63e-4d8c-9b75-203b2bfb6790/Untitled.png)
  - 재할당: 가능
  - 생략: 가능 → 권장 X
  - 사장
- `let` : 변수
  - 재정의: 불가
- `const` : 상수
  - 초기화: 필수
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e8f11927-b70c-4524-9227-a3efac08e7aa/a529e143-15c9-4641-80cb-d191be82cc20/Untitled.png)
