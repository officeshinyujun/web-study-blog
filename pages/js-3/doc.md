# JS기초 3 - 루프와 반복

모든 것들은 mdn 문서를 기준으로 합니다.

---

## 반복문
for, do...while, while문은 아니까 생략

**레이블문**

이 프로그램 내에서 이 부분부터 다시 참조해야할때 사용한다.
```js
label : {
    statements
}
```
label - 자바스크립트에서 사용 가능한 식별자면 다 가능<br>
statement - 구문 , for이 될수도 있고, while이 될수도 있고.

대체로 반복문에 레이블을 붙이고, break나 continue 구문을 사용해 반복문의 어느 위치에서 작업을 멈추고 다시 수행할지를 알려줄수 있습니다.

```js
let i,j;

loop : 
for (i = 0; i<3; i++){
    loop2:
    for (j = 0; j<3; j++){
        if (i===1 && j===1){
            continue loop
        }
        console.log(i,j)
    }
}
//0 0
//0 1
//0 2
//1 0
```

**for...in문**

for in 문은 객체 내의 것들을 열거 가능하게 해줍니다. 예를들면
```js
const list = {a:1, b:2,c:3};

function printList(list){
    for (const property in list){
        console.log(`${property} :${list[property]}`)
    }
}
//a : 1 
//b : 2
//c : 3
```
이렇게 객체 내부의 것들을 열거 가능하게 해준다.<br>
또한 배열 요소를 사용할수도 있는데, 대체로 for in문 말고 for문을 권장한다.

**for...of**

반복가능한 개체들인 Array, Map, set, String등에 대해 반복할수 있게 해주는 것, 예로들면
```js
const array = [1,2,3];

for (const element of array){
    console.log(element)
}
//1, 2, 3
```

근데 이럼 for문과 차이가 없어 보이는데, 무엇이 다르나면, **문자열**에도 적용이 가능하다
```js
const string = "asdf"

for(const text of string){
    console.log(text)
}
// 'a' 's' 'd' 'f'
```
