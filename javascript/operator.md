# ??

**nullish 병합연산자**  
널 병합 연산자 (??) 는 왼쪽 피연산자가 null 또는 undefined일 때 오른쪽 피연산자를 반환하고, 그렇지 않으면 왼쪽 피연산자를 반환하는 논리 연산자

a ?? b  
a가 null, undefined 둘다 아니면 a  
a가 null, undefined라면 b

```jsx
a ?? b === (a !== null && a !== undefined) ? a : b;
```

단축평과들과 동시에 사용하면 에러가 발생하며, ()로 감싸줄 경우 가능하다.  
단축평가 `||`와도 비슷하게 왼쪽식에서 null,undefined가 아닌것이 판명나면 오른쪽 식은 평가하지 않는다.  
단 `||`의 경우 truthy한 값에 따라 판단하고 `??`는 null,undefined가 아닌경우를 판단하는것이 중요한 차이

<br>

# ?.

**옵셔널 체이닝**

. 과는 다르게 참조하는 객체가 undefined,null 이라면 에러를 발생시키지 않고 undefined로 취급한다.

```jsx
obj.first?.second === obj.first && obj.first.second;
```

<br>

# ~

**tilde 연산자**

비트 연산자로 not에 해당하는 연산을 할 수 있다.

응용으로 `~`를 두번 사용한 `~~`를 이용해 Math.floor와 비슷한 효과를 낼 수 있지만 완전히 동일하진 않다.

```jsx
~5.5; // => -6
~-6; // => 5
~~5.5; // => 5  (same as Math.trunc(5.5) and Math.floor(5.5))
~~-5.5; // => -5 (same as Math.trunc(-5.5) but NOT the same as Math.floor(-5.5), which would give -6 )
```

<br>

참고한곳  
[mdn](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing_operator)
