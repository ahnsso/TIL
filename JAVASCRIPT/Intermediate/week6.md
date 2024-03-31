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

#### setTimeout
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
