## hook-form 적용기

일단 우리 회사에서는 E2E 테스트를 cypress를 사용하고 있다.

근데 웃긴게 cypress에서 타이핑이 돌아가면 validation이 돌아가지 않는 문제가 발생한다.

난 공식문서 그대로 register와 validate 등록을 했는데 왜 안되는걸까 고민을 했었는데 ~~_(사실 아직도 이유를 찾지는 못 한 상태)_~~

무튼 어찌저찌 해결은 하였기 때문에 일단 방법을 정리해보겠다.

### 발생한 문제

기존에 사용하던 input을 react-hook-form을 적용했더니 일반 dev 환경에서는 문제 없이 동작하였으나 cypress 테스트에서 `.type` 에 대한 validation check을 하지 못하는 문제가 발생 따라서 에러 메세지를 띄우는지 확인을 할 수가 없었다.

```tsx
import React, { useRef } from 'react';
import { useForm } from 'react-hook-form';

type Input = {
  username: string;
};

const App = () => {
  const { register, handleSubmit } = useForm<Input>({
    mode: 'onChange',
    reValidateMode: 'onChange',
  });

  const inputRef = useRef<HTMLInputElement | null>(null);

  return (
    <form>
      <input
        ref={(e) => {
          register(e);
          inputRef.current = e;
        }}
        name="username"
        type="text"
      />
      <button>submit</button>
    </form>
  );
};

export default App;
```

### 해결 방안

일단 ref와 register를 같이 하는 부분에서 잘못된 방법이 있었던것 같다. stackoverflow를 참고해서 위와같은 방법을 사용했으나 공식문서에서는 아래와 같이 사용하라고 적혀있다.

```tsx
import React, { useRef } from 'react';
import { useForm } from 'react-hook-form';

type Input = {
  username: string;
};

const App = () => {
  const { register, handleSubmit } = useForm<Input>({
    mode: 'onChange',
    reValidateMode: 'onChange',
  });

  const { ref, ...rest } = register('username');

  const inputRef = useRef<HTMLInputElement | null>(null);

  return (
    <form>
      <input
        ref={(e) => {
          ref(e);
          inputRef.current = e;
        }}
        name="username"
        type="text"
      />
      <button>submit</button>
    </form>
  );
};

export default App;
```

무튼 내가 선택한 해결방법은 이 방법은 아니였고 일단 form 객체를 따로 분리한 후에 register 함수 option에 넣어주었다.

```ts
// form.ts
export const form = {
  username: {
    name: 'username',
    label: 'Username',
    register: {
      validate: {
        ...validation,
      },
    },
  },
};
```

```tsx
// App.ts
import React, { useRef } from 'react';
import { useForm } from 'react-hook-form';

import { form } from './form';

type Input = {
  username: string;
};

const App = () => {
  const { register, handleSubmit } = useForm<Input>({
    mode: 'onChange',
    reValidateMode: 'onChange',
  });

  const inputRef = useRef<HTMLInputElement | null>(null);

  return (
    <form>
      <input
        ref={(e) => {
          register(e, form.username.register);
          inputRef.current = e;
        }}
        name="username"
        type="text"
      />
      <button>submit</button>
    </form>
  );
};

export default App;
```

일단 문제를 해결하였지만 정확한 원인을 찾지는 못 했다.
주말에 좀 더 찾아보고 업데이트 할 예정 (근데 hook form의 버전에 따라서 공식문서에서 제시한 방법이 안 돌아갈 수도 있는 것 같다.)

공식문서에 나와 있는 방법을 레퍼런스로 다시 리팩토링 해보는것도 좋을 거 같다.
