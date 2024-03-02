# 6. 비교 연산자, 조건문(if, else, else if)

### 비교 연산자

* = 한 개는 할당, == 두 개는 같다(동등 연산자), != 는 다르다 는 뜻을 가지며, <br />
  반환값은 boolean 형으로 true or false 이다.

<br />

```javascript
console.log(10 > 5); //true
console.log(10 == 5); //false
console.log(10 != 5); //true
```

<br />

* 동등 연산자(==)의 경우 type 까지는 비교하지 않기 때문에 정확성을 위하여 <br />
  일치 연산자(===)를 사용해 주는 것이 좋다.
  
<br />

```javascript
const a = 1;
const b = "1";

console.log(a == b); //true
console.log(a === b); //false
```

<br />

### 조건문

* 조건문은 어떤 조건에 따라 이후 행동이 달라지게 만들어 주는 역할이다.
* if문 - 괄호 안에 들어가는 조건을 평가해서 true일 경우 실행된다.
* else절 - if문의 조건이 false일 경우 실행된다.

<br />

```javascript
const age = 30;

if(age > 19) {
  console.log("환영합니다.");
}
if(age <= 19) {
  console.log("안녕히 가세요.");
}
```

위 코드를 if 와 else 를 사용하여 간단하게 적을 수 있다.
```javascript
const age = 30;

if(age > 19) {
  console.log("환영합니다.");
} else {
  console.log("안녕히 가세요.");
}

//환영합니다.
```

+) 추가 요구사항 - 19살일 경우 수능 잘치세요 라는 문구를 보여주세요.
```javascript
const age = 19;

if(age > 19) {
  console.log("환영합니다.");
} else if(age === 19) {
  console.log("수능 잘치세요.");
} else {
  console.log("안녕히 가세요.");
}

//수능 잘치세요.
```

<br />
<br />
<br />
<br />

# 7. 논리 연산자(AND, OR, NOT)

### ||(OR)

* 여러개 중 하나라도 true 면 true, <br />
  즉, 모든 값이 false 일 때만 false 반환한다.
* OR 는 첫번째 ture 를 발견하는 즉시 평가를 멈춘다.

<br />

이름이 Tom 이거나, 성인이면 통과
```javascript
const name = "Mike";
const age = 30;

if(name === "Tom" || age > 19 ) {
  console.log("통과");
}

//통과
```

<br />

### &&(AND)

* 여러개 중 하나라도 false 면 false, <br />
  즉, 모든 값이 true 일 때만 true 반환한다.
* AND 는 첫번째 false 를 발견하는 즉시 평가를 멈춘다.

<br />

이름이 Tom 이고, 성인이면 통과
```javascript
const name = "Mike";
const age = 30;

if(name === "Tom" && age > 19 ) {
  console.log("통과");
} else {
  console.log("통과X");
}

//통과X
```

<br />

### !(NOT)

* true 면 false, false 면 true <br />
  반대값으로 바꿔서 반환한다.

<br />

나이를 입력받아 성인이 아닐 경우 통과X
```javascript
const age = prompt("나이를 입력하세요.");
const isAdult = age > 19;

if(!isAdult) {
  console.log("통과X");
}

//미성년 나이를 입력한 경우 통과X
```

<br />

## 우선순위


### 적은 확률의 순서대로 평가해 주는 것이 시간단축과 성능 최적화에 도움을 준다. <br />
ex) 운전면허가 있고 시력이 좋은 여군 <br />
운전면허(전체 군인의 80%) / 좋은 시력(전체 군인의 60%) / 여군(전체 군인의 7%) <br />
=> '여군인데 시력이 좋고 운전면허가 있는 사람' 으로 조건의 순서를 조정

<br />

### AND 가 OR 보다 우선순위 높다.

남자이고, 이름이 Mike 이거나 성인이면 통과
```javascript
const gender = "F";
const name = "Julia";
const isAdult = true;

if(gender === "M" && (name === "Mike" || isAult)) { 
  console.log("통과");
} else {
  console.log("통과X");
}

//통과X
```

<br />
<br />
<br />
<br />

# 8. 반복문(for, while, do while) 

반복문 loop 동일한 작업을 여러번 반복할 수 있다.

### for
* for문은 세미콜론으로 구분하며 세부분으로 나눌 수 있다.
* 초기값을 지정하고, 조건이 true이면 코드를 실행하고 괄호 세번째 부분의 작업을 진행한다. <br />
  반복하다 조건이 false가 되면 반복문을 빠져나온다.

```javascript
for(let i = 0; i < 10; i++) {
  //반복할 코드
}
```
```javascript
let i = 0; //초기값 설정
i < 10; //조건, 조건이 false가 되면 반복문 멈춤
i++ //코드 실행 후 작업, 반복문 한번 실행된 후 해야하는 작업을 뜻함

즉, i=0 으로 10보다 작으므로 코드 실행되며 i값이 1씩 증가한다.
i가 증가하며 10이 되는 경우 반복문을 빠져나온다.
```

<br />

1부터 10까지 로그하는 세가지 코드
```javascript
for(let i = 0; i < 10; i++) {
  console.log(i+1);
}
```
```javascript
for(let i = 1; i <= 10; i++) {
  console.log(i);
}
```
```javascript
for(let i = 1; i < 11; i++) {
  console.log(i);
}
```

<br />

### while

* while문의 조건을 확인 후 반복문 실행되므로 한번도 실행되지 않을 수도 있다.

<br />

아래 코드의 경우 i가 계속 0이므로, 무한반복을 하다가 브라우저가 뻗어버린다.
```javascript
let i = 0;

while(i < 10) {
  //반복할 코드
}
```

따라서 아래와 같이 while문 안에 i를 증가시키는 코드를 추가해주면 된다.
```javascript
let i = 0;

while(i < 10) {
  //반복할 코드
  i++;
}
```

<br />

1부터 10까지 로그
```javascript
let i = 1;

while(i <= 10) {
  console.log(i);
  i++;
}
```

<br />

### do.. while

* 일단 do 의 코드를 실행한 후 while의 조건을 확인하기 때문에 (br />
  적어도 한번은 실행된다는 것이 while문과의 큰 차이점이다.

<br />

i가 10보다 작으면 do 내부의 코드를 실행
```javascript
let i = 0;

do {
  //반복할 코드
  i++;
while(i < 10) {
 
}
```

<br />

1부터 10까지 로그
```javascript
let i = 1;

do {
  console.log(i);
  i++;
}
while(i < 10) {
  console.log(i);
}
```

<br />
<br />

## 반복문을 빠져나오는 기능

### break

break 는 만나는 순간 즉시 코드 실행을 멈추고, 반복문을 빠져나온다.
 
```javascript
while(true) {  //무한반복되는 while(true)는 조심해서 사용하기
  let answer = confirm("계속 할까요?");
  if(!answer){
    break;  //확인창의 '취소'를 누를 경우 answer가 false가 되며 반복문에서 빠져나올 수 있음
}
```

<br />

### continue

continue 는 코드 실행을 멈추고, 다음 반복문으로 이동한다.

<br />

짝수만 로그
```javascript
for(let i = 0; i < 10; i++) {
  if(i % 2){  
    continue;  //2로 나눴을 때 나머지가 1이면 continue문을 만나 로그를 찍지않고 다음작업인 i++ 로 바로 넘어감
  }
  console.log(i);
}

//0
//2
//4
//6
//8
```

<br />

## 참고

명확한 횟수가 정해져 있으면 for문, 그게 아니라면 while 사용을 추천한다. (do.. while은 거의 사용안함) <br />
개발자는 항상 코드를 줄이기 위해 노력해야 성능도 좋아진다. <br />
반복문은 코드를 줄이는 아주 좋은 방법 중 하나이다. <br />


<br />
<br />
<br />
<br />
<br />

# 9. switch문 

모든 switch문은 if..else로도 작성 가능하다.<br />
case가 다양할 경우, 보다 간결하게 쓸 수 있다는 장점때문에 사용한다.

```javascript
switch(평가) {
  case A :
    //A일 때 코드
  case B :
    //B일 때 코드
  ...
```
위의 switch문과 동일한 if else 코드
```javascript
if(평가 == A) {
  //A일 때 코드
} else if(평가 == B) {
  //B일 때 코드
} ...
```

<br />

사고 싶은 과일을 물어보고 가격 알려주기
```javascript
let fruit =  prompt("무슨 과일을 사고싶나요?");

switch(fruit) {
  case "사과" :
    console.log("100원 입니다.");
    break; 
  case "바나나" :
    console.log("200원 입니다.");
    break;
  case "키위" :
    console.log("300원 입니다.");
    break;
  case "멜론" :
    console.log("400원 입니다.");
    break;
  case "수박" :
    console.log("500원 입니다.");
    break;
}

//참고로 break를 하지 않으면 해당 값 외에도 이후의 모든 코드를 다 실행하기 때문에 넣어주어야 함
```


<br />
<br />
<br />
<br />

# 10. 함수(function)의 기초 

서비스를 만들다보면 같거나 비슷한 동작들이 생기기 마련이다. <br />
팝업을 띄운다던지 결제와 같은 동작들을 자주 사용하거나 여러곳에서 사용한다면 <br />
중복되는 코드도 줄이고 유지보수도 편하게 하기 위해 하나로 만든 다음 재활용하는 것이 좋다. <br />
함수는 이것을 가능하게 해준다.

<br />

앞서 이미 몇가지 함수를 사용해 보았는데, <br />
브라우저가 이미 가지고 있는 내장함수인 console, alert, confirm 이다.

<br />

## 함수 작성방법

```javascript
function sayHello(name) {
  console.log(`Hello, ${name}`); //`주의
}
```
```javascript
function //함수
sayHello //함수명, 함수의 이름은 자유롭게 정함
(name) //매개변수, 매개변수는 없을 수도 있고 여러개인 경우 쉼표로 구분함
{
  console.log(`Hello, ${name}`); //중괄호 내부는 함수의 실행코드를 작성함
}
```
함수는 함수명 뒤에 괄호를 붙여서 호출가능하며 매개변수가 필요하다면 괄호안에 넣어준다.
```javascript
sayHello("Mike");

//Hello, Mike
```

<br />

1. 매개변수가 없는 함수
```javascript
function showError() {
  alert("에러가 발생했습니다. 다시 시도해주세요.");
}

showError();
```

<br />

2. 매개변수가 있는 함수
```javascript
function sayHello(name) {
  const msg = `Hello, ${name}`;
  console.log(msg);
}

sayHello("Mike");
sayHello("Tom");
sayHello("Julia");

//Hello, Mike
//Hello, Tom
//Hello, Julia
```
이처럼 함수를 하나 만들어 놓으면 매개변수를 바꿔가며 다양하게 대응가능하다.

<br />

만약 매개변수가 없어 이름을 모르는 경우는?  <br />
=> 중괄호 내부 조건문 처리
```javascript
function sayHello(name) {
  console.log(name);
  let msg = 'Hello';
  if(name){
    msg = `Hello, ${name}`;
  }
  console.log(msg);
}

sayHello();

//undefined
//Hello  (name 이 undefined 이기 때문에 msg만 출력됨)
```

<br />

### 지역 변수

함수 내부에서만 접근가능한 변수는 그 함수의 지역변수(local varable)
```javascript
function sayHello(name) {
 let msg = 'Hello';  //msg는 함수 내부에서만 사용가능(지역변수), 외부에서도 사용하고 싶다면 함수 밖으로 빼주기
  if(name){
    msg += ', ' + name;  //혹은 msg += `, ${name}`; 으로 백틱사용하여 작성 가능
  }
  console.log(msg);
}

sayHello();
sayHello("Mike");
console.log(msg);

//Hello
//Hello, Mike
//지역변수의 외부 호출로 에러발생
```

<br />

### 전역 변수

어디서나 접근할 수 있는 변수는 전역변수(global varable)
```javascript
let msg = 'Hello';  //전역변수가 된 msg
console.log("함수 호출 전");
console.log(msg);

function sayHello(name) {
  if(name){
    msg += `, ${name}`;
  }
  console.log("함수 내부");
  console.log(msg);
}

sayHello("Mike");
console.log("함수 호출 후");
console.log(msg);

//함수 호출 전
//Hello

//함수 내부
//Hello, Mike

//함수 호출 후
//Hello, Mike
```

<br />

## 전역 변수와 지역 변수

함수 내부에서 let으로 전역변수와 동일한 이름으로 지역변수를 선언할 수 있고, 서로 간섭받지 않는다.
```javascript
let msg = 'Welcome'; //전역 변수
console.log("함수 호출 전");
console.log(msg);

function sayHello(name) {
  let msg = 'Hello'; //지역 변수
  console.log("함수 내부");
  console.log(msg + ' ' + name);
}

sayHello("Mike");
console.log("함수 호출 후");
console.log(msg);

//함수 호출 전
//Welcome

//함수 내부
//Hello, Mike

//함수 호출 후
//Welcome
```

<br />

```javascript
let name = 'Mike';

function sayHello(name) {
  console.log(name);
}

sayHello(); //전역변수에 name 이 선언되었으니 매개변수는 없어도 되는 걸까?
sayHello("Julia");

//undefined (위 질문의 정답은 X)
//Julia
```
=> 매개변수로 받은 값은 복사된 후 함수의 지역변수가 된다. <br />
전역변수가 많아지면 관리가 힘들어지기 때문에 전체서비스에서 공통으로 바라봐야하는 변수를 제외하고는 <br />
지역변수를 쓰는 습관을 들이는 것이 좋다.

<br />
<br />

### 함수 + OR 

```javascript
function sayHello(name) {
  let newName = name || 'friend';
  let msg = `Hello, ${newName}`;
  console.log(msg);
}

sayHello();
sayHello("Julia");

//Hello, friend
//Hello, Julia
```

<br />

기본값(default value) 설정 시 위 코드보다 더 깔끔, 간단하게 사용 가능
```javascript
function sayHello(name = 'friend') {
  let msg = `Hello, ${newName}`;
  console.log(msg);
}

sayHello();
sayHello("Julia");

//Hello, friend
//Hello, Julia
```

<br />

### return 으로 값 반환

```javascript
function add(num1, num2) {
  return num1 + num2;  //return 오른쪽의 값 반환
}

const result = add(2,3);
console.log(result);

//5
```

<br />

return문이 없는 함수도 항상 undefined 값을 반환한다.
```javascript
function showError() {
  alert("에러가 발생했습니다.");
}

const result = showError();
console.log(result);

//undefined
```

<br />

return 문이 있는 경우 그 즉시 return 오른쪽에 있는 값을 반환하고 종료한다.
```javascript
function showError() {
  alert("에러가 발생했습니다.");
  return;
  alert("이 코드는 절대 실행되지 않습니다.");
}

const result = showError();
console.log(result);

//undefined
```
따라서 함수를 종료하는 목적으로 return 을 사용하기도 한다.

<br />

## 팁

* 함수는 한번에 한 작업만 하는 것이 좋다. <br />
  하나의 함수가 여러작업을 진행하면 함수를 더 잘게 나눠서 사용하는 것을 권장한다.
* 변수가 그렇듯이 함수도 읽기 쉽고 어떤 동작인지 알 수 있게 네이밍하는 것이 중요하다. <br />
  - showError  //에러를 보여줌
  - getName  //이름을 얻어옴
  - createUserData  //유저데이터 생성
  - checkLogin  //로그인 여부 체크 <br />
    ...
    
