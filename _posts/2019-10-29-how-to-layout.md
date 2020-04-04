---
title: "지킬(Jekyll) 깃허브 블로그에 레이아웃 수정하는 법"
date: 2019-10-29T00:10:00-09:00
categories: 
  - blogging
tags:
  - width
  - 너비
  - Jekyll

---

minimal-mistakes 테마 기준 

```css
\_sass\minimal-mistakes\_variables.scss 에

$right-sidebar-width-narrow: 50px !default;
$right-sidebar-width: 75px !default;
$right-sidebar-width-wide: 100px !default;

이 부분 수정하여 너비 넓힘
```

utterance 댓글창의 너비 늘리는 법(기존엔 75%너비로 좁아보인다.)

```css
\assets\css\main.scss에

.utterances {
    max-width: 100% !important;
}

위 부분을 붙여 넣는다.
```

