## react-hook-form 적용 전 조사(1)

### 특징

- 타입스크립트 적용이 쉽다.
- 유효성 검사를 위한 자체 기능이 존재한다. yup도 사용 가능
- 폼을 위한 필드, 컴포넌트가 따로 필요 없다. 그냥 HTML 사용
- 타 라이브러리에 비해 성능이 우수
- Hooks
- 리랜더링 분리가 쉽다. 렌더링 최소화가 가능하다.
- 마운트 속도가 빠르다.

### Install

`$ yarn add react-hook-form`

### Get started

#### 기본적인 코드 형태

```ts
import React from 'react';
import { useForm } from 'react-hook-form';

// ref 관리
type Inputs = {
  example: string;
  exampleRequired: string;
};

export default function App() {
  const { register, handleSubmit, watch, errors } = useForm<Inputs>();
  const onSubmit = (data) => console.log(data);
  console.log(watch('example'));
  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <input name="example" defaultValue="test" ref={register} />
      <input name="exampleRequired" ref={register({ required: true })} />
      {errors.exampleRequired && <span>This field is required</span>}
      <input type="submit" />
    </form>
  );
}
```

1. **register**
   비제어 컴포넌트를 Hook 과 연결하여 값이 검사될 수 있도록 만들고 폼을 제출할 때 한꺼번에 모아지도록 하는 것이다.

`ref = {register({옵션})}`

옵션에 **required, maxLength, minLength, max, min, pattern, validate** 을 추가할 수 있다.

2. **name**
   각 필드의 등록 과정의 key로 사용하기 위해 name 속성이 반드시 필요하다.

3. **error**
   validation error가 발생하면 error 객체를 제공한다.

4. **Ts**
   React Hook Form은 타입스크립트로 만들어져, 폼 내 값 타입을 FormData 로 설정할 수 있다.

5. **watch**
   deps에 name값을 넣어줘서 변화 감지

### 예시 코드 확인

[링크](https://github.com/react-hook-form/react-hook-form/tree/master/examples)
