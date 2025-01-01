# JS기초 1 - 문법과 자료형

모든 것들은 mdn문서를 기준으로 합니다.

---
## js란?
웹사이트에서 동적 상호작용이 가능한 완전한 동적 프로그래밍 언어

---
## 기초 변수
변수란 ? : 기초적인 값을 저장할수 있도록 하는 컨테이너

```js
let myDog = "Rover"; //example
test = "fasdf" //오류남, 선언을 안하고 쓰면 안됨
```
| 종류    | 특징               |설명|
|-------|------------------|-|
| **var**   | 전역 변수나 지역 변수로 가능 |테스트3|
| **let**   | 스코프 내의 지역 변수     |테스트3|
| **const** | 스코프 내의 지역 변수     |테스트3|

**변수 스코프**<br>
어떤 함수의 바깥쪽에 변수를 선언하면, 현재 문서의 다른 코드에 변수 사용 가능함, 이를 전역 변수라 부름니다.
근데 var 변수는 안에 선언해도, 전역으로 쓸 수 있음
```js
if(true){
    let y=5;
}
console.log(y) // 원래 이러면 안됨

if(true){
    var x = 0;
}
console.log(x); // 이럴땐 됨
```

**변수 호이스팅**<br>
> 지금 변수가 선언이 되지 않았어도 참조가 가능함
```js
console.log(x === undefined) //true
var x=3;

var mybar = "asdf"
function asdf(){
    console.log(mybar); //undefined
    var mybar = "asdf" //얘가 호이스팅되어서 그럼
}
```
이래서 var변수는 코드 최상단에 넣는게 좋음

**함수 호이스팅** // 나중에 합시다. 함수 들어갈때

**전역 변수**<br>
> 전역 변수는 사실 전역 객체의 속성입니다. 웹 페이지의 전역 개체는 window이므로, window.{전역변수이름}하면 전역변수 볼수있음

```js
var x = "Asdf"
console.log(windows.x) //Asdf
```

**상수**<br>
> 읽기 전용 변수

- 스크립트 실행 중에는 **대입을 통해 값을 바꿀수 없음, 재선언도 불가능**
- 같은 이름으로 또다른 변수,함수 설정 불가능

```js
const x = 0;
function x (){} // 안됨

const y = 0;
let y ; //안됨
```
근데 이제 상수에 할당된 객체는 고칠수 있고, 리스트도 마찬가지임
```js
const MY_OBJ = {key :"value"};
MY_OBJ.key = "othervalue" // 가능

const MY_LS = ['asdf', 'ASDF'];
MY_LS.push("JS")
console.log(MY_LS) // ["asdf", "ASDF", "JS"]
```
---
## 데이터 구조 및 형

- boolean : 참과 거짓
- null : null값을 나타내는 특수한 키워드, 값없음
- undefined : 값의 정의되어있지 않은 속성
- Number, BigInt : 정수형 또는 실수형 숫자, 후자는 정밀한 정수
- String : 문자열
- Symbol : 인스턴스가 고유하고 불변의 형

js는 데이터 형을 언제든지 다시 지정 가능한 동적 정지형 언어이다. 고로 다음과 같은게 된다.
```js
var answer = 42
answer = "Asdf" //이게됨
```
또, 숫자와 문자열을 합치거나 뺄수 있음(?) 맨 앞에 있는 것으로 형식이 결정남
```js
37 - "7" //30
"37" + 7 //377
```
마지막으로 숫자를 나타내는 값이 문자일경우, 변환하는 메서드가 있음
> parseInt(), parseFloat()
```js
parseInt("101", 2/*진법*/) //5
```

---
## 리터럴

값을 나타내기 위해 리터럴을 사용합니다. 이는 스크립트에 부여된 고정 값입니다. 이게 뭔뜻이냐면 <br>
>상수가 변하지 않는 변수를 뜻한다면, 리터럴은 데이터 그 자체를 의미함.
```js
let coffees = ["French Roast", "Colombian", "Kona"]; 
```
-> 이럴 때에는 coffees가 상수(변수), 리터럴은 = 뒤의 부분, **이를 배열 리터럴이라 부름**

이 외에도 **불리언 리터럴, 숫자 리터럴, 정수 리터럴** 등 다양한 것들이 있음