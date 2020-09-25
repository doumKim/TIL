![](https://images.velog.io/images/kdo0129/post/44e450bc-ad68-432d-b64e-a11734568d44/image.png)

# Passport

passport는 Node 용 인증 미들웨어다. 요청 인증이라는 단일 목적을 제공하기 위해 설계되었다.

## 내가 passport를 사용한 이유

이번 surf 프로젝트에서는 다양한 인증 방식을 기획했다. _(통합해서 로그인이라고 부르겠다.)_

종류를 살펴보면 총 4가지이다.

1. 로컬 로그인 (직접 아이디, 패스워드를 이용해 로그인 하는 방법)
2. 카카오 로그인
3. 구글 로그인
4. 네이버 로그인

따라서 각각의 인증 방법, 구현 방법이 다 다르기 때문에 작업이 굉장히 복잡해진다.

**그렇다면 passport를 사용하면 어떤 장점이 있길래 직접 구현하지 않고 passport를 사용하는가?**

1. 세션과 쿠키 처리 등의 복잡한 작업이 많기 때문에 검증된 모듈을 사용하는 장점.

2. 카카오, 구글, 네이버 각각의 인증기관의 각각 다른 인증 방법, 구현 방법의 복잡성을 어느정도 통일화 시킬 수 있는 장점.

**장점이 있으면 단점이 있는 법** passport를 사용하는 것은 결과적으로 인증을 보다 쉽게 구현할 수 있지만 passport 그 자체는 직접 인증을 구현하는 방법보다는 더 복잡할 수 있다.

## 공식문서 살펴보기

> passport 공식 사이트 - [passportjs.org](http://www.passportjs.org/)

### 인증

기본적인 요청 인증은 아래와 같이 구현한다.

```js
app.post('/login', passport.authenticate('local'), function (req, res) {
  // If this function gets called, authentication was successful.
  // `req.user` contains the authenticated user.
  res.redirect('/users/' + req.user.username);
});
```

passport.authenticate() 의 인자에 사용할 전략을 넣어주고 그 뒤에 콜백함수로 인증 성공 여부에 따라 어떻게 처리할지 결정을 한다.

```js
app.post(
  '/login',
  passport.authenticate('local', {
    successRedirect: '/',
    failureRedirect: '/login',
  }),
);
```

이런 식으로 아예 authenticate 메서드의 두번째 인자에 인증의 결과에 따른 리디렉션 옵션을 설정할 수도 있다.

```js
app.get('/login', function (req, res, next) {
  passport.authenticate('local', function (err, user, info) {
    if (err) {
      return next(err);
    }
    if (!user) {
      return res.redirect('/login');
    }
    req.logIn(user, function (err) {
      if (err) {
        return next(err);
      }
      return res.redirect('/users/' + user.username);
    });
  })(req, res, next);
});
```

애플리케이션이 성공 또는 실패를 처리 할 수 있도록 사용자 정의 콜백을 제공할 수 있다.

### 전략

passport는 요청을 인증하는 전략을 사용한다. 여기서 전략은 사용자 이름, 비밀번호 확인, OAuth를 사용한 위임 인증까지 다양하게 존재한다.

따라서 passport에 요청 인증을 하기 전에 전략을 구성을 해야한다.

use 메서드를 통해 전략과 그 구성이 제공된다. 아래는 LocalStrategy 전략으로 사용자 이름/ 비밀번호 인증에 사용하는 예이다.

```js
var passport = require('passport'),
  LocalStrategy = require('passport-local').Strategy;

passport.use(
  new LocalStrategy(function (username, password, done) {
    User.findOne({ username: username }, function (err, user) {
      if (err) {
        return done(err);
      }
      if (!user) {
        return done(null, false, { message: 'Incorrect username.' });
      }
      if (!user.validPassword(password)) {
        return done(null, false, { message: 'Incorrect password.' });
      }
      return done(null, user);
    });
  }),
);
```

위의 예에서 중요한 컨셉이 있다. 바로 확인 콜백이다. 이것의 목적은 일련의 자격 증명을 소유한 사용자를 찾는 것이다.

**자격 증명이 유효한 경우**

```js
return done(null, user);
```

**자격 증명이 유효하지 않은 경우 (ex: 암호가 잘못된 경우)**
인증 실패를 나타내기 위해 user 대신 false를 넣어준다.

```js
return done(null, user);
```

**추가 정보 메세지**

```js
return done(null, false, { message: 'Incorrect password.' });
```

**자격 증명을 확인하는 동안 예외 발생하는 경우 (ex: DB를 사용할 수 없는 경우)**

```js
return done(error);
```

### 미들웨어

express 기반의 애플리케이션에서는 passport 초기화를 위해서 passport.intitialize() 미들웨어가 필요하다.

또한 영구 로그인 세션을 사용한다면 passport.session() 미들웨어도 반드시 사용해야한다.

```js
app.use(passport.initialize());
app.use(passport.session());
```

### 세션

대부분의 애플리케이션에서 사용자 인증에 사용되는 credential들은 로그인 요청 중에 만 전송된다.

인증이 성공되면 사용자 브라우저에 설정된 쿠키를 통해 세션이 설정되고 유지가 된다.

각 후속 요청에는 credential이 포함되지 않고 세션을 식별하는 고유 한 쿠키가 포함된다.

로그인 세션을 지원하기 위해 passport는 세션에서 인스턴스를 serializeUser, deserializeUser 한다.

```js
passport.serializeUser(function (user, done) {
  done(null, user.id);
});

passport.deserializeUser(function (id, done) {
  User.findById(id, function (err, user) {
    done(err, user);
  });
});
```

serializeUser는 세션 객체에 어떠한 데이터를 저장할지 선택한다. 매개변수로 user(로그인 사용자 정보)를 받아서 done 함수 두 번째 인자로 user.id를 넘기고 있다.

여기서 id 값만 넘겨주는 이유는 세션 내에 저장된 데이터 양을 적게 유지하기 위해서이다.

deserializeUser는 매 요청 시 실행이된다. passport.session() 미들웨어가 이 메서드를 호출한다.

serializeUser에서 세션에 저장했던 user.id를 받아 DB에서 사용자 정보를 조회한다.

즉, 쉽게 serializeUser는 사용자 정보 객체를 세션에 아이디로 저장하고 deserializeUser는 세션에 저장한 아이디를 통해 사용자 정보 객체를 불러오는 것이다.

**세션에 불필요한 데이터를 담아두지 않기 위한 과정인 것이다.**

### passport 이용한 인증 과정

#### 로그인 전

1. 로그인 요청
2. passport.authenticate 메서드 호출
3. 로그인 전략 수행
4. 로그인 성공 시 사용자 정보 객체와 함께 req.login 호출
5. req.login 메서드가 passport.serializeUser 호출
6. req.session에 사용자 아이디만 저장
7. 로그인 완료

#### 로그인 후

1. 모든 요청에 passport.session() 미들웨어가 passport.deserializeUser 메서드 호출
2. req.session에 저장된 아이디로 DB에서 사용자 조회
3. 조회된 사용자 정보를 req.user에 저장
4. 라우터에서 req.user 객체 사용 가능
