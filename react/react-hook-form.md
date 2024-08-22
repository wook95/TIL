# React hook form

### 컨트롤드 인풋과 언컨트롤드 인풋

`Controlled` : 리액트에서 인풋을 사용할 때 value와 onChange를 바인딩 한 뒤 직접 컨트롤

`UnControlled` : Dom을 통해 직접 매핑

컨트롤드 인풋을 사용할 때엔 state가 바뀜에 따라 re-render가 빈번하게 일어난다.

하지만 유효성 검사를 하거나 조금이라도 조작이 필요한 경우 컨트롤드 인풋을 사용하게 된다.

특정 상황에선 state-co-location ([참고자료](https://kentcdodds.com/blog/state-colocation-will-make-your-react-app-faster)) 등을 통해 최적화 할 수 있지만, 모두 그렇진 않다.

따라서 react-hook-form 사용 시 state를 줄여 조금 더 편하게 쉽게 최적화된 인풋 구현이 가능했다.

<br />

### re-render 조건

1. state 변경
2. props의 업데이트
3. 부모 컴포넌트의 rerender

<br />

### 사용

```tsx

import { useState } from "react";
import { FieldValue, useForm } from "react-hook-form";

type FormData = {
  answer: string;
};

function App() {
  const [question, setQuestion] = useState("바나나");
  const [result, setResult] = useState("");
  const {
    register,
    handleSubmit
    reset,
    formState: { errors },
  } = useForm<FormData>();


  const judgeAnswer = (data: FieldValue<FormData>) => {
    const answer = data.answer;
    const result = question.slice(-1) === answer.slice(0, 1) ? "정답" : "땡";
    setResult(result);
    setQuestion(answer);
    reset();
  };

  return (
    <>
      <p>{question}</p>

      <form onSubmit={handleSubmit(judgeAnswer)}>
        <input
          {...register("answer", {
            required: "한글 또는 영어을 입력해주세요",
            pattern: /^[a-zA-Z가-힣]+$/,
          })}
        />
        <button>입력</button>
      </form>

      <p>{errors.answer?.message}</p>
      <p>{result}</p>
    </>
  );
}

export default App;

```

### 후기

전체적인 사용법은 이전에 사용했던 폼 라이브러리와 비슷했다.  
defaultValue 설정, 유효성검사 등 기본적인 부분 모두 지원하고, Controlled Input용으로도 지원하는 API가 있었다.

앵귤러 사용 시에 자연스럽게 사용했던 폼 기능을 리액트에서 사용하고 싶어 찾아보았는데 .. 적합한 기술은 있을진 몰라도 안되는건 없는걸 한번 더 체감했다.

https://react-hook-form.com/
