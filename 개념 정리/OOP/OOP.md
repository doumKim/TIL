# 객체 지향 프로그래밍(OOP)

![](https://media.vlpt.us/images/kdo0129/post/da38badc-0ea4-4caa-ad56-e7488d4bcdbb/1024px-Unofficial_JavaScript_logo_2.svg.jpg)

대부분의 자바스크립트 서적이나 설명을 보면 자바스크립트는 객체 지향 프로그래밍을 지원한다고 설명한다.

그렇다면 과연 여기서 말하는 객체 지향 프로그래밍이 무엇일까?

## 객체 지향 프로그래밍?

객체 지향 프로그래밍 (Object Oriented Programming, OOP) 의 정의를 보자면 다음과 같다.

> **객체 지향 프로그래밍(영어: Object-Oriented Programming, OOP)은** 컴퓨터 프로그래밍의 패러다임 중 하나이다. 객체 지향 프로그래밍은 컴퓨터 프로그램을 명령어의 목록으로 보는 시각에서 벗어나 여러 개의 독립된 단위, 즉** "객체"들의 모임으로 파악**하고자 하는 것이다. 각각의 객체는 메시지를 주고받고, 데이터를 처리할 수 있다.
>
> 객체 지향 프로그래밍은 **프로그램을 유연하고 변경이 용이하게 만들기** 때문에 대규모 소프트웨어 개발에 많이 사용된다. 또한 **프로그래밍을 더 배우기 쉽게 하고 소프트웨어 개발과 보수를 간편하게 하며**, 보다 **직관적인 코드 분석을 가능하게** 하는 장점을 갖고 있다. 그러나 지나친 프로그램의 객체화 경향은 실제 세계의 모습을 그대로 반영하지 못한다는 비판을 받기도 한다.
> [-출처 위키백과](https://ko.wikipedia.org/wiki/%EA%B0%9D%EC%B2%B4_%EC%A7%80%ED%96%A5_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D)

> 객체지향 프로그래밍은 **실제 세계에 기반한 모델을 만들기 위해 추상화를 사용하는 프로그래밍 패러다임**이다. 객체지향 프로그래밍은 **modularity, polymorphism, encapsulation**을 포함하여 이전에 정립된 패러다임들부터 여러가지 테크닉들을 사용한다. 오늘날 많은 유명한 프로그래밍 언어(자바, 자바스크립트, C#, C++, 파이썬, PHP, 루비, 오브젝트C)는 객체지향 프로그래밍을 지원한다.
>
> 객체지향 프로그래밍은 함수들의 집합 혹은 단순한 컴퓨터의 명령어들의 목록 이라는 기존의 프로그래밍에 대한 전통적인 관점에 반하여, **관계성있는 객체들의 집합이라는 관점으로 접근하는 소프트웨어 디자인**으로 볼 수 있다. 객체지향 프로그래밍에서, 각 객체는 메시지를 받을 수도 있고, 데이터를 처리할 수도 있으며, 또다른 객체에게 메시지를 전달할 수도 있다. **각 객체는 별도의 역할이나 책임을 갖는 작은 독립적인 기계로 볼 수 있는 것**이다.
>
> 객체지향 프로그래밍은 보다** 유연하고 유지보수성**이 높은 프로그래밍을 하도록 의도되었고, 대규모 소프트웨어 공학에서 널리 알려져 있다. 객체지향 프로그래밍이 갖는 modularity에 기반한 강력한 힘에 의해, 객체지향적인 코드는** 개발을 보다 단순하게** 했고, 시간이 흐른 뒤에도 보다 **쉽게 이해할 수 있도록 했으며**, 복잡한 상황이나 절차들을 덜 모듈화된 프로그래밍 방법들보다 **더 직접적으로 분석하고, 코딩하고, 이해할 수 있도록 만들었다.**
> [-출처 MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Introduction_to_Object-Oriented_JavaScript#Object-oriented_programming)

### OOP의 목적

위 2가지 설명에서 **공통적으로 말하는 내용이** 있다.

1. 객체지향 프로그래밍은 실제 세계에 기반한 모델을 만들기 위해 추상화를 사용하는 **프로그래밍 패러다임이다.**

2. 프로그램을 관계성있는 객체들의 집합으로 파악한다.

3. 각 객체는 별도의 역할이나 책임을 갖는 작은 독립적인 기계로 볼 수 있다.

4. 소프트웨어 개발과 유지보수를 쉽게 해주고 가독성에도 도움을 준다.

#### ✔️ 응집력과 결합력

_소프트웨어 공학에는 **응집력과 결합력**이란게 있는데 여기서 **응집력이란** 프로그램의 하나의 모듈이 해당 기능을 수행하기 위해 얼마만큼의 연관된 책임과 역할을 뭉쳐있는지를 나타내는 정도를 의미하고 **결합력이란** 프로그램의 하나의 모듈이 다른 모듈과 얼마나 강력하게 연결되어 있는지 서로 얼마나 의존적인지 나타내는 정도이다._

따라서 위의 4가지 내용을 기준으로 응집력과 결합력을 따져보자면 **OOP의 경우**에는 클래스에 하나의 문제 해결을 위해 데이터를 모아 놓은 객체를 활용한 프로그래밍을 지향하기 때문에 **응집력을 강화**하고 각 클래스 간에 독립적인 디자인으로 **결합력을 약하게** 할 수 있다.

### OOP의 기본 구성요소

- **Class**
  객체 즉, 인스턴스를 찍어내는 공장으로 생각할 수 있다.

- **Instance**
  Class 즉, 공장에서 찍어내는 결과물이고 상위 class의 속성도 가지고 있고 각각 개별적인 특성과 메소드를 가지고 있다.

- **Property & Method**
  인스턴스의 속성 및 어떠한 기능을 수행하는 역할을 한다.

![class 기본 구성요소 설명](https://images.velog.io/images/kdo0129/post/53d25a8b-fd14-414d-aca2-cea3a1a7aca5/image.png)

위의 그림을 직접 구현해보기 전에 의사 코드를 작성해보자면 아래와 같다.

#### 👨‍💻 Pseudo code

```js
1. 동물이라는 결과물을 찍어내는 공장 Animal 클래스를 생성.
2. 공통적인 속성인 동물이라는 속성은 모두에게 준다.
3. 하지만 생성할 인스턴스는 각자 종이 다르다. 그에 맞게 속성과 메소드를 줘야한다.
4. 인스턴스 생성..!
```

#### 👩‍💻 Write code

```js
class Animal {
  constructor(species, sound) {
    this.species = species;
    this.sound = sound;
  }

  makeSound() {
    console.log(this.sound);
  }
}

const dog = new Animal('강아지', '멍멍!!');
const cow = new Animal('소', '음메~!');
const cat = new Animal('고양이', '냐옹~!');

dog.makeSound(); // 멍멍!!
cow.makeSound(); // 음메~!
cat.makeSound(); // 냐옹~!
```

### OOP의 특성

- **캡슐화 (encapsulation)**
  데이터 구조와 데이터를 다루는 방법들을 결합 시켜 묶는 것. 객체가 맡은 역할을 수행하기 위한 하나의 목적을 한 곳에 묶는다고 생각하면 된다. 또한 내부 데이터를 외부에서 직접 접근하지 못하게 은닉화를 시켜준다.

- **상속 (inheritance)**
  상위 개념의 속성을 하위 개념이 물려받는 것. 차를 만드는 클래스가 있다. 그리고 차에는 종류가 여러 종류가 있다. 일반 승용차, 또는 트럭, 버스 등.... 하지만 기본적으로 차라는건 동일하다. 하지만 승용차, 트럭, 버스 각기 용도는 다르다. 이런 공통적인 차의 기능을 물려주는 것을 바로 상속이라고 한다.

![상속](https://images.velog.io/images/kdo0129/post/27219455-1fe2-45ce-b4c6-54662d7b5d46/image.png)

- **추상화 (abstraction)**
  공통의 속성이나 기능을 묶어 이름을 붙이는 것. 위에서 강아지 소 고양이 객체를 만들었는데 그것들을 동물이라는 기준으로 하나로 묶으려고 하면 그게 바로 추상화이다. 다른 예시를 들어보자면 컴퓨터를 사용하는 대부분의 사람들이 컴퓨터가 어떻게 동작하고 어떻게 만들어졌는지 100% 알지 못한다. 중요한건 이 컴퓨터를 어떻게 사용하는지 모니터에 어떤 화면이 출력되는지 이다.

![추상화](https://images.velog.io/images/kdo0129/post/4fe9264b-ffa5-4c38-a7c6-72751033676d/image.png)

- **다형성 (polymorphism)**
  부모 클래스에서 물려받은 함수를 자식 클래스 내에서 오버라이딩 되어 사용되는 것. 서로 다른 클래스의 객체가 같은 메시지를 받았을 때 각자의 방식으로 동작하는 능력이다. 위의 동물 클래스에서 고양이와 강아지 소의 울음소리를 따로 들을 수 있는 이유가 다형성과 상속에 있다.

## 자바스크립트에서 객체를 만드는 법

자바스크립트에서 객체를 생성하는 방법은 크게 3가지 방법이 있다.

- 생성자 함수

- 클래스

- Object.create()

### 생성자 함수

생성자 함수는 간단하다. 함수이면서 호출할 때 new 연산자를 사용해주면 인스턴스를 생성한다. 또한 new 연산자로 인해 this는 인스턴스를 바인딩하게된다. 직접 코드로 살펴보자.

#### 👨‍💻 Pseudo code

```js
1. 유저를 만들어내는 생성자 함수를 만든다.
2. 유저는 각자 이름과 성별의 속성을 가져야한다.
3. 인스턴스 생성..!
```

#### 👩‍💻 Write code

```js
function User(name, age) {
  this.name = name;
  this.age = age;

  this.sayName = function () {
    console.log(this.name);
  };
}

const user1 = new User('Lee', 20);

console.log(user1); // User {name: "Lee", age: 20, sayName: function (), constructor: Object}
user1.sayName(); // Lee
```

근데 여기서 한가지 살펴봐야할 점이 있다. 위의 코드에서 상상력을 발휘해 엄청나게 많은 유저의 수가 있고 메소드도 많고 복잡하다고 가정을 해보면? 모든 인스턴스마다 메소드를 추가해주는 메모리 누수가 발생을 한다.

이런 문제를 해결하기 위해 **프로토 타입** 이라는 상속 방식을 사용하면 된다.

예를 들어 설명을 하자면 자식밖에 모르는 부모와 등골 브레이커 자식이 있다고 가정해보자.

부모는 자식이 금전적으로 부족함을 느끼게 해주기 싫어 자식을 위한 비상금을 **금고**에 넣어두고 자식에게 비밀번호를 알려줬다.

그리고 시간이 흘러 돈이 필요한 등골 브레이커 자식은 금고의 문을 열고 비상금을 빼서 사용을 할 것이다.

여기서 **금고가 프로토 타입**이 되는 것이다.

금고를 들고 다니는게 아니다. 은행에 금고가 있다면 은행에 가서 돈만 저장을 하고 찾고하는 그저 멀리 위치해 있는 보관용 상자에 불가하다.

따라서 프로토 타입을 사용하여 메모리 누수를 줄일 수 있다.

근데 이 등골 브레이커 기질은 어디서 뚝 떨어져 생긴게 아니라 자기 부모를 닮았던 것이다.

그렇게 조부모에서 부모 또 부모에서 자식 이렇게 등골을 빼 먹고 있던 것이다.

따라서 결국 조부모 비상금이 부모의 비상금으로 부모의 비상금이 자식의 비상금으로 **체인처럼 연결**이 된다.

이것이 **바로 프로토타입 체인**이다.

프로토타입 체인은 가장 최상위 객체까지 이어져있다.

부모의 금고를 확인해서 비상금이 없다면 조부모의 금고까지 확인을 한다. 만약 거기에도 돈이 없다면 파산 즉, 참조 에러가 발생한다.

![](https://images.velog.io/images/kdo0129/post/f4c078b6-47ce-4349-8c21-09d85c1eca01/image.png)

따라서 위의 코드를 프로토타입을 이용해 수정해 본다면

#### 👩‍💻 Write code

```js
function User(name, age) {
  this.name = name;
  this.age = age;
}

User.prototype.sayName = function () {
  console.log(this.name);
};

const user1 = new User('Lee', 20);

console.log(user1); // User {name: "Lee", age: 20, sayName: function (), constructor: Object}
user1.sayName(); // Lee
```

이런식으로 수정이 가능하다. 그럼 이제 prototype에 대해서는 알겠는데 그럼 \_\_proto\_\_ 이녀석은 뭐지?

![](https://images.velog.io/images/kdo0129/post/827d77ea-5537-4bb0-bb17-54858bc1b47f/image.png)

#### prototype vs \_\_proto\_\_

간단하게 관점의 차이다. 아까 금고를 생각하면 부모 입장에서 금고는 자식에게 줄 금고이다.

반면에 자식 입장에서는 부모에게 받은 금고이다. 나누는 이유는 간단하다. 시간이 흘러 이 자식이 자식을 낳아서 똑같이 상속을 시켜주고 받고를 해야하기 때문이다.

- **prototype**
  상속을 시켜 줄 무언가

- **\_\_proto\_\_**
  상속을 받는 무언가

---

### 클래스

위에서 살펴 본 생성자 함수를 이용해서 충분히 객체 지향 프로그래밍을 할 수 있다.

하지만 java와 같은 객체 지향 프로그래밍 언어에서 사용하는 것과 유사하게 class를 사용할 수 있게 문법을 제공하기 위해 ES6 추가된 Syntactic sugar 이다.

사용 방법만 다를 뿐 생성자 함수와는 큰 차이가 없다.

1. **class** 키워드 사용

2. **constructor** 생성자 메소드 사용하여 객체 인스턴스를 생성하고 초기화한다.

3. **extends** 키워드 사용해 클래스 간 상속 가능

4. **super** 키워드 사용해 부모클래스의 constructor메서드를 부르거나 부모클래스의 프로퍼티를 참조할 수 있다.

이외의 차이점도 있지만 여기서는 기본적인 클래스 기능만 알아보겠다.

#### 👨‍💻 Pseudo code

```js
1. 부모의 이름과 성별 속성과 이름을 말하는 메소드를 가지는 부모 클래스를 만든다.
2. 부모 클래스를 상속 받는 자식 클래스를 만들고 gender 속성을 추가해 준다.
3. 인스턴스 생성..!
```

#### 👩‍💻 Write code

```js
class Parent {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  sayName() {
    console.log(this.name);
  }
}

const parent = new Parent('Chulsu', 40);

console.log(parent); // User {name: "Chulsu", age: 40, sayName: function (), constructor: Object}
parent.sayName(); // Chulsu

class Children extends Parent {
  constructor(name, age, gender) {
    super(name, age);
    this.gender = gender;
  }
}

const child = new Children('Gildong', 2, 'male');

console.log(child); // Children {name: "Gildong", age: 2, gender: "male", constructor: Object}
child.sayName(); // Gildong
```

---

### Object.create()

프로토타입을 설정하기 위한 모던한 방법이 있다. 바로 Object.create 메소드를 사용해서 객체를 생성하는 것이다.

\_\_proto\_\_는 브라우저를 대상으로 개발하고 있다면 다소 구식이기 때문에 더는 사용하지 않는 것이 좋다.

- **Object.create(prototype)**
  prototype을 넣어 객체를 생성한다. 인자로 null을 넣어주면 아무것도 상속받지 않는 객체를 만들 수 있다.

- **Object.getPrototypeOf(obj)**
  해당 객체의 프로토 타입을 가져올 수 있다.

- **Object.setPrototypeOf(obj, proto)**
  해당 객체의 프로토 타입을 설정할 수 있다.

#### 👨‍💻 Pseudo code

```js
1. iphone이라는 객체를 생성하고 applePay가 가능하면 true 불가하면 false 속성을 넣어준다.
2. proto라는 객체에 프로토 타입으로 사용할 내용을 넣어준다.
3. Object.setPrototypeOf() 를 사용해서 iphone 객체에 proto를 프로토 타입으로 추가해준다.
4. Object.create() 메소드를 이용해 IphoneInKorea의 프로토 타입 객체를 만들어준다.
5. iphoneInKorea의 applePay 속성을 설정하면 프로토 타입 체인을 거슬러 올라가 canIUseApplePay 메소드를 사용할 수 있게 된다.
```

#### 👩‍💻 Write code

```js
function Iphone() {
  this.applePay = true;
}

const proto = {
  canIUseApplePay: function () {
    console.log(this.applePay);
  },
};

const iphone = new Iphone();
Object.setPrototypeOf(iphone, proto);
iphone.canIUseApplePay(); // true

function IphoneInKorea() {
  this.applePay = false;
}
IphoneInKorea.prototype = Object.create(proto);

const iphoneInKorea = new IphoneInKorea();
iphoneInKorea.canIUseApplePay(); // false
```
