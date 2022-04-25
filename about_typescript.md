# TypeScript

# 참고 사이트

- [https://heropy.blog/2020/01/27/typescript/](https://heropy.blog/2020/01/27/typescript/)

# 개요

- 마이크로소프트에서 개발
- 아파치 라이센스가 부여된 오픈소스
- 런타임이 아닌 컴파일 환경에서 에러 발견
- 자바스크립트는 타입이 없는 동적 프로그래밍 언어, 타입스크립트는 타입이 있는 정적 프로그래밍 언어.

# 사용법

- .ts 확장자
- 타입스크립트 컴파일러를 통해 자바스크립트 파일로 컴파일하여 사용.

# 문법

## 함수

- 파라미터, 일반변수, 반환타입에 모두 타입을 지정할 수 있다.

```tsx
function add(a: number, b: number): number {
  return a + b;
}

const sum: number = add(1, 23);
console.log(sum);
```

## 문자열

```tsx
let str: string;
let red: string = "red";
let green: string = "green";
let color: string = `my color is ${red}`;
console.log(color);
```

## Boolean

```tsx
let isBoolean: boolean;
let isDone: boolean = false;
console.log(isDone);
```

## 배열

```tsx
// 문자열 배열
let fruits: string[] = ["tv", "pc"];
let fruits2: Array<String> = ["tv", "pc"];

console.log(fruits);
console.log(fruits2);

// 숫자 배열
let student: number[] = [1, 2, 33, 55];
let student2: Array<number> = [4, 3, 2, 4];

console.log(student);
console.log(student2);
```

## 유니언 타입(다중 타입) ⇒ 예를 들어 문자와 숫자를 동시에 가지는 배열도 가능

```tsx
// 문자열 || 숫자 => 유니언 타입
let language: (string | number)[] = ["java", 1, "python", 2];
let language2: Array<string | number> = ["java", 1, "python", 2];
console.log(language);
console.log(language2);
```

## 여러 타입의 값이 들어가는 배열일 경우

```tsx
let someArr: any[] = [0, [], false];
```

## 인터페이스와 커스텀타입을 사용할 수 있다

```tsx
interface Hello {
  name: string;
  age: number;
  isValid: boolean;
}

let userArr: Hello[] = [
  { name: "hello", age: 12, isValid: true },
  { name: "james", age: 122, isValid: false },
];

console.log(userArr);
```

## 읽기 전용 배열 생성 가능

```tsx
let arrA: readonly number[] = [1, 2, 3, 4];
let arrB: ReadonlyArray<number> = [3, 4, 4, 4];
```

## ❗❗❗튜플❗❗❗

- 배열과 유사
- 배열과 차이점: 정해진 타입, 고정된 길이 배열이다.

```tsx
let tuple: [string, boolean];
tuple = ["a", false];
tuple = ["aaa", false];

console.log(tuple); // [ 'aaa', false ] 맨 마지막 VALUE로 값이 지정된다.
```

- Tuple 타입의 배열(2차원 배열)을 사용할 수 있다.

```tsx
let users: Array<[number, string, boolean]>;
users = [
  [1, "typist", false],
  [2, "admin", false],
];
console.log(users); // [ [ 1, 'typist', false ], [ 2, 'admin', false ] ]
```

- Tuple은 정해진 타입의 고정된 길이 배열을 표현하지만, 이는 할당(Assign)에 국한된다.
- .push()나 .splice() 등을 통해 값을 넣는 행위는 막을 수 없다.
- 읽기 전용의 튜플을 생성할 수도 있음

```tsx
let arr: readonly [string, number] = ['aaaaa', 1];
```

## ❗❗❗Enum(열거형)❗❗❗

- Enum은 숫자 혹은 문자열 값 집합에 이름을 부여할 수 있는 타입으로, 값의 종류가 일정한 범위로 정해져 있는 경우 유용하다.
- 기본적으로 0부터 시작하며 값은 1씩 증가한다.

```tsx
enum Week {
  sun,
  mon,
  tue,
  wed,
  thu,
  fri,
  sat,
}
console.log(Week);
/*
{
  '0': 'sun',
  '1': 'mon',
  '2': 'tue',
  '3': 'wed',
  '4': 'thu',
  '5': 'fri',
  '6': 'sat',
  sun: 0,
  mon: 1,
  tue: 2,
  wed: 3,
  thu: 4,
  fri: 5,
  sat: 6
}
*/

console.log(Week.mon); // 1
```

```tsx
// 수동으로 값을 변경할 수 있음 - 값을 변경한 부분부터 다시 1씩 증가함.
enum Week_t {
  sun,
  mon = 22,
  tue,
  wed,
  thu,
  fri,
  sat,
}

console.log(Week_t);
/*
 {
  '0': 'sun',
  '22': 'mon',
  '23': 'tue',
  '24': 'wed',
  '25': 'thu',
  '26': 'fri',
  '27': 'sat',
  sun: 0,
  mon: 22,
  tue: 23,
  wed: 24,
  thu: 25,
  fri: 26,
  sat: 27
}
*/
```

- Enum 타입은 역방향 매핑을 지원한다.
- Enum은 숫자 값 열거뿐만 아니라, 문자열 값으로 초기화도 가능하다. 다만, 역방향 매핑은 지원하지 않아, 개별적으로 초기화를 해야 한다.

```tsx
enum Hello {
  red = "red",
  blue = "blue",
  green = "green",
}

console.log(Hello.red);
console.log(Hello["green"]);
```

## 모든 타입

- Any는 모든 타입을 의미한다.

```tsx
let any: any = 123;
any = 'Hello world';
any = {};
any = null;
```

<aside>
💡 강한 타입 시스템의 장점을 유지하기 위해 Any사용을 엄격하게 금지하려면, 컴파일 옵션 “noImplicitAny”: true를 통해 Any 사용 시 에러를 발생시킬 수도 있음.

</aside>

## **알 수 없는 타입: Unknown**

- Any와 같이 최상위 타입인 Unknown은 알 수 없는 타입을 의미.
- Any와 같이 Unknown에는 어떤 타입의 값도 할당할 수 있지만, Unknown을 다른 타입에는 할당할 수 없습니다.
- any는 어디든 할당할 수 있음
- unknown은 any를 제외한 다른 타입에 할당할 수 없음
- unknown 보단 좀 더 명확한 타입을 사용하는 것이 좋음.

```tsx
interface IUser {
  name: string;
  age: number;
  isValid: boolean;
}

type Result =
  | {
      success: true;
      value: unknown;
    }
  | { success: false; error: Error };

export default function getItems(userArr: IUser): Result {
  const id: boolean = true;
  if (id.isValid) {
    return {
      success: true,
      value: ["aaa", 12312],
    };
  } else {
    return {
      success: false,
      error: new Error("Invalid user"),
    };
  }
}
```

## 객체: Object

- 기본적으로  typeof 연산자가 “object”로 반환하는 모든 타입을 나타낸다.
- 컴파일러 옵션에서 엄격한 타입 검사(strict)를 true로 설정하면, null은 포함하지 않는다.

```tsx
let obj: object = {};
let arr: object = [];
let func: object = function () {};
let nullValue: object = null;
let date: object = new Date();
```

- 여러 타입의 상위 타입이기 때문에 그다지 유용하지는 않다.
- 정확한 타입 지정을 위해서 객체 속성들에 대한 타입을 개별적으로 지정할 수 있다.

```tsx
let userA: { name: string; age: number } = {
  name: "any",
  age: 12,
};
```

## Null 과 Undefined

- 기본적으로 Null과 Undefined는 모든 타입의 하위 타입으로, 각 타입에 할당 할수 있고, 서로 타입에 할당할 수도 있다.

```tsx
let num: number = undefined;
let str: string = null;
let obj: { a: 1, b: false } = undefined;
let arr: any[] = null;
let und: undefined = null;
let nul: null = undefined;
let voi: void = null;
```

- 컴파일 옵션 **"strictNullChecks": true 를 통해 을 통해 엄격하게 Null과 Undefined 서로의 타입까지 더 이상 할당할 수 없게 한다.**
- 단 void는 undefined를 할당할 수 있음

## Void

- 일반적으로 값을 반환하지 않는 함수에서 사용한다.
- 값을 반환하지 않는 함수는 실제는 undefined를 반환한다.

```tsx
function hello(msg: string): void {
  console.log("hello");
}

const hi: void = hello("hello"); // hello 출력
console.log(hi); // undefined
```

## Never

- 절대 발생하지 않을 값을 나타냄, 어떠한 타입도 적용할 수 없음.

```tsx
function error(msg: string): never {
  throw new Error(msg);
}

// 보통 다음과 같이 빈 배열을 타입으로 잘못 선언한 경우, Never를 볼 수 있다.
const never: [] = [];
never.push(3);
```

## Union(유니언)

- 2개 이상의 타입을 허용하는 경우, 유니언이라고 한다.
- vertical bar(|)를 통해 구분을 하고, ()는 선택사항이다.

```tsx
let union: string | number;
union = "hello";
union = 123;
```

## 인터섹션 (intersection)

- &를 사용해 2개 이상의 타입을 조합하는 경우를 인터섹션이라고 한다.
- 인터섹션은 새로운 타입을 생성하지 않고 기존의 타입들을 조합할 수 있기 때문에 유용하지만, 자주 사용되는 방법은 아니다.

```tsx
interface IUser {
  name: string;
  age: number;
}
interface IValidation {
  isValid: boolean;
}
const user: IUser = {
  name: "james",
  age: 12,
};
const validUser: IUser & IValidation = {
  name: "james",
  age: 12,
  isValid: false,
};
```

## 함수

- 화살표 함수를 이용해 타입을 지정할 수 있음

```tsx
// 2개의 숫자 타입 인수를 가지고, 숫자 타입을 반환하는 함수
let myFunc: (test: number, test1: number) => number;
myFunc = function (x, y) {
  return x + y;
};

// 인수가 없고, 반환도 없는 경우
let funcMy: () => void;
funcMy = function () {
  console.log("hello world");
};
```

## 타입 추론

- 명시적으로 타입이 선언되어 있지 않은 경우, 타입스크립트는 타입을 추론해 제공한다.
- num 초기화 시 숫자를 할당했기 때문에 Number 타입으로 추론이 되었다. 그렇기 때문에 num에 문자열을 할당할 경우 에러가 난다.

```tsx
let num = 12;
num = 'HELLO WOLRD';
```

- 타입스크립트가 타입을 추론하는 경우
    - 초기화된 변수
    - 기본값이 설정된 매개 변수
    - 반환 값이 있는 함수

## 타입단언

## **Non-null 단언 연산자**

- !를 사용하는 Non-null 단언 연산자(Non-null assertion operator)를 통해 피연산자가 Nullish(**`null`**
이나 **`undefined`**) 값이 아님을 단언할 수 있는데, 변수나 속성에서 간단하게 사용할 수 있기 때문에 유용함.

```tsx
// null이나 undefined때문에 에러가 발생할 수 있는데, !로 nullish를 단언할 수 있다. 
function fnE(x: number | null | undefined) {
  return x!.toFixed(2);
}
```

## 인터페이스

- 타입스크립트의 여러 객체를 정의하는 일종의 규칙이고 구조이다.
- `interface` 키워드와 같이 사용한다.

```tsx
interface User {
  name: string;
  age: number;
  isAdult: boolean;
}
```

```tsx
// 선택적 속성을 정의할 수 있고, 초기화 하지 않아도 에러가 나지 않는다.
interface User2 {
  name: string;
  age: number;
  isAdult?: boolean;
}
let UserTest: User2 = {
  name: "Neo",
  age: 12,
};
```

- 읽기 전용 속성도 가능

```tsx
interface IUser {
  readonly name: string,
  age: number
}

// 초기화
let user: IUser = {
  name: 'Neo',
  age: 36
};

user.age = 85; // Ok
user.name = 'Evan'; // Error - TS2540: Cannot assign to 'name' because it is a read-only property.
```

- 함수 타입을 인터페이스로 지정하는 경우, 호출 시그니처를 사용
    - 호출 시그니처는 함수의 매개변수와 반환타입을 지정한다.

```tsx
interface IName {
  (PARAMETER: PARAM_TYPE): RETURN_TYPE // Call signature
}
```

## 클래스 타입 - interface

```tsx
// 인터페이스로 클래스 정의
interface IUser {
  name: string;
  getName(): string;
}

class User implements IUser {
  constructor(public name: string) {}
  getName() {
    return this.name;
  }
}

const neo = new User("Neo");
const name2: string = neo.getName();
console.log(name2); // Neo
```

 

### 호출 불가능한 인터페이스 구조

- **ICat은 호출이 불가능한 구조이다.**

```tsx
interface ICat {
  name: string
}

class Cat implements ICat {
  constructor(public name: string) {}
}

function makeKitten(c: ICat, n: string) {
  return new c(n); // Error - TS2351: This expression is not constructable. Type 'ICat' has no construct signatures.
}
const kitten = makeKitten(Cat, 'Lucy');
console.log(kitten);
```

### 호출 가능한 인터페이스 구조 - 구성 시그니처

- new 키워드를 사용해야 함.

```tsx
interface IName {
  new (PARAMETER: PARAM_TYPE): RETURN_TYPE // Construct signature
}
```

- **`ICatConstructor`**라는 구성 시그니처를 가지는 호출 가능한 인터페이스를 정의하면, 문제없이 동작하는 것을 확인할 수 있습니다.

```tsx
// 일반 인터페이스
interface ICat {
  name: string;
}

// 구성 시그니처를 가지는 인터페이스
interface ICatConstructor {
  new (name: string): ICat;
}

class Cat implements ICat {
  constructor(public name: string) {}
}

function makeKitten(c: ICatConstructor, n: string) {
  return new c(n);
}

const kitten = makeKitten(Cat, "AMY");
console.log(kitten);
```

## 인덱싱 가능 타입

## keyof

- 인덱싱 가능 타입에서 keyof를 사용하면 속성 이름을 타입으로 사용할 수 있다.
- 인덱싱 가능 타입의 속성 이름들이 유니온 타입으로 적용된다.

## 인터페이스 확장

- 인터페이스도 클래스처럼 extends 키워드를 사용해서 상속할 수 있음.

## 타입별칭 **Type Aliases**

- type 키워드를 사용해서 새로운 타입 조합을 만들 수 있다.
- 하나 이상의 타입을 조합해서 별칭을 부여한다. 정확히는 조합한 각 타입들을 참조하는 별칭을 만드는 것.
- 일반적인 경우 둘 이상의 조합으로 구성하기 위해 유니온을 많이 사용.

```tsx
type MyType = string;
type YourType = string | number | boolean;
type TUser = {
  name: string,
  age: number,
  isValid: boolean
} | [string, number, boolean];

let userA: TUser = {
  name: 'Neo',
  age: 85,
  isValid: true
};
let userB: TUser = ['Evan', 36, false];

function someFunc(arg: MyType): YourType {
  switch (arg) {
    case 's':
      return arg.toString(); // string
    case 'n':
      return parseInt(arg); // number
    default:
      return true; // boolean
  }
}
```

## **제네릭(Generic)**

- Generic은 재사용을 목적으로 함수나 클래스의 선언 시점이 아닌, **사용 시점에 타입을 선언**
할 수 있는 방법을 제공합니다.
- 타입을 인수로 받아서 사용.
- 함수 이름 우측에 **`<T>`**를 작성해 시작합니다. `T`는 타입변수로 사용자가 제공한 타입으로 변환될 식별자이다.

```tsx
function toArray<T>(a: T, b: T): T[] {
  return [a, b];
}

toArray<number>(12, 2);
toArray<string | number>(1, "2");
```

### **제약 조건(Constraints)**

- 인터페이스나 타입 별칭을 사용하는 제네릭을 작성할 수도 있다.
- 다음 예제는 별도의 제약 조건(Constraints)이 없어서 모든 타입이 허용된다.
