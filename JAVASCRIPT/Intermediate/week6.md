# 9. 클로저 (Closure)

자바스크립트는 어휘적 환경(Lexical Environment)을 갖는다.

```javascript
let one;
one = 1;

function addOne(num) {
  console.log(one + num);
}

addOne(5); //6
```  
코드가 실행되면 스크립트 내에서 선언된 변수들이 Lexical 환경에 올라간다. <br />
처음 let으로 선언된 변수 one도 호이스팅되지만 초기화는 되지 않으므로 사용불가하다. <br />
let one;에 값이 아직 할당되지 않아 undefined 값을 가지면 사용가능해진다. 

<br />

그에 비해 함수선언문 addOne은 변수와 달리 바로 초기화되어 사용가능하다. <br />

```
전역 Lexical 환경

one: 1
addOne: function
``` 

```
내부 Lexical 환경

num: 5
``` 

위 코드에서 one과 num의 값은 내부 Lexical 환경에서 먼저 찾고, 없을 경우 외부로 넓혀서 전역 Lexical 환경에서 찾는다. <br />
따라서, 1 + 5 = 6

```javascript
function makeAdder(x) {
  return function(y) { //이 함수는 자신이 y를 가지고 있고, 상위함수인 makeAdder의 매개변수인 x에 접근 가능
    return x+y;
  }
}

const add3 = makeAdder(3);
console.log(add3(2)); //5, add3함수가 생성된 이후에도 상위함수는 makeAdder의 x에 접급 가능

const add10 = makeAdder(10);
console.log(add10(5));
console.log(add3(1));
```

<br />

위와 같은 것을 Closure이라고 한다.
* 함수와 렉시컬 환경의 조합
* 함수가 생성될 당시의 외부 변수를 기억하고, 생성된 이후에도 계속 접근 가능

```javascript
function makeCounter() {
  let num = 0;

  return function() { 
    return num++;
  }
}

let counter = makeCounter();

console.log(counter()); //0
console.log(counter()); //1
console.log(counter()); //2,오직 counter로 증가시키고 반환하므로 숫자 변경 불가능함.
```

<br />
<br />
<br />
<br />

# 10. setTimeout / setInterval

-setTimeout : 일정시간이 지난 후 함수 실행 <br />
-setInterval : 일정시간 간격으로 함수 반복

<br />

### setTimeout
* 두 개의 매개변수로 받는다.
```javascript
function fn() {
  console.log(3);
}

setTimeout(fn, 3000); //3000=3s, 3초 후 로그찍음
```
위 코드는 아래와도 같다.
```javascript
setTimeout(function() {
  console.log(3);
},3000);
```

<br />

* 인수가 필요하다면 시간 뒤에 적어준다.
```javascript
function showName(name) {
  console.log(name);
}

setTimeout(showName, 3000, 'Mike'); //setTimeout(함수, 시간, 인수);, Mike는 showName(name)의 첫번째 인수로 전달됨
```

<br />

* clearTimeout 은 예정된 작업을 없앤다.
```javascript
const tId = function showName(name) {
  console.log(name);
}

setTimeout(showName, 3000, 'Mike');

clearTimeout(tId); //3초 지나기 전에 이 코드가 실행되기 때문에 아무일도 일어나지 않음
```

<br />

* 주의사항: dalay 시간을 = 0으로 주어도 바로 실행되지 않는다.
```javascript
setTimeout(function() {
  console.log(2);
}, 0);

console.log(1);
//1
//2
```
1이 먼저 찍히고, 2가 나중에 찍힌다. <br />
이유는 현재 실행 중인 스크립트가 종료된 이후 스케줄링 함수 실행되기 때문이다. <br />
또한, 브라우저는 기본 4ms~ 정도의 대기 시간이 있다.

<br />

### setInterval
* 한번 수행하고 끝나는게 아니라 반복 수행된다.
* 중간에 중단하려면 claerInterval 사용
```javascript
function showName(name) {
  console.log(name);
}

const tId = setInterval(showName, 3000, 'Mike'); //3초마다 Mike 반환
```
```javascript
clearInterval(tId); //중단
```

<br />

-접속시간 알림
```javascript
let num = 0;

function showTime() {
  console.log('안녕하세요. 접속하신지 ${num++}초가 지났습니다.');
}

setInterval(showTime, 1000); //1초에 한번씩 메세지 반환
```
+) 5초까지만 보여주고 싶다면
```javascript
let num = 0;

function showTime() {
  console.log(`안녕하세요. 접속하신지 ${num++}초가 지났습니다.`);
  if(num > 5) {
    clearInterval(tId);
  }
}

const tId = setInterval(showTime, 1000);
```

<br />
<br />
<br />
<br />

# 11. call, apply, bind
함수의 this 값 지정

### call
: call 메서드는 모든 함수에서 사용할 수 있으며, this를 특정값으로 지정할 수 있다. 
```javascript
const mike = {
  name: 'Mike',
};

const tom = {
  name: 'Tom',
};

function showThisName() {
  console.log(this.name); //this.name = window.name
};

showThisName(); //window.name이 비어있기때문에 아무것도 출력되지 않음
showThisName.call(mike); //Mike, 함수호출하면서 call을 사용하고 this로 사용할 객체 mike를 넘기면 해당 함수가 주어진 객체의 메서드인 것처럼 사용 가능
showThisName.call(tom); //Tom
```

<br />
+) call - update 

```javascript
const mike = {
  name: 'Mike',
};

const tom = {
  name: 'Tom',
};

function showThisName() {
  console.log(this.name);
};

function update(birthYear, occupation) {
  this.birthYear = birthYear;
  this.occupation = occupation;
};

update.call(mike, 1999, 'singer');
console.log(mike); //{name: 'Mike', birthYear: 1999, occupation: 'singer'}

update.call(tom, 2002, 'teacher');
console.log(tom); //{name: 'Tom', birthYear: 2002, occupation: 'teacher'}
```

<br />

### apply
: apply는 함수매개변수를 처리하는 방법을 제외하면 call과 완전히 같다. <br />
call은 일반적인 함수와 마찬가지로 매개변수를 직접 받지만, apply는 매개변수를 **배열**로 받는다.

```javascript
const mike = {
  name: 'Mike',
};

const tom = {
  name: 'Tom',
};

function showThisName() {
  console.log(this.name);
};

function update(birthYear, occupation) {
  this.birthYear = birthYear;
  this.occupation = occupation;
};

update.apply(mike, [1999, 'singer']); //매개변수를 배열로 받는 것만 다르고 결과값은 같음
console.log(mike); //{name: 'Mike', birthYear: 1999, occupation: 'singer'}

update.apply(tom, [2002, 'teacher']);
console.log(tom); //{name: 'Tom', birthYear: 2002, occupation: 'teacher'}
```
apply는 배열요소를 함수매개변수로 사용할 때 유용하다.

<br />

```javascript
const nums = [3, 10, 1, 6, 4];
const minNum = Math.min(...nums);
const maxNum = Math.max(...nums);

console.log(minNum); //1
console.log(maxNum); //10
```
위 코드를 apply를 사용한 코드로 바꿔보면 아래와 같다.

```javascript
const nums = [3, 10, 1, 6, 4];
//const minNum = Math.min(...nums);
//const maxNum = Math.max(...nums);

const minNum = Math.min.apply(null, nums); //null 자리는 this로 사용될 값인데 Math.min과 Math.max 메소드는 딱히 this가 필요하지 않으므로 아무값이나 넣어줌
          // = Math.min.apply(null, [3, 10, 1, 6, 4]);

//const maxNum = Math.max.apply(null, nums);
//만약 call을 사용한다면
const maxNum = Math.max.call(null, ...nums);

console.log(minNum); //1
console.log(maxNum); //10
```
apply는 두번째 매개변수로 배열을 전달하며 그 요소들을 차례대로 인수로 사용한다. <br />
call과 apply는 동작방식은 같고, 매개변수를 받는 방식만 다르다. <br />
call은 순서대로 직접받고, apply는 배열상태로 받는다.

<br />

### bind
: bind를 사용하면 함수의 this 값을 영구히 바꿀 수 있다.

<br />

아까 봤던 update를 이리저리 옮기면서 호출할 때 this 값은 항상 'Mike'가 되게끔 하기위해 bind 사용
```javascript
const mike = {
  name: 'Mike',
};

function update(birthYear, occupation) {
  this.birthYear = birthYear;
  this.occupation = occupation;
};

const updateMike = update.bind(mike); //이 함수는 Mike를 항상 this로 받음

updateMike(1980, 'police');
console.log(mike); //{name: 'Mike', birthYear: 1980, occupation: 'police'}
```

<br />

```javascript
const user = {
  name: 'Mike',
  showName: function() {
    console.log(`Hello, ${this.name}`);
  },
};

user.showName(); //Hello, Mike

let fn = user.showName;

fn(); //Hello,
//메소드는 user.showName()의 점 앞에 있는 user가 this인데, fn만 호출하므로 이름이 없이 나온다.

//call과 apply사용
fn.call(user); //Hello,Mike
fn.apply(user); //Hello,Mike

//bind사용
let boundFn = fn.bind(user);

boundFn(); //Hello, Mike
```

<br />
<br />
<br />
<br />

# 12. 상속, 프로토타입(Prototype)

### 프로토타입
* hasOwnProperty : 객체에 자신이 프로퍼티를 가지고 있는지 확인하는 메소드 
```javascript
const user = {
  name: 'Mike'
};

user.hasOwnProperty('name'); //true
user.hasOwnProperty('age'); //false
```
그런데 hasOwnProperty는 만든 적이 없는데 어디 있는걸까? <br />
바로 __proto__라는 객체가 있는데 이것을 프로토타입이라고 한다. <br />
일단 객체에서 property를 읽으려고 하는데 없으면 여기서 찾는다. 

<br />

그럼 만약 hasOwnProperty가 객체 안에 있으면 어떻게 될까?
```javascript
const user = {
  name: 'Mike',
  hasOwnProperty : function(){
      console.log('haha');
  }
};

user.hasOwnProperty(); //haha
```
방금 만든 메소드로 동작한다. <br />
이유는 객체에 property가 있으면 거기서 탐색을 멈추기 때문이다. <br />
없을때만 프로토타입에서 property를 찾는다.

<br />

### 상속
프로토타입이 어떻게 동작하는지 보기 위해서 상속이라는 개념을 이용해 보자.

<br />

wheels와 drive같이 공통된 부분을 어떻게  처리할 수 있을까? 
```javascript
const bmw = {
  color: 'red',
  wheels: 4,
  navigation: 1,
  drive() {
      console.log('drive..');
  },
};

const benz = {
  color: 'black',
  wheels: 4,
  drive() {
      console.log('drive..');
  },
};

const audi = {
  color: 'blue',
  wheels: 4,
  drive() {
      console.log('drive..');
  },
};
```
방금 살펴봤던 __proto__로 해결할 수 있다.
```javascript
//car라는 상위개념의 객체 생성
const car = {
  wheels: 4,
  drive() {
      console.log('drive..');
  },
};

const bmw = {
  color: 'red',
  navigation: 1,
};

const benz = {
  color: 'black',
};

const audi = {
  color: 'blue',
};

//car를 차들의 프로토타입으로 만들기 위해, 차들을 car의 상속을 받게 함.
bmw.__proto__ = car; //bmw.wheels는 4로 __proto__에서 찾을 수 있게 됨
benz.__proto__ = car;
audi.__proto__ = car;
```

<br />

상속은 계속 이어질 수 있다.
```javascript
//car라는 상위개념의 객체 생성
const car = {
  wheels: 4,
  drive() {
      console.log('drive..');
  },
};

const bmw = {
  color: 'red',
  navigation: 1,
};

bmw.__proto__ = car;

const x5 = {
  color: 'white',
  name: 'x5',
};

x5.__proto__ = bmw; //x5.navigation은 1

for(p in x5) {
  console.log(p);
};
//color
//name
//navigation
//wheels
//drive
```
car - bmw - x5 로 이어지는 상속 <br />
이것을 **Prototype Chain** 이라고 한다.

<br />

```javascript
Object.keys(x5); //(2) ['color', 'name']
Object.values(x5); //(2) ['white', 'x5']
```
값과 관련된 객체 내 메소드는 상속된 property는 나오므로, 잘 구분해서 사용해야 한다.

<br />

만약, for in 문에서 구분하고 싶다면 hasOwnProperty를 사용한다.
```javascript
for(p in x5) {
  if(x5.hasOwnProperty(p)) {
      console.log('O', p);
  } else {
      console.log('X', p);
  }
};

//O color
//O name
//X navigation
//X wheels
//X drive
```

<br />

### 생성자 함수

```javascript
const car = {
  wheels: 4,
  drive() {
      console.log('drive..');
  },
};

const Bmw = function(color) {
  this.color = color;
};

const x5 = new Bmw('red');
const z4 = new Bmw('blue');

x5.__proto__ = car;
z4.__proto__ = car;
```
위 코드에서 생성자 함수를 이용하면 비슷한 객체들을 간단하게 만들 수 있다.
```javascript
const Bmw = function(color) {
  this.color = color;
};

//생성자함수가 생성하는 객체에 __proto__를 wheel과 drive 로 설정한다는 의미
Bmw.prototype.wheels = 4;
Bmw.prototype.drive = function() {
      console.log('drive..');
};

//생성자함수 추가 
Bmw.prototype.navigation = 1;
Bmw.prototype.stop = function() {
      console.log('STOP!');
};

const x5 = new Bmw('red');
const z4 = new Bmw('blue');

x5.wheels; //4
z4.drive(); //drive...
x5.stop(); //STOP!
```
생성자함수 작업을 한번만 해준다면 생성자로 만들어진 모든 객체에 일일이 .__proto__작업을 해줄 필요가 없어지므로 중복코드를 줄일 수 있다. 

<br />

생성자함수가 새로운 객체를 만들어낼 때 그 객체는 생성자의 instance라고 불려진다. <br />
자바스크립트에는 이를 편리하게 확인할 수 있는 instanceof 연산자가 있다. <br />
instanceof를 이용해서 객체와 생성자를 비교할 수 있고 이는 해당객체가 그 생성자로부터 생성된 것인지를 판단하여 true 혹은 false를 반환한다.

#### instanceof
```javascript
const Bmw = function(color) {
  this.color = color;
};

//생성자함수가 생성하는 객체에 __proto__를 wheel과 drive 로 설정한다는 의미
Bmw.prototype.wheels = 4;
Bmw.prototype.drive = function() {
      console.log('drive..');
};

//생성자함수 추가 
Bmw.prototype.navigation = 1;
Bmw.prototype.stop = function() {
      console.log('STOP!');
};

const x5 = new Bmw('red');
const z4 = new Bmw('blue');

z4 instanceof Bmw; //true
```
생성자로 만들어진 instance 객체에는 constructor라는 프로퍼티가 존재한다.
constructor는 생성자를 가르킨다.
```javascript
z4.constructor === Bmw;
//true
```

<br />

생성자함수 생성을 더 깔끔하게 아래와 같이 프로토타입을 한번에 덮어쓰면 constructor가 사라진다.
```javascript
const Bmw = function(color) {
  this.color = color;
};

//Bmw.prototype.wheels = 4;
//Bmw.prototype.drive = function() {
//      console.log('drive..');
//}; 
//Bmw.prototype.navigation = 1;
//Bmw.prototype.stop = function() {
//      console.log('STOP!');
//};

Bmw.prototype = {
  wheels: 4,
  drive() {
      console.log('drive..');
  },
  navigation: 1,
  stop() {
      console.log('STOP!');
  },
};

const x5 = new Bmw('red');
const z4 = new Bmw('blue');

x5.constructor === Bmw;
//false
```
따라서 이런 현상을 방지하기 위해 하나씨가 프로퍼타입을 추가하는게 좋은 방법이고, <br />
아니면  아래와 같이 수동으로 constructor를 명시하는 방법도 있다.
```javascript
Bmw.prototype = {
  constructor: Bmw,
  wheels: 4,
  drive() {
      console.log('drive..');
  },
  navigation: 1,
  stop() {
      console.log('STOP!');
  },
};
```
이렇듯 자바스크립트는 명확한 constructor를 보장하지는 않는다. <br />
개발자에 의해서 언제든지 수정될 수 있다는 점을 염두해두자.

<br />

### getColor
지금까지 본 예제들에서는 차의 색상을 아무나 바꿀 수 있었지만 클로저를 이용해서 방지할 수 있다.
```javascript
const Bmw = function(color) {
  const c = color;
  this.getColor = function() {
    console.log(c);
  };
};

const x5 = new Bmw('red');

x5.getColor(); //red
```
getColor함수가 생성될 당시의 context를 기억하므로 <br />
초기에 세팅한 색상값을 얻을 수만 있고 바꿀 수 있는 방법은 없다.
