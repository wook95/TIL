# 포탈

> 포탈은 부모 컴포넌트 DOM 계층 구조 바깥에 있는 DOM 노드로 자식을 렌더링한다.

출처 : 리액트 공식문서

## 개요

리액트로 랜더링 되는 index.html의 `<div id="root"></div>` 말고 다른곳에 렌더링 될 수 있도록 하는 역할이다.

모달 컴포넌트를 만들때 모달이 강조 될 수 있도록 배경색이 어두워질수 있도록 구현할때 overflow: hidden, z-index등을 신경쓰지 않도록 도와준다. 호버 카드나 툴팁도 그 예시이다...!

추가로 공식 문서에서는 이벤트 버블링에 대해서도 설명하고 있다.  
(버블링은 물에 있는 거품처럼 이벤트 전파가 상위 노드로 가는것)

portal은 dom트리 어디에 있건 일반적인 react 자식처럼 동작한다.
돔 트리에서는 형제 요소라고 해도 react 트리에 포함된 상위로 전파된다. context와 같은 기능도 정상 동작한다.

조금 더 풀어서 설명하면, 포탈 컴포넌트로 감싸진 컴포넌트가 렌더링 되는 DOM트리가 어디에 있건 상관 없이 해당 jsx,tsx파일에서 가지는 계층 구조에 따라 이벤트 전파가 가능하다는 뜻!

## 구제척인 사용법

1. `index.html`에 렌더링 될 돔을 설정

   ```jsx
   ...
    <body>
    <div id="root"></div>
    <div id="modal"></div>
   </body>
   ...
   ```

2. Portal.js 컴포넌트 작성

   ```jsx
   import reactDom from 'react-dom';

   function Portal({ children }) {
     const node = document.getElementById('modal');
     return reactDom.createPortal(children, node);
   }

   export default Portal;
   ```

3. 실제 사용시에 포탈 컴포넌트로 감싸준다.

   ```jsx
   function Practice() {
     const [isModalOpen, setIsModalOpen] = useState(false);
     return (
       <div>
         <button type='button' onClick={() => setIsModalOpen(true)}>
           모달 여는 버튼
         </button>
         {isModalOpen && (
           <Portal>
             <Modal message='메세지' onClose={() => setIsModalOpen(false)} />
           </Portal>
         )}
       </div>
     );
   }
   ```
