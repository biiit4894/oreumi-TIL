- reference : 이스트소프트 오르미 백엔드 개발자 양성과정 4기 - 한재현 강사님 교안

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

## 2. sections

### article

`section` 태그와 유사하게 헤더 태그를 넣어주는 것이 권장된다.

article 태그 내부의 요소들은 하나의 독립적인 컨텐츠로 취급

### section

- **어떤 제목으로 엮을 수 있는 하나의 영역**

❗`section` 요소에는 제목 요소가 필요하기 때문에 `section`의 첫 자식으로는 `헤더 태그`가 들어간다.

### aside

- 문서 본문의 내용과 직접적 상관은 없고 보조적 역할
- ex. 다음 탑 화면(메인 화면)의 기획전 광고

## 3. Contents

### h1, h2, h3, h4, h5, h6

- heading 태그로 1~6이 범위이다
- `h1` 태그는 한 문서에 한 개가 주어져야 한다.
- 부모-자식 관계를 만들고자 한다면 `h1 → h2 → h3` … 반드시 순서대로 태그를 사용해야 한다.
  - `h1 → h3` 이런 식으로 단계를 건너뛰는 것은 권장되지 않는다.
- block 레벨 요소

### a

- 하이퍼링크 생성
- `href` : hypertext reference (하이퍼텍스트 참조)

  - `tel` : 전화번호
  - `mailto` : 이메일 주소
  - tel, mailto a 태그 클릭 시 윈도우는 메일, 맥은 페이스타임 등 관련 프로그램으로 연결시켜준다.
    ```html
    <a href="mailto:google@gmail.com">google@gmail.com</a>
    <a href="tel:010-0000-0000">010-2423-4894</a>
    ```

- target 속성값
  - `_self` : 현재 페이지에서 바로 새 페이지 오픈
    ```html
    <a href="mailto:google@gmail.com">google@gmail.com</a>
    <a href="tel:010-0000-0000">010-2423-4894</a>
    <a href="test.html">test로 이동합니다.</a>
    ```
  - `_blank` : 현재 페이지가 아니라 별도의 새 탭에서 페이지 오픈
- `download` : 링크로 이동하지 않고 사용자에게 URL에 위치하는 대상을 저장할지 물어본다. 브라우저가 바로 열 수 있는 파일이면 열어준다.
  ```html
  <a href="test.hwp" download="hangle">test로 이동합니다.</a>
  ```

### p

- 블록 요소
- 문단을 나타내며 이미, 입력 폼 등 서로 관련있는 콘텐츠는 무엇이나 될 수 있음

### strong

- 인라인 요소, p태그 내부에서 사용 가능하다
- 중대하거나 긴급한 콘텐츠
- 스크린 리더로 화면을 낭독할 때 **거센 억양으로 발음됨**

❓`b` 태그와 `strong` 태그의 차이는?

- b 태그는 strong과 동일하게 굵은 글씨를 나타내지만 CSS가 없던 시절에 문서의 스타일을 HTML 요소를 이용해 표현하려 할 때 사용된 태그이다. **의미 없이 굵은 글씨를 표현하기 때문에 사용을 지양하자.**

### br

- break, 줄을 나눈다는 의미.

❗줄바꿈을 위해 사용 ⭕ 간격을 벌리기 위해 여러 번 사용 ❌

### hr

- 이야기에서 장면 전환 또는 문단 안에서 주제가 바뀌었을 때 사용
- 단락 구분 용도이기 때문에 `p` 태그 내에서 사용하지 않는다.

### code

- 짧은 코드 조각(한 줄)
- 하이라이트는 불가

### pre

- HTML에 작성한 내용 그대로를 표현
- 들여쓰기, 줄바꿈 등도 그대로 반영된다.

## 4. 목록 태그

### ol

- 순차적 목록, 정렬되고 순서가 있는 (보통) 숫자 목록
- `type` : 항목을 셀 때 사용할 카운터 유형(디자이너의 의도에 따라가야 하기 때문에 잘 사용 x)
  - `1`
  - `a`
  - `A`
  - …
- `start` : 항목의 첫번째 수, 아라비아 숫자 가능
- `reversed` : 순서 역전

### ul

- 비순차적 목록

### li

- 목록의 항목
- 단독 사용 불가, `**ol`, `ul`의 자식요소로만 사용 가능함.\*\*

❗ 참고

- `ol`, `ul`의 자식요소로는 `li`만 사용할 수 있다.
- `ol`, `ul`의 자손요소로는 다른 태그도 사용 가능

### dl

설명 목록

https://developer.mozilla.org/ko/docs/Web/HTML/Element/dl

```html
<dl>
  <dt></dt>
  <dd></dd>
</dl>
```

## 5. Media

### img

- 문서에 이미지를 삽입
- 모자이크 웹 브라우저를 개발한 **마크 로웰 앤드리슨**은 이미지 태그를 만들었다
  - 글자와 이미지를 한 번에 보여주기 위해 모자이크 브라우저에 이미지 태그를 적용했다.
- ❓ 넷스케이프, 내비게이터, 그리고 코드네임
  - IE와의 경쟁 끝에 넷스케이프 내비게이터는 사업을 철수했지만 그 코드를 무료로 공개해 누구나 브라우저를 만들 수 있도록 했다.
  - 이후로 넷스케이프를 기반으로 파이어폭스, 사파리, 오페라와 같은 브라우저들이 출시됨.
  - Netscape의 codeName: `Mozilla`
  - Netscape에 대한 예우로 대부분의 브라우저는 appCodeName을 `Mozilla`로, appName을 `Netscape`로 설정한다.
- `src` : 경로
- `alt` : 이미지에 대한 설명으로, 대체 텍스트임.
  - 이미지 로딩에 실패했을 때 사용자에게 이미지에 대한 설명을 제공하기도
  - 시각장애인을 위한 스크린리더를 지원하나, `alt` 텍스트와 `img` 이후 텍스트가 중복된다면 스크린리더가 두 번 이상 동일한 내용을 읽기 때문에 `alt=""` 빈 값을 부여한다.
  - `alt` 속성값을 아예 부여하지 않는다면 이미지 소스의 경로값을 모두 읽어버리는 참사가 발생하기도..

<aside>
❓ 이미지 하단에 빈 공간이 생긴다면?

</aside>

이미지 요소 주변의 다른 요소에 `margin` 값을 `0`으로 주더라도 작은 간격이 계속 존재함.

**`img`가 인라인 요소**이기 때문에 발생하는 현상이다.

인라인 요소이기 때문에 `img`의 세로 정렬이 글자의 baseline을 따른다.

아래의 초기값을 부여하면 해결할 수 있다.

# 양식(form)

## form

- 사용자가 조작할 수 있는, 상호작용이 가능한 문서 구획
- 입력한 데이터를 제출, 전송하기 위해 사용하기 때문에 별도로 제출할 필요가 없다면 사용하지 않아도 괜찮다.
- **단점 : 데이터 전송 후 새로고침이 됨. (새로고침을 막는 것도 가능하기는 하다-기획에 따라 달라질것)**
  - form 내부 데이터를 서버에 전송하면, 브라우저는 서버로부터 어떤 응답을 받을 것이라고 기대한다.
  - 페이지를 다시 렌더링 → 갱신할 필요 없는 정보까지 다시 화면에 그리며 시간이 소요된다.
  - ex) 가령 지도 페이지를 보는데, 다른 영역의 지도를 보려고 드래그를 할 때마다 모든 영역이 다시 렌더링되어 계속 새로고침이 된다면 매우 불편할 것.
- ❓ `form` vs `AJAX`
  - form을 이용해 데이터를 요청/전송해야 할 경우 : form이 필요한 경우
  - AJAX를 이용해 데이터를 요청/전송해야 할 경우 : form이 굳이 필요 없는 경우

## `method` 속성

- 양식 제출에 사용할 HTTP 메서드
  - 크게 GET, POST가 있음

### POST

- 양식 데이터를 요청 본문으로 전송한다.
- 브라우저에 의해 캐시되지 않는다 → 기록이 남지 않는다는 이야기
- POST 방식의 HTTP 요청에 의한 데이터는 쿼리문자열과는 별도로 전송된다.
  - 쿼리를 전달하는 방식으로 데이터를 전송하지 않는다는 이야기
- `enctype` 속성
  - \***\*\*\*\*\***\*\*\***\*\*\*\*\***MIME 타입(Multipurpose Internet Mail Extensions)\***\*\*\*\*\***\*\*\***\*\*\*\*\***
    클라이언트에 전송된 문서의 다양성을 알려주기 위한 메커니즘.
    브라우저는 리소스를 내려받았을 때 해야 할 기본 동작이 무엇인지 결정하기 위해 사용한다.
  - `application/x-www-form-urlencoded` : 기본값
  - `multipart/form-data`: `<input type="file">`이 존재하는 경우 사용

### GET

- `https://example.com**?name=한빛&age=999**`
  - 양식 데이터를 action URL과 **?** 구분자 뒤에 이어 붙여서 전송.
- GET 방식의 HTTP 요청은 **브라우저에 의해 캐시되어 저장**
- 보통 쿼리 문자열에 포함되어 전송되므로 **길이의 제한**이 있음(URL 길이제한은 브라우저마다 다름)
- POST에 비해 보안상 취약점이 존재하기 때문에 중요한 데이터는 POST 방식으로 요청해야 한다.

❓ GET이 POST에 비해 장점이 존재할까?

❓ GET의 보안상 취약점 더 알아보기?

### name/value

- 사용자가 아무것도 입력하지 않은 경우 처음 설정한 `value`값으로 서버에 데이터가 보내진다.
- 사용자가 무언가 입력하면 `value` 값이 사용자의 입력값으로 바뀔 것.

### `action` 속성

- 양식 데이터를 처리할 프로그램의 URI를 적는다. 데이터를 어디로 보낼지 저장됨.
- 지정하지 않으면 `form`이 있는 페이지의 URL로 보내진다.(자기자신에게)

### `autocomplete` 속성

- 이전에 입력한 내용을 브라우저가 기억하고 힌트를 제공함.
- 해당 양식에 입력된 값이 있었다면 자동완성.

## label

- 이름표.
- `form` 내부에서 사용자와의 상호작용에 사용되는 사용자 인터페이스의 항목을 나타냄.
- 태그의 의미상 `input`과 함께 쓰는 것이 권장된다.

## button

- `form` 내부, 필요한 곳 어디든 배치 가능
- `button`
- `submit`
- `reset`

- `form` 내부에서 사용할 때는 `type`을 `submit`으로 꼭 지정할 필요는 없음

### button의 타입(type=””)

- `button` : 기본 타입. 기본 행동이 없음. JS와 연결.
  - 양식 제출용이 아니면 타입을 button으로 지정하자.
- `submit` : 서버로 양식 데이터 제출
- `reset`: 초깃값으로 되돌림

### `<a>` vs `<button>`

- `a` : 하이퍼링크 기능. 다른 페이지나 페이지 내 특정 영역으로 **\*\***이동**\*\***한다.
- `button` : 버튼 클릭 시 이 페이지 내부에서 일이 일어나기를 원한다면 사용하자

## input

### 공통 속성

### input 유형 <input type=”_____”>

중요한 몇 가지만 보기로

- button
- submit
- reset
- email : 이메일 입력(이메일 형식인지 확인)
- search : 검색 문자열 입력(삭제 아이콘 포함)
  ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e8f11927-b70c-4524-9227-a3efac08e7aa/5e87c611-45e0-4848-acb7-a05a17b8b7eb/Untitled.png)
- url
- checkbox
- radio: 여러 항목 중 하나 선택

<aside>
** 🤔 어떤걸 써야할까?**
`<**input** type=”button” value=”버튼”>`
`**<button type="button">버튼</button>**`

input 태그의 경우 빈태그 요소이기 때문에 `value` 특정에 텍스트 값 밖에 지정할 수 없습니다.
button 태그의 경우 여는태그와 닫는 태그 사이에 **여러 컨텐츠 삽입**이 가능합니다!

</aside>

기능상의 차이는 크게 없다.

button 태그는 자식 요소로 다른 요소들을 넣을 수 있다.

input 태그는 닫힌 태그이기 때문에 추가적인 컨텐츠의 삽입이 어렵다.

button 태그처럼 열고 닫는 태그는 UI를 커스터마이징 할 수 있다.

## text / password / url / search / tel

- **`maxlength`**: 문자수 최대 길이
- **`minlength`**: 문자수 최소 길이

## checkbox/radio

- `checkbox` : 단일 값을 선택하거나 선택 해제할 수 있음
- `radio` : 선택 후 선택 해제가 안됨
  - 동일한 카테고리 중 한 가지를 선택할 때 사용
  ```html
  <label>
    사과
    <input type="radio" name="과일" />
  </label>
  <label>
    배
    <input type="radio" name="과일" />
  </label>
  <label>
    수박
    <input type="radio" name="과일" />
  </label>
  ```

## fieldset

- 반드시 `legend`로 제목을 부여한다.

### legend

```html
<fieldset>
  <legend>아무거나</legend>
  <label for="animals">동물을 선택하세요: </label>
  <select id="animals">
    <optgroup label="포유류">
      <option>원숭이</option>
      <option>개</option>
      <option>고양이</option>
    </optgroup>
    <optgroup label="파충류">
      <option>도마뱀</option>
      <option>뱀</option>
    </optgroup>
  </select>
</fieldset>
```

## textarea

- 여러 줄의 text를 입력받을 수 있다

### textarea 속성

- `rows`, `cols`를 통해 입력창의 줄 수와 너비를 나타낸다.
- 텍스트 크기도 영향을 주기 때문에 `cols` 수 만큼 글자를 입력할 수 있다는 의미는 아님
- `rows`도 처음 보여지는 행의 개수이고 사용자가 `textarea` 크기를 조절할 수 있음
  - 사용자가 크기를 조절하는 것을 막고 싶다면
    ```html
    textarea{ resize:none; }
    ```

# 표(table)

- `<table>`은 테이블 데이터의 컨테이너 요소이다.

## tr, th, hd

- `tr` : table row. 테이블의 행
- `th` : table header. 테이블의 행, 열의 제목을 나타내는 셀
- `td` : table data. 셀 내용

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <style>
      table {
        border-collapse: collapse; /**/
      }

      table,
      th,
      td {
        border: 1px solid black;
      }
    </style>
  </head>

  <body>
    <table>
      <tr>
        <th>월요일</th>
        <th>수요일</th>
        <th>금요일</th>
      </tr>
      <tr>
        <td>짜장면</td>
        <td>짬뽕</td>
        <td>탕수육</td>
      </tr>
      <tr>
        <td>짜장면</td>
        <td>짬뽕</td>
        <td>탕수육</td>
      </tr>
      <tr>
        <td>짜장면</td>
        <td>짬뽕</td>
        <td>탕수육</td>
      </tr>
      <tr>
        <td>짜장면</td>
        <td>짬뽕</td>
        <td>탕수육</td>
      </tr>
    </table>
  </body>
</html>
```

## caption

- CSS `caption-side` 속성 : 많이 사용은 안하지만 caption의 위치 설정 가능

## thead, tbody, tfoot

- 선택적으로 사용하면 됩니다. 필수 요소는 아닙니다. 코드의 가독성을 위해 명시적으로 사용하면 좋습니다

## 속성값

### colspan, rowspan

- 셀병합 속성
- `colspan` : 열 병합
- `rowspan` : 행 병합

## colgroup

## col

- col에 영향을 주는 CSS 요소
  https://www.w3.org/TR/CSS21/tables.html#columns

## time

https://developer.mozilla.org/ko/docs/Web/HTML/Element/time
