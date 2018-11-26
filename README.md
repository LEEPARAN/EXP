# Coding Experience value

## 개발하면서 겪은 유용한 경험들을 규칙에 얽매이지 않고 편하게 적어내는 곳

### 1. ios에서 video 태그가 정상 동작하도록 구현
작업 중 영상이 보이도록 작업을 진행해달라고 해서 pc버전과 내가 가지고 있는 android 폰으로 확인하였는데 이상이 없었으나
회사 직원이 가지고 있는 ios 폰으로 확인을 했더니 영상이 나오지가 않았다. 그래서 이를 해결하기 위해 구글링을 열심히
하였더니 stack overflow에서 나와 같은 고민에 대한 답으로 video 태그 속성에 controls 만 적지말고 true와 같은 속성 값을 
적어야된다고 하였다. ~~그래서 controls="true"를 하였으나 별 도움은 되지 않았다.~~
그러고나서 source에 어차피 여러가지 파일 형식으로 올리면 알아서 되는걸 보여주니까 소스 추가해서 더 다양한 영상을
넣어보자는 생각으로 mov 파일 형식을 올렸더니 동작은 하나 시작 이미지가 android와 달리 깨져보였다.
그래서 이부분은 video 태그의 poster 속성을 활용하여 해결하였다.

```
<video controls="true" poster="/images/test1.jpg">
  <source src="/video/test2.mp4"></source>
  <source src="/video/test2.mov"></source>
</video>
```
