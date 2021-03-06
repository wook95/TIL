# DOM 과 virtualDOM

## 돔이란

브라우저의 렌더링 엔진은 HTML 문서를 파싱해, 브라우저가 이해할 수 있는 자료구조인 DOM을 만든다.  
DOM은 HTML 문서의 계층적 구조와 정보를 표현하고, 이것들을 제어할 수 있는 프로퍼티와 메소드를 제공하는 트리 자료구조이다.

## 돔 조작

돔을 삭제, 교체, 생성하면 리플로우와 리페인트가 발생한다. 이는 성능에 영향을 준다.  
따라서 DOM 조작은 성능 최적화를 위해 `주의`해야한다.

## 가상 돔

데이터가 변경되었을때 UI에서 변경된 부분을 빨리 찾기 위해 사용하는 도구.  
브라우저에서 돔을 변경하는것은 비교적 오래 걸리는 작업이다.(하나의 조작이 레이아웃의 변화, 트리의 변화, 렌더링을 일으킨다.)  
버추얼돔은 일종의 버퍼같은것이다.

1. 변화가 일어나면 버츄얼 돔에 적용시킨다.
2. 렌더링 되지 않기에 연산 비용이 적다.
3. 연산이 끝나고 최종적인 변화를 실제 DOM에 던져준다. 모든 변화를 묶어서.

직접 해도 되는 작업이지만, 일일히 하기보다 버츄얼돔을 만들어 추상화시켜서 자동화 시키고 컴포넌트들간 돔 조작 정보를 공유할 필요가 없기에 좋다.

<br>

참고

자바스크립트 딥다이브  
실전 리액트 프로그래밍  
https://velopert.com/3236
