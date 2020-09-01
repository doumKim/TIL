# SSR, CSR

이번 포스팅에서는 서버 사이드 렌더링, 클라이언트 사이드 렌더링에 대해서 정리를 해보려고 한다.

![](https://media.vlpt.us/images/kdo0129/post/9a450441-c2a2-407c-924b-13dd8aa219ba/ssrCsr.png)

## Server-side Rendering

SSR은 서버에서 유저에게 보여줄 페이지를 모두 구성하여 유저에게 페이지를 보여주는 방식이다.

클라이언트에게 요청을 받으면 각 요청에 맞는 html 파일을 내려줘서 상황에 맞는 화면을 보여준다.

즉, 서버에서 렌더링을 작업하는 방식이다.

![](https://images.velog.io/images/kdo0129/post/14753408-aa2e-4eed-948f-4b6bcef026b5/image.png)

_[그림 출처 - The Benefits of Server Side Rendering Over Client Side Rendering](https://medium.com/walmartglobaltech/the-benefits-of-server-side-rendering-over-client-side-rendering-5d07ff2cefe8)_

### 장점

서버를 이용해 페이지를 구성하여 사용자는 빠른 초기 응답을 경험할 수 있다.

또한 서버 쪽에서 이미 완성된 html 파일을 보내주기에 SEO 적용이 용이하다는 장점이 있다.

### 단점

단점으로는 모든 요청에 대해 필요한 부분을 수정하는게 아닌 새로운 html 페이지를 내려주기 때문에 속도 저하나 새로고침이 발생한다.

또한 화면에 html 요소를 다 그려줬지만 js가 다 받아지지 않아 제대로 동작이 되지 않는 경우도 있다.

즉, 사용자 경험을 좋지 않게 만든다.

---

## 웹의 발전

![](https://images.velog.io/images/kdo0129/post/eb3fb7e3-2bb0-463b-b0bb-71867c064a9f/image.png)

[참조 - The Evolution of the Web](https://evolutionofweb.appspot.com/#/evolution/night)

웹의 성능 발전에 따라 웹에서 구현하는 기능이 많아지고 자연스럽게 서버에 대한 요청은 많아졌다.

즉, static한 정보만을 보여주는 기존의 역할을 넘어 유저와 자연스럽게 interation이 가능해져야 했다.

또한 많은 요청을 받은 server는 당연히 부하가 커지게 되고 위에서 말한 사용자 경험을 안좋게 만드는 단점들도 부각이 되었다.

ajax라는 기술이 나오고 새로 html을 받아 그리는게 아닌 우리가 원하는 일부분만을 새로 바꿔주는게 가능해졌다.

그렇게 생긴 개념이 SPA이다. url이 바뀌더라도 html을 다시 받아서 그리고 싶지 않은 것이다.

이 말이 무엇이냐? 서버에서 렌더링을 하지 않고 클라이언트 측에서 알아서 렌더링을 하겠다는 것이다.

그럼 CSR에 대해서 알아보자.

---

## Client-side Rendering

CSR은 클라이언트 측에서 HTML을 반환한 후에 script가 동작하면서 데이터만을 주고 받아 클라이언트에서 렌더링을 진행하는 것이다.

쉽게 설명을 하자면 클라이언트에서 요청이 오면 서버는 완성된 HTML을 보내주는게 아닌 스크립트 링크가 걸린 HTML 파일을 응답으로 보내준다.

그러면 클라이언트는 자바스크립트를 다운 받고 실행하고 화면에 DOM을 그려준다.

즉, 클라이언트 쪽에서 렌더링을 하는 것이다.

![](https://images.velog.io/images/kdo0129/post/3edb3957-d148-4eca-8d12-e796ae42b3cb/image.png)

_[그림 출처 - The Benefits of Server Side Rendering Over Client Side Rendering](https://medium.com/walmartglobaltech/the-benefits-of-server-side-rendering-over-client-side-rendering-5d07ff2cefe8)_

### 장점

그러면 SSR과 렌더링 방식이 다르다는건 알겠는데 CSR의 장점은 무엇일까?

가장 큰 장점이라면 CSR은 사용자의 action에 따라 필요한 부분만 수정을 해주기 때문에 SSR 대비 조금 더 빠른 상호작용이 가능하다.

또한 SPA를 가능하게 만들어 주기 때문에 자연스러운 사용자 경험과 서버의 부하를 덜어주고 컴포넌트별 개발을 용이하게 만들어주는 등의 장점이 있다.

### 단점

그러면 무조건 SSR보다 CSR을 적용하는게 좋은건가?

**당연히 그렇지 않다.**

위에서 말한 것처럼 번들링된 자바스크립트 파일을 받아서 렌더링을 한다.

만약 application의 규모가 커진다면 번들링 파일도 덩달아 커지는 현상이 생긴다.

사용자 경험을 향상을 위해 CSR을 사용했다가 오히려 **초기 로딩이 길어져 사용자 경험이 나빠지는 현상**을 경험할 수 있다.

아래 그림은 초기 로딩화면을 시간별로 캡쳐한 스크린샷이다. CSR 방식의 초기 로딩이 오래 걸린다는걸 직접 보여준다.

![](https://images.velog.io/images/kdo0129/post/7e6a6ea3-8d3a-4a11-9e0f-9256d979d54d/image.png)

_[그림 출처 - The Benefits of Server Side Rendering Over Client Side Rendering](https://medium.com/walmartglobaltech/the-benefits-of-server-side-rendering-over-client-side-rendering-5d07ff2cefe8)_

또한 서버에서 완성된 HTML을 보내주는게 아닌 클라이언트에서 렌더링을 하기 때문에 **검색엔진최적화 (SEO)**에서 어려움을 겪는다.

---

## 정리

정리를 하자면 어떠한 방식을 사용해도 트레이드 오프는 존재한다.

상황에 맞는 적절한 방식을 선택하는게 중요하다. 이런게 어렵다면 아래를 참고하자.

react 라이브러리에서는 next.js라는 프레임워크를 사용하여 2가지 렌더링 방식을 적절히 상황에 맞게 적용을 하여 개발자에게 좀 더 쉽고 편한 선택지를 제시해준다.

![](https://images.velog.io/images/kdo0129/post/06275ff4-f52e-4055-bb9e-d576e424839f/image.png)

> Next.js gives you the best developer experience with all the features you need for production: hybrid static & server rendering, TypeScript support, smart bundling, route pre-fetching, and more. No config needed.

[next.js 공식 페이지](https://nextjs.org/)

### 마치며..

이번에 SSR, CSR에 대해서 처음 공부하였기 때문에 위에서 설명한 내용 중에 틀린 내용이 엄~~~청 많을 것이다.

이번 포스팅을 작성하면서 렌더링 방식에 대해서 알아가는 것도 좋았지만 항상 생각 중이였던 next.js를 사용하기 전에 프레임워크의 등장 배경과 왜 사용하는지에 대해서 알게 된 점이 만족스럽다.

물론 아직도 렌더링 방식에 대해서 100% 올바르게 이해한 것은 아니지만 그래도 나쁘지 않은 시도였고 혹시나 이 글을 읽고 틀린 점이 있다면 댓글로 지적 부탁 드린다.
