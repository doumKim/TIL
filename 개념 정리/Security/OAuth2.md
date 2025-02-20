# OAuth

## 배경

OAuth가 등장한 이유에 대해서 살펴보자면 다음과 같다.

우리가 만약에 어플리케이션을 운영하는데 있어서 사용자가 어플리케이션 내에서 다른 서비스 즉, 구글이나 페이스북, 카카오 등의 서비스를 사용할 수 있게 하고 싶다면 어떻게 하면 될까?

정말 간단한 방법을 생각해보자면 사용자에게 다른 서비스의 유저 정보 (쉽게 구글 아이디, 비밀번호)를 받아서 다른 서비스 (구글)을 이용하는 방법을 사용할 수 있다.

하지만 이러한 방법은 굉장히 단순하여 보기에는 편리해 보이지만 사용자 , 클라이언트(나), 다른 서비스(구글) 모두에게 위험하고 골치 아픈 일이다.

사용자는 나에게 구글의 모든 권한을 줘야한다라는 문제점이 발생하고 나는 이러한 중요한 사용자의 정보를 관리를 해야하는 문제점도 생긴다.

또한 구글 입장에서도 신뢰하지 않는 서비스가 자기의 유저의 권한을 가지고 서비스를 이용할 수 있다라는 문제점이 발생한다.

따라서 제일 위에서 설명한 니즈를 충족 시키면서 문제점까지 방지하기 위해서 나온게 바로 OAuth이다.

## OAuth 2의 승인 방식

OAuth2 승인 방식에는 여러가지가 있지만 Authorization Code Grant Type 만을 다뤄 볼 예정이다.

위에서 말한 고전적인 방식 (사용자가 직접 클라이언트에게 구글 정보를 주는 방식)이 아닌 google에서 클라이언트에게 Acess Token을 발급해주는 방식이다.

google 입장에서는 사용자 정보 전체가 아닌 일부를 Token에 넣어서 준다는 장점과 권한 부분 선택이 가능하다는 장점이 있다.

또한 클라이언트 입장에서는 사용자의 중요한 정보가 아닌 token만을 관리하면 되니 위험 부담이 훨씬 줄어든다.

이러한 동작 방식을 이용하면 구글 서비스를 이용하는데 그치지 않고 애초에 사용자 정보를 보관하지 않고 회원을 식별할 수가 있다.

### Authorization Code Grant Type

![](https://images.velog.io/images/kdo0129/post/bea01b54-9338-4d48-a274-bd4d662000cf/image.png)

1. 클라이언트가 파라미터로 Client_id, redirect_url, response_type을 구글 서버에 전달하고 정상적으로 인증이 된다면 권한 부여 코드를 클라이언트에 보내준다.

2. 클라이언트는 권한 부여 코드를 사용해 Access token을 추가로 요청한다. 여기서 필요한 파라미터는 Client_id, redirect_url, Client_secret, Auth 타입이다.

3. Access token이 발급되면 클라이언트는 토큰을 사용해 리소스 서버에 접근할 수 있다.
