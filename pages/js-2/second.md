# JS 기초 2 - 제어 흐름과 오류 처리

모든 것들은 mdn문서를 기준으로 합니다.

---

## 명령문

**블록문**

if, while, for등과 같이 자주 쓰는 가장 기본적인 명령문

```js
if(true){
    console.log(asdf)
}
//저기서 { ... } <- 이 부분이 블록문이다.
```
---
## 조건문
for, if, switch 문은 다 알거고...

**throw**<br>
예외처리를 할때 사용하는 구문, 말 그대로 뭐든지 던져서 보여줄수 있음
```js
throw "asdf" //string
throw 42 //number
throw true //boolean
//이렇게 타입을 던져줄수 있음
```

**try...catch**<br>
이건 실행할 시도할 블록을 표시하고, 그 안에서 예외가 발생할 경우, 처리를 맡을 명령문을 지정합니다.
쉽게 말해, 시도문하고 예외처리두는 if else문과 비슷하다 보면 됨

```js
function rand(){
    const random = parseInt(Math.random()*10)
    console.log(random)
    const list = [1,2,3,4,5,6]
    if (list[random] != undefined){
        console.log("값있음")
        return "값있음"
    } else{
        throw "오류수고"
    }
}
try{
    rand()
} catch (e){
    console.log(e);
}
```
이렇게 사용

**finally**
try..catch문 뒤에 붙으면서 그것이 무엇이든지 무조건 실행하는 제어문
```js
try {
  console.log('Some Try Block!');
} catch (e) {
  console.log('Some Catch Block!');
} finally {
  console.log('Some Finally Block!');
} //이러면 try문과 finally문만 실행된다.
```
**무조건 실행이기 때문에 기존의 값을 덮어쓰는 경우도 있다.**
```js
function fn() {
  try {
    return 0;
  } catch (e) {
    return 1;
  } finally {
    return 2;
  }
}

console.log(fn());
```
이럴때, 0이 원래 들어가지만, finally로 인해 최종값은 2가 된다.
