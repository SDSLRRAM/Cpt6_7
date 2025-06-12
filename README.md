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

### 6-5: constructor 접근 경로를 통한 인스턴스 생성

- `Person(name)` 생성자를 이용해 다양한 방식으로 인스턴스를 생성
- 모두 결과적으로 동일한 생성자(Person)를 참조하고 있으므로, 각각의 객체는 instanceof Person 판별 시 모두 true를 출력함

### 6-6: 인스턴스에서 프로토타입 메서드 오버라이딩

- `Person.prototype.getName()`은 모든 인스턴스가 공유하는 메서드
- 하지만 특정 인스턴스 `iu`에서 `getName`을 재 정의 시, 자신의 메서드를 우선 사용하게 됨 --> 프로토타입 체인에서 하위 객체의 속성이 상위보다 우선하기 때문에

### 6-7: 배열 요소와 hasOwnProperty()

- 배열 인덱스는 문자열 속성으로 저장됨 ("0", "1") 그 후 인덱스 "2"에 새 요소 추가
- `hasOwnProperty(prop)`는 주어진 키가 상속(prototype)이 아닌 인스턴스 자체에 존재하는지를 확인하는 메서드

### 6-8: toString() 메서드와 오버라이딩 동작

- 배열 `arr = [1, 2]`는 기본적으로 `Array.prototype.toString()`을 상속받아 동작
- 만약 `Object.prototype.toString.call(arr)` 사용 시, 내부 `[[Class]]`를 확인
- 이후 인스턴스에서 `toString()`을 오버라이딩을 진행

### 6-9: Object.prototype.getEntries() 구현

- 모든 객체에 공통적으로 사용할 수 있는 유틸리티 함수 `getEntries()`를 `Object.prototype`에 직접 정의
- `for...in` 루프와 `hasOwnProperty()`를 조합하여 해당 객체의 직접 속성만 추출
- 각 속성은 `[key, value]` 형태의 배열로 구성되어 `.push()`됨

### 6-10: 배열처럼 동작하는 유사 배열 객체 생성

- `Grade()` 생성자는 `arguments` 객체를 이용해 전달된 값을 유사 배열 구조로 초기화
- `this[0] = ...`, `this[1] = ...` 등으로 각 인자를 프로퍼티로 저장
- `this.length = 인자의 개수` 를 설정


