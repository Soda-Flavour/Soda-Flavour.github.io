---
title: Kata - A Chain adding function(문제풀이)
description: A Chain adding function
categories:
  - Kata
tags:
---

# 알아야 할 내용

1. '(소괄호)'의 쓰임에 대해 알아야 한다.
2. 원시값과 함수의 동작에 대해 알아야한다.

# 문제

- (5kyu) - A Chain adding function

```javascript
add(1)(2)(3); // 6
add(1)(2)(3)(4); // 10
add(1)(2)(3)(4)(5); // 15
```

# 알아보기

### 자바스크립트에서의 소괄호

자바스크립트에서 소괄호`()`는 두가지의 기능을 한다.

1. 그룹핑 연산자

그룹핑 연산자는 소괄호의 평가 결과를 반환한다.

```javascript
let a = (1 + 3);
```

2. 함수 실행

함수의 끝에 붙는다면 해당 함수를 실행하여 반환한다.
즉, 함수에서 소괄호는 함수를 실행하겠다란 뜻이 된다.

```javascript
let fn = function(){
  return 'Hi';
}();

console.log(fn);  // Hi
```



### 윈시값의 출력

`valueOf()`메서드는 특정 객체의 원시 값을 반환한다.
원시값을 출력은 보통 자동으로 이루어 지기 때문에 호출할 일이 드믈다.

# 해답


`add(1)` 실행 후, `add(2)`가 동작하려면, add의 반환이 값을 받는 함수여야 한다.
함수가 연결적으로 체인이 되게 하기위해 재귀 호출을 한다.

```javascript
function add(n){
  return function(x){
    return add(n+x);
  }
}

add(1)(2); // 결과값 : [Function]

```

결과값이 함수객체인 이유는 우리가 보통 변수에 값을 넣어 선언후 호출하면
자동으로 프리미티브값(원시값)이 출력되게된다.

```javascript
let num = 123;

console.log(hi);  //결과값 123;
```

하지만 `add` 함수는 마지막에 함수 호출 소괄호를 마친 후, 전달할 값을 모르기 때문에 함수 객체를 반환한다.
따라서 함수 호출이 아닐시(끝날때), 값을 반환할 수 있도록 valueOf()값을 설정해주면된다.


```javascript
function add(n){
  let sum = function(x){
    return add(n+x);
  }
  sum.valueOf = function(){
    return n;
  }
  return sum;
}
```


# 참고
> [MDN - valueOf()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/valueOf)

> [MDN - 식 및 연산자](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators)
