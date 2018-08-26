---
layout: post
title: "마크다운 markdown 작성법"
subtitle: "허니몬님의 마크다운 작성법을 따라서 쳐보면서 스터디 하기"
categories: study
tags: markdown
---
[공통] 마크다운 markdown 작성법  
===============================
마크다운 작성법 스터디  
------------------------------- 

# 마크다운에 관하여
## 마크다운
[**Markdown**](http://whatismarkdown.com)은 텍스트 기반의 마크업언어로 2004년 존그루버에 의해 만들어졌으며 쉽게 쓰고
읽을 수 있으며 HTML로 변환이 가능하다. 특수기호와 문자를 이용한 매우 간단한 구조의 문법을 사용하여 웹에서도 보다 빠르게
컨텐츠를 작성하고 보다 직관적으로 인식할 수 있다.
마크다운이 최근 각광받기 시작한 이유는 깃헙([https://github.com](https://github.com)) 덕분이다.
깃헙의 저장소(**Repository**)에 관한 정보를 기록하는 README.md는 깃헙을 사용하는 사람이라면 누구나 가장 먼저 접하게
되는 마크다운 문서였다. 마크다운을 통해서 설치방법, 소스코드 설명, 이슈 등을 간단하게 기록하고 가독성을 높일 수 있다는
강점이 부각되면서 점점 여러 곳으로 퍼져가게 된다.

## 마크다운의 장-단점
### 장점
    1. 간결하다.
    2. 별도의 도구없이 작성 가능하다.
    3. 텍스트(Text)로 저장되기 때문에 용량이 적어 보관이 용이하다.
    4. 텍스트파일이기 때문에 버전관리시스템을 이용하여 변경이력을 관리할 수 있다.
    5. 지원하는 프로그램과 플랫폼이 다양하다.
### 단점
    1. 표준이 없다.
    2. 표준이 없기 때문에 도구에 따라서 변환방식이나 생성물이 다르다.
    3. 모든 HTML 마크업을 대신하지 못한다.

****
# 마크다운 사용법(문법)
## 헤더(**Headers**)
* 큰제목: 문서 제목
    ```
    This is an H1  
    =============
    ```
    This is an H1  
    =============

* 작은제목: 문서 부제목
    ```
    This is an H2  
    -------------
    ```

    This is an H2  
    -------------

* 글머리: 1~6까지만 지원

> `<h1>`부터 `<h6>`까지 제목을 표현할 수 있습니다.

```
# This is a H1
## This is a H2
### This is a H3
#### This is a H4
##### This is a H5
###### This is a H6
```
# This is a H1
## This is a H2
### This is a H3
#### This is a H4
##### This is a H5
###### This is a H6
####### This is a H7

## 인용문(BlockQuote)

`<blockquote>` 태그로 변환됨.

이메일에서 사용하는 `>` 블럭인용문자를 이용한다.

```
인용문(blockQuote)

> 남의 말이나 글에서 직접 또는 간접으로 따온 문장.
> _(네이버 국어 사전)_

BREAK!

> 인용문을 작성하세요!
>> 중첩된 인용문(nested blockquote)을 만들 수 있습니다.
>>> 중중첩된 인용문 1
>>> 중중첩된 인용문 2
>>> 중중첩된 인용문 3
```

인용문(blockQuote)

> 남의 말이나 글에서 직접 또는 간접으로 따온 문장.
> _(네이버 국어 사전)_

BREAK!

> 인용문을 작성하세요!
>> 중첩된 인용문(nested blockquote)을 만들 수 있습니다.
>>> 중중첩된 인용문 1
>>> 중중첩된 인용문 2
>>> 중중첩된 인용문 3


이 안에서는 다른 마크다운 요소를 포함할 수 있다.
```
> ### This is a H3
> * List
>   ```
>   code
>   ```
```

> ### This is a H3
> * List
>   ```
>   code
>   ```

## 코드블럭(Code Blocks)
빈칸 4개로 코드블럭 시작
```
    코드 블럭
```
    코드 블럭

## 목록(List)

`<ol>`, `<ul>` 목록 태그로 변환됩니다.

```
1. 순서가 필요한 목록
2. 순서가 필요한 목록
  - 순서가 필요하지 않은 목록(서브) 
  - 순서가 필요하지 않은 목록(서브) 
1. 순서가 필요한 목록
  1. 순서가 필요한 목록(서브)
  1. 순서가 필요한 목록(서브)
1. 순서가 필요한 목록

- 순서가 필요하지 않은 목록에 사용 가능한 기호
  - 대쉬(hyphen)
  * 별표(asterisks)
  + 더하기(plus sign)
```

1. 순서가 필요한 목록
1. 순서가 필요한 목록
  - 순서가 필요하지 않은 목록(서브) 
  - 순서가 필요하지 않은 목록(서브) 
1. 순서가 필요한 목록
  1. 순서가 필요한 목록(서브)
  1. 순서가 필요한 목록(서브)
1. 순서가 필요한 목록

- 순서가 필요하지 않은 목록에 사용 가능한 기호
  - 대쉬(hyphen)
  * 별표(asterisks)
  + 더하기(plus sign)

**현재까지는 어떤 번호를 입력해도 순서는 내림차순으로 정의된다.**
```
1. 첫번째
2. 세번째
3. 두번째
```
1. 첫번째
3. 세번째
2. 두번째

딱히 개선될 것 같지는 않다. 존 그루버가 신경안쓰고 있다고...

### ● 순서없는 목록(글머리 기호)
```
* 빨강
  * 녹색
    * 파랑

+ 빨강
  + 녹색
    + 파랑

- 빨강
  - 녹색
    - 파랑
```
* 빨강
  * 녹색
    * 파랑

+ 빨강
  + 녹색
    + 파랑

- 빨강
  - 녹색
    - 파랑

혼합해서 사용하는 것도 가능하다
```
* 1단계
    - 2단계
        + 3단계
            =4단계
```
* 1단계
    - 2단계
        + 3단계
            =4단계

## 코드(Code) 강조
`<pre>`, `<code>`로 변환됩니다.

숫자 1번 키 왼쪽에 있는 `(Grave)를 입력하세요

### 인라인(inline) 코드 강조

```
`background`혹은 `background-image` 속성으로 요소에 배경 이미지를 삽입할 수 있습니다.
```
`background`혹은 `background-image` 속성으로 요소에 배경 이미지를 삽입할 수 있습니다.

### 블록(block) 코드 강조

`를 3번 이상 입력하고 코드 종류도 적습니다.

````
```html
<a href="https://www.google.co.kr/" target="_blank">GOOGLE</a>
```

```css
.list > li {
  position: absolute;
  top: 40px;
}
```

```javascript
function func() {
  var a = 'AAA';
  return a;
}
```

```bash
$ vim ./~zshrc
```

```python
s = "Python syntax highlighting"
print s
```

```
No language indicated, so no syntax highlighting. 
But let's throw in a tag.
```
````

```html
<a href="https://www.google.co.kr/" target="_blank">GOOGLE</a>
```

```css
.list > li {
  position: absolute;
  top: 40px;
}
```

```javascript
function func() {
  var a = 'AAA';
  return a;
}
```

```bash
$ vim ./~zshrc
```

```python
s = "Python syntax highlighting"
print s
```

```
No language indicated, so no syntax highlighting. 
But let's throw in a tag.
```

## 표(Table)

`<table>` 태그로 변환됩니다.

헤더 셀을 구분할 때 3개 이상의 `-`(hyphen/dash) 기호가 필요합니다.

헤더 셀을 구분하면서 `:`(Colons) 기호로 셀(열/칸) 안에 내용을 정렬할 수 있습니다.

가장 좌측과 가장 우측에 있는 `|`(vertical bar) 기호는 생략 가능합니다.

```
| 값 | 의미 | 기본값 |
|---|:---:|---:|
| `static` | 유형(기준) 없음 / 배치 불가능 | `static` |
| `relative` | 요소 자신을 기준으로 배치 |  |
| `absolute` | 위치 상 부모(조상)요소를 기준으로 배치 |  |
| `fixed` | 브라우저 창을 기준으로 배치 |  |

값 | 의미 | 기본값
---|:---:|---:
`static` | 유형(기준) 없음 / 배치 불가능 | `static`
`relative` | 요소 **자신**을 기준으로 배치 |
`absolute` | 위치 상 **_부모_(조상)요소**를 기준으로 배치 |
`fixed` | **브라우저 창**을 기준으로 배치 |
```

| 값 | 의미 | 기본값 |
|---|:---:|---:|
| `static` | 유형(기준) 없음 / 배치 불가능 | `static` |
| `relative` | 요소 자신을 기준으로 배치 |  |
| `absolute` | 위치 상 부모(조상)요소를 기준으로 배치 |  |
| `fixed` | 브라우저 창을 기준으로 배치 |  |

값 | 의미 | 기본값
---|:---:|---:
`static` | 유형(기준) 없음 / 배치 불가능 | `static`
`relative` | 요소 **자신**을 기준으로 배치 |
`absolute` | 위치 상 **_부모_(조상)요소**를 기준으로 배치 |
`fixed` | **브라우저 창**을 기준으로 배치 |

## 수평선(Horizontal Rule)
아래 줄은 모두 수평선을 만든다. 마크다운 문서를 미리보기로 출력할 때 *페이지 나누기* 용도로 많이 사용한다.

각 기호를 3개 이상 입력.

```

***

* * *

*****

- - -

___

--------------------------------

```

***

* * *

*****

- - -
  
___

--------------------------------

## 줄바꿈(Line Breaks)

```
동해물과 백두산이 마르고 닳도록 
하느님이 보우하사 우리나라 만세   <!--띄어쓰기 2번-->
무궁화 삼천리 화려 강산<br>
대한 사람 대한으로 길이 보전하세
```

동해물과 백두산이 마르고 닳도록  
하느님이 보우하사 우리나라 만세  
무궁화 삼천리 화려 강산<br>
대한 사람 대한으로 길이 보전하세

> 일반 줄비꿈이 동작하지 않는 환경(설정 및 버전에 따라)의 경우, ‘2번의 띄어쓰기’나 <br>를 활용할 수 있습니다.

## 문자열 강조(Emphasis)

각각 `<em>`, `<strong>`, `<del>` 태그로 변환됩니다.  
밑줄은 `<u></u>` 태그로 변환됩니다.

```
*기울인 글씨1*
_기울인 글씨2_
**진한 글씨1**
__진한 글씨2__
**_이텔릭체_와 두껍게**
~밑줄~
~~취소선~~
```
*기울인 글씨1*  
_기울인 글씨2_  
**진한 글씨1**  
__진한 글씨2__  
**_이텔릭체_와 두껍게**  
~밑줄~  
~~취소선~~  

## 할일 관리(Task Lists)
체크박스를 표현하여 할일 관리를 할 수 있습니다. 표현하는 방식은 - [ ], - [x]로 사용합니다.
```
- [x] @mentions, #refs, [links](), **formatting**, and <del>tags</del> supported
- [x] 완료된 항목
- [ ] 미완료 항목
- [x] ~~삭제된 항목~~
```
- [x] @mentions, #refs, [links](), **formatting**, and ~~tags~~ supported
- [x] 완료된 항목
- [ ] 미완료 항목
- [x] ~~삭제된 항목~~

## 원시 HTML(Raw HTML)

마크다운 문법이 아닌 원시 HTML 문법을 사용할 수 있습니다.

```
<u>마크다운에서 지원하지 않는 기능</u>을 사용할 때 유용하며 대부분 잘 동작합니다.

<img width="150" src="http://www.gstatic.com/webp/gallery/4.jpg" alt="Prunus" title="A Wild Cherry (Prunus avium) in flower">

![Prunus](http://www.gstatic.com/webp/gallery/4.jpg)
```

<u>마크다운에서 지원하지 않는 기능</u>을 사용할 때 유용하며 대부분 잘 동작합니다.

<img width="150" src="http://www.gstatic.com/webp/gallery/4.jpg" alt="Prunus" title="A Wild Cherry (Prunus avium) in flower">

![Prunus](http://www.gstatic.com/webp/gallery/4.jpg)

## 링크(Links)

`<a>`로 변환됩니다.

```
[GOOGLE](https://google.com)  
[NAVER](https://naver.com "링크 설명(title)을 작성하세요.")  
[상대적 참조](../users/login)  
[Dribbble][Dribbble link]  
[GitHub][1]  

문서 안에서 [참조 링크]를 그대로 사용할 수도 있습니다.

다음과 같이 문서 내 일반 URL이나 꺾쇠 괄호(`< >`, Angle Brackets)안의 URL은 자동으로 링크를 사용합니다.
구글 홈페이지: https://google.com
네이버 홈페이지: <https://naver.com>

[Dribbble link]: https://dribbble.com
[1]: https://github.com
[참조 링크]: https://naver.com "네이버로 이동합니다!"
```

[GOOGLE](https://google.com)  
[NAVER](https://naver.com "링크 설명(title)을 작성하세요.")  
[상대적 참조](../users/login)  
[Dribbble][Dribbble link]  
[GitHub][1]  

문서 안에서 [참조 링크]를 그대로 사용할 수도 있습니다.

다음과 같이 문서 내 일반 URL이나 꺾쇠 괄호(`< >`, Angle Brackets)안의 URL은 자동으로 링크를 사용합니다.

구글 홈페이지: https://google.com  
네이버 홈페이지: <https://naver.com>  

[Dribbble link]: https://dribbble.com
[1]: https://github.com
[참조 링크]: https://naver.com "네이버로 이동합니다!"

## 이미지(Images)

`<img>`로 변환됩니다.  

링크과 비슷하지만 앞에 `!`가 붙습니다.

```
![대체 텍스트(alternative text)를 입력하세요!](http://www.gstatic.com/webp/gallery/5.jpg "링크 설명(title)을 작성하세요.")

![text](/path/to/img.jpg)

![석촌호수 러버덕][text]
![text](/path/to/img.jpg "Optional title")
```

![석촌호수 러버덕](http://cfile6.uf.tistory.com/image/2426E646543C9B4532C7B0)

![석촌호수 러버덕][text]

[text]:http://cfile6.uf.tistory.com/image/2426E646543C9B4532C7B0 "RubberDuck"

사이즈 조절 기능은 없기 때문에 `<img width="" height=""></img>`를 이용한다.

### 이미지에 링크
마크다운 이미지 코드를 링크 코드로 묶어 줍니다.
```
[![Vue](/images/vue.png)](https://kr.vuejs.org/)
```
[![Vue](/images/vue.png)](https://kr.vuejs.org/)

### 이미지 링크 고급
Markdown 문서로 웹링크에 이미지 삽입이 가능합니다. 
링크에 이미지를 합치면 아래와 같이 표시할 수 있습니다
```
[![the google logo][logo]][google]
```
위의 줄은 다음처럼 링크 정의와 함께 결합시킬 수 있습니다.

```
[logo]: http://www.google.com/images/logo.gif
[google]: http://www.google.com/ "click to visit Google.com"
```
[![the google logo][logo]][google]

[logo]: http://www.google.com/images/logo.gif

[google]: http://www.google.com/ "click to visit Google.com"

## 각주(Footnotes)
```
각주입니다 [^id]
[^id]: 각주에 대한 설명. 
```
각주입니다 [^id]  
[^id]: 각주에 대한 설명.

## 이모티콘 자동 완성(Emoji autocomplete)
:를 타이핑하면 이모티콘 추천 목록을 불러온다. :+1:

## 이스케이프 문자 표기(Escape)
이스케이프 문자는 `\`를 붙여 표기합니다.
```
\\      backslash
\`      backtick
\*      asterisk
\_      underscore
\{\}    curly braces
\[\]    square brackets
\(\)    parentheses
\#      hash mark
\+      plus sign
\-      minus sign (hyphen)
\.      dot
\!      exclamation
```
\\      backslash  
\`      backtick  
\*      asterisk  
\_      underscore  
\{\}    curly braces  
\[\]    square brackets  
\(\)    parentheses  
\#      hash mark  
\+      plus sign  
\-      minus sign (hyphen)  
\.      dot  
\!      exclamation  

****

# 마크다운 사용기
## 이지웍(WSYWIG) 에디터
우리가 흔하게 접하는 웹에서 사용되는 에디터(네이버, 다음, 구글 등)이 대부분 이지웍 에디터에 속하며 기본적으로 HTML을 이용하여 스타일을 적용하여  
문장을 꾸미는 형태를 취하게 된다. 그래서 하루패드와 같은 마크다운 에디터의 View 영역의 내용을 복사하여 붙여넣기를 하면 대체적으로 View영역에서 보이는 그대로 복사되는 편이다.  
다만, 붙여넣기 이후에 문장들을 수정하려고 할 때 문제가 되는데, 이는 스타일이 포함된 태그가 수정과정에서 변형되면서
전체적인 영향을 끼치는 탓이다. 티스토리 블로그에서는 쉽지 않고... 워드프레스의 경우에는 마크다운으로 작성된 포스트를 HTML로 변환해주는 기능을 활용하는 것이 좋다.  
결론은, **복사해서 붙여넣기하면 가급적이면 본문은 수정하지 않는 것이 좋다.**

## 깃헙Github, 비트버킷Bitbucket과 요비Yobi 등
최근 유행하는 협업개발플랫폼의 경우에는 마크다운을 변환하는 컨버터 기능을 기본탑재하고 있기 때문에 마크다운 문법으로
작성한 텍스트를 그대로 복사해서 붙여넣거나 업로드하는 것만으로 마크다운의 적용이 가능핟.

## MS워드 적용
View 영역의 항목을 그대로 붙여넣거나 HTML 내보내기 등으로 생성한 파일을 불러오는 형태로 사용가능핟. 적용한 헤더를 워드가 읽어드리면서 목차에
적용하기 때문에 이를 활용하면 목차까지도 손쉽게 적용이 가능해진다.

****
# 정리
마크다운은 기본문법만 알고 있다면 일반 텍스트편집기에서도 손쉽게 작성이 가능한 마크업언어다. 현재 다양한 도구와 플랫폼에서 지원하고 있기 때문에  
더욱 손쉽게 스타일적용된 문서를 작성할 수 있기 때문에 점점 널리 사용되고 있다.  
마크다운을 이해하고 사용하면서 쉽고 빠르게 스타일문서를 작성해보세요.  
저는 Dropbox 프로를 구매해서 집-랩탑-스마트폰에 각각 연동을 시켜서 사용하고 있습니다. 드롭박스에 저장된 마크다운 문서는 Dropbox 웹서비스 상에서
제공하기 때문에 웹상에서 바로 열람할 수도 있어 링크를 걸어서 다른 사람과 공유하는 형식으로 사용하고 있다.  
* 링크 예: [Markdown 설명](https://www.dropbox.com/s/1e7hbtd0yr0egft/20141021_markdown_use_tip.md?dl=0)

## ○ 참고문서
* [78 Tools for writing and previewing Markdown](http://mashable.com/2013/06/24/markdown-tools/)
* [John gruber 마크다운 번역](http://nolboo.github.io/blog/2013/09/07/john-gruber-markdown/)
* [깃허브 취향의 마크다운 번역](http://nolboo.github.io/blog/2014/03/25/github-flavored-markdown/)
* [허니몬의 마크다운 작성법](http://www.slideshare.net/ihoneymon/ss-40575068)