---
title: "지킬(Jekyll) 깃허브 블로그에 폰트 적용하는 법"
date: 2019-10-29T00:10:00-09:00
categories: 
  - blogging
tags:
  - font
  - 폰트
  - Jekyll
---

minimal-mistakes 테마 기준 "D2Coding" Font 적용방법 4단계

```css
\_sass\minimal-mistakes\_variables.scss 에

$serif: "D2Coding" !default;  //"D2Coding ligature"도 가능
$sans-serif: "D2Coding" !default;
$monospace: "D2Coding" !default;

로 내용일부수정
```

```css
\assets\css\main.scss에

@font-face {
    font-family: "D2Coding";
    src: url("/assets/fonts/D2Coding-Ver1.3.2-20180524.ttf") format('truetype');
    font-weight: normal;
    font-style: normal;
}
@font-face {
    font-family: "D2Coding ligature";
    src: url("/assets/fonts/D2Coding-Ver1.3.2-20180524-ligature.ttf") format('truetype');
    font-weight: normal;
    font-style: normal;
}

이 부분 추가(ligature버전은 선택)
```

src:url(경로) 부분의 경로에 fonts폴더 만들고 [폰트ttf파일] 넣기

깃 add, commit, push

끝

[폰트ttf파일]:  https://github.com/naver/d2codingfont