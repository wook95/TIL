## 이벤트

[https://www.w3schools.com/howto/howto_js_dropdown.asp]

를 보다가 발견한 event.target.matches('.dropbtn')를 알기 위해 공부한 내용:

1. 이벤트 버블링, 이벤트 캡쳐
    - 이벤트 버블링 : 특정 요소에서 이벤트 발생시, 상위의 요소로 전파, 기본속성
    - 이벤트 캡쳐 : 버블링의 반대, 상위요소에서 하위요소로 이벤트 전파, capture: true 설정
    - event.stopPropagation()를 쓰면 전파되지 않는다

2. 이벤트 위임

   - 부모에서 자식들의 이벤트를 다룬다.
   - 버블링과 캡쳐의 전파되는 속성을 사용해 반복을 줄여준다.
   - ul - li -a 로 내려가는 구조에서 a태그가 무한히 많아질때 모두 이벤트를 등록해 줄수 없는 상황에서 버블링을 활용, ul태그에 이벤트를 걸어주면 모든 a태그에 적용

3. event.target

   - 이벤트 버블링의 가장 마지막 요소 리턴

4. event.currentTarget

   - 이벤트가 바인딩 된 요소,,, 바로 그 요소를 리턴

5. event.target.matches, event.target.closest

```html
<button type="button" class="dropdown" onclick="dropdownFunction()">
        <i class="bi bi-three-dots"></i>
</button>
```

```javascript
window.onclick = function(event) {
    if (!event.target.matches('.dropdown')) {
      let dropdowns = document.getElementsByClassName("dropdown-content");
      let i;
      for (i = 0; i < dropdowns.length; i++) {
        let openDropdown = dropdowns[i];
        if (openDropdown.classList.contains('show')) {
          openDropdown.classList.remove('show');
        }
      }
    }
  }
```

- 버튼태그에 match가 적용되어 그 자식은 i태그는 적용이 안된다
- 이벤트 위임을 위해 event.target.closet를 쓰면 해당 요소나 부모에 해당 선택자가 있는지 체크

w3c에서본 예제 코드가 실행이 안되었던 이유 : 내 코드에선 자식이 있엇는데 w3c코드에선 자식이 없었다 → 자식에서도 기능을 할 수 있도록 event.taget.matches→ event.target.closet로변경

<hr />

### 추가   

- 이벤트 리스너를 걸어준다고 해서, 타겟에서 바로 이벤트가 발생하는것이 아니다.   
- 이벤트 발생을 위해 캡쳐링, 타겟에서의 이벤트 리스너의 콜백 실행, 버블링 단계가 차례로 일어난다.   
- 따라서 캡쳐링 단계에서 이벤트를 발생시키기 위한 특수한 옵션도 존재하고, 이벤트 위임을 통해 부모에서 이벤트를 잡아줄 수도 있고, 버블링이 되지 않도록 막아줄 수도 있다.   
