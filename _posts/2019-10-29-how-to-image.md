---
title: "지킬(Jekyll) 깃허브 블로그의 이미지 첨부하는 법"
date: 2019-10-29T00:10:00-09:00
categories: 
  - blogging
tags:
  - image
  - 이미지
  - Jekyll
---

.github.io폴더 아래 assets/images폴더 아래에 이미지파일을 넣었다면    
아래와 같은 태그를 이미지가 들어가는 곳에 적는다. width와 height로 크기를 조절할 수 있다.    

```html
<img src="/assets/images/8.png" width="90%" height="90%" title="제목" alt="아무거나"/> 
```

또는

```md
![제목](/assets/images/8.png)
```

typora를 사용할 경우 각 post의 맨위 yaml공간에 

```
typora-root-url: ../
```

를 붙인다.