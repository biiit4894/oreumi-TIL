- reference : 이스트소프트 오르미 백엔드 개발자 양성과정 4기 - 한재현 강사님 교안

# CSS 기본

## CSS란?

- Cascading Style Sheets
- 스타일이 우선순위를 가지고 적용되어 마치 폭포처럼 위에서 아래로 떨어진다.
  - 외부 CSS(4순위) → head의 CSS(3순위) → inline CSS(2순위, `style="CSS 문법"`) → 유저가 적용한 CSS (1순위)
  - ❓유저가 적용한 CSS? : 브라우저를 사용하는 일반적인 유저가 브라우저가 적용한 CSS. ex) 다크모드

## 작성방법

```css
선택자 {
  속성: 속성값;
   {
    /*선언*/
  }
}
 {
  /*선언블록 종료*/
}
```

[Color Hex Color Codes](https://www.color-hex.com/)

색상은 hex code로도 입력 가능

# CSS 적용하기

## 1. 인라인 방식

- 태그 자체에 `style` 속성으로 스타일을 준다.
- 오래된 방식, 잘 사용 x
- 일부 스타일 적용에 제한이 있다. (`:hover` 가상 클래스, `::before`, `::after` 가상 요소 등)

  - ❓ 가상 요소?

    - CSS에서 작성한 내용이 실제 HTML 컨텐츠/요소처럼 존재하게 만든다.
    - 예시

      ```css
      <!DOCTYPE html>
      <html lang="ko">

      <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>로그인</title>
        <style>
          h1 {
            color: lightgreen;
            /**/
          }

          /* 가상요소 */
          p::before {
            content: '안녕!';
          }
        </style>
      </head>

      <body>
        <h1>로그인</h1>
        <form action="">
          <p>아이디와 비밀번호를 입력하고 로그인하세요</p>
          <label for="user-id">
            아이디 <input type="text" required>
          </label>
          <br>
          <label for="user-password">
            비밀번호 <input type="password" required>
          </label>
          <br>
          <label for="user-id-save">
            <input type="checkbox" name="id-save"> 아이디 저장
          </label>
          <br>
          <button type="submit">로그인</button>
        </form>

      </body>

      </html>
      ```

```css
<p style=:color:yellow;">Hello World<p>
```

## 2. 내부 스타일

- head 태그 안에 `style` 태그 사용하기
- 코드가 길어질수록 HTML 파일 길이가 길어져 효율성 낮음

## 3. 외부 스타일

- HTML/CSS 분리 → 가장 권장되는 방법
- `head` 태그 내부에 `link` 태그를 작성해 현재 문서와 외부 리소스의 관계를 명시함.
  - `rel` : 관계, 대상 파일의 속성. css 파일은 **stylesheet**로 작성
  - `href` : 경로. 연결 시 참조할 파일의 위치.

```html
<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>로그인</title>
    <style>
      h1 {
        color: lightgreen;
        /**/
      }

      /* 가상요소 */
      p::before {
        content: "안녕!";
      }
    </style>
    <link rel="stylesheet" href="style.css" />
  </head>

  <body>
    <h1>로그인</h1>
    <form action="">
      <p>아이디와 비밀번호를 입력하고 로그인하세요</p>
      <label for="user-id"> 아이디 <input type="text" required /> </label>
      <br />
      <label for="user-password">
        비밀번호 <input type="password" required />
      </label>
      <br />
      <label for="user-id-save">
        <input type="checkbox" name="id-save" /> 아이디 저장
      </label>
      <br />
      <button type="submit">로그인</button>
      <!-- form 내부 button은 자동으로 type이 submit이지만 
      명시적으로 써줘도 괜찮다 -->
    </form>
  </body>
</html>
```

```css
p {
  color: royalblue;
  font-size: 20px;
}
```

# CSS 상속

## 같은 css를 여러 곳에 적용하기

- 동일한 CSS를 여러 개의 태그에 적용하는 법

  1. 태그별로 개별적으로 인라인 스타일 적용하기

     ```html
     <p style="color:red">Hi</p>
     <div style="color:red">Hello</p>
     <span style="color:red">Bonjour</p>
     ```

  2. 태그 선택자별로 CSS 일일이 작성하기

     ```css
     p {
       color: red;
     }
     div {
       color: red;
     }
     span {
       color: red;
     }
     ```

  3. 그룹 선택자(`,`로 묶기) 로 적용하기

     ```css
     p,
     div,
     span {
       color: red;
     }
     ```

  4. 상속 이용하기

     ```html
     <div>
     	<p>Hi</p>
     	<div>Hello</p>
     	<span>Bonjour</p>
     </div>
     ```

     ```css
     div {
       color: red;
     }

     p {
       color: royalblue;
       font-size: 20px;
     }
     ```

## 상속(Inheritance)

- 상속되지 않는 속성 : `width`, `height`, `margin`, `padding`, `border`
  - 크기와 관련된 속성은 상속되지 않는다
  - ??가 밀리는 것을 방지하기 위함이라고 설명하셨는데 놓쳤음
- `inherit` : 부모와 동일한 속성값을 상속받음
  - 실무 잘 사용 x
- `initial` : 브라우저 기본 스타일 속성을 따름
  - 실무 잘 사용 x

# CSS 선택자

선택자는 복합적으로 사용할 수 있다

```css
[class="color-red"],
#second-h2 p {
  color: red;
}
```

color-red를 class로 가진 요소와 second-h2를 id로 가진 p 요소를 모두 선택한다.

## 전체 선택자

- `html`을 포함한 HTML 문서 내의 모든 요소를 선택함.
  ```css
  * {
    margin: 0;
    padding: 0;
  }
  ```
- reset CSS : 보통 별도 CSS 파일에 분리해 개발자간 공유해 동일한 백지에서 시작
  [meyerweb.com](https://meyerweb.com/eric/tools/css/reset/index.html)
  브라우저마다 공통적인 디자인이 적용되도록 reset CSS 가능하나, 오래된 방법이다.
  전체 선택자 \* 사용 가능
- normalize.css
  [Normalize.css: Make browsers render all elements more consistently.](https://necolas.github.io/normalize.css/)
  reset CSS와 달리 브라우저의 CSS를 제거하기보다는 통일하는 데 초점이 있음
  FE에서 가장 많이 사용하는 편

## 타입(유형) 선택자 (태그 선택자, 요소 선택자)

- 요소(태그)의 이름을 그대로 선택자로 사용하는 것
- 해당 태그/요소가 모두 선택됨

## 아이디 선택자(`#`)

- HTML 페이지 내에서 하나의 id는 한 번만 사용해야 한다. 중복사용 ❌
- 좀 더 구별되는 용례
  - `label`의 `for` 속성값과 `input`의 `id` 속성값을 통일시켜 연결하기
  - `a` 태그 `href` 속성값으로 `#id값`
- JS, 해시 링크와 함께 사용

## 클래스 선택자(`.`)

- HTML 페이지 내에 여러 개가 존재할 수 있음. 중복사용 ⭕
- 아이디 선택자와 클래스 선택자도 붙여 쓸 수 있으나 크게 자주 사용하지 않음

## 특성 선택자(`[]`)

- 주어진 특성을 가진 모든 요소를 선택함

  ```css
  [type="button"] {
    border: 0;
    cursor: pointer;
  }
  [class="btn"] {
    color: #fff;
    background: royalblue;
  }
  ```

  type이 button인 모든 요소를 선택함. class가 btn인 모든 요소를 선택함

  ```css
  [type] {
    border: 0;
    cursor: pointer;
  }
  ```

  type 속성을 사용하는 모든 요소를 선택함

  ```css
  .color-red {
    color: red;
  }

  [class="color-red"] {
    color: red;
  }
  ```

  위 두 CSS는 같은 의미를 갖는다.

  ```css
  h1 {
    font-weight: bold;
  }
  h2 {
    font-weight: bold;
  }
  h3 {
    font-weight: bold;
  }
  h4 {
    font-weight: bold;
  }
  h5 {
    font-weight: bold;
  }
  h6 {
    font-weight: bold;
  }
  ```

## 그룹 선택자(`,`)

```css
h1,
h2,
h3,
h4,
h5,
h6 {
  font-weight: bold;
}
```

## 복합 선택자

### 자손(하위) 선택자 ( ``) - 공백!

- `section p` → section 태그의 자식 태그인 p 태그 모두 선택

### 자식 선택자(`>`)

- **직계자손만**을 선택함.
- `section > p` → section 태그의 직계자손 태그인 p 태그 두가지만 선택

### 일반 형제 선택자(`~`)

- 뒤에 나오는 형제만 (**\*\***모두)**\*\*** 선택함
- `section ~ p` → section 뒤의 형제태그 3가지인 p 태그만 선택

### 인접 형제 선택자(`+`)

- 바로 뒤에 인접한 형제만 선택함
- `section + p` → section태그 바로 뒤의 p 태그 **하나만** 선택

---

## 가상 클래스 선택자

- pseudo selector

### 가상 클래스

- `:link`
- `:visited`
- `:hover`
- `:active`
- `:focus`

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <link rel="stylesheet" href="style.css" />
  </head>

  <body>
    <section>asdf</section>
    <p>dd</p>
    <div>
      **<a href="https://www.daum.net">다음으로 이동하기</a>
      <a href="https://www.naver.com">네이버로 이동하기</a>**
      <h1 class="color-red">Hello</h1>
      <h2 class="color-red" id="first-h2">Hello</h2>
      <h2 id="second-h2">Hello</h2>
      <p>Hello</p>
    </div>
  </body>
</html>
```

```css
section ~ p {
  color: red;
}

/* a 요소 중 아직 방문하지 않은 a를 선택 */
a:link {
  color: teal;
}
a:visited {
  color: yellow;
}

/* 마우스를 올렸을 때 노란색으로 색상 변경 */
a:hover {
  color: yellow;
}

/* p 영역을 누르면 배경색 변경 */
p:active {
  background-color: teal;
}

/*(Tab을 이용해) 포커스가 이동할 경우 배경색 변경*/
a:focus {
  background-color: royalblue;
}
```

## 구조적 가상 선택자

- `:first-child` : **우선 부모를 찾아 들어가서** 형제 요소 그룹 중 첫번째 요소

  - ex) `div input:first-child` : div의 자식 중 input이 첫번째 자식일 경우 style을 부여함.
    - 가령 div의 첫번째 자식요소가 p이고 input이 두번째 요소라면 style이 적용되지 않음
    - 그 경우 `div p:first-child` 로 작성해야 할 것.
  - ❗ ex) `div:first-child` : `div`가 `body`의 첫번째 자식일 경우 style을 부여한다.
    ```css
    div:first-child {
      border: 3px solid pink;
    }
    ```
  - ex) table의 첫번재 열에 테두리 스타일을 적용하고 싶을 경우

    - `table tr td:first-child` : table의 자식 요소인 tr의 자식요소인 td가 첫번째 자식 요소일 경우 style을 부여한다

      - ```css
        <!DOCTYPE html>
        <html lang="en">

        <head>
          <meta charset="UTF-8">
          <meta name="viewport" content="width=device-width, initial-scale=1.0">
          <title>Document</title>
          <link rel="stylesheet" href="style.css">
        </head>

        <body>
          <table>
            <tr><td>hello1</td><td>hello2</td><td>hello3</td></tr>
            <tr><td>hello1</td><td>hello2</td><td>hello3</td></tr>
            <tr><td>hello1</td><td>hello2</td><td>hello3</td></tr>
          </table>
          <div>!!!</div>

          <section>
            asdf
          </section>
          <p>dd</p>
          <div>
            <p>hello world!!</p>
            <input type="password">
            <a href="https://www.daum.net">다음으로 이동하기</a>
            <a href="https://www.naver.com">네이버로 이동하기</a>
            <h1 class="color-red">Hello</h1>
            <h2 class="color-red" id="first-h2">Hello</h2>
            <h2 id="second-h2">Hello</h2>
            <p>Hello</p>
          </div>

        </body>

        </html>
        ```

        ```css
        #first-h2 {
        }

        #second-h2 {
          color: blue;
        }

        .color-red {
          color: red;
        }

        [class="color-red"] , #second-h2 p{
          color: red;
        } */

        section ~ p {
          color: red;
        }

        /* a 요소 중 아직 방문하지 않은 a를 선택 */
        a:link {
          color: teal;
        }

        a:visited {
          color: yellow;
        }

        a:hover {
          color: yellow;
        }

        p:active {
          background-color: teal;
        }

        a:focus {
          background-color: royalblue;
        }

        div:first-child {
          border: 3px solid pink;
        }

        **table tr td:first-child {
          border: 1px solid pink;
        }**
        ```

- `:last-child` : **형제들 중에서,** 형제 요소 그룹 중 마지막 요소

  - `div:last-child`

    ```html
    <!DOCTYPE html>
    <html lang="en">
      <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>Document</title>
        <link rel="stylesheet" href="style.css" />
      </head>

      <body>
        <table>
          <tr>
            <td>hello1</td>
            <td>hello2</td>
            <td>hello3</td>
          </tr>
          <tr>
            <td>hello1</td>
            <td>hello2</td>
            <td>hello3</td>
          </tr>
          <tr>
            <td>hello1</td>
            <td>hello2</td>
            <td>hello3</td>
          </tr>
        </table>
        <div>!!!</div>

        <section>asdf</section>
        <p>dd</p>
        <div>
          <p>hello world!!</p>
          <input type="password" />
          <a href="https://www.daum.net">다음으로 이동하기</a>
          <a href="https://www.naver.com">네이버로 이동하기</a>
          <h1 class="color-red">Hello</h1>
          <h2 class="color-red" id="first-h2">Hello</h2>
          <h2 id="second-h2">Hello</h2>
          <p>Hello</p>
        </div>
      </body>
    </html>
    ```

    ```css
    section ~ p {
      color: red;
    }

    /* a 요소 중 아직 방문하지 않은 a를 선택 */
    a:link {
      color: teal;
    }

    a:visited {
      color: yellow;
    }

    a:hover {
      color: yellow;
    }

    p:active {
      background-color: teal;
    }

    a:focus {
      background-color: royalblue;
    }

    div:first-child {
      border: 3px solid pink;
    }

    table tr td:first-child {
      border: 1px solid pink;
    }

    **div:last-child {
      border: 1px solid red;
    }**
    ```

- `:nth-child` : 형제 사이에서의 순서에 따라 요소를 선택할 수 있음

  - 다만 실무에서 잘 쓰기 어려운 것이, 새로운 요소들이 추가되는 것을 바로 반영하기 어려울 수 있음.

  ```css
  /* 2번째 li */
  li:nth-child(2) {
    color: lime;
  }
  /* 홀수번째 li */
  li:nth-child(odd) {
    color: lime;
  }

  /* 짝수번째 li */
  li:nth-child(even) {
    color: lime;
  }
  /* 2n+1번째 li. (n은 0부터 1씩 증가합니다)*/
  li:nth-child(2n + 1) {
    color: lime;
  }
  ```

  - 기타 예시

    ```html
    <!DOCTYPE html>
    <html lang="en">
      <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>Document</title>
        <link rel="stylesheet" href="style.css" />
      </head>
      <body>
        <ul>
          <div>0</div>
          <li>1</li>
          <li>2</li>
          <li>3</li>
          <li>4</li>
        </ul>
        <table>
          <tr>
            <td>hello1</td>
            <td>hello2</td>
            <td>hello3</td>
          </tr>
          <tr>
            <td>hello1</td>
            <td>hello2</td>
            <td>hello3</td>
          </tr>
          <tr>
            <td>hello1</td>
            <td>hello2</td>
            <td>hello3</td>
          </tr>
        </table>
        <div>!!!</div>

        <section>asdf</section>
        <p>dd</p>
        <div>
          <p>hello world!!</p>
          <input type="password" />
          <a href="https://www.daum.net">다음으로 이동하기</a>
          <a href="https://www.naver.com">네이버로 이동하기</a>
          <h1 class="color-red">Hello</h1>
          <h2 class="color-red" id="first-h2">Hello</h2>
          <h2 id="second-h2">Hello</h2>
          <p>Hello</p>
        </div>
      </body>
    </html>
    ```

    ```css
    ul li:nth-child(3) {
      background-color: hotpink;
    }
    ```

    ul의 자식 중 li를 선택해 그 li가 세번째 자식일 경우 스타일을 부여함

    ```css
    ul li:nth-child(2n + 1) {
      background-color: hotpink;
    }
    ```

- `:not` : 부정 선택자
  ```css
  li:not(:first-child) {
    margin-top: 20px;
  }
  ```
  첫번째 자식이 아니면 margin 부여

## 가상 요소 선택자

- HTML에 존재하지 않는 선택자를 만든다
- 크게 두가지
  - `::before`
  - `::after`
- `content` : 가상 요소만 사용할 수 있는 속성
- 일반적인 CSS에서 사용할 수 있는 속성을 그대로 사용할 수 있음.
- `inline` 속성을 가짐.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <link rel="stylesheet" href="style.css" />
  </head>

  <body>
    <article>hello element!</article>
    <ul>
      <div>0</div>
      <li>1</li>
      <li>2</li>
      <li>3</li>
      <li>4</li>
    </ul>
    <table>
      <tr>
        <td>hello1</td>
        <td>hello2</td>
        <td>hello3</td>
      </tr>
      <tr>
        <td>hello1</td>
        <td>hello2</td>
        <td>hello3</td>
      </tr>
      <tr>
        <td>hello1</td>
        <td>hello2</td>
        <td>hello3</td>
      </tr>
    </table>
    <div>!!!</div>

    <section>asdf</section>
    <p>dd</p>
    <div>
      <p>hello world!!</p>
      <input type="password" />
      <a href="https://www.daum.net">다음으로 이동하기</a>
      <a href="https://www.naver.com">네이버로 이동하기</a>
      <h1 class="color-red">Hello</h1>
      <h2 class="color-red" id="first-h2">Hello</h2>
      <h2 id="second-h2">Hello</h2>
      <p>Hello</p>
    </div>
  </body>
</html>
```

```css
section ~ p {
  color: red;
}

/* a 요소 중 아직 방문하지 않은 a를 선택 */
a:link {
  color: teal;
}

a:visited {
  color: yellow;
}

a:hover {
  color: yellow;
}

p:active {
  background-color: teal;
}

a:focus {
  background-color: royalblue;
}

div:first-child {
  border: 3px solid pink;
}

table tr td:first-child {
  border: 1px solid pink;
}

div:last-child {
  border: 1px solid red;
}

ul li:nth-child(2n + 1) {
  background-color: hotpink;
}
li:not(:first-child) {
  margin-top: 20px;
}

**article::after {
  content: "first-child!";
}**
```

# CSS 선택자 우선순위

## 1. 후자우선의 원칙

- 동일한 선택자에 동일한 속성(attribute)이 사용되면 나중에 적힌 속성(attribute)을 따른다.
- 가중치가 같을 때 후자우선의 원칙이 적용된다.

## 2.구체성의 원칙(Specificity)

- 선택자가 구체적일수록 우선순위가 높다.
- ex) `body p`가 `p`보다 우선순위가 높다
- 가중치를 통해 점수에 따라 그 구체성을 판단한다.

### 2.1 가중치

```css
body p {
  background-color: green;
} /* 2점 */

p.text {
  background-color: red;
} /* 11점 */

#txt {
  background-color: pink;
} /* 100점 */
```

개발자들이 inline style을 잘 사용하지 않는 것은 inline style의 가중치가 너무 높기 때문

### 2.2 우선 순위 계산

| inline-style                    | 1000점 |
| ------------------------------- | ------ |
| id 선택자 #                     | 100점  |
| class ., 가상클래스, 속성선택자 | 10점   |
| 타입, 가상요소 선택자           | 1점    |
| 전체선택자 \*                   | 0점    |

점수화하기는 했지만, 아무리 점수가 더 낮더라도더라도 (ex. class 선택자 10점 < 타입 선택자 10회로 10점) 더 높은 순위의 선택자의 우선순위가 점수가 더 높은 낮은 순위의 선택자보다 우선순위가 높다.

## 3. 중요성의 원칙

`!important` : 다른 어떤 선언보다도 우선한다. 그러다 오류/버그 발생 대응을 어렵게 하기 때문에 사용을 지양하자.

# display 속성

<aside>
💡 [주의] CSS 속성으로 시각적인 부분이 바뀌었을 뿐 태그 자체의 요소가 블록 레벨로 바뀐 것은 아닙니다!

</aside>

설명 놓침..

- `block` : 요소 전후에 줄 바꿈을 생성합니다.
- `inline` : 요소 전후에 줄 바꿈을 생성하지 않는 인라인 요소 상자를 생성합니다. 정상적인 흐름에서 공간이 있으면 다음 요소는 같은 줄에 있습니다.
- `inline-block`: inline 줄 바꿈 없이 한 줄에 놓이지만, block처럼 box-model의 width, height, margin, padding 값을 모두 설정할 수 있습니다.
  - 한 줄에 놓일 수 있지만 inline과 달리 크기조정 가능
- `flex`: 내부 자식 요소들의 위치를 부모 컨테이너 요소 안에서 x, y축 단방향(1차원적)으로 설정합니다.
  - 컨테이너 내부의 자식들을 정렬하기 위해 설정
- `grid`: 내부 자식 요소들의 위치를 부모 컨테이너 요소 안에서 x, y축 모두 이용해(2차원적) 설정합니다.
  - 컨테이너 내부의 자식들을 정렬하기 위해 설정
- `none`: 해당 속성은 접근성 트리(DOM 트리)에서 해당 요소가 제거됩니다. 이렇게 되면 해당 요소 및 해당 하위 요소가 사라지고, 스크린리더에도 읽히지 않습니다.
  - HTML 상에는 존재하지만 DOM트리에서 제거되어 화면상에 보이지 않음

# CSS Box Model

- contents, padding, border까지의 합을 p 태그의 영역으로 본다.

```css
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <style>
    /* body p {
      background-color: green;
    }

    p.text {
      background-color: red;
    }

    #txt {
      background-color: pink;
    } */

    p {
      width: 200px;
      height: 300px;
      border: 3px solid red;
      padding: 50px 50px 50px 50px;
      margin: 50px 50px 50px 50px;
      background-color: pink;

    }
  </style>

</head>

<body>
  <p class="text">Lorem ipsum dolor sit amet consectetur adipisicing elit. Iure vero reprehenderit molestias, voluptas,
    excepturi
    perferendis aspernatur officiis doloremque ullam exercitationem dolorum quod labore? Iure ad eligendi sequi modi ab
    perspiciatis!</p>

</body>

</html>
```

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e8f11927-b70c-4524-9227-a3efac08e7aa/beee737f-bc3c-449c-9dc6-a94b8abb3471/Untitled.png)

## width

- 기본값: `auto` → 브라우저에 입력된대로 알아서 너비값이 설정된다. (부모 요소의 크기 기준으로 가득 채움)

## height

- 기본값: `auto` → 브라우저에 입력된대로 알아서 너비값이 설정된다. (자식 요소의 크기 기준으로 가득 채움)

## padding

- 요소 **\*\*\*\***내부**\*\*\*\***의 여백 공간 생성
- `padding-top`, `padding-right`, `padding-bottom`, `padding-left`로 축약해 쓸 수 있으나 한번에 작성할 수도 있음.

## margin

- 요소 \***\*외부\*\***의 여백 공간 생성
- 요소 간 여백을 만들고 싶을 때 사용한다.
- `margin-auto`: 수평 정렬 ⭕ 세로 정렬 ❌ ⇒ **margin**을 동등히 분배함
  - ❓왜 수평 정렬만 가능할까?
    - 멘토님 왈, 마우스 휠은.. 세로로만 스크롤이 된다. 웹 표준상 세로 정렬은 불필요했다~
  - 보통 가운데 정렬로 `margin: 0 auto;`를 사용한다.
- block 레벨 요소는 자기가 가진 영역 외의 부분을 모두 **margin**으로 채우기 때문에 다른 요소가 옆의 남은 영역으로 올라올 수 없다.

### 마진병합 현상(Margin Collapsing)

```css
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <style>

    p {
      width: 200px;
      height: 300px;
      border: 3px solid red;
      /* padding: 100px 50px 50px 50px; */
      margin: 30px 30px 30px 30px;
      background-color: pink;

    }
  </style>

</head>

<body>
  <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Iure vero reprehenderit molestias, voluptas,
    excepturi
    perferendis aspernatur officiis doloremque ullam exercitationem dolorum quod labore? Iure ad eligendi sequi modi ab
    perspiciatis!</p>
  <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Iure vero reprehenderit molestias, voluptas,
    excepturi
    perferendis aspernatur officiis doloremque ullam exercitationem dolorum quod labore? Iure ad eligendi sequi modi ab
    perspiciatis!</p>

</body>

</html>
```

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e8f11927-b70c-4524-9227-a3efac08e7aa/78357678-4227-4a24-8698-e37c434a6b30/Untitled.png)

p 요소 사이에 60px의 margin이 존재하지 않고 30px

```css
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <style>
    /* body p {
      background-color: green;
    }

    p.text {
      background-color: red;
    }

    #txt {
      background-color: pink;
    } */

    p {
      width: 200px;
      height: 300px;
      border: 3px solid red;
      /* padding: 100px 50px 50px 50px; */
      **margin: 30px 30px 70px 30px;**
      background-color: pink;

    }
  </style>

</head>

<body>
  <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Iure vero reprehenderit molestias, voluptas,
    excepturi
    perferendis aspernatur officiis doloremque ullam exercitationem dolorum quod labore? Iure ad eligendi sequi modi ab
    perspiciatis!</p>
  <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Iure vero reprehenderit molestias, voluptas,
    excepturi
    perferendis aspernatur officiis doloremque ullam exercitationem dolorum quod labore? Iure ad eligendi sequi modi ab
    perspiciatis!</p>

</body>

</html>
```

### 마진병합 현상 해결방법

1. 부모 요소에 `overflow` 속성 값 적용하기
   - 자식요소가 부모요소의 영역을 벗어날 때
   - hidden : 숨기기
   - scroll : 부모 요소에 scroll을 만들어 더 보게 하기
2. 부모 요소에 `display: inline-block` 적용하기
3. 부모 요소에 `border` 값 정하기
4. 부모 요소에 `display:flow-root` 사용하기 (IE X)

## border

## box-sizing

- 넓이/ 높이값 하나로 요소의 전체적인 크기를 정할 수 있음
- `content-box` : 기본값. width, height에 border, padding을 포함하지 않음
- `**border-box` : width, height에 border, padding을 포함함.\*\*
  - width = 콘텐츠 너비 + obrder + padding
  - 실무에서 자주 사용함

## overflow, overflow-x, overflow-y

## border-radius

- radius: border의 꼭짓점 근처에서 그려줄 원의 반지름의 길이

## opacity

- 투명도
