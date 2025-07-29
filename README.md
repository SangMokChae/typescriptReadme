# typescriptReadme
/* page2
// import * as http from "http";

// const port = 3000;
// const hostname = "0.0.0.0";

// const server = http.createServer((_req, res) => {
//   res.statusCode = 200;
//   res.setHeader("Content-Type", "text/plain");
//   res.end("Hello, World!\n");
// });

// server.listen(port, hostname, () => {
//   console.log(`Server running at http://${hostname}:${port}/`);
// });

let car = "bmw"; // == let car:string = "bmw";

car = "benz";

let age = 31;
let isAult: boolean = true;
let a: number[] = [1, 2, 3];
let a2: Array<number> = [4, 5, 6];

let b: String[] = ["a", "b", "c"];
let b2: Array<String> = ["d", "e", "f"];

// 튜플 -> 배열의 길이가 고정되고 각 요소의 타입이 지정되어 있는 배열 형식
let c: [String, number];

c = ["z", 1];
// c = [1, "z"]; --> X

c[0].toUpperCase();
// c[1].toUpperCase(); --> X

function sayHello(): void {
  console.log("hello");
}

function showError(): never {
  throw new Error();
}
// ===
function infLoop() {
  while (true) {
    // do someting
  }
}

// enum -> 열거형
enum Os {
  window = 3,
  Ios = 10,
  Android, // 11 자동 다음
}

console.log(Os["Android"]);

enum Os2 {
  window = "win",
  Ios = "ios",
  Android = "and",
}

let myOs: Os2;

// myOs = Os2.fds; -> 없는 값은 넣을 수 없다.
myOs = Os2.window; // 특정값만 강제

// null, undefined
let nl: null = null;
let udf: undefined = undefined;

// 객체
let user: object; //

user = {
  name: "xx",
  age: 30,
};

// 하위 추가
type Score = "A" | "B" | "C" | "F";

// console.log(user.name); --> X 특정속성값이 없기 때문
// ==>

// interface는 객체의 구조를 정의할 때 사용
interface User {
  name: string;
  age: number;
  gender?: string; // optional ==> 있어도 되고 없어도 되는 설정
  readonly birthYear: number;
  // 1: String;
  // 2: String;
  // 3: String;
  // 4: String; --> X ==> index signature
  // [grade:number]: string // [key:value] 가능 ===>
  [grade: number]: Score; // [key:Score value]
}

let user2: User = {
  name: "bob",
  age: 31,
  birthYear: 2000,
  1: "A",
  // 2: 'D', --> score에 없는 값은 넣을 수 없다.
};

// user2.age = '11'; --> X
user2.age = 11;
user2.gender = "male";

// user2.birthYear = 1999; // --> X readonly 설정

console.log(user2);

// interface 함수
interface Add {
  (num1: number, num2: number): number;
  // return number (반환값)
}

const add: Add = function (x, y) {
  return x + y;
};
// add 함수는 Add Interface를 구현해야 한다.

console.log(add(10, 20));
// console.log(add(10, 20, 30)); // --> X

interface IsAdult {
  (age: number): boolean;
}

const ad: IsAdult = (age) => {
  return age > 19;
};

console.log(`age1 : ${ad(32)} or age2 : ${ad(18)}`);

// interface 클래스
interface Car {
  color: string;
  wheels: number;
  start(): void;
}

class audi implements Car {
  color;
  wheels = 4;

  constructor(c: string) {
    this.color = c;
  }

  start() {
    console.log("go");
  }
}

const audiA3 = new audi("red");
console.log(audiA3);
audiA3.start(); // go


// extends

interface Benz extends Car {
  door: number;
  stop(): void;
}

const benzCar:Benz = {
  door: 5,
  stop() {
    console.log('stop');
  },
  // 모두 입력
  color: 'black',
  wheels: 4,
  
  start() {
    console.log('go');
  }
}

console.log(benzCar);
benzCar.start();
benzCar.stop();

// 확장
interface Toy {
  name: string;
}

interface toyCar extends Toy, Car {
  price: number;
}

const ToyCar:toyCar = {
  name: '타요',
  price: 1000,
  color: 'blue',
  wheels: 4,
  start() {
    console.log('start');
  }
}

console.log(ToyCar);
ToyCar.start();
*/

/////////////////////////////////////////////////////////////

/* page2
// function
function plus(num1: number, num2: number): void {
  // return num1 + num2; --> X
  console.log(num1 + num2);
}

function hello(name: string, age?: number) {
  // 명시적 필요 -> ?는 선택적 매게 변수 : 있어도 되고 없어도 되게 하기 / String | undefined
  // return `Hello, ${name || 'world'}`;
  // 자리 위치 바뀌면 안됨! age?: number, name: string --> X
  // 만약 자리 바꿔서 쓰겠다면
  // function hello(age: number | undefined, name: string): string {...}
  if (age !== undefined) {
    return `Hello, ${name}. You are ${age}`;
  } else {
    return `Hello, ${name}`;
  }
}

// const result3 = hello(123); --> X
console.log(hello("sam"));
console.log(hello("Sam", 30));

function add(...nums: number[]) {
  // 나머지 매게 변수 -> 배열로 받음
  return nums.reduce((result, num) => result + num, 0);
}

console.log(add(1, 2, 3));
console.log(add(1, 2, 3, 4, 5, 6, 7, 8, 9, 10));

// this
interface User {
  name: string;
}

const Sam: User = { name: "Sam" };

function showName(this: User, age: number, gender: "m" | "f") {
  // this:User -> this가 User 타입이라는 것을 명시적으로 지정
  console.log(this.name);
}

const a = showName.bind(Sam);
a(30, "m"); // this 다음 부터

interface User2 {
  name: string;
  age: number;
}

// overloading
function join(name: string, age: number): User2;
function join(name: string, age: string): string;
function join(name: string, age: number | string): User2 | string {
  if (typeof age === "number") {
    return {
      name,
      age,
    };
  } else {
    return "나이는 숫자로 입력해 주세요.";
  }
}

const jane: User2 = join("jane", 22); // 뭘로 받을지 모르기 때문에 any로 받음
console.log(`jane : ${jane}`);

*/

/////////////////////////////////////////////////////////////


// Literal Types
const userName1 = "Bob";
let userName2: string | number = "Tom";

userName2 = 3;

type Job = "police" | "developer" | "teacher";

interface User3 {
  name: string;
  job: Job;
}

const user3:User3 = {
  name: 'Bob',
  job: 'developer',
  // job: 'student', --> X
}

interface HighSchoolStudent {
  name: string;
  grade: 1 | 2 | 3; // union type
}

interface Car {
  name: "car";
  color: string;
  start(): void;
}

interface Mobile {
  name: "mobile";
  color: string;
  call(): void;
}

function getGift(gift: Car | Mobile) {
  console.log(gift.color);
  if (gift.name === "car") {
    gift.start();
  } else {
    gift.call();
  }
}

// Intersection Types

interface Car2 {
  name: string;
  start(): void;
}

interface Toy {
  name: string;
  color: string;
  price: number;
}

const toyCar: Toy & Car2 = { // 모든 속성을 다 가져야 함
  name: "타요",
  start() {},
  color: "blue",
  price: 1000,
}
