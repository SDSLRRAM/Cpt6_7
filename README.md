### 6-1: 생성자 함수와 프로토타입 메서드

- `Person`은 생성자 함수로, `new` 키워드를 통해 객체를 생성
- `this._name`은 인스턴스 고유의 속성으로 설정됨
- `Person.prototype.getName`을 통해 모든 인스턴스가 공유하는 메서드를 정의


### 6-2: 생성자 함수와 인스턴스의 프로토타입 구조

- `Constructor`는 이름을 인자로 받는 생성자 함수
- `method1()`과 `property1`은 `Constructor.prototype`에 정의되어 모든 인스턴스가 공유함
- `console.dir(Constructor)`: 생성자 함수 자체의 구조 출력
- `console.dir(instance)`: 인스턴스가 `[[Prototype]]`을 통해 `Constructor.prototype`에 접근하는 구조를 확인 가능
