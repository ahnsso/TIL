# 1. 변수

### let, const, var 의 비교

<br />

1. var 는 let 과 달리 한번 선언된 변수를 다시 선언할 수 있다.

```javascript
var name = 'Mike';
console.log(name); //Mike

var name = 'Julia';
console.log(name); //Julia
```
```javascript
let name = 'Mike';
console.log(name); //Mike

let name = 'Julia';
console.log(name); //error!
```

<br />

2. var 는 선언하기 전에 사용할 수 있다.
 
```javascript
console.log(name); //undefined
var name = 'Mike';
```
위 코드는 아래와 같이 동작한다.
```javascript
var name; //hoisting
console.log(name); //undefined
name = 'Mike'; //할당이 처리되는 곳
```
var 로 선언한 모든 변수는 코드가 실제로 이동하지는 않지만, <br />
최상위로 끌어올려진 것처럼 동작하는데 이를 **'호이스팅(hoisting)'** 이라고 한다. <br />
선언은 hoisting 되지만 할당은 hoisting 되지 않기때문에 두번째 줄에서 값은 undefined 이다. 

<br />
hoisting 은 스코프 내부 어디서든 변수 선언은 최상위에 선언된 것 처럼 행동한다는 뜻으로 <br />
let 과 const 도 모두 호이스팅 된다. 

```javascript
console.log(name); //ReferenceError
let name = 'Mike';
```

그런데 let 은 왜 변수 선언 전 사용 시 var 처럼 동작하지 않고, 위처럼 에러가 발생하는 것일까?

<br /> 

그 이유는 바로 **TDZ(Temporal Dead Zone)** 때문이다.

```javascript
console.log(name); //TDZ 영역, 사용불가!
const name = 'Mike'; //함수 선언 및 할당
console.log(name); //사용 가능
```
TDZ 영역에 있는 변수들은 사용이 불가능하며,<br />
let 과 const 는 TDZ 의 영향을 받으므로 할당을 하기 전에는 사용할 수 없다. <br />
이는 코드를 예측 가능하게 하고 잠재적 버그를 줄일 수 있게 한다.

<br />

3. 변수의 생성 과정

* var
```
1. 선언 및 초기화 단계
2. 할당 단계
```
var 는 선언과 초기화가 동시에 진행된다. <br />
그래서 할당 전 호출 시에도 에러를 내지 않고,undefined 가 출력된다.

<br />

* let
```
1. 선언
2. 초기화 단계
3. 할당 단계
```
let 은 선언과 초기화 단계가 분리되어 진행된다. <br />
호이스팅 되면서 선언단계가 이뤄지지만 초기화단계는 실제코드에 도달했을 때 되기 때문에 <br />
위에서 봤던 것처럼 레퍼런스에러가 발생하는 것이다.

<br />

* const
```
1. 선언 + 초기화 + 할당
```
const 는 선언과 할당이 동시에 되어야 한다. <br />
let 과 var 는 선언만 해두고 나중에 할당하는 것을 허용하고, 할당값을 바꿀 수 있기 때문에 어찌 보면 당연한 일이다.

<br />

```javascript
let name;
name = 'Julia';

var age;
age = 28;

const gender; //error 발생, 선언과 동시에 할당하지 않았기 때문
gender = 'female'; 
```

<br />

#### - var : 함수 스코프(function-scoped)

#### - let, const : 블록 스코프(block-scoped) 

블록 스코프란, 모든 코드블록 내에서 선언된 변수는 코드블록 내에서만 유효하며 외부에서는 접근할 수 없다는 의미이다. <br />
즉, 코드불록 내부에서 선언한 변수는 지역변수이고, <br />
여기서 말하는 코드 블록은 함수, if문, for문, while문, try/catch문 등을 의미한다. 

<br />

예시 >>>

```javascript
const age = 28;

if(age > 19) {
  var txt = '성인';
}

console.log(txt); //성인
```
위 코드처럼 if문 안에서 var 로 선언한 변수는 if문 밖에서도 사용 가능하다. <br />
그러나 if문 안의 let, const 는 if문 밖에서 사용 불가능하며, 이를 블록 스코프라고 하는 것이다.

<br />

```javascript
function add(num1 + num2) {
  var result = num1 + num2;
}

add(2,3);

console.log(result); // error 발생
```
var 도 함수 안에서 선언했을 경우에는 함수 밖에서 사용 불가능하다. <br />
var 가 유일하게 벗어날 수 없는 스코프가 함수이다.

<br />

예측 가능한 결과를 내고, 버그를 줄일 수 있는 let, const 사용을 권장한다.

<br />
<br />
<br />
<br />

# 2. 생성자 함수

개발 시 회원, 상품 등과 같이 비슷한 객체를 여러개 만들어야할 때 사용하는 것이 생성자 함수이다. 

<br />

생성자 함수는 보통 첫글자를 **대문자**로 함수를 만들며, <br />
**new** 연산자를 사용하여 호출한다.

```javascript
function User(name, age) {
  this.name = name;
  this.age = age;

  this.sayName = function() {
      console.log(this.name);
  }
}

let user1 = new User('Mike', 30);
let user2 = new User('Julia', 28);

let user3 = User('Tom', 23);
console.log(user3); //undefined (new를 붙이지 않았기 때문)

let user4 = new User('Ahn', 20);
user4.sayName(); //Ahn
```

<br />
<br />
<br />
<br />

# 3. Object - methods / Computed property

### Computed property

```javascript
let a = 'age';

const user = {
  name : 'Mike',
  [a] : 30 //age : 30
}
```

이처럼 대괄호[ ] 로 묶어줄 경우 a라는 문자열이 아니라 변수 a에 할당된 값이 들어가며, <br />
이를 Computed property(계산된 프로퍼티) 라고 부른다.

<br />

```javascript
const user = {
  [1 + 4] : 5,
  ["안녕" + "하세요"] : "Hello"
}

console.log(user); //{ 5: 5, 안녕하세요: "Hello" }
```
위처럼 식 자체를 넣는 것도 가능하다.

<br />

예제 > 

```javascript
function makeObj(key, val) {
  return {
    [key]: val,
  };
}

const obj makeObj("성별", "female");

console.log(obj); //{성별: "female"}
```

<br />

어떤 게 key값이 될지 모르는 객체를 만들 때 유용하다.

<br />
<br />

### 객체에서 사용할 수 있는 몇가지 메소드


**1. Object.assign() : 객체 복제**

```javascript
const user = {
  name : 'Mike',
  age : 30
}

const cloneUser = user; //cloneUser와 user를 하나의 객체로 판단하므로 정상적인 복제가 아님
cloneUser.name = "Tom";

console.log(cloneUser); //{name: 'Tom', age: 30 }
console.log(user);  //{name: 'Tom', age: 30 }, user의 name까지 전부 Tom으로 변경됐음
```

<br />


```javascript
const user = {
  name : 'Mike',
  age : 30
}

const newUser = Object.assign({}, user);
                      //빈객체 {}는 초기값이며, 두번째 매개변수 user의 객체들이 초기값에 병합되며 동일하게 복제가능
newUser.name = "Tom";

console.log(newUser); //{name: 'Tom', age: 30 }
console.log(user);  //{name: 'Mike', age: 30 }, user의 name이 여전히 Mike로 정상적으로 복제 완료
```
newUser != user

<br />

만약, 초기값에 성별값을 넣으면 user의 객체들이 병합되어 총 3개의 프로퍼티를 갖게 된다.

```javascript
const user = {
  name : 'Mike',
  age : 30
}

const newUser = Object.assign({ gender: 'male' }, user);
console.log(newUser); //{ gender: 'male', name: 'Mike', age: 30 }
```

<br />

또한, 병합 시 key값이 같으면 덮어쓰여 진다.

```javascript
const user = {
  name : 'Mike',
  age : 30
}

const newUser = Object.assign({ name: 'Tom' }, user);
console.log(newUser); //{ name: 'Mike', age: 30 } //덮어써져서 Tom이 아닌 Mike
```

<br />

두 개 이상의 객체도 병합 가능하다.

```javascript
const user = {
  name : 'Mike'
}

const info1 = {
  age : 30
}

const info2 = {
  gender : 'male'
}

const newUser = Object.assign(user, info1, info2);
console.log(newUser);  //{ name: 'Mike', age: 30, gender: 'male' }
```

<br />
<br />

**2. Object.keys() : 키 배열 반환**

```javascript
const user = {
  name : 'Mike',
  age : 30,
  gender : 'male',
}

console.log( Object.keys(user) ); //["name","age","gender"]
```
키를 배열로 만들어 반환한다.

<br />

**3. Object.values() : 값 배열 반환**

```javascript
const user = {
  name : 'Mike',
  age : 30,
  gender : 'male',
}

console.log( Object.values(user) ); //["Mike",30,"male"]
```
값을 배열로 만들어 반환한다.


<br />

**4. Object.entries() : 키,값 모두 배열 반환**

```javascript
const user = {
  name : 'Mike',
  age : 30,
  gender : 'male',
}

console.log( Object.entries(user) ); //[ ["name","Mike"], ["age",30], ["gender","male"] ]
```
키와 값 모두를 배열로 만들어 반환한다.


<br />

**5. Object.fromEntries() : 키, 값 배열을 모두 객체로**

```javascript
const arr =
[
  ["name","Mike"],
  ["age",30],
  ["gender","male"]
];

console.log( Object.fromEntries(arr) ); //{ name: 'Mike', age: 30, gender: 'male' }
```
키와 값을 쌍으로 묶은 배열을 객체로 만들어 반환한다.

<br />
<br />
<br />
<br />

# 4. 심볼(Symbol)

### 객체의 property key

#### 1. 문자형

```javascript
const obj = {
  1: '1입니다.',
  false: '거짓'
}

console.log( Object.keys(obj) ); //["1", "false"] => key를 숫자형 1과 불린형 false로 만들어도 문자형으로 반환됨

console.log(obj['1']);  //"1입니다." => 값 출력 시에도 문자열로 접근 가능 (obj[1] 또는 obj[false]도 가능)
console.log(obj['false']); //"거짓"
```

<br />

#### 2. 심볼형 : 유일성 보장

```javascript
const a = Symbol(); //new를 붙이지 않는다.
const b = Symbol(); 

console.log(a); //Symbol()
console.log(b); //Symbol()

console.log(a===b); //false
console.log(a==b); //false
```
위 코드를 보면 Symbol()로 같아보이지만 일치연산자와 동등연산자로 확인 시 false가 나온다. <br />
이를 통해 Symbol 은 **유일한 식별자**를 만들 때 사용한다는 것을 알 수 있다.

<br />

```javascript
const id = Symbol('id'); //설명 또는 이름 삽입
```
Symbol 뒤 괄호 안에 문자열로 설명을 넣어줄 수 있으며, 디버깅 시 도움이 된다. <br />
또한, 이 문자열은 심볼 생성에 어떠한 영향도 미치지 않는다. <br />
그리고 변수이름.description; 을 통해 설명(이름)을 알 수 있다.

<br />

```javascript
const id = Symbol('id');

const user = {
  name : 'Mike',
  age : 30,
  [id] : 'myid'
}

console.log(user); //{ name: 'Mike', age: 30, Symbol(id): 'myid' }
console.log(user[id]); //"myid"

console.log(id.description); //'id'


//아래 메소드들 또는 for..in문 사용하는 경우, key가 심볼형인 프로퍼티일 때 값을 출력하지 않고 건너뜀
Object.keys(user);  //["name", "age"]
Object.values(user); //["Mike", 30]
Object.entries(user); //[["name","Mike"], ["age",30]]
```

<br />

그렇다면 심볼형은 어디에 사용가능할까?

<br />

특정 객체의 원본데이터는 건드리지 않고, 속성을 추가할 수 있다. 
```javascript
const user = {
  name : 'Mike',
  age : 30,
}

const id = Symbol('id');
user[id] = 'myid';
```

<br />

```javascript
user.name = 'myname' //덮어쓰기 때문에 사용하면 안됨 X
user.a_key_no_one_used = 'hahaha'; //X
```
Symbol형을 쓰는 이유는 위 코드처럼 다른 사람이 만들어 놓은 객체에 자신만의 속성을 추가해서 덮어써버리면 안되기 때문에 이런 경우 사용한다.

<br />

숨겨진 Symbol key 보는 법은 Object.getOwnPropertySymbols() 이다. <br />
또한, Reflect.ownKeys()는 Symbol key를 포함한 객체의 모든 key 를 보여준다.

```javascript
const id = Symbol('id');

const user = {
  name : 'Mike',
  age : 30,
  [id] = 'myid'
}

console.log( Object.getOwnPropertySymbols(user) ); //[Symbol(id)]
console.log( Reflect.ownKeys(user) ); //["name","age",Symbol(id)]
```

그러나 대부분의 라이브러리, 내장함수 등은 위와 같은 메소드를 사용하지 않는다. 
그러므로 유일한 프로퍼티를 추가하고 싶을 때 Symbol을 사용하면 된다.

<br />

예제 >  

```javascript
// 다른 개발자가 만들어 놓은 객체
const user = {
  name : 'Mike',
  age : 30,
}

// 내가 작업
const showName = Symbol('show name');
user[showName] = function () {
  console.log(this.name);
};

user[showName](); //Mike

//사용자가 접속하면 보는 메세지
for(let key in user) {
  console.log('His ${key} is ${user[key]}.');
}
  //His name is Mike.
  //His age is 30.
```

<br />

원래 있던 코드에 같은 이름의 메소드가 있었는지, 다른 사람의 프로퍼티를 덮어쓰지는 않을지 걱정하지 않아도 되는 것이 Symbol을 쓰는 장점이다.

<br />

#### 3. Symbol.for() : 전역 심볼

심볼은 이름이 같더라도 모두 다른 존재이다. <br />
그런데 가끔 전역변수처럼 이름이 같으면 같은 객체를 의미해야 할 때가 있는데, <br />
이럴 때 사용가능한 것이 바로 Symbol.for() 이다.

* 없으면 만들고, 있으면 가져오기 때문에 **하나**의 심볼만 보장받을 수 있다.
* Symbol함수는 매번 다른 Symbol값을 생성하지만, Symbol.for 메소드는 하나를 생성한 뒤 키를 통해 같은 Symbol을 **공유**한다.
* Symbol.for()은 전역심볼이라고 부르며, 코드 어디에서든 사용가능하다.
* 이름을 얻고 싶을 때는 Symbol.keyFor()을 사용하면 된다.

```javascript
const id1 = Symbol.for('id'); 
const id2 = Symbol.for('id'); 

console.log(id1===id2); //true, 심볼형때와 다르게 동일함

console.log(Symbol.keyFor(id1)); //'id'
```

<br />
<br />
<br />
<br />

# 5. 숫자, 수학 method (Number, Math)

### toString()

* 이 메소드는 숫자를 문자로 바꿔준다.
* 괄호 안의 숫자를 쓰면 그 숫자의 진법으로 변환한다.

<br />

10진수 -> 2진수/16진수

```javascript
let num = 10;

num.toString(); //"10"
num.toString(2); //"1010", 2진법 변환

let num2 = 255;

num.toString(16); // "ff"
```

<br />

### Math

* 수학과 관련된 메소드

```javascript
//대표적인 예시 - 파이의 원주율값

Math.PI; //3.141592653589793
```

<br />

#### Math.ceil() : 올림

```javascript
let num1 = 5.1;
let num2 = 5.7;

Math.ceil(num1); //6
Math.ceil(num2); //6
```

<br />

#### Math.floor() : 내림

```javascript
let num1 = 5.1;
let num2 = 5.7;

Math.floor(num1); //5
Math.floor(num2); //5
```

<br />

#### Math.round() : 반올림

```javascript
let num1 = 5.1;
let num2 = 5.7;

Math.round(num1); //5
Math.round(num2); //6
```

<br />

#### Math.random() : 랜덤 숫자 생성

0 ~ 1 사이 무작위 숫자 생성

```javascript
Math.random(); //0.8975219182702923
Math.random(); //0.589014415306562
Math.random(); //0.46728718498026933
...
```

<br />

만약, 1 ~ 100 사이 임의의 숫자를 뽑고 싶다면?
```javascript
//곱한 수까지 중의 하나를 뜻함 = 100까지 숫자 중 하나, 버림을 했을 때 0이 나올 것을 대비하여 +1
Math.floor( Math.random() * 100 ) + 1;

//1 ~ 5까지 임의의 숫자뽑기
Math.floor( Math.random() * 5 ) + 1;

//0 ~ 100 일 경우, +1 빼주기
Math.floor( Math.random() * 100 );
```

<br />

#### Math.max() / Math.min() : 최대값, 최소값

괄호 안의 인수들 중 최대값, 최소값을 구한다.

```javascript
Math.max(1, 4, -1, 5, 10, 9, 5.54); //10

Math.min(1, 4, -1, 5, 10, 9, 5.54); //-1
```

<br />

#### Math.abs() : 절대값

abs 는 absolute 의 약자로 절대값을 구한다.

```javascript
Math.abs(-1); //1
Math.abs(-3); //3
```

<br />

#### Math.pow(n, m) : 제곱

n의 m승값, 즉 거듭제곱값을 구한다.

```javascript
Math.pow(2, 10); //1024, 2의 10승
Math.pow(5, 3); //125, 5의 3승
```

<br />

#### Math.sqrt() : 제곱근

sqrt 는 square root의 약자로, 제곱근을 구해준다.

```javascript
Math.sqrt(16); //4, 루트16 = 4를 제곱해서 얻은 값 16
Math.sqrt(144); //12
```

<br />

### 소수점 자릿수 : toFixed()

예를 들어,소수점 **둘째자리**까지 표현해야 하는 경우 (소수점 셋째 자리에서 반올림) <br />
100을 곱하고 반올림을 해준 뒤, 다시 100으로 나눠줘도 되지만, <br />
toFixed()를 사용해도 된다. 

<br />

toFixed() 괄호 안의 숫자를 소수점 이하 갯수에 반영하므로 훨씬 간단하다.

```javascript
let userRate = 30.1234;

Math.round(userRate * 100)/100 //30.12
userRate.toFixed(2); //"30.12"

userRate.toFixed(0); //"30"

userRate.toFixed(6); //"30.123400", 원래 소수점자리갯수보다 많으면 0으로 채워줌
```

toFixed()는 문자열을 반환하기 때문에 주의해야 한다. <br />
그래서 반환받은 이후 Number로 변환해 작업하는 경우가 많다.

<br />

### isNaN()

* NaN은 잘못된 입력으로 인해 계산을 할 수 없음을 나타내는 기호이다.
* isNaN은 NaN인지 아닌지 판단한다.
* 판단은 동등연산자, 일치연산자 모두 불가능하며 오직 isNaN만이 NaN인지 아닌지 판단할 수 있다.

```javascript
let x = Number('x'); //NaN

//정상적인 판단 불가능
x == NaN //false
x === NaN //false
NaN == NaN //false

//정상적인 판단
isNaN(x); //true
isNaN(3); //false
```

<br />

### parseInt()

* parseInt()는 문자열을 숫자로 바꿔준다.
* Number 와 다른 점은 문자가 혼용되어 있어도 동작한다는 점이다.
* 소수점 이하는 무시하고 정수만 반환한다.

```javascript
let margin = '10px';

parseInt(margin); //10
Number(margin); //NaN
```

* parseInt는 읽을 수 있는 부분까지 읽다가 문자를 만나면 숫자를 반환하기 때문에
  숫자로 시작하지 않으면 NaN 을 반환한다.
* 그러나 두번째 인수를 받아서 진수를 지정할 수도 있다.

```javascript
let redColor = 'f3';

parseInt(redColor); //NaN
parseInt(redColor, 16); //245, f3을 16진수로 읽고 10진수로 변환한 값

parseInt('11', 2); //3, 문자열 11을 2진수로 받아 10진수로 변환한 값
```

<br />

### parseFloat()

* parseInt()와 동일하게 동작하지만 **부동 소수점**을 반환한다.

```javascript
let padding = '18.5%';

parseInt(padding); //18
parseFloat(padding); //18.5
```
