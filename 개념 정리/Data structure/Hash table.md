# Data structure - Hash table

<img src="https://media.vlpt.us/images/kdo0129/post/a4b4e7fa-58e9-4457-aec1-66b1d3a3a0f5/dataStructure.jpg">

## Hash table

해싱 : 데이터를 단시간에 삽입하거나 저장된 데이터를 가져올 때 사용하는 기법, 해시 테이블 자료구조를 이용한다.

장점은 데이터를 빠르게 삽입, 삭제하거나 가져올 수 있다. 단점으로는 최솟값, 최댓값 등 검색 동작 효율이 나쁘다.

해시 테이블은 배열을 이용한다.
배열은 크기가 정해져 있지만 필요하다면 크기를 늘릴 수 있다.
key라 불리는 데이터 요소로 배열에 저장된 데이터 요소를 참조할 수 있다.

해시 함수는 각 키를 자체 배열 요소로 저장한다.
키가 한 곳에 집중되지 않도록 저장하는 것이 좋다. 해시 함수에서는 결과값이 같을 경우가 발생한다. 이를 충돌이라 한다.

해시 함수를 만들기 전 해시 테이블에 사용할 배열의 크기를 보통 소수로 지정하는게 좋다.

해시 테이블의 요소의 개수는 **25% ~ 75%**를 유지하는게 최상의 효율을 낼 수 있다.

### 충돌 해결 방법

해시 함수에서 두 개 이상의 값을 계산한 결과가 같을 때 충돌이 발생한다.
따라서 충돌을 해결해 줄 방법 2가지를 알아보자.

배열의 크기가 저장할 요소의 절반 이하라면 Seperate chaining을 사용하고 배열의 크기가 저장할 요소의 두 배까지 될 수 있는 상황이라면 Open addressing을 택하는게 좋다.

#### Seperate chaining

충돌이 일어나도 생성된 인덱스에 키를 저장할 수 있어야 한다. 하지만 배열의 요소에는 한 개의 데이터 밖에 저장할 수 없다. 따라서 해시 테이블의 각 배열 요소가 배열 같은 다른 자료구조를 포함하고 그 다른 자료구조에 키를 저장한다.

#### Open addressing

충돌이 발생하면 해시 테이블의 다음 요소가 비어 있는지 확인한다. 비어있는 요소가 나올 때까지 선형 조사를 계속 한다. 빈 요소를 발견하면 요소에 키를 저장한다.

대부분의 해시 테이블에는 비어 있는 공간이 많이 있으므로 비어 있는 공간을 이용해 키를 저장한다는 것이 선형 조사 기법의 핵심이다.

**ex) 전화번호 검색 **

대표적인 프로퍼티와 메서드는 아래와 같다.

- table : 배열을 이용해 해싱 함수의 결과값을 인덱스로 하는 밸류를 저장

- insert(key) : 테이블에 데이터 삽입

- retrieve(key) : 테이블의 데이터를 가져오는 함수

- remove(key) : 데이터를 삭제하는 함수

- resize(limit) : 배열의 크기를 바꿔주는 함수

### 🎨 그림으로 표현해보기 🎨

**Hash table**

![Hash table 구조](https://images.velog.io/images/kdo0129/post/7cca5096-2296-4298-8347-db1226471fc4/image.png)

**Seperate chaining**

![Seperate chaining](https://images.velog.io/images/kdo0129/post/6ab006da-ccc7-4ec4-8fc2-4721fd2eaae7/image.png)

**Open addressing**

![Open addressing](https://images.velog.io/images/kdo0129/post/9ed97de1-1f55-44ff-b409-c5303e51496c/image.png)

### 💻 Pseudo code 💻

```
insert
1. 충돌 상황을 위한 bucket 객체 생성
2. 해당 index에 값이 없으면 bucket의 key ,value 할당 후 set 메서드 사용해 storage에 저장
3. 해당 index에 값이 있으면 bucket을 get 메서드를 사용해 storage에 있는 기존의 bucket을 재할당 후 2번 반복
4. 사이즈 += 1
5. insert 후 변경 된 사이즈가 제한 크기의 75 퍼센트를 초과하면 resize(this._limit * 2)

retrieve
1. get 메서드 사용해서 특정 index에 값이 있으면 반환 없으면 undefined 반환

remove
1. get 메서드로 제거할 대상이 있는지 확인 후 없으면 undefined 반환
2. 삭제할 bucket의 prop을 변수에 담아주고 prop 삭제
3. 사이즈 -= 1
4. remove 후 변경 된 사이즈가 제한 크기의 25퍼센트 미만이면 resize(this._limit / 2)
5. 변수에 담아준 삭제한 값을 반환

resize
1. 이전 storage 변수에 담아서 저장
2. size, limit, storage 초기화
3. each 메서드 사용해서 새로운 storage에 rehash.
```

### 👩‍💻 구현 👨‍💻

```js
class HashTable {
  // hashFunction - 미리 구현되어 있는 해시 함수.
  // LimitedArray - 미리 구현되어 있는 해시테이블에서 사용할 storage 배열 만드는 함수 get, set ,each 메서드
  constructor() {
    this._size = 0;
    this._limit = 8;
    this._storage = LimitedArray(this._limit);
  }

  insert(key, value) {
    const index = hashFunction(key, this._limit);
    let bucket = {};
    if (!this._storage.get(index)) {
      bucket[key] = value;
      this._storage.set(index, bucket);
    } else {
      bucket = this._storage.get(index);
      bucket[key] = value;
      this._storage.set(index, bucket);
    }
    this._size += 1;

    if ((this._size / this._limit) * 100 > 75) {
      this._resize(this._limit * 2);
    }
  }

  retrieve(key) {
    const index = hashFunction(key, this._limit);
    if (!this._storage.get(index)) return undefined;
    return this._storage.get(index)[key];
  }

  remove(key) {
    const index = hashFunction(key, this._limit);
    if (!this._storage.get(index)) {
      return undefined;
    } else {
      const willDeleted = this._storage.get(index)[key];
      delete this._storage.get(index)[key];
      this._size -= 1;
      if ((this._size / this._limit) * 100 < 25) {
        this._resize(this._limit / 2);
      }
      return willDeleted;
    }
  }

  _resize(newLimit) {
    let prevStorage = this._storage;
    this._size = 0;
    this._limit = newLimit;
    this._storage = LimitedArray(this._limit);

    const reHash = (bucket) => {
      for (let item in bucket) {
        this.insert(item, bucket[item]);
      }
    };

    prevStorage.each(reHash);
  }
}
```
