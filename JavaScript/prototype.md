- reference : https://ji5485.github.io/post/2021-02-05/javascript-core-concept-summary-prototype-chaining-1/

---

2주차는 HTML/CSS 학습의 마무리과 함께 JavaScript 기초 문법을 학습했습니다. 이후 Javascript를 통해 객체지향프로그래밍이란 무엇인가 접한 후, DOM, AJAX에 대한 이해의 시간을 가졌는데 그 중 가장 이해되지 않았던 JavaScript가 가진 독특한 면모 중 하나인 프로토타입과 프로토타입 체이닝에 대해 정리해보려 합니다.

위의 글을 출처로 참고했습니다.

## **[[Prototype]] 링크? prototype 프로퍼티?**

_자바스크립트에서 모든 객체는 자신을 생성한 생성자 함수의 prototype 프로퍼티가 가리키는 프로토타입 객체를 자신의 부모 객체로 설정하는 [[Prototype]] 링크로 연결한다._

- \__proto\_\_\_ ? [[Prototype]] ?_
  `Object.prototype`의 `__proto__` 속성은 접근하고자 하는 객체의 내부 속성인 `[[Prototype]]`를 노출하는 접근자 속성(getter 및 setter 함수)입니다. (MDN)

```java
var Student = function (name, grade) {
  this.name = name;
  this.grade = grade;
};

var freshman = new Student('Hyun', 1);
```

Student 생성자 함수 정의 ⇒ Student.prototype 객체 생성 ⇒ Student 생성자 함수의 prototype 프로퍼티로 접근 가능

Student 생성자 함수를 통해 만든 객체는 [[Prototype]] 링크를 통해 Student.prototype 객체와 연결된다. (~를 가리킬 수 있다)

**객체를 생성하는 것은 생성자 함수의 몫이지만, 생성된 객체의 부모 역할은 하는 것은 생성자 함수의 prototype 프로퍼티가 가리키는 프로토타입 객체이다.** (생성자 함수가 부모 역할 X)

## 프로토타입 체이닝

_객체에서 자기 자신의 프로퍼티 뿐만 아니라, 자신의 부모 역할을 하는 프로토타입 객체의 프로퍼티도 자신의 프로퍼티처럼 사용할 수 있음_

### 객체 리터럴 방식으로 생성한 객체의 프로토타입 체이닝

```java
const obj = {
  name: 'test'
}

console.log(obj.hasOwnProperty('name'));

const arr = [1,2,3];

console.log(arr.hasOwnProperty('name'));
```

```java
var student = {
  name: 'Hyun',
  grade: 1,
};

console.log(student.name); // Hyun
console.log(student.valueOf()); // { name: 'Hyun', grade: 1 }
```

student 객체는 어쩌다가 valueOf 메서드를 사용할 수 있게 되었나?

리터럴 방식으로 생성된 객체는 `Object` 생성자 함수를 통해 객체가 생성된다. (student)

- 리터럴 방식?
  - **리터럴표기법 : 변수를 선언함과 동시에 그 값을 지정해주는 표기법**
    ```java
    //리터럴 표기법
    var no = 3;
    var obj = { name: 'JY', age: 20 }; // 객체리터럴 방식으로 만든 객체
    ```

리터럴 방식으로 만들어진 어떤 객체의 프로퍼티에 접근했을 때, 해당 프로퍼티가 존재한다면 바로 출력하겠지만 **그 프로퍼티가 존재하지 않는다면 [[ProtoType]] 링크로 연결된 프로토타입 객체에서 해당 프로퍼티를 검색한다.**

valueOf 메서드(JS 표준 API)는 Object.prototype 객체에 존재하기 때문에 호출된 것.

### 생성자 함수로 생성한 객체의 프로토타입 체이닝

```java
var Student = function (name, grade) {
  this.name = name;
  this.grade = grade;
};

var freshman = new Student('Hyun', 1);
```

freshman 객체는 Student.prototype 객체까지 접근 가능 + Student.prototype 객체도 객체이기 때문에 [[Prototype]] 링크로 Object.prototype 객체를 연결한다 ?!!
⇒ 결론적으로 freshman 객체 - Student.prototype 객체 - Object.prototype 객체까지 체이닝이 되는 것..

※ 프로토타입 체이닝의 마지막은 Object.prototype 객체이다
