### 6-1: 생성자 함수와 프로토타입 메서드

- `Person`은 생성자 함수로, `new` 키워드를 통해 객체를 생성
- `this._name`은 인스턴스 고유의 속성으로 설정됨
- `Person.prototype.getName`을 통해 모든 인스턴스가 공유하는 메서드를 정의


### 6-2: 생성자 함수와 인스턴스의 프로토타입 구조

- `Constructor`는 이름을 인자로 받는 생성자 함수
- `method1()`과 `property1`은 `Constructor.prototype`에 정의되어 모든 인스턴스가 공유함
- `console.dir(Constructor)`: 생성자 함수 자체의 구조 출력
- `console.dir(instance)`: 인스턴스가 `[[Prototype]]`을 통해 `Constructor.prototype`에 접근하는 구조를 확인 가능

### 6-3: 배열의 constructor를 통한 새로운 배열 생성

- 자바스크립트 배열은 내부적으로 `Array` 생성자에 의해 만들어짐
- `arr.constructor`는 `Array`를 의미함 즉, `arr.constructor === Array` → `true` 임임
- 따라서 이와 같은 방식으로 생성자 공유를 통한 인스턴스 생성이 가능함

### 6-4: constructor 변경과 instanceof 판별

- 다양한 데이터 타입(Number, String, Array, Function 등)을 가진 배열 `dataTypes`를 구성
- 각 요소의 `.constructor` 속성을 임의로 `NewConstructor`로 변경
- .constructor는 단순히 참조용 프로퍼티일 뿐이며, constructor를 변경해도 인스턴스의 실제 생성자와는 무관