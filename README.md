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

### 7-1: 인스턴스 메서드 vs 정적 메서드

- `Rectangle`은 생성자 함수로, `width`와 `height` 속성을 갖는 사각형 객체를 생성
- `getArea()`는 `Rectangle.prototype`에 정의되어, 모든 인스턴스가 공유하는 인스턴스 메서드
- `isRectangle()`은 `Rectangle` 생성자 함수에 직접 붙인 정적 메서드
- `rect1.isRectangle(...)` 은 오류 발생--> isRectangle은 인스턴스가 아닌 Rectangle 생성자에만  정의되어 있기 때문에

### 7-2: 유사 배열 객체에 배열 프로토타입 연결

- `Grade()`는 `arguments`를 반복하며며 `this[0]`, `this[1]`, ... 와 같이 속성을 설정
- `this.length`도 명시적으로 설정해 유사 배열(array-like) 형태 완성
- 생성자 함수의 프로토타입을 빈 배열로 설정함으로써, Grade 인스턴스가 Array.prototype 메서드(push, join 등)를 사용할 수 있음

### 7-3: 배열 메서드와 length 속성의 관계

- `Grade()`는 유사 배열 객체를 생성하고, `Grade.prototype = []` 설정으로 배열 메서드 사용 가능
- `g.push(90)` 호출 시, `this.length = 2`이므로, 인덱스 2에 `90` 추가되고 `length`는 3으로 증가
- 이후 `delete g.length` 수행, `length` 속성이 삭제되면 `push()`는 내부적으로 `this.length || 0`을 사용하여 0부터 다시 시작
- 따라서 다음 `g.push(70)` 호출 시, `this.length`가 없으므로 기본값 0으로 간주 → `this[0] = 70`

### 7-4: length 속성 삭제 후 프로토타입의 length 사용 사례

- `Grade.prototype = ['a', 'b', 'c', 'd']`로 설정됨 즉, `g` 인스턴스는 배열 프로토타입을 상속받으며 `length` 속성이 없을 경우 `prototype.length`를 사용하게 됨
- g.length = 2 → push(90) → g[2] = 90, g.length = 3

### 7-5: Rectangle과 Square의 생성자 및 면적 계산

- `Rectangle(width, height)`는 사각형 객체를 생성하고, `getArea()` 메서드는 너비와 높이의 곱을 반환
- `Square(width)`는 정사각형을 생성하고, `getArea()` 메서드는 `width * width` 형태로 재정의
- 이때, 두 생성자는 서로 독립적인 구조이며, 각자의 prototype.getArea() 메서드를 가지고 있음

### 7-6: 정사각형의 width와 height 동시 설정

- `Square(width)` 에서 `this.height = width`로 설정함으로써, 정사각형은 가로와 세로 길이가 같은 특성을 가지도록 구현
- `Square.prototype.getArea()`는 `width * height`로,`Rectangle`과 같은 로직이지만 별도로 정의되어 있음
- Square와 Rectangle이 구조와 메서드를 중복 정의하고 있음

### 7-7: Square가 Rectangle을 상속

- `Rectangle.call(this, width, width)`을 통해 Square 인스턴스가 Rectangle의 생성자 로직을 재사용
- `Square.prototype = new Rectangle()`을 통해 Rectangle의 메서드(getArea 등)를 상속받는 프로토타입 체인 완성
- call()로 생성자 재사용, constructor 속성은 덮어씌워졌기 때문에 다음 단계에서는 constructor 복원 필요

### 7-8: 헬퍼 함수 extendClass1을 통한 상속 구현

- `extendClass1(SuperClass, SubClass, subMethods)` 함수를 통해 클래스 상속 구조를 구현현
- SubClass의 prototype을 SuperClass 인스턴스로 초기화, 기존 prototype 속성 삭제 후, subMethods 덮어쓰기 진행

### 7-9: Bridge 함수 활용 프로토타입 상속

- `extendClass2`는 SuperClass와 SubClass 사이에 중간 `Bridge` 생성자를 두어 상속
- `Bridge.prototype = SuperClass.prototype` 으로 연결하고, `SubClass.prototype = new Bridge()`로 인스턴스를 생성
- `new SuperClass()`를 직접 호출하지 않고도 프로토타입 체인 연결
- 메모리 공유 문제 방지, 상속 안정성 확보, SuperClass 실행을 피할 수 있는 장점 존재