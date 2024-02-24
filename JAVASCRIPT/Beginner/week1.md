# 1. 변수

변수는 어떤 정보에 이름을 붙여 저장하고 싶을 때 사용된다.

<br />

```javascript
name = "mike";
age = 30;
```

name 이라는 변수 안에는 mike 라는 값이 들어가고, age 에서 30 이라는 값이 들어간다는 뜻이다.

위처럼 자바스크립트에서 문자열을 사용할 때는 반드시 따옴표 혹은 작은따옴표 를 사용해 주어야 한다.

<br />

또한, 자바스크립트에서 이미 문법적으로 사용되고 있는 단어인 '예약어' 같은 경우 변수명으로 사용할 수 없다. <br />
( ex. class="수업"; ❌ )

<br />

### 변수에 접근하기 위한 두가지 함수

* 경고장 띄우는 함수
alert()

* 로그를 찍는 함수
console.log()

<br />

```javascript
name = "mike";
age = 30;

console.log(age);
alert(name);
```

<br />

## let / const
중복되는 변수명 방지를 위하여 변수명 앞에 사용된다.

<br />

### let

* 최초로 선언하는 변수에 let 을 붙인다면 이미 사용하고 있을 경우 에러를 통해 알 수 있다.
* let 은 한번 선언 후에 값을 바꿀 수 있으며, 그 경우 let 의 생략이 가능하다.
<br />

```javascript
let grade = "A";

// ..100 lines

grade = "A+";
```

<br />

### const

* 절대로 바뀌지 않는 상수를 입력할 때 사용한다.
* const 로 선언된 변수를 바꾸려고 하면 에러가 발생한다.
* 따라서 파이, 최대값, 생일 등 바뀌지 않는 값을 입력할 때 사용하며,<br />
  대문자로 선언하는 것이 좋다. (다른 개발자들에게 상수라는 것을 알리기 위함)
  
<br />

```javascript
const PI = 3.14;

const SPEED_LIMIT = 50;

const BIRTH_DAY = '1996-11-16';
```

<br />

## 정리
### 자바스크립트에서 변하지 않는 값은 const, 변할 수 있는 값은 let 으로 변수 선언한다. 
팁 : 모든 변수를 일단 const 로 선언 후, 나중에 변경될 여지가 있는 변수의 경우 let 으로 바꾸기

<br />

1. 변수는 문자와 숫자, $와 _만 사용 가능하다.d
2. 첫글자는 숫자가 될 수 없다.
3. 예약어는 사용할 수 없다.
4. 가급적 상수는 대문자로 선언해준다.
5. 변수명은 읽기 쉽고 이해할 수 있게 선언한다.

<br />

```javascript
const MY_HOME = "..."; 
let $ = 1; 
let _ = 3;
let userNumber = 3;
```

```javascript
let 1st = 100; ❌
let let = 20; ❌
let a = 1; ❌
```

<br />
<br />
<br />
<br />


# 2. 자료형

문자형, 숫자형, Boolean, null 과 undefined, 객체형과 심볼형(추후강의예정), typeof 연산자

<br />

### 문자형

* 따옴표로 감싸주는 문자열
* 문자형은 아래와 같이 3가지 방식으로 작성할 수 있다

<br />
  
```javascript
const name = "mike"; // 문자형 String
const name1 = "mike"; //큰따옴표
const name2 = 'mike'; //작은따옴표
const name3 = `mike`; //백틱
```

```javascript
const message = "I'm a girl";
const message2 = 'I\'m a girl'; //작은따옴표만을 사용하고 싶다면 역슬래쉬 앞에 넣어주면 특수문자로 인식
```

```javascript
const message3 = `My name is ${name}`; //백틱은 문자열 내부에 변수를 표현해줄때 사용하면 편리
console.log(message3); //My name is mike

const message4 = "My name is ${name}";
console.log(message4); //My name is ${name}; //일반 따옴표 사용 시 변수명이 그대로 노출되므로 주의
```

```javascript
const message5 = `나는 ${20+7}살 입니다.`; //바로 표현식을 넣어줄 수도 있음
console.log(message5); //나는 27살 입니다.
```

<br />

### 숫자형

* 숫자형은 소수점 표현 및 사칙연산이 가능하다.
* 더하기, 빼기, 곱하기, 나누기, 나머지(%)

<br />

```javascript
const age = 30; // 숫자형 Number
const PI = 3.14;
```

```javascript
const x = 1/0;
console.log(x); //infinity (숫자를 0으로 나누면 무한대라는 결과값)
```

```javascript
const name = "mike";
const y = name/2;
console.log(y); //NaN (문자를 숫자로 나누면 Not a Number 결과값)
```
=> 숫자와 관련된 작업 시 결과값이 NaN 이 아닌지 항상 염두에 두면서 작업해야 한다.

<br />
<br />

아래와 같이 '문자형 + 문자형' / '숫자형 + 문자형' 의 형식도 가능하다.

```javascript
const name = "mike"; 

const a = "나는 ";
const b = "입니다.";

console.log(a + name + b); //나는 Mike 입니다.
```

<br />

'숫자형 + 문자형' 의 경우 문자형으로 변환된다.

```javascript
const age = "27"; //Number

const a = "나는 ";
const b = "입니다.";

console.log(a + age + "살" + b); //나는 27살 입니다.
```

<br />

### Boolean

* Boolean 은 논리적인 요소를 나타낸다.
* true 참, false 거짓

<br />

```javascript
const name = "mike";
const age = 30;

console.log(name == "Mike"); //true
console.log(age > 40); //false
```

<br />

### null 과 undefined

* 존재하지 않는 값은 null
* undefined 는 값이 할당되지 않았다는 뜻이다.

<br />

```javascript
let age;
console.log(age); //undefined (변수를 선언만 하고 값을 할당하지 않은 경우)

let user = null;
```

<br />

### typeof 연산자

* 변수의 자료형을 알아낼 수 있다.
* 다른 개발자가 작성한 변수의 type 을 알아야 하거나,<br />
  api 통신을 통해 받아온 data 를 type 에 따라 다른 방식으로 처리해야 할 때 많이 사용된다.

<br />

```javascript
const name = "mike";

console.log(typeof 3); //number
console.log(typeof name); //string
console.log(typeof true); //boolean
console.log(typeof "xxx"); //string
console.log(typeof null); //object (object는 객체형을 의미)
console.log(typeof undefined); //undefined
```
null 은 객체가 아니지만 자바스크립트 초기버전의 오류로 인해 type 이 object 로 나오며, 하위호환성 유지를 위해 수정하지 않는다고 한다.

<br />
<br />
<br />
<br />


# 3. alert / prompt / confirm
알려줌 / 입력받음 / 확인받음

<br />

### alert()

* alert 함수가 실행되면 알림창이 실행되고, 사용자가 확인 버튼을 누르기 전까지는 계속 떠있다.
* 일방적으로 알리는 용도로 비밀번호 오류, 회원가입 시 등 자주 볼 수 있다.

<br />

### prompt()

* prompt 함수는 사용자에게 어떤 값을 입력받을 때 사용한다.
* 메세지를 보여주고, 값을 입력받을 수 있는 필드를 제공한다.
* 두 개의 인수를 받을 수 있다.
* 취소 버튼 선택 시 null 이 반환된다.

<br />

기본
```javascript
const name = prompt("이름을 입력하세요");
alert("환영합니다, " + name + "님"); //name 의 자리에 prompt 에서 입력한 값이 들어가게 됨
```

<br />

백틱 사용
```javascript
const name = prompt("이름을 입력하세요");
alert(`안녕하세요, ${name}님, 환영합니다.`);
```

<br />

두 개의 인수 중 첫번째 값은 메세지, 두번째 값을 입력받을 default 값이다.
```javascript
const name = prompt("예약일을 입력하세요.", "2024-02-"); //default 값으로 무언가를 안내하거나 힌트를 줄 때 유용함
```
<br />

### confirm()

* comfirm 함수는 무언가를 확인받을 때 사용할 수 있다.
* 확인 버튼 외에 취소 버튼이 있다는 것이 alert 과 다른 점이다.
* 예를 들어 결제, 삭제 등 사용자의 액션을 한번 더 확인해 줄 때 유용하게 사용된다.

<br />
  
```javascript
const isAdult = confirm("당신은 성인 입니까?");
console.log(isAdult);  //확인 버튼을 누르면 true, 취소 버튼을 누르면 false 라는 값을 이용하여 작업 진행 가능
```

<br />

## 단점

위처럼 기본적으로 제공되는 창들은 간단하게 사용할 수 있다는 장점이 있지만 단점도 존재한다.

1. 창이 떠있는 동안 스크립트가 일시 정지되어 창을 닫기 전에는 동작에 제한을 받는다.
2. 스타일링이 불가능하여 위치나 모양을 정할 수 없고, 브라우저마다 모양이 다르다.

하지만, 빠르고 간단하게 적용 가능하다는 장점때문에 굉장이 많이 사용되는 기본 메서드이다.

<br />
<br />
<br />
<br />


# 4. 형변환

String() / Number() / Boolean() = 문자형 / 숫자형 / 불린형 으로 변환

<br />

### 형변환이 필요한 이유

* 다른 자료형끼리 더하면 의도치 않은 동작이 발생할 수 있다.
  
<br />

<b> - 수학과 영어의 점수를 받아 평균내기 </b>

```javascript
const mathScore = prompt("수학 점수를 입력하세요."); //90
const engScore = prompt("영어 점수를 입력하세요."); //80
const result = (mathScore + engScore) / 2;

console.log(result); //4540, 형변환을 하지 않은 채로 값을 입력받아 계산할 경우 이상한 값이 나옴
```
위와 같은 결과가 나오는 이유가 무엇일까? <br />
그 이유는 prompt 로 입력받은 값은 무조건 '문자형' 이기 때문이다.<br />
즉, 90 + 80 은 170 이라는 결과값이 아니라 문자열을 이어준 형태인 9080 이 된다. <br />
9080 은 숫자형이 아니지만 나누기 같은 표현식의 경우 숫자형으로 자동형변환되어 계산되므로, <br />
9080 / 2 = 4540 이라는 값이 나오게 되는 것이다.

<br />

'자동형변환'이 편리하다고 생각할 수 있지만 원인을 찾기 힘든 에러를 발생시킬 수 있으므로 <br />
항상 의도를 가지고 원하는 타입으로 변환해 주는 것이 좋다. <br />
이것을 '명시적 형변환'이라고 한다.

<br />

## 명시적 형변환

### String()
* String() 은 괄호 안의 type 을 문자형으로 바꿔준다.

<br />

```javascript
console.log(
String(3),
String(true),
String(false),
String(null),
String(undefined)
);
// 3 true false null undefined, 문자열로 변경됨
```

<br />

### Number()
* Number() 은 괄호 안의 type 을 숫자형으로 바꿔준다.
* 보통 사용자로부터 입력받은 값이 문자형일 경우 자주 사용된다.

<br />

```javascript
console.log(
Number("1234")
);
// 1234, 문자열 1234 가 숫자 1234 로 변경됨
```

<br />

만약, 문자열 안에 글자가 들어가 있을 경우 NaN 이 되므로 주의해야 한다.

```javascript
console.log(
Number("1234dafasdfl")
);
// NaN
```

<br />

참고로, true 와 false 를 숫자형으로 형변환 시킬 경우

```javascript
console.log(
Number("true"),
Number("false")
);
// 1 0
```
1 과 0 의 값을 가진다.

<br />

true 는 1, false 는 0 기억하기

<br />

### Boolean()

* Boolean() 은 괄호 안의 type 을 불린형으로 바꿔준다.
* 불린형으로의 변환은 false 의 케이스만 기억하면 된다.

<br />

<b>false</b>
1. 숫자 0 
2. 빈문자열 ""
3. null
4. undefined
5. NaN 

이 외에는 모두 <b>ture</b> 를 반환하게 된다.

<br />

```javascript
console.log(
Boolean(0),
Boolean(""),
Boolean(null),
Boolean(undefined),
Boolean(NaN)
);
// false false false false false
```

```javascript
console.log(
Boolean(1),
Boolean("javascript"),
Boolean(123)
);
// true true true
```

<br />

## 주의사항

```javascript
console.log(
Number(null) //0 
Number(undefined) //NaN
Number("문자") //NaN
);
```

<br />
<br />
<br />
<br />


# 5. 기본 연산자

더하기 (+), 빼기 (-), 곱하기 (*), 나누기 (/), 나머지 (%)

<br />

### 나머지(%)

* 나머지 값은 생각보다 유용하고 자주 사용된다.
* 예를 들어 2로 나눈 나머지가 1인지 0인지에 따라 홀수 와 짝수로 나눌 수 있고,<br />
  5보다 작은 수를 얻고 싶으면 아무리 큰 수라도 5로 나눈 나머지가 0 ~ 4 의 값만 반환된다는 것을 통해 가능하다.

<br />

### 거듭제곱
* 거듭제곱을 하고 싶을 때는 곱하기를 뜻하는 별을 두번 적어주면 된다.

<br />

```javascript
const num = 2**3;

console.log(num); //8, 2의 거듭제곱
```

<br />

### 우선순위
* 곱셈과 나눗셈은 덧셈과 뺄셈보다 우선순위가 높다.
* 원하는 값을 얻기 위해서는 괄호를 적절히 사용해야 한다.

<br />

### 줄여쓰기

```javascript
let num = 10;
num = num + 5;

console.log(num); //15
```

위 식을 아래와 같이 줄여쓸 수 있다.

```javascript
let num = 10;
num += 5; //num = num + 5;

console.log(num); //15
```

<br />

덧셈이외의 모든 연산자도 이처럼 줄여서 사용 가능하다. <br />
+=, -=, *=, /=, %=

<br />

### 증가 연산자, 감소 연산자

* 증가 연산자와 감소 연산자는 값을 1만큼 증가 또는 감소 시킨다.
* '+' 를 두 번 적거나 '-' 를 두 번 적어 사용한다.

<br />

연산자를 변수 앞에 쓰느냐 뒤에 쓰느냐에 따라 차이가 있다.

```javascript
let num = 10;
let result = num++;

console.log(result); //10, 증가 연산자가 뒤에 있을 경우 증가시키기 전의 값을 result 에 넣으므로 값이 변경되지 않음
```

```javascript
let num = 10;
let result = ++num;

console.log(result); //11, 앞에 있을 경우 증가시킨 값을 result 에 넣음
```



