# [HTML5 Introduction & Syntax](https://poiemaweb.com/html5-syntax)

## HTML

`HTML (HyperText Markup Language)`은 웹페이지를 기술하기 위한 `마크업 언어`이다. 조금 더 자세히 말하면 웹페이지의 **내용(content)** 과 **구조(structure)** 을 담당하는 언어로써 HTML 태그를 통해 정보를 구조화하는 것이다.

**HTML5는 2014년 10월 28일 확정된 차세대 웹 표준으로 아래와 같은 기능들이 추가되었다.**

`멀티미디어(Multimedia)`

    플래시와 같은 플러그인의 도움없이 비디오 및 오디오 기능을 자체적으로 지원한다.

`그래픽(Graphics & Effects)`

    SVG, 캔버스를 사용한 2차원 그래픽과 CSS3, WebGL을 사용한 3차원 그래픽을 지원한다.

`통신(Connectivity)`

    지금까지의 HTML은 단방향 통신만이 가능하였으나 HTML5는 서버와의 소켓 통신을 지원하므로 서버와의 양방향 통신이 가능하다.

`디바이스 접근(Device acess)`

    카메라, 동작센서 등의 하드웨어 기능을 직접적으로 제어할 수 있다.

`오프라인 및 저장소(Offline & Storage)`

    오프라인 상태에서도 애플리케이션을 동작시킬 수 있다. 이는 HTML5가 플랫폼으로서 사용될 수 있음을 의미한다.

`시맨틱 태그(Semantics)`

    HTML 요소의 의미를 명확히 설명하는 시맨틱 태그를 도입하여 브라우저, 검색엔진, 개발자 모두에게 콘텐츠의 의미를 명확히 설명할 수 있다. 이를 통해 HTML 요소의 의미를 명확히 해석하고 그 데이터를 활용할 수 있는 시맨틱 웹을 실현할 수 있다.

`CSS3`

    HTML5는 CSS3를 완벽하게 지원한다.

<br />

---

## Hello HTML5

HTML5 문서는 반드시 `<!DOCTYPE html>`으로 시작하여 문서 형식(document type)을 HTML5로 지정한다.

실제적인 HTML document은 2행부터 시작되는데 `<html>`과 `</html>` 사이에 기술한다.

`<head>`와 `</head>` 사이에는 `document` `title`, `외부 파일의 참조, 메타데이터의 설정 등이 위치`하며 `이 정보들은 브라우저에 표시되지 않는다.`

웹브라우저에 출력되는 모든 요소는 `<body>`와 `</body>` 사이에 위치한다.

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>Hello World</title>
  </head>
  <body>
    <h1>Hello World</h1>
    <p>안녕하세요! HTML5</p>
  </body>
</html>
```

<br />

---

## 빈 요소 (Empty Element)

**빈 요소 중 대표적인 요소는 아래와 같다.**

- br
- hr
- img
- input
- link
- meta

**글로벌 어트리뷰트 (HTML Global Attribute)** || [Global Attribute](https://www.w3.org/TR/2010/WD-html-markup-20101019/global-attributes.html)

    글로벌 어트리뷰트는 모든 HTML 요소가 공통으로 사용할 수 있는 어트리뷰트다. 몇몇 요소에는 효과가 적용되지 않을 수 있지만, 글로벌 어트리뷰트는 대체로 모든 요소에 사용될 수 있다.

    자주 사용되는 글로벌 어트리뷰트는 아래와 같다.

| Attribute  | Description                                                                                |
| :--------- | :----------------------------------------------------------------------------------------- |
| `id`       | 유일한 식별자(id)를 요소에 지정한다. 중복 지정이 불가하다.                                 |
| `class`    | 스타일시트에 정의된 class를 요소에 지정한다. 중복 지정이 가능하다.                         |
| `hidden`   | css의 hidden과는 다르게 의미상으로도 브라우저에 노출되지 않게 된다.                        |
| `lang`     | 지정된 요소의 언어를 지정한다. 검색엔진의 크롤링 시 웹페이지의 언어를 인식할 수 있게 한다. |
| `style`    | 요소에 인라인 스타일을 지정한다.                                                           |
| `tabindex` | 사용자가 키보드로 페이지를 내비게이션 시 이동 순서를 지정한다.                             |
| `title`    | 요소에 관한 제목을 지정한다.                                                               |

<br />

---
