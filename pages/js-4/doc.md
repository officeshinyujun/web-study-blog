# 함수

모든 것은 mdn 문서를 기준으로 합니다.

---

함수란? : **js의 가장 기본이 되는 요소중 하나입니다**. js의 함수는 작업을 수행하거나 값을 계산하는 명령문의 집합입니다.
그냥 뭘 넣었을때 무언가를 반환하는 마술박스라 생각하면 편함

## 함수 정의
함수를 정의하려면 다음의 것들이 필요합니다.
- 함수의 이름
- 함수의 매개변수들(괄호로 묶고, 쉼표로 구분합니다.)
- 함수를 정의하는 중괄호 문으로 묶기

ex)
```js
function square/*<- 함수의 이름*/(num/*함수의 매개변수*/){
    return num*num// 함수가 반환하는 값을 지정
}
```
예로들어 위의 함수는 제곱을 반환하는 함수입니다.

기본적으로 num과 같은 매개변수는 값으로 함수에 전달됨, 그러므로, 함수에서 매개변수 안의 값을 바꿧다 해도 밖에서 정의되어있는 변수는 바뀌지 않음
```js
 function myFunc(theObject) {
    theObject.make = "Toyota";
}

const mycar = {
    make: "Honda",
    model: "Accord",
    year: 1998,
};

// `x`의 값은 "Honda"입니다.
const x = mycar.make;

// `make` 속성은 함수에 의해 `Toyota`로 변경됩니다.
myFunc(mycar);

// `y`의 값은 "Toyota"입니다.
const y = mycar.make;
console.log(x) // honda <- 위에서 바꾼다 해도 여기선 바뀌지 않음!
```

**함수 표현식**<br>
함수는 구문상 명령문이지만, 함수 표현식이란걸로도 만들수 있음<br>
쉽게 말하자면, 변수에 함수를 할당 가능한거임 예로들어,
```js
const square = function (num){
    return num*num
}

const x = square(4); // 이러면 16
```

저런데서 쓰이는 이름 없는 함수들을 **익명 함수**라 한다, 굳이 이름을 가지지 않아도 됨을 의미.
이름을 넣어서 쓸수도 있음, 예로들면

```js
const factorial = function fac(n) {
    return n < 2 ? 1 : n * fac(n - 1);//이렇게 맨 위의 함수는 한번만 호출했음에도, 안에서 또 기능을 쓰기 위해 함수 호출 가능
};

console.log(factorial(3));

```
이런 용도로 쓰임.

함수 표현식은, 함수를 다른 함수의 매개변수로 사용할때 진가를 발휘함, 예로들면
```js
function map(fn, arr) {
    const result = new Array(arr.length);
    for (let i = 0; i < arr.length; i++) {
        result[i] = fn(arr[i]);//함수 내에서 함수 표현식으로 되어있는 함수 참조, 이렇게 쓸수있다~
    }
    return result;
}

const fn = function (x) {
    return x * x * x;
};

const numbers = [0, 1, 2, 5, 10];
const cube = map(fn, numbers);
console.log(cube);//[0,1,8,125,1000] 이렇게 나옴

```
---
## 함수 호출

함수를 지정만 해놓고 호출을 안하면 실행이 안됨<br>
재귀적으로도 사용 가능함, 예로들어
```js
function fac(x){
    if (x==0 || x==1) return 1;
    else return x * fac(x-1);
}

fac(3) // 6
```
이렇게 팩토리얼 계산하기도 가능하다~

## 함수 호이스팅

함수도 변수와 마찬가지로 **호이스팅**이 됨, 왜냐하면 프로그램 상에서 함수를 아무리 아래 선언해놔도, 최상단으로 끌어올리기 때문에 가능함, 예로들면

```js
console.log(square(3));
function square(x){
    return x * x
}//된다.
```

함수는 **함수 선언**에만 적용됨, 함수 표현식에서는 다음과 같이 됨

```js
console.log(square)//undefined , 함수 표현식이 호이스팅되면 초기에는 undefined가 된다.
square(x);// TypeError: square는 함수가 아니다.
square = function (num){
    return num*num
} //이게 됨
```
---
## 함수 스코프

함수 내에서 정의된 변수는 함수 내에서만 사용 가능함, 함수도 마찬가지인데, 전역으로 선언된 함수나 변수는 어떤 부분 내에서 정의된 함수에 불러오기 가능
예로들어,
```js
const num1 = 1;
const num2 = 3;
const name = "asdf"
function add(){
    return num1+num2
}

add() // 4

function getS(){
    const num1 = 2; //위에거랑 다른거임
    const num2 = 5; //위에거랑 다른거임

    function rem(){
        return `${name}'s score is ${num1 + num2}`
    }

    return rem
}

getS()//asdf's score is 7
```
이런 식으로 동작한다~

## 재귀

**재귀**<br>
함수는 자기 자신을 참조 및 호출 가능합니다. 재귀는 js에서 다음과 같은 방식으로 호출 가능함
1. 함수이름
2. argument.callee() `//권장안한다네요`
3. 함수 표현식 내의 함수 이름

js에서 재귀를 사용하는 경우는 DOM과 같은 트리 구조의 노드를 가져오는데 사용됩니다. 예를들어
```js
function walkTree(node) {
    if (node == null) {
        return;
    }
    console.log(node)
    for (var i = 0; i < node.childNodes.length; i++) {
        walkTree(node.childNodes[i]);
    }
}

```
---
## 중첩된 함수와 클로저

js에선 함수 내에 함수를 끼워넣기가 가능합니다. 내부의 함수는 그것을 포함하는 상위의 함수에서만 작동 가능합니다. 이것이 **함수 중첩**입니다. 예를 들자면
```js
function add(){
    function min(){
        console.log('min')
    }
    min()
    return console.log('min is played');
}
min() //x 안에서만 선언
add()
// min 
// min is played
```

또한 이것은 **클로저**라는것을 생성하는데요,<br>
클로저란, **함수와 함수가 선언되었을때의 렉시컬 조합입니다.** 정의가 다소 어려운데, 쉽게 설명하자면<br>
- 자신이 선언된 당시의 환경을 기억하는 변수입니다.
- 또, 생명주기가 끝난 외부 함수의 변수에 참조 가능하게 해줍니다.

예를 들자면
```js
function outerFunc() {
    // 외부 함수의 변수
    var x = 10;

    // 내부 함수에서 외부 함수의 변수에 접근할 수 있습니다.
    var innerFunc = function () {
        console.log(x);
    };

    return innerFunc;
}

var inner = outerFunc();
inner(); // 10
```
여기서, outerFunc는 내부 함수 innerFunc를 반환하고 생애주기에 의해 생을 마감했습니다.<br>
하지만 inner를 실행하면, 내부의 함수 innerFunc가 실행되고, innerFunc는 위 변수인 x를 호이스팅한것을 기억하고 있어서,<br>
10을 돌려줄수 있게 됩니다. <br>
이와 같이 생명 주기가 끝난 외부 함수의 변수에 접근할 수 있는 함수를 **클로저**라고 합니다.

이런 클로저는 현재 상태를 기억하고, 변경된 최신 상태를 유지할수 있게 됩니다.

**다중 중첩 함수**<br>
함수는 또한 다중으로 중첩될수 있습니다. 예를 들자면,<br>
```js
function A(x) {
    function B(y) {
        function C(z) {
            console.log(x + y + z);//지금까지의 값을 다 더해줄수 있음 (클로저)
        }
        C(3);//b에 2가 들어오면 c에 3 전달,
    }
    B(2);//a에 1을 넣으면 b에 2 전달,
}
A(1); // logs 6 (1 + 2 + 3)
```
여기서, 함수 a에는 함수 b가 포함되며, b에는 c가 포함되게 됩니다.<br>
b는 a의 클로저가 되어 값을 불러올수 있게 되고, c는 b의 클로저가 되어 b의 값을 불러올수 있게 됩니다.<br>
또한, c는 b가 a에 접근이 가능하기 때문에, a에도 접근이 가능합니다.
역순으론 불가능합니다.

**이름 충돌**<br>

클로저의 스코프에서 두 개의 인수 혹은 변수의 이름이 같은 경우, 이름이 같아 서로 충돌하게 되는데,
이를 **이름 충돌**이라 부릅니다.<br>
이 경우에는 **더 안쪽 스코프가 우선순위를 갖습니다**.<br>
바깥부터 안쪽으로 들어올수록 우선순위를 높게 책정하는데,이를 **스코프 체인**이라 부릅니다. 예를 들자면

```js
function outside() {
    var x = 10;
    function inside(x) {
        return x * 2;
    }
    return inside;
}
result = outside()(20);
//inside에 20을 넣었음에도, 스코프 체인때문에 x는 10이 되며 20이 출력되게 됩니다.
```
---
## 인수 객체 사용하기

함수의 인수는 배열과 비슷한 객체로 다룰수 있습니다. 예를 들면<br>
```js
function func1(a, b, c) {
    console.log(arguments[0]);
    // Expected output: 1

    console.log(arguments[1]);
    // Expected output: 2

    console.log(arguments[2]);
    // Expected output: 3
}

func1(1, 2, 3);
```
이렇게 넣은 인수를 배열처럼 접근이 가능합니다.<br>
하지만 이 인수들은 **배열이 아닙니다.**, 배열로 바꾸길 원한다면 Array문을 사용하여 배열로 바꾸어야 합니다.
---
## 함수의 매개변수

js에는 일반적인 함수의 기본 매개변수 이외에도, 나머지 매개변수라는 것이 존재합니다.<br>
**기본 매개변수**<br>
js에서 함수의 매개변수는 undefined가 기본으로 설정됩니다. 하지만 경우에 따라 다른 기본값을 줘야 할수도 있습니다. 더하기를 하는 변수는 매개변수가 필요하듯이요.

**나머지 매개변수**<br>
나머지 매개변수를 사용하면 배열로 임의 개수의 변수를 나타낼 수 있습니다.<br>
쉽게 설명하자면, 만약 님이 넣는 대로 다 더해주는 함수를 만들고 싶습니다. 근데 개수가 정해지지 않아 더하기 힘들죠?
그럴때 이 나머지 매개변수를 사용합니다. 코드 예시를 봅시다.
```js
function sumAll(...args) { // args는 배열의 이름입니다.
  let sum = 0;

  for (let arg of args) sum += arg;//arg의 길이만큼 sum에 계속 더해주게 됨

  return sum;
}

alert( sumAll(1) ); // 1
alert( sumAll(1, 2) ); // 3
alert( sumAll(1, 2, 3) ); // 6
```
이렇게 사용합니다.
<br>또한 기본 매개변수와 함꼐 쓸수도 잇습니다. 예를 들면
```js
function showName(firstName, lastName, ...titles) {
  alert( firstName + ' ' + lastName ); // Bora Lee 
  // 나머지 인수들은 배열 titles의 요소가 됩니다.
  // titles = ["Software Engineer", "Researcher"]
  alert( titles[0] ); // Software Engineer
  alert( titles[1] ); // Researcher
  alert( titles.length ); // 2
}

showName("Bora", "Lee", "Software Engineer", "Researcher");
```
저렇게 따로 나누어 쓸 수도 있습니다.

---
## 화살표 함수
함수 표현식보다 더욱 간결히 나타낼수 있는데요, 그것이 바로 화살표 함수입니다.<br>
예시를 들자면
```js
var a = ["Hydrogen", "Helium", "Lithium", "Beryllium"];

var a2 = a.map(function (s) {
  return s.length;
});
console.log(a2); // logs [8, 6, 7, 9] 이렇게 길던게

// 화살표 함수 사용
var a3 = a.map((s) => s.length);
console.log(a3); // logs [8, 6, 7, 9] 이렇게 짧아질수 있습니다.
```
