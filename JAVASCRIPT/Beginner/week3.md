# 11. 함수 표현식, 화살표 함수(arrow function)

함수 선언문 vs 함수 표현식

<br />

#### 함수 선언문

```javascript
function sayHello() {
  console.log(`Hello`);
}

sayHello();
```

#### 함수 표현식

이름이 없는 함수로 만들고, 변수를 선언해서 함수를 할당해주는 것을 '함수 표현식'이라고 한다.

```javascript
let sayHello = function() {
  console.log(`Hello`);
}

sayHello();
```

<br />

### 차이점

함수 표현식과 함수 선언문은 실행과 동작 방식 모두 동일하다. <br />
그렇다면 이 둘은 작성하는 문법 외에 어떤 차이점이 있을까? <br />
바로, 호출할 수 있는 타이밍이다.

<br />
<br />

## * 함수 선언문 - 어디서든 호출 가능

<br />

```javascript
console.log(num);  //Error. num is not defined

let num = 1;
```
위 코드는 에러가 발생한다.

<br />

```javascript
sayHello(); 

function sayHello() {
  console.log(`Hello`);
}
```
위 코드는 에러가 발생하지 않는다.

<br />

자바스크립트는 위에서 아래로 차례대로 한 줄씩 읽으면서 실행한다. <br />
이렇게 순차적으로 실행되고, 즉시 결과를 반환하는 프로그램의 언어를 '인터프리터 언어(Interpreted language)라고 한다. <br />
그런데 어떻게 두번째 코드가 정상적으로 실행될 수 있을까? <br />

<br />

이것은 자바스크립트 내부 알고리즘 때문이다. <br />
자바스크립트는 실행 전 초기화 단계에서 코드의 모든 함수 선언문을 찾아서 생성해 둔다. <br />
즉, 눈으로 봤을때는 저런 코드이지만 함수를 사용할 수 있는 범위는 코드 위치보다 위로 올라가는 것이다. <br />
이것을 호이스팅(hoisting) 이라고 하는데, 코드위치가 실제로 올라가는 것으로 오해해서는 안된다. 

<br />
<br />

## * 함수 표현식 - 코드에 도달하면 생성

<br />

반면, 함수 표현식은 자바스크립트가 한 줄씩 읽으면서 실행하고, <br />
해당 코드에 도달해서야 비로소 생성된다. <br />
그렇기 때문에 그 이후에만 사용가능하다.

<br />

```javascript
let sayHello = function() {  //생성
  console.log(`Hello`);      //사용가능
}

sayHello();
```

<br />
<br />

#### 그렇다면, 함수 선언문과 함수 표현식 중 어떤 것을 사용하는 것이 더 좋을까?

에러가 발생하면 위로 옮기면 그만이기 때문애 대부분의 상황에서는 어떻게 쓰든 상관없다. <br />
그러나 신경쓰기 싫다면 그냥 함수 선언문을 쓰는 것이 더 자유롭고 편안하게 사용할 수 있다.

<br />
<br />
<br />

## 화살표 함수(arrow function)

화살표 함수를 사용하면 지금까지 배운 함수를 보다 간결하게 작성할 수 있다.

<br />


```javascript
let add = function( num1, num2 ) { 
  return num1 + num2;
}
```
위 코드를 화살표 함수로 바꾸면,

<br />

function 이라는 단어가 없어지고, 대신 괄호 뒤쪽에 화살표가 생긴다.
```javascript
let add = ( num1, num2 )=> { 
  return num1 + num2;
}
```

<br />

위 예제는 코드 부분이 한 줄이고, return문이 있기 때문에 <br />
아래와 같이 return문은 return을 지우고, 중괄호가 아닌 일반괄호로 변경가능하다.
```javascript
let add = ( num1, num2 )=> (
  num1 + num2;
)
```

<br />

또한, 위처럼 return문이 한 줄일 경우 return문의 괄호도 생략할 수 있다.
```javascript
let add = ( num1, num2 )=> num1 + num2;
```

<br />

인수가 딱 하나라도, 해당 괄호를 생략할 수 있다.
```javascript
let sayHello = name => `Hello, ${name}`;
```

<br />

만약, 인수가 없는 함수라면 괄호를 생략할 수 없다.
```javascript
let sayError = () => {
  alert('error!');
}
```

<br />

return문이 있다고 해도 return 전에 여러 줄의 코드가 있는 경우에는 <br />
일반 괄호를 사용할 수 없다.
```javascript
let add = ( num1, num2 )=> {
  const result = num1 + num2;
  return result;
}
```

<br />
<br />
<br />
<br />

# 12. 객체(Object)

* 객체는 중괄호로 작성하고, 키(key)와 값(value)로 구성된 프로퍼티(property)가 들어간다. <br />
* 각 프로퍼티는 쉼표로 구분한다.
* 프로퍼티의 마지막 쉼표는 없어도 되지만 있는 것이 수정/삭제/이동 시 용이하다.
* 객체에 접근/추가하고 싶을 때는 . (온점) 혹은 [ ] (대괄호)를 사용한다.
* 삭제는 'delete' 키워드를 사용하며, 삭제할 프로퍼티 앞에 붙여준다.

<br />

아래는 superman 객체이다
```javascript
const superman = {
  name: 'clark',  //key: name, value: clark
  age: 33,
}

//접근
superman.name //clark
superman['age'] //33

//추가
superman.gender = 'male';
superman['hairColor'] = 'black';

//삭제
delete superman.hairColor;
```

<br />

### 단축 프로퍼티
단축 프로퍼티를 사용하면 보다 간단하게 객체를 작성할 수 있다.

<br />

```javascript
const name = 'clark';
const age = 33;

const superman = {
  name: 'clark',
  age: 33,
  gender: 'male',
}
```
위 코드는 <br />
아래와 같이 단축하여 쓸 수 있다.

```javascript
const name = 'clark';
const age = 33;

const superman = {
  name,  //name: name, 의 축약형
  age,   //age: age, 의 축약형
  gender: 'male',
}
```

<br />

만약 존재하지 않는 프로퍼티에 접근하게 되면 에러가 발생하는게 아니라 <br />
undefined 값이 나온다. 
```javascript
const superman = {
  name: 'clark',
  age: 33,
}

console.log(superman.birthDay); //undefined
```

<br />


이때, in 연산자를 이용하면 프로퍼티 존재여부를 확인할 수 있다.
```javascript
const superman = {
  name: 'clark',
  age: 33,
}

console.log('birthDay' in superman); //false
console.log('age' in superman); //true
```

<br />

점과 대괄호가 아닌 in 을 사용하는 시점은 언제일까? <br />
함수 인자로 받거나 api통신을 통해 데이터를 받아올 때 등 <br />
어떤 값이 나올지 확신할 수 없을 때 사용하면 된다.

<br />

예제1 >
```javascript
function makeObject(name, age) {
  return {
    name,
    age,
    hobby: 'football'
  }
}

const Mike = makeObject('clark', 33);
console.log(Mike); //각 name과 age 값에 위 값이 들어감
```

<br />

예제2 > 나이를 확인하고, 성인인지 아닌지 구분해주는 함수
```javascript
function isAdult(user) {
  if(!('age' in user) || user.age < 20) {
  //user 안에 age가 없거나 age값이 20보다 작을 경우
    return false;
  }
  return true;  //else 생략
}

const Mike = {
  name: 'Mike',
  age: 30,
}

const Julia = {
  name: 'Julia',
}

console.log(isAdult(Mike)); //true
console.log(isAdult(Julia)); //false
```

<br />
<br />

### for ... in 반복문

for ... in 반복문을 사용하면 객체를 순회하면서 값을 얻을 수 있다.
```javascript
const superman = {
  name: 'clark',
  age: 33,
}

for(let key in superman) {  //let key 가 아니라 그냥 key 해도 됨
  console.log(key);  //key값은 name, age
  console.log(superman[key]);
  //superman['name'], superman['age']와 같은 뜻으로 clark, 33 값이 나옴
}
```

<br />
<br />

### method

객체에 함수를 추가하여, 객체 프로퍼티로 할당된 함수를 method 라고 한다.

```javascript
const superman = {
  name: 'clark',
  age: 33,
  fly: function() {  //fly는 superman객체의 method
    console.log('날아갑니다');
  }
}

superman.fly(); //날아갑니다.
```

<br />

또한, 위 코드는 아래와 같이 function 키워드를 생략하여 단축 가능하다.
```javascript
const superman = {
  name: 'clark',
  age: 33,
  fly() { 
    console.log('날아갑니다');
  }
}

superman.fly(); //날아갑니다.
```
<br />

### this
객체와 method의 관계

<br />

method에서는 ${user.name}처럼 객체명을 직접 써주는 것보다 this 사용를 사용하는 것이 좋다.
```javascript
const user = {
  name: 'Mike',
  sayHello() { //sayHello: function() { 
    console.log(`Hello, I'm ${this.name}`);
  }
}

user.sayHello(); //Hello, I'm Mike (점 앞의 user가 sayHello method의 this가 됨)
```
<br />

this는 실행하는 시점 즉, 런타임에 결정된다.
```javascript
let boy = {
  name: 'Mike',
  sayHello() { 
    console.log(`Hello, I'm ${this.name}`);
  },
}

let girl = {
  name: 'Julia',
  sayHello() { 
    console.log(`Hello, I'm ${this.name}`);
  },
}

boy.sayHello(); //Hello, I'm Mike
girl.sayHello(); //Hello, I'm Julia
```
따라서 boy.sayHello()의 this.name은 Mike, <br />
girl.sayHello()의 this.name은 Julia가 되는 것이다.

<br />

화살표 함수는 일반함수와는 달리 자신만의 this를 가지지 않는다.  <br />
화살표 함수 내부에서 this를 사용한다면 그 this는 외부의 값, 전역객체를 가져오므로 <br />
객체의 method를 작성할 때 this를 사용해서 객체에 접근해야 한다면 화살표 함수는 사용하지 않는 것이 좋다. <br />
(참고로, 브라우저 환경에서의 전역객체는 window이고, Node.js 환경에서는 global이 된다.)

<br />
<br />
<br />
<br />

# 13. 배열(Array)

* 배열을 대괄호로 묶고, 쉼표로 구분해서 작성한다.
* 배열을 탐색할 때는 고유번호 index를 사용한다.
* index는 0부터 시작한다.

<br />

```javascript
let students = ['철수', '영희', ... '영수'];

//탐색
console.log(students[0]); //철수

//수정
students[0] = '소연';
console.log(students); //['소연', '영희' ... '영수']
```

<br />

### 배열의 특징

#### 1. 배열은 문자뿐만 아니라 숫자, 객체, 함수 등도 포함할 수 있다.
```javascript
let arr = [
  '민수', //문자
  3, //숫자
  false, //boolean
  {
    name: 'Mike', //객체
    age: 30,
  },
  function() { //함수
    console.log('TEST');  
  }
];
```

<br />

#### 2. length
length는 배열의 길이를 구할 수 있으며, <br />
배열이 가지고 있는 요소의 개수를 반환한다.
```javascript
let students = ['철수', '영희', '영수'];

console.log(students.length); //3
```

<br />

#### 3. 배열이 가지고 있는 method들
- push() : 배열 맨 끝에 요소를 추가해주는 method
```javascript
let days = ['월', '화', '수'];

days.push('목');
console.log(days); //['월', '화', '수', '목']
```  

<br />

- pop() : 배열 맨 끝에 요소를 제거해주는 method
```javascript
let days = ['월', '화', '수'];

days.pop();
console.log(days); //['월', '화']
```  

<br />

- shift(), unshift() : 배열 맨 앞에 제거/추가 해주는 method
```javascript
let days = ['월', '화', '수'];

days.unshift('일');
console.log(days); //['일', '월', '화', '수']

days.shift();
console.log(days); //['월', '화', '수']
```

<br />

+) push와 unshift는 여러 요소를 한번에 추가 가능하다.
```javascript
let days = ['월', '화', '수'];

days.unshift('요일:', '일');
console.log(days); //['요일:', '일', '월', '화', '수']

days.push('목', '금', '토');
console.log(days); //['요일:', '일', '월', '화', '수', '목', '금', '토']
```

<br />

#### 4. 반복문

배열을 쓰는 가장 큰 이유 중 하나는 반복을 위해서이다. <br />
length를 통해 배열의 길이를 알 수 있으므로, for문의 사용이 가능하다.

<br />

- for
```javascript
let days = ['월', '화', '수'];

for(let index = 0; index < days.length; index++) { //index 0~2까지 반복됨
  console.log(days[index]);
}
//월
//화
//수
```

<br />

- for...of
```javascript
let days = ['월', '화', '수'];

for(let day of days) {
  console.log(day);
}
//월
//화
//수
```
배열 days를 돌면서 day 라는 이름으로 요소에 접근할 수 있으며, <br />
for문 보다는 간단하지만 index를 못 얻는다는 단점이 있다.

<br />
<br />
<br />
<br />

# 마치며

사실 처음에는 모두 이미 전에 배웠던 쉬운 것들이라고 생각했는데, 전보다 더 자세하고 확실하게 그리고 새롭게 알게 된 것들이 많아서 좋았다. <br />
중급 강의에서는 지금 배운 것을 토대로 실무에서 사용할 수 있는 각종 실용적인 method 등 이번에 배웠던 것들에 대해 더 깊게 배울 수 있다고 하여 기대가 된다.
