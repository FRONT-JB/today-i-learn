# [Link](https://poiemaweb.com/html5-tag-link)

<br />

## href 어트리뷰트

href 어트리뷰트는 이동하고자 하는 파일의 위치(경로)를 값으로 받는다. 경로(path)란 파일 시스템 상에서 특정 파일의 위치를 의미한다.

<br />

### 디렉터리(Directory)

디렉터리는 파일과 다른 디렉터리를 갖는 파일 시스템 내의 존재물로서 폴더라고도 불리운다.

`루트 디렉터리`
파일 시스템 계층 구조 상의 최상위 디렉터리이다.

    Unix: /
    Windows: C:\

<br />

`홈 디렉터리`
시스템의 사용자에게 각각 할당된 개별 디렉터리이다.

    Unix: /Users/{계정명}
    Windows: C:\Users\{계정명}

<br />

`작업 디렉터리`
작업 중인 파일의 위치한 디렉터리이다.

    ./

<br />

`부모 디렉터리`
작업 디렉터리의 부모 디렉토리이다.

    ../

---

### 파일 경로(File path)

파일 경로는 파일 시스템에서 파일의 위치를 나타내는 방법이다. 경로에는 `절대경로`와 `상대경로`가 있다.

`절대경로(Absolute path)`

**현재 작업 디렉터리와 관계없이 특정 파일의 절대적인 위치**를 가리킨다. 루트 디렉터리를 기준으로 파일의 위치를 나타낸다.

    http://www.mysite.com/index.html
    /Users/leeungmo/Desktop/myImage.jpg
    C:\users\leeungmo\Desktop\myImage.jpg
    /index.html

<br />

`상대경로(Relative path)`
**현재 작업 디렉터리를 기준으로 특정 파일의 상대적인 위치**를 가리킨다.

    ./index.html
    ../dist/index.js
    ../../dist/index.js
    index.html
    html/index.html

<br />

**href 어트리뷰트에 사용 가능한 값은 아래와 같다.**

| Value                 | Description                                                    |
| :-------------------- | :------------------------------------------------------------- |
| `절대 URL`            | 웹사이트 URL (href=”http://www.example.com/default.html”)      |
| `상대 URL `           | 자신의 위치를 기준으로한 대상의 URL (href=”html/default.html”) |
| `fragment identifier` | 페이지 내의 특정 id를 갖는 요소에의 링크 (href=”#top”)         |
| `메일`                | mailto:                                                        |
| `script`              | href=”javascript:alert(‘Hello’);”                              |

```html
<!DOCTYPE html>
<html>
  <body>
    <a href="http://www.google.com">URL</a><br />
    <a href="html/my.html">Local file</a><br />
    <a href="file/my.pdf" download>Download file</a><br />
    <a href="#">fragment identifier</a><br />
    <a href="mailto:someone@example.com?Subject=Hello again">Send Mail</a><br />
    <a href="javascript:alert('Hello');">Javascript</a>
  </body>
</html>
```

## target 어트리뷰트

target 어트리뷰트는 링크를 클릭했을 때 윈도우를 어떻게 오픈할 지를 지정한다.

| Value    | Description                                                     |
| :------- | :-------------------------------------------------------------- |
| `_self`  | 링크를 클릭했을 때 연결문서를 현재 윈도우에서 오픈한다 (기본값) |
| `_blank` | 링크를 클릭했을 때 연결문서를 새로운 윈도우나 탭에서 오픈한다   |

```html
<!DOCTYPE html>
<html>
  <body>
    <a href="http://www.google.com" target="_blank" rel="noopener noreferrer"
      >Visit google.com!</a
    >
  </body>
</html>
```

`target="_blank"`를 사용해 외부 페이지를 오픈하는 경우, 이동한 외부 페이지에서
자바스크립트 코드를 사용해 악의적인 페이지로 리다이렉트할 수 있는 **보안 취약점(Tabnabbing 피싱 공격)이 있다.** 따라서 `rel="noopener noreferrer"`를 추가해
**Tabnabbing 피싱 공격에 대비할 것을 권장**한다. 참고로 **noopener 속성은 성능 상
이점도 있는 것으로 알려져 있다.** 자세한 내용은 아래 링크를 참고하기 바란다.
