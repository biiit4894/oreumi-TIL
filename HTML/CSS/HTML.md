HTML 강의를 수강하며 새로 배운 부분들과 이미 알고 있었더라도 다시 한 번 정리하기 위한 내용들을 적어봅니다.

HTML을 안다고 생각했지만 HTML 자체와 개별 태그가 실제로 가지는 의미를 다시 정리하니 모르는 부분들이 생각보다 많이 나와 다시 정리를 해본다.

div를 무조건 사용하기 보다는 section을 나타내는 다양한 시멘틱 태그를 사용하는 것이 더 나은 선택이 될 수 있음에는, 의미 있는 코드 작성이라는 이유 뿐만 아니라 웹 접근성과 SEO라는 또다른 뜻깊은 이유를 알 수 있었다.

<br/>

# HTML 기본

- W3C **Markup Validation Service**
  - IntelliJ와 같이 마크업을 자동으로 검사해주는 IDE를 사용하기 어려운 환경이라면 Markup Validation Service에서 Direct Input을 선택해 소스코드를 검사해보는 것도 방법이다.

## 태그, 요소의 포함

- <></> 태그를 통해 요소 표현
- 부모 요소 내에 자식 요소를 포함시키고 요소 간에 형제관계도 성립할 수 있다.

## 빈 요소/셀프 클로징

- self closing, void closing
  - ex) `<br>`
- 엄격한 문법 준수를 위해 XHTML 마크업 언어가 만들어졌지만 현재의 HTML Leading Standard 에서는 이것이 통합되어 굳이 사용할 필요가 없어졌다.
  - ex) `<br/>`

## 주석

- 포스트 프로세서를 돌리면 주석처리, 띄어쓰기, 줄바꿈과 같은 부분을 제거해 코드 용량을 줄여주는 최적화를 할 수 있다.
- 그래도 기밀사항은 적지 말기!

- 용도

  1. 태그의 시작과 끝을 적어놓기

     ```html
     <!-- start -->
     <!-- //end -->

     <!-- 태그이름 -->
     <!-- //태그이름 -->
     ```

     - 이렇게 구분지으면 나중에 **컴포넌트 분할**에도 도움이 된다.
       ❓ 리액트 컴포넌트화는 알겠는데, 컴포넌트 분할?
       자바는 ThymeLeaf(자바와 HTML을 섞어 사용 가능)를 사용할 때 HTML을 컴포넌트 단위로 분리한다.

  2. 협업할 때

     ```html
     <!-- 휴대폰번호 인증필요 -->
     <input type="tel" />

     <!-- #2022.02.20 4:00 업데이트 -->
     ```

  3. 사용하지 않지만 지우기 애매/위험해서 임시 처리

### 부모, 형제, 자식, 자손

❓ 자손

기준이 되는 태그의 자식 태그가 가진 또다른 자식태그

```java
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <p>
        HTML은 요소 안에
        <strong>다른 요소</strong>가 들어갈 수 있습니다
    </p>
    <main> // 조상
        <section> // 부모
            <div> // 기준
                <p> // 직계자식
                    <a href=""></a> // 자손
                </p>
                <p></p>
                <p></p>
                // emit 문법 : p*3 + Tab
            </div>
        </section>
    </main>

    <!-- 잘못 사용된 예 -->
    <!-- 주석 -->
    <p>
        HTML은 요소 안에
        <strong>다른 요소 가 들어갈 수 있습니다</strong>
    </p>

</body>
</html>
```

<br/>

# Web, 그리고 HTML

html 파일 생성 시 꼭 기재해야 하는 !DOCTYPE 태그. html 문서 내에서 DOCTYPE은 문서의 타입을 의미하고, document는 HTML 문법을 가지고 작성된 모든 내용을 의미한다.

HTML은 어쩌다가 탄생했을까?

팀 버너스 리는 모든 사람들이 같은 화면을 어디서든 볼 수 있는 시스템을 만들기 위해 Web을 만들었고, HTML은 동일한 타입으로 문서를 조회하기 위해 만들어진 포맷이다.

Web의 주요한 세가지 발명품은 아래와 같다.

1. `HTTP` (Hyper Text Transfer Protocol)
   - 하이퍼 텍스트를 이동시키는 통신 규약
   - 하이퍼 텍스트: 책장을 넘기며 보는 실물 텍스트와 달리 **링크**를 클릭해 이동 가능하다.
2. `HTML` (Hyper Text Markup Language)
   - file format, 언어 문법
   - 초문자를 마크업 언어로 표현한다.
3. `URL` (Uniform Resource Locator)
   - HTML 파일을 HTTP 규약으로 전달해서 저장하는 방법
     <br/>

# HTML 문서 해부

## 1. `<!DOCTYPE html>`

- 이 문서는 **html Living Standard 문서\***라는 의미
  ❓ 최신 HTML standard 문서는 HTML5 아닌가요?
  이제는 HTML 버전을 구분하지 않고 **HTML Living Standard**라는 단어로 통합적으로 표현한다.
- DTD (Document Type Definition) 로, 문서의 타입에 대한 정보를 제공함. 어떤 모드로 페이지를 렌더링할지 결정한다.
- 작성하지 않더라도 기본적으로 브라우저의 예외처리에 의해 알아서 처리된다
  ⇒ 쿼크 모드로 html 렌더링
  ⇒ ‘이 문서는 오래된 버전의 HTML 문서이구나’라고 인식하고 브라우저 나름의 방법으로 렌더링한다. 브라우저마다 이전 문서를 렌더링하는 방법이 다르다.
- 그치만! 반드시 넣는 것이 좋다.

## 2. `<html lang=”en”>`

- 주 언어 설정은 html 태그에 하나로 설정한다.
- 검색엔진, 스크린리더, 번역 기능 제공 등 웹 접근성에 필요.
- 자식 요소 중 하나를 다른 주언어를 사용하도록 하고 싶으면 속성값으로 `lang="**"`을 지정해주자.

## 3. `head`

- 기계가 식별할 수 있는 문서 정보(메타데이터)
- 검색엔진을 위한 정보를 담음
- 이 내부 내용은 화면상에 보이지 않음

### meta

- 메타데이터: **어떤 목적을 위해 만들어진 데이터”**
- 검색엔진은 메타정보를 살펴보고 페이지의 다양한 정보를 가져갑니다.

### charset

character set → 문자 설정

### http-equiv="X-UA-Compatible" content="IE=edge"

- 이 웹페이지는 internet explorer의 edge 버전에 맞춰져 있는 페이지라는 이야기. 사실 없어도 크게 상관은 없음.

### viewport

- `width=device-width` : width가 현재 화면을 보여주는 디바이스의 width와 동일하다는 의미.
- `user-scalable=no` : 유저가 이를 조정할 수 있는가 - no.(보통 모바일 기기가 이렇게 설정된다)
- `initial-scale=1.0` : 초기 크기 설정으로, 2.0이면 화면 크기가 2배가 된다.
- `maximum scale` : 최대 크기
- `minimum scale` : 최소 크기

### `title`

- 검색엔진 노출을 위해 중요!
  - 인터넷을 사용하는 사용자가 `title`에 담긴 내용(제목)을 보고 탐색할 페이지를 선택합니다.
- 페이지마다 적당한 제목이 노출되도록 개발하는 것도 중요합니다.
  ⇒ SEO (Search Engine Optimization)에 `title`이 상당히 중요하다!
  ex) 에어비앤비 | 휴가지 숙소, 통나무집, 해변가 주택 등
  저런 키워드를 검색하는 유저들이 유입되기를 바라는 의도가 있을 수도.

### `link`

- 외부의 리소스를 이 페이지 내에 가져오려고 할 때 사용하는 태그
- 스타일 시트, 폰트, 파비콘을 연결할 때 사용한다
  ❓ favicon : favorite icon, 상단 탭의 아이콘
- `rel` : 대상 파일의 속성.
  - 이 링크로 불러오는 대상 파일의 성격이 무엇인지 나타냄.
- `href` : hyper-references 경로. 연결 시 참조할 파일의 위치를 나타낸다.
  - 가져와야 할 리소스의 위치

## 4. body

- 사용자에게 보여줄 본격적인 작성 영역

<br/>

# 블록 레벨 요소 vs 인라인 레벨 요소

## block

- 페이지의 큰 구조를 만들고 싶을 때 block 레벨 요소를 만든다
- 줄바꿈 O
- 크기 지정 및 padding, border, margin 사용 가능
- <블록 요소> <인라인 요소> </인라인 요소> </블록요소> ⭕
- <인라인요소> <블록 요소> </블록 요소> </인라인 요소> ❌
  - `div` 안에 `span`은 괜찮지만 `span` 안에 `div`는 ❌
  ```html
  <span>
    Loren ipsum dolor.
    <p lang="en">Lorem ipsum dolor</p>
  </span>
  <span>hello</span>
  ```
- `div` `p` `form` …

## inline

- 컨텐츠에 따라 할당된 공간만 차지 → 작은 부분에 대해서만 적용
- 줄바꿈 X
- 크기지정 불가, padding, border, margin(top, bottom 안됨) 사용 가능
- `a` `label` `input` `span`

## block / inline / inline-block

<br/>

# 다양한 태그들

📌 일반적인 HTML 문서 틀

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    .. 중략
  </head>
  <body>
    <header>
      <nav></nav>
    </header>
    <main></main>
    <footer></footer>
  </body>
</html>
```

## 1. div, span

### div

<aside>
💡 div 태그는 스타일 적용을 위한 용도로 사용할것을 권장합니다.
(검색엔진최적화, 코드 가독성, 접근성 등의 이유)

header, footer, main, section, article, nav 등 다양한 시맨틱한 태그들을 사용하여 콘텐츠를 분할하고 그룹핑하는 것이 더 잘 작성한 코드이다.

- 시멘틱한 코드
  의미를 부여한, 의미있는 코드

📌 div만 존재하는 html을 작성하지 말고, 의미있는 HTML을 작성하자
⇒ div만 있는 html은 브라우저, 스크린 리더 모두 그 문서의 용도를 정확히 읽어낼 수 없고, 결국 SEO에도 부정적 영향을 끼친다

</aside>

❓ 그런데 왜 네이버 홈페이지를 개발자 도구로 조회하면 `div`가 난무할까?

- 시멘틱 태그 (ex. `main` )를 MDN에서 조회하면 브라우저 호환성에 있어 IE를 포함하지 않는 경우가 많다.
- 네이버와 같은 대규모 검색엔진은 IE 사용자까지 수용해야 하기에, 시멘틱 태그를 사용하는 데에 리스크가 있음. 어떤 사용자라도 화면을 잘 볼 수 있도록 하기 위함.

### span

- `div`와 마찬가지로 스타일 부여 전에는 콘텐츠, 레이아웃에 아무 영향을 주지 않음.
  <br/>

## 2. Sections

Section 관련 태그는 페이지 단위로 구획을 나눌때 사용한다.

다만, 구획별로 의미를 담아 구분하기 위해 용례에 따라 태그 이름을 선택하자.

### header

- 중첩 사용 불가
- 헤더 태그 내부에 푸터 태그 사용 불가.
- 검색 / 네비게이션을 위한 내용들이 보통 들어간다.

### nav

- 현재 페이지 내, 또는 다른 페이지로의 링크를 보여줌
- 메뉴, 목차, 브레드크럼으로 사용

❓ 브레드크럼

주로 페이지 상단 우측에 자리하여 유저가 웹사이트 내에서 어디에 있는지 알려주는 네비게이션 텍스트

ex) 무신사 홈페이지에서 내가 어느 대분류, 중분류, 소분류의 의류를 조회하고 있는지 브레드크럼으로 조회할 수 있음

### footer

- 페이지 작성자, 저작권 정보, 관련 문서

### main

- body의 **주요** 콘텐츠를 나타낸다
  → dominant content

### article

- **독립적**으로 구분해 배포하거나 재사용할 수 있는 구획
- 게시판, 블로그 글, 매거진, 뉴스 기사
  - 기사 홈페이지 메인 화면에서 기사 배너 하나(`article`)가 생략되더라도 전체 흐름에 영향을 주지 않음

### section

- section도 구획을 나누는 데 사용하지만, 제목 요소를 자식으로 포함해야 한다.

📌 `div`와의 차이점?
의미를 가지고 구획을 나눈다. 디자인상의 이유만으로 `section`을 나누지 X.

📝 예시
가령 다음 포털의 로그인과 핫딜 영역을 모두 묶어 `section`으로 구분하는 것은 좋은 선택이 아니다.

‘로그인, 핫딜 섹션’ 이라고 이름을 짓는 것도 적합하지 ❌
`section` 대신 `div`로 로그인, 핫딜 영역을 구분하기 ⭕

### aside

- 각주, 광고 배너
  <br/>

## 3. Contents

### h1, h2, h3, h4, h5, h6

heading 태그들은 보통 section 태그로 묶어서 쓴다.

### a

```html
<!-- <a> 요소로 아래의 구획에 연결 -->
<p><a href="#Section_further_down">아래 제목으로 건너뛰기</a></p>

<!-- 링크가 향할 제목 -->
<h2 id="Section_further_down">아래의 제목</h2>
```

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta
      name="viewport"
      content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0"
    />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Document</title>
    <style>
      p {
        display: inline; // 한 라인을 다 차지하다가 이제는 요소 자체의 영역만 차지함.
        background-color: teal;
      }

      section {
        height: 1000px;
      }
    </style>
  </head>
  <body>
    <!-- <a> 요소로 아래의 구획에 연결 -->
    <p><a href="#Section_further_down">아래 제목으로 건너뛰기</a></p>
    <section>hello</section>
    <!-- 링크가 향할 제목 -->
    <section>
      <h2 id="Section_further_down">아래의 제목</h2>
    </section>
  </body>
</html>
```

- a 태그 href 속성의 '#' 값 : 페이지 내부에서 다른 요소로 이동할 때 사용
- 클릭 이벤트가 발생할 때 페이지 전환이 되지 않도록 하기 위해 쓴다는 것은 부차적인 내용이다.
