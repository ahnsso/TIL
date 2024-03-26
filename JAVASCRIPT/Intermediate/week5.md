# 6. 배열 메소드(Array methods)

- 기초강의 복습 
  - push() : 뒤에 삽입
  - pop() : 뒤에 삭제
  - unshift() : 앞에 삽입
  - shift() : 앞에 삭제

<br />

이외의 배열 메소드에 대해 더 알아보자.

* arr.splice(n,m) : 배열의 특정요소 지움 (n번째 요소부터 m개만큼 지우라는 뜻)
```javascript
let arr = [1, 2, 3, 4, 5];
arr.splice(1, 2);

console.log(arr); //[1, 4, 5]
```  

<br />

* arr.splice(n,m,x) : 배열의 특정요소 지우고 추가 (n번째 요소부터 m개만큼 지우고, x 추가)
```javascript
let arr = [1, 2, 3, 4, 5];
arr.splice(1, 3, 100, 200);

console.log(arr); //[1, 100, 200, 5]
```

+) 두번째 인수가 0일 경우에는 아무것도 지우지 않고, 중간에 새로운 요소추가가 가능하다.
```javascript
let arr = ["나는", "철수", "입니다"];
arr.splice(1, 0, "대한민국","소방관"); //arr[1]부터 0개 지워지므로 arr[1]과 arr[0]사이에 요소추가

console.log(arr); //[1, 100, 200, 5] //["나는", "대한민국","소방관", "철수", "입니다"];
```

<br />

* arr.splice() : 삭제된 요소 반환
```javascript
let arr = [1, 2, 3, 4, 5];

let result = arr.splice(1, 2);

console.log(arr); //[1, 4, 5]
console.log(result); //[2, 3]
```  

<br />

* arr.slice(n,m) : 인덱스 n부터 m-1까지 반환 (m포함이 아닌 바로 앞자리 까지이고, m을 생략할 경우 n부터 배열 끝까지를 의미한다.)
```javascript
let arr = [1, 2, 3, 4, 5];
arr.splice(1, 4);

console.log(arr); //[2, 3, 4]
```  

+) 만약, 괄호 안을 비울 경우 배열이 복사된다.
```javascript
let arr = [1, 2, 3, 4, 5];
let arr2 = arr.splice();

console.log(arr2); //[1, 2, 3, 4, 5]
```

<br />

* arr.concat(arr2, arr3 ...) : 인자로 주어진 배열이나 값들을 기존 배열에 합쳐서 새배열로 반환
```javascript
let arr = [1, 2];
arr.concat([3, 4]);

console.log(arr); //[1, 2, 3, 4]
```
```javascript
let arr = [1, 2];
arr.concat([3, 4], [5, 6]);

console.log(arr); //[1, 2, 3, 4, 5, 6]
```
```javascript
let arr = [1, 2];
arr.concat([3, 4], 5, 6);

console.log(arr); //[1, 2, 3, 4, 5, 6]
```


<br />

* arr.forEach(fn) : 함수를 인수로 받아 배열 반복 <br />
그 함수에는 세개의 매개변수가 있다.<br />
첫번째 해당 요소(item), 두번째 인덱스(index), 세번째 해당 배열 자체(arr) <br />
(보통 첫번째와 두번째만 사용)
```javascript
let arr = ['Mike', 'Tom', 'Jane'];
arr.forEach((name, index) => {
  console.log(`${index + 1}. ${name}`);
});

//1. Mike
//2. Tom
//3. Jane
```

<br />

* arr.indexOf(n) : n을 발견하면 해당 요소의 인덱스를 반환하고, 없으면 -1 반환
```javascript
let arr = [1, 2, 3, 4, 5, 1, 2, 3];

console.log(arr.indexOf(3)); //2
```

+) 인수가 두개인 경우, 2번째 인수는 탐색 시작하는 위치를 의미
```javascript
let arr = [1, 2, 3, 4, 5, 1, 2, 3];

console.log(arr.indexOf(3, 3)); //7
```

+) arr.lastIndexOf(n) : 맨 뒤에서부터 탐색하고 싶은 경우 사용
```javascript
let arr = [1, 2, 3, 4, 5, 1, 2, 3];

console.log(arr.lastIndexOf(3)); //7
```

<br />

* arr.includes(n) : 배열내 n포함하는지 확인 (인덱스 확인X)
```javascript
let arr = [1, 2, 3];

console.log(arr.includes(2)); //true
console.log(arr.includes(8)); //false
```

<br />

* arr.find(fn) : indexOf 처럼 찾는다는 의미는 동일하지만, 보다 복잡한 연산이 가능하도록 함수 전달가능 <br />
주의할 점은 첫번째 true 값만 반환하고, 만약 없을 경우 undefined 반환한다. <br />
```javascript
let arr = [1, 2, 3, 4, 5];

const result = arr.find((item) => {
  return item % 2 === 0;
});

console.log(result); //2 (짝수를 구하는데 첫번재 true값 반환하고 멈추므로 2까지만 반환)
```

+) 미성년자 찾기 <br />
아래와 같이 객체가 들어있는 배열은 indexOf로 찾기 힘들기 때문에 find를 사용해준다.
```javascript
let userList = [
  { name: "Mike", age: 30 },
  { name: "Julia", age: 29 },
  { name: "Tom", age: 17 },
];

const result = userList.find((user) => {
  if(user.age < 19) {
    return true;
  }
  return false;
});

console.log(result); //{name: 'Tom', age: 17}
```

+) arr.findIndex(fn) : 해당 index를 반환하고, 없으면 -1 반환
```javascript
let userList = [
  { name: "Mike", age: 30 },
  { name: "Julia", age: 29 },
  { name: "Tom", age: 17 },
];

const result = userList.findIndex((user) => {
  if(user.age < 19) {
    return true;
  }
  return false;
});

console.log(result); //2
```

<br />

* arr.filter(fn) : 만족하는 모든 요소를 배열로 반환
```javascript
let arr = [1, 2, 3, 4, 5];

const result = arr.filter((item) => {
  return item % 2 === 0;
});

console.log(result); //[2, 4]
```

<br />

* arr.reverse() : 배열을 역순으로 재정렬 <br />
게시판에서 최근 작성한 순 혹은 최근 가입된 유저 순으로 정렬할 때 자주 사용된다.
```javascript
let arr = [1, 2, 3, 4, 5];

console.log(arr.reverse()); //[5, 4, 3, 2, 1]
```

<br />

* arr.map(fn) : 함수를 받아 특정 기능을 시행하고 새로운 배열을 반환 <br />
실무에서 많이 사용된다.
```javascript
let userList = [
  { name: "Mike", age: 30 },
  { name: "Julia", age: 29 },
  { name: "Tom", age: 17 },
];

let newUserList = userList.map((user, index) => {
  return Object.assign({}, user, {
    id: index + 1,
    isAult: user.age > 19,
  });
});

console.log(newUserList);
//0: {name: 'Mike', age: 30, id: 1, isAult: true}
//1: {name: 'Julia', age: 29, id: 2, isAult: true}
//2: {name: 'Tom', age: 17, id: 3, isAult: false}
```

<br />

* arr.join() : 배열을 합쳐서 문자열을 만듦 <br />
인수를 전달하지 않으면 쉼표로 구분되어 반환된다.
```javascript
let arr = ["안녕" ,"나는", "철수야"];

let result = arr.join();

console.log(result); //안녕,나는,철수야
```
```javascript
let arr = ["안녕" ,"나는", "철수야"];

let result = arr.join(" "); //공백 삽입

console.log(result); //안녕 나는 철수야
```
```javascript
let arr = ["안녕" ,"나는", "철수야"];

let result = arr.join("-"); //특수문자 삽입

console.log(result); //안녕-나는-철수야
```

<br />

* arr.split() : 문자열을 나눠서 배열로 만듦 <br />
  괄호 안의 문자를 기준으로 나눈다.
```javascript
const users = "Mike,Julia,Tom,Joy";

const result = users.split(",");

console.log(result); //["Mike", "Julia", "Tom", "Joy"]
```

+) 빈 문자열 기준으로 나눌 경우, 띄어쓰기 부분까지 배열로 반환된다.
```javascript
let str = "Hello, My name is Julia";

const result = str.split("");

console.log(result); //['H', 'e', 'l', 'l', 'o', ',', ' ', 'M', 'y', ' ', 'n', 'a', 'm', 'e', ' ', 'i', 's', ' ', 'J', 'u', 'l', 'i', 'a']
```

<br />

* Array.isArray() : 배열인지 확인 (true) <br />
  자바스크립트에서 배열은 객체형에 속하기 때문에 typeof는 객체(object)라고 알려주어 일반객체와 구분할 수 없기때문에 사용한다.
```javascript
let user = {
  name: "Julia",
  age: 29,
};

let userList = ["Mike", "Tom", "Julia"];

console.log(typeof user); //object
console.log(typeof userList); //object

console.log(Array.isArray(user)); //false
console.log(Array.isArray(userList)); //true
```

<br />

* arr.sort() : 배열을 재정렬 (배열 자체가 변경되므로 주의) <br />
인수로 정렬 로직을 담은 함수를 받는다.
```javascript
let arr = [1, 5, 4, 2, 3];

arr.sort();

console.log(arr); //[1, 2, 3, 4, 5]
```
```javascript
let arr = ["a", "c", "d", "e", "b"]; 

arr.sort(); //문자열 정렬도 가능

console.log(arr); //['a', 'b', 'c', 'd', 'e']
```

<br />
<br />

```javascript
let arr = [27, 8, 5, 13]; 

arr.sort()

console.log(arr); //[13, 27, 5, 8] 문자열로 받아들여서 1과 2로 시작하는 13과 27이 앞으로 정렬됨
```
그러나 위 코드와 같은 경우 제대로된 정렬을 위해 <br />
아래 코드와 같이 함수를 전달해줘야 한다.
```javascript
let arr = [27, 8, 5, 13];

arr.sort((a, b) => {
  return a - b;  //인수들을 뺄셈 비교해서 작은 수를 앞으로 정렬할 수 있게함
});

console.log(arr); //[5, 8, 13, 27]
```
또는, [Lodash](https://lodash.com/docs) 같은 라이브러리를 사용한다. (_.sortBy) <br />
Lodash는 실무에서 정말 많이 사용된다고 한다.

<br />
<br />

* arr.reduce() : 인수로 함수를 받음. (누적 계산값, 현재값) => { return 계산값 };

배열의 모든 수 합치기 (for, for of, forEach 사용 가능)
```javascript
let arr = [1, 2, 3, 4, 5]; 

let result = 0;
arr.forEach(num => {
  result += num;
})

console.log(result);
```
위 작업을 한번에 처리할 수 있는 것이 arr.reduce()이다.
```javascript
let arr = [1, 2, 3, 4, 5]; 

const result = arr.reduce((prev, cur) => {
  return prev+cur;
}, 0); //초기값 0으로 설정한 것, 안 써도 되며 안 쓸 경우 배열의 첫번째 요소(1)가 초기값으로 자동설정됨

console.log(result); //15
```

<br />

아래 코드는 좀 더 실용적인 예제이다.
```javascript
// 성인들만 배열에 넣기
let userList = [
  { name: "Mike", age: 30 },
  { name: "Julia", age: 29 },
  { name: "Tom", age: 17 },
  { name: "Sue", age: 20 },
  { name: "June", age: 15 },
  { name: "Sarah", age: 29 },
];

let result = userList.reduce((prev, cur) => {
  if(cur.age > 19) {
    prev.push(cur.name);
  }
  return prev;
}, []); //초기값 빈배열

console.log(result); //['Mike', 'Julia', 'Sue', 'Sarah']
```
```javascript
// 전체 나이 더하기
let userList = [
  { name: "Mike", age: 30 },
  { name: "Julia", age: 29 },
  { name: "Tom", age: 17 },
  { name: "Sue", age: 20 },
  { name: "June", age: 15 },
  { name: "Sarah", age: 29 },
];

let result = userList.reduce((prev, cur) => {
  return prev += cur.age;
}, 0);

console.log(result); //140
```
```javascript
// 이름이 3글자인 사람들만 배열에 넣기
let userList = [
  { name: "Mike", age: 30 },
  { name: "Julia", age: 29 },
  { name: "Tom", age: 17 },
  { name: "Sue", age: 20 },
  { name: "June", age: 15 },
  { name: "Sarah", age: 29 },
];

let result = userList.reduce((prev, cur) => {
  if(cur.name.length === 3) {
    prev.push(cur.name);
  }
  return prev;
}, []);

console.log(result); //['Tom', 'Sue']
```

<br />

+) arr.reduceRight()는 arr.reduce()의 기능과 동일하나, 배열의 우측부터 기능을 수행한다는 차이점이 있다.

<br />
<br />
<br />
<br />

# 7. 구조 분해 할당(Destructuring assignment)
구조 분해 할당 구문은 배열이나 객체의 속성을 분해해서 그 값을 변수에 담을 수 있게 하는 표현식

<br />

#### 배열 구조 분해
```javascript
let [x, y] = [1, 2];

console.log(x); //1
console.log(y); //2
```
```javascript
let users = ['Mike', 'Julia', 'Sarah'];
let [user1, user2, user3] = users;  //구조 분해 할당

console.log(user1); //Mike
console.log(user2); //Julia
console.log(user3); //Sarah
```
```javascript
let str = 'Mike-Julia-Sarah';
let [user1, user2, user3] = str.split('-');

console.log(user1); //Mike
console.log(user2); //Julia
console.log(user3); //Sarah
```

<br />

+) 배열 구조 분해 - 기본값
```javascript
let [a,b,c] = [1, 2]; //c처럼 할당된 값이 없을 경우 undefined

console.log(a); //1
console.log(b); //2
console.log(c); //undefined
```
```javascript
//let [a,b,c] = [1, 2]; //c처럼 할당된 값이 없을 경우 undefined

let [a=3, b=4, c=5] = [1, 2]; //기본값 세팅해주면 오류를 방지할 수 있다.

console.log(a); //1
console.log(b); //2
console.log(c); //5
```

<br />

+) 배열 구조 분해 - 일부 반환값 무시 (공백, 쉼표 사용)
```javascript
let [user1, ,user2] = ['Mike', 'Julia', 'Sarah', 'Tom']; //공백으로 두번째 요소 무시, 할당받은 곳이 없는 네번째 요소도 무시됨

console.log(user1); //Mike
console.log(user2); //Sarah
```

<br />

+) 배열 구조 분해 - 바꿔치기
```javascript
//b에 a값을 넣고, a에 b값을 넣고 싶은 경우
let a = 1;
let b = 2;

//새로운 임수 변수 c에 a값을 잠시 저장해두고 b에 a값을 넣어줌
let c = a;
a = b;
b = c;

console.log(a); //2
console.log(b); //1
```
구조 분해 할당을 사용하면 위 코드도 간단하게 구현 가능하다.
```javascript
//b에 a값을 넣고, a에 b값을 넣고 싶은 경우
let a = 1;
let b = 2;

[a, b] = [b , a];

console.log(a); //2
console.log(b); //1
```

<br />

#### 객체 구조 분해
```javascript
let user = {name: 'Julia', age: 29};
//let {name, age} = user;
let {age, name} = user; //순서 상관없음, 순서바꿔도 동일한 결과

console.log(name); //Julia
console.log(age); //29
```

<br />

+) 객체 구조 분해 - 새로운 변수 이름으로 할당 가능
```javascript
let user = {name: 'Julia', age: 29};
let {name: userName, age: userAge} = user;

console.log(userName); //Julia
console.log(userAge); //29
```

<br />

+) 객체 구조 분해 - 기본값
```javascript
let user = {name: 'Julia', age: 29};
let {name, age, gender = 'female'} = user;

console.log(name); //Julia
console.log(age); //29
console.log(gender); //female
```
```javascript
let user = {name: 'Julia', age: 29, gender: 'female'};
let {name, age, gender = 'male'} = user;

console.log(name); //Julia
console.log(age); //29
console.log(gender); //female, 객체로부터 받은 값이 undefined일 때만 초기값 'male'이 사용될 수 있음
```

<br />
<br />
<br />
<br />
