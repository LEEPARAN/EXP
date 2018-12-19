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

### 2. Object.keys(), eval()
```
var obj = {
  key1: "value1",
  key2: "value2",
  key3: "value3"
}
```

예시로 위와 같은 코드를 뿌려줘야되는 상황이라 object의 length 만큼 for문을 돌려서 호출하려고 아래와 같은 코드를 작성하였다.

```
for(var i = 1; i <= obj.length; i++) {
  console.log(obj.key + i);
}
```

여기서 obj.length는 undefined가 출력되어 for문 자체가 실행도 되지않는다.
그래서 구글링을 해본 결과 object의 자식의 길이 체크를 Object.keys() 메소드에서 할 수 있다고 하였고 정상적으로 동작하였다.

```
for(var i = 1; i <= Object.keys(obj).length; i++) {
  console.log(obj.key + i);
}
```

이젠 되겠지하고 하는데 뭐 하면서 안될거라고 생각하긴 했는데 obj.key + i 한다고 해서 역시나 obj.key1, 2, 3이 되지는 않았다.
그래서 이것도 구글링해서 나온 결과 eval()이라는 함수안에 값을 넣어주면 String 형태의 js코드를 동적으로 이용할 수 있다.
MDN에서 eval() 함수를 속도나 보안 등의 이유로 비권장하는데 일단 작업하는데 시간이 없어서 대안에 하는 코드를 읽어보지 못하였는데
여유가 생긴다면 확인해보고 수정작업을 해야될 것 같다. 아무튼 아래와 같은 코드를 작성하였다.

```
for(var i = 1; i <= Object.keys(obj).length; i++) {
  console.log(eval("obj.key" + i)); // 출력: value1, value2, value3
}
```

### 3. for in 문
이 코드는 존재에 대해 몰랐던 것은 절대 아닌데 사용할 일이 없다가 실무에서 처음 사용하게 되어 적어본다.
객체의 key와 value 값을 모두 뽑아내고 싶을 때 아주 유용한 코드이다. 졸려서 별 다른 사족은 없다.
```
var object1 = {a: 1, b: 2, c: 3};
for(key in object1) {
  console.log("key": key); // 출력: a, b, c
  console.log("object1[key]': objecct1[key]); // 출력: 1, 2, 3
}
```
