# 넥스트

버셀에서 만든 리액트 기반 프레임워크

### SPA의 단점

1. 모든 자바스크립트 코드를 불러와야해서 처음 페이지 불러오는 시간이 길다.
2. SEO에 좋지 않음.

### SSR의 단점

1. SSR은 페이지 이동시 새로운 html을 요청하기에 페이지 깜빡임 존재
2. 페이지 이동시 템플릿을 중복해서 로딩
3. 서버에 부담을 주기에 성능상 약간 좋지 않음

**넥스트**는 위와같은 단점을 해결하기 위해 리액트-spa-에 SSR기능을 더해 장점들을 가진다.

<br>

## 특징

1. 사전 렌더링 및 SSR
   - 빌드 시 만든 모든 페이지를 미리 렌더링한다. 서버의 데이터를 필요로 한다면 오청 시 SSR로 HTML을 생성한다.
2. 자동 코드 분할
   - 불필요한 코드가 페이지에 로드되지 않는다. 코드의 모든 가져오기가 번들로 묶이기 때문
3. 설정 필요 없음
   - 웹팩, 바벨 설정 되어 있음
4. 파일 기반 네비게이션
   - 폴더의 경로에 따라 페이지의 경로 설정 가능
5. styled-jsx 지원
   - 자체 CSS-in-JS 지원
6. hot code reloaing
   - 개발 환경에서 코드 변경이 될 때 자동 로드

<br>

## 프로젝트 시작

1. CNA  
   `npx create-next-app`
2. 수동 설치
   - 1. `yarn add next react react-dom`
   - 2. package.json에 scripts 바꿔주기

<br>

## 기본 기능

<br>

### 라우팅

page 폴더 안에 넣어주는 컴포넌트 파일 이름들이 그대로 경로가 된다.

> pages/index.jsx --> '/'  
> pages/tomato.jsx --> '/tomato'  
> pages/vegetable/[name].jsx --> '/vegetable/\*'

동적라우팅을 할 경우, useRouter로 router객체를 확인해봤을 때 pathname 프로퍼티의 값은 아래와 같은 객체가 된다.
`{ []를 이용해 지어준 파일 이름: 주소창에 친 pathname } `

<br>

### 주소 이동

1. Link 컴포넌트

```jsx
  href: 이동할 경로, url
  as?: 브라우저의 url에 표시될 값
  replace?: boolean으로 history 스택에 url추가 없이 현 상태를 변경한다
  scroll?: boolean으로 스크롤을 맨 위로 올릴지 설정
  shallow?: boolean으로 서버에서 데이터 불러오는 작업을 스킵할때 사용
  passHref?: boolean으로 자식에게 href전달
  prefetch?: boolean으로 백그라운드에서 페이지를 미리 가져온다.
```

2.  라우터 객체  
    `router.push()`  
    `router.replace()`  
    `router.back()`

<br>

### 정적 파일 사용

/public 아래에 놓은 파일, 폴더를 부를 수 있다.
`/public/cheese.jpg`를 `<img src="/cheese" alt="치즈" />`로 부를 수 있다.

<br>

### 서버에서 데이터 불러오기

넥스트엔 사전렌더링 방법이 두가지 있다.  
**정적 생성:** 빌드시 html을 만들어 놓고, 요청할때 준다.  
**정적 생성:** 페이지 요청하면 SSR을 통해 HTML을 준다.

1. **getServerSideProps**  
   페이지의 데이터(props)를 서버에서 제공받는 기본 API이다. 페이지 요청시 마다 실행이 되며 해당 함수에서 페이지로 전달한 데이터를 서버에서 렌더링한다. 서버에서 실행이 된다.

   사용 시 컴포넌트의 prop로 데이터를 넘겨주게 되고, getServerSideProps 라는 이름 그대로 써야하는 이 함수는 export를 해줘야 하고, return은 객체안에 props라는 프로퍼티 명으로 넘겨줄 값을 적어준다.

2. **getStaticProps**  
   1번 함수와 다르게 요청시마다가 아닌, 빌드시에 데이터를 불러오고 결과를 json으로 저장하 논 후 계속 사용한다.  
   만약 props 데이터 변경을 원할 땐 return하는 객체의 프로퍼티로 revalidate: number를 주면 된다. number는 초 단위로, 해당 시간마다 데이터가 갱신된다.

   동적 라우팅 시 1번 함수에선 query를 활용했던것과 다르게 `getStaticPath` 함수를 통해 경로를 지정해주고, 여기서 나온 params를 통해 pathname을 불러온다.

3. getInitialProps  
   9.3 버전 이전에 위의 두 함수의 역할을 해주던 함수
   컴포넌트 함수에 프로퍼티로 getInitialProps를 추가하는 방식으로 사용, return에선 props 속성 없이 리턴, 초기 랜더링 시엔 서버에서 데이터를 불러오고 클라이언트측 네비게이션 사용 시 클라이언트에서 데이터를 불러온다.

<br>

### styled-jsx

```jsx
import css from 'styled-jsx/css';

const style = css`
  h2{
    margin-left:20px;
  }
`
const username = ()=>{
  return(
    <h2>wook</h2>
    <style jsx>{style}</style>
  )
}
```

- 네스팅 불가능

<br>

### 공통 페이지

모두 pages 안에 존재한다.

1. \_app.jsx

- 모든 페이지의 공통 페이지 역할을 한다.
- 페이지들의 공통된 레이아웃
- 글로벌 CSS
- 추가 데이터의 주입

```jsx
const MyApp = ({ Component, pageProps }) => {
  return (
    <>
      <Component {...pageProps} />
      <style jsx global>{`
        body {
          margin: 0;
        }
      `}</style>
    </>
  );
};
```

Component는 불러오는 페이지, props는 getServerSideProps등으로 넘겨주는 props
navbar와 같은 공통컴포넌트를 ` <Component {...pageProps} />` 위쪽에 넣어주면 모든 페이지에서 navbar를 볼 수 있다.

2. \_document.jsx

공통 html 문서를 편집할 수 있다.
폰트 link를 넣어주고, meta태그를 편집할 수 있다.

3. 에러페이지

404는 404.jsx로 500은 \_error.jsx로 에러 페이지 커스텀이 가능하다.

출처: 클론코딩으로 시작하는 Next.js 이창주 저
