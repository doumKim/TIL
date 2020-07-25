# Stack, Queue

## Stack

스택은 가장 윗 부분에서만 자료의 추가와 삭제가 발생한다. **실행 속도가 빠르고 구현이 쉬운 효율적인 자료구조**이다.

요소 리스트로 구성이 되어있고, **Top**이라는 리스트의 한쪽 끝으로만 접근이 가능하다.

**선형 구조**, 후입선출 (**LIFO**) 자료 구조이다.

Top에 있지 않은 요소에는 한번에 접근할 수 없다. 따라서 특정 요소에 접근하려면 특정 요소 위에 쌓여있는 요소들을 모두 제거할 수 밖에 없다.

**ex) Call stack**

대표적인 프로퍼티와 메서드는 아래와 같다.

- top : Top index
- push() : 새로운 데이터를 추가.
- pop() : top 데이터 제거 및 반환
- peek() : top 데이터 확인
- size() : 데이터 개수 확인

### 🎨 그림으로 표현해보기 🎨

![Stack의 구조](https://images.velog.io/images/kdo0129/post/0157cfb0-f5c0-4b77-b3cd-1b306c06d5d6/image.png)

### 👩‍💻 Pseudo code 👨‍💻

```
1. store = {}, top = 0;

2. push(value) => (storage[top] = value, top + 1)

3. pop() => (popData 저장 , sorage[top -1] 제거 , top - 1, popData 반환)

4. peek() => storage[top - 1] 반환

5. size() => top 반환
```

### 👩‍💻 구현 👨‍💻

```js
class Stack {
  constructor() {
    this.store = {};
    this.top = 0;
  }
  push(value) {
    this.store[this.top] = value;
    this.top += 1;
  }
  pop() {
    const popedData = this.store[this.top - 1];
    delete this.store[this.top - 1];
    this.top -= 1;
    return popedData;
  }
  peek() {
    return this.store[this.top - 1];
  }
  size() {
    return this.top;
  }
}

const stack = new Stack();

stack.push('안녕');
stack.push('반가워');
stack.push('Hello');
console.log(stack.pop()); // "Hello"
console.log(stack.peek()); // "반가워"
console.log(stack.store); // {0: "안녕", 1: "반가워"}
console.log(stack.size()); // 2
```

## Queue

큐는 **끝 부분으로 데이터가 삽입**되고 **앞 부분에 데이터가 꺼내지는** 자료 구조이다.

**선입선출(FIFO)** 방식의 구조이다. 일어난 순서대로 데이터를 저장하는 자료 구조이다.

**ex) Event Queue**

대표적인 프로퍼티와 메서드는 아래와 같다.

- front : 큐의 제일 앞 요소 인덱스
- back : 큐의 마지막 요소 인덱스
- enqueue() : 새로운 데이터를 추가
- dequeue() : top 데이터 제거 및 반환
- peek() : front 데이터 확인
- size() : 데이터 개수 확인

### 🎨 그림으로 표현해보기 🎨

![Queue 구조](https://images.velog.io/images/kdo0129/post/0651f1a0-8c17-4b69-b597-6dc480329055/image.png)

![Queue는 줄 서서 무언가를 주문하는거랑 비슷하다.](https://images.velog.io/images/kdo0129/post/8a899bc2-d3f1-4842-8605-001d6a2fe76a/image.png)

_**<center>Queue의 구조와 비슷한 줄 서기</center>**_

### 💻 Pseudo code 💻

```
1. store = {} , front = 0, back = 0

2. enqueue(value) => ( store[back] = value )

3. dequeue => store[front + 1] 이 있으면 front + 1

4. peek() => store[front] 반환

5. back - front + 1 반환
```

### 👩‍💻 구현 👨‍💻

```js
class Queue {
  constructor() {
    this.store = {};
    this.front = 0;
    this.back = 0;
  }
  enqueue(value) {
    this.store[this.back] = value;
    this.back += 1;
  }

  dequeue() {
    const deletedValue = this.store[this.front];
    delete this.store[this.front];
    if (this.store[this.front + 1]) this.front += 1;
    return deletedValue;
  }

  peek() {
    return this.store[this.front];
  }

  size() {
    return this.back - this.front + 1;
  }
}

const queue = new Queue();

queue.enqueue('hello');
queue.enqueue('world');
queue.enqueue('!');
console.log(queue.dequeue()); // hello
queue.enqueue('asdasd');
console.log(queue.peek()); // world
console.log(queue.size()); // 4
console.log(queue.store); // {1: "world", 2: "!", 3: "asdasd"}
```
