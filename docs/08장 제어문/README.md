## 📔 **읽은 범위**

> 08장 제어문 (93p ~ 107p)

---

제어문(control flow statement)은 조건에 따라 코드 블록을 실행(조건문)하거나 반복 실행(반복문)할 때 사용한다. 일반적으로 코드는 위에서 아래 방향으로 순차적으로 실행된다. 제어문을 사용하면 코드의 실행 흐름을 인위적으로 제어할 수 있다.

하지만 코드의 실행 순서가 변경된다는 것은 단순히 위에서 아래로 순차적으로 진행하는 직관적인 코드의 흐름을 혼란스럽게 만들기 때문에 가독성을 해치는 단점이 있다.

## 8.1 블록문

블록문(block statement/compound statement)은 0개 이상의 문을 중괄호로 묶은 것으로, 코드 블록 또는 블록이라고 부른다.

- 블록문은 단독으로 사용할 수도 있지만 보통 제어문이나 함수를 정의할 때 사용하는 것이 일반적이다.
- 블록문은 언제나 문의 종료를 의미하는 자체 종결성을 갖기 때문에 끝에는 세미콜론을 붙이지 않는다.

```javascript
// 블록문

{
	var foo = 10;
}

// 제어문

var x = 1;
if (x < 10) {
	x++;
}

// 함수 선언문

function sum(a, b) {
	return a + b;
}
```

## 8.2 조건문

조건문은 주어진 조건식의 평가 결과에 따라 코드 블록(블록문)의 실행을 결정한다. 조건식은 `불리언 값`으로 평가될 수 있는 표현식이다.

- 자바스크립트는 if...else 문과 switch 문으로 두 가지 조건문을 제공한다.

### `8.2.1 if...else 문`

if...else 문은 주어진 조건식(불리언 값으로 평가될 수 있는 표현식)의 평가 결과, 즉 논리적 참 또는 거짓에 따라 실행한 코드 블록을 결정한다.

```javascript
if (조건식) {
	// 조건식이 참이면 이 코드 블록이 실행된다.
} else {
	// 조건식이 거짓이면 이 코드 블록이 실행된다.
}
```

- if 문의 조건식은 불리언 값으로 평가되어야 한다.
- if 문의 조건식이 불리언 값이 아닌 값으로 평가되면 자바스크립트 엔진에 의해 암묵적으로 불리언 값으로 강제 변환되어 실행할 코드 블록을 결정한다.

조건 식을 추가하여 조건에 따라 실행될 코드 블록을 늘리고 싶으면 else if 문을 사용한다.

```javascript
if (조건식1) {
	// 조건식1이 참이면 이 코드 블록이 실행된다.
} else if (조건식2) {
	// 조건식2가 참이면 이 코드 블록이 실행된다.
} else {
	// 조건식1과 조건식2가 모두 거짓이면 이 코드 블록이 실행된다.
}
```

- else if 문과 else 문은 옵션이기 때문에 사용할 수도 있고 사용하지 않을 수도 있다.
- if 문과 else 문은 2번 이상 사용할 수 없지만 else if문은 여러 번 사용할 수 있다.
- `코드 블록 내의 문이 하나뿐이라면 중괄호를 생략할 수 있다.`

```javascript
var num = 2;
var kind;

if (num > 0) kind = "양수";
else if (num < 0) kind = "음수";
else kind = "영";

console.log(kind); // 양수
```

경우의 수가 3가지일 때 삼항 조건 연산자 예시

```javascript
// 0은 false로 취급된다.

var num = 2;
var kind = num ? (num > 0 ? "양수" : "음수") : "영";

console.log(kind); // 양수
```

### `8.2.2 switch 문`

- switch 문은 주어진 표현식을 평가하여 그 값과 일치하는 표현식을 갖는 case문으로 실행 흐름을 옮긴다.
- case 문은 상황을 의미하는 표현식을 지정하고 콜론으로 마친 뒤 그 뒤에 실행할 문들을 위치시킨다.
- switch 문의 표현식과 일치하는 case 문이 없다면 실행 순서는 default 문으로 이동한다. default문은 선택사항이다.

```javascript
switch(표현식) {
  case 표현식1:
    switch 문의 표현식과 표현식1이 일치하면 실행될 문;
    break;
  case 표현식2:
    switch 문의 표현식과 표현식2가 일치하면 실행될 문;
    break;
  default:
    switch 문의 표현식과 일치하는 case 문이 없을 때 실행될 문;
}
```

- if...else 문의 조건식은 불리언 값으로 평가되어야 하지만 switch 문의 표현식은 불리언 값보다는 문자열이나 숫자 값인 경우가 많다.
- if...else 문은 논리적 참, 거짓으로 실행할 코드 블록을 결정한다.
- switch 문은 논리적 참, 거짓보다는 다양한 case에 따라 실행할 코드 블록을 결정할 때 사용한다.

`폴스루(fall through)`

- case 문에 해당하는 문의 마지막에 break 문을 사용하지 않으면 다음 case 값으로 계속 재할당이 되기 때문에 원하는 값을 가져오기 어렵다.
- 즉, case 문의 표현식과 일치하지 않아도 실행 흐름이 다음 case 문으로 이동한다.

추가적으로 default 문에서 break 문을 생략하는 것이 일반적이다. 그 이유는 default 문은 switch 문의 맨 마지막에 위치하므로 default 문의 실행이 종료되면 switch 문을 빠져나간다.

🔥 if...else 문으로 해결할 수 있다면 해결하는 편이 좋지만 조건이 너무 많다면 사용하는 편이 좋다.

## 8.3 반복문

반복문(loop statement)은 조건식의 평가 결과가 참인 경우 코드 블록을 실행한다. 그 후 조건식을 다시 평가하여 여전히 참인 경우 코드 블록을 다시 실행한다.
이는 조건이 거짓일 때까지 반복된다.

### `8.3.1 for 문`

for 문은 조건식이 거짓으로 평가될 때까지 코드 블록을 반복 실행한다.

```javascript
for (변수 선언문 또는 할당문; 조건식; 증감식;) {
  조건식이 참인 경우 반복 실행될 문;
}
```

```javascript
for (var i = 0; i < 2; i++) {
	console.log(i);
}
// 0
// 1
```

- for 문은 i 변수(for 문의 변수 선언문의 변수 이름은 반복을 의미하는 iteration의 i를 일반적으로 사용한다)가 0으로 초기화된 상태에서 시작하여 i가 2보다 작을 때까지 코드 블록을 2번 반복 실행한다.

for 문 내에 for 문을 중첩해 사용할 수 있다. 이를 중첩 for 문이라 한다.

```javascript
// 중첩 for 문을 활용해 주사위 2개 던져서 두 눈의 합이 6이되는 경우 출력

for (var i = 1; i <= 6; i++) {
	for (var j = 1; j <= 6; j++) {
		if (i + j === 6) console.log(`[${i},${j}]`);
	}
}

// [1, 5]
// [2, 4]
// [3, 3]
// [4, 2]
// [5, 1]
```

### `8.3.2 while 문`

while 문은 주어진 조건식의 평가 결과가 참이면 코드 블록을 계속해서 반복 실행한다.

- for 문은 반복 횟수가 명확할 때 주로 사용한다.
- while 문은 반복 횟수가 불명확할 때 주로 사용한다.

while 문은 조건문의 평가 결과가 거짓이 되면 코드 블록을 실행하지 않고 종료한다.

- 조건식의 평가 결과가 불리언 값이 아니면 불리언 값으로 강제 변환하여 논리적 참, 거짓을 구별한다.

```javascript
var count = 0;

// count가 3보다 작을 때까지 코드 블록을 계속 반복 실행한다.

while (count < 3) {
	console.log(count); // 0 1 2
	count++;
}
```

조건식의 평가 결과가 언제나 참이면 무한루프가 된다.

- 무한루프에서 탈출하기 위해서는 코드 블록 내에 if 문으로 탈출 조건을 만들고 break 문으로 코드 블록을 탈출한다.

```javascript
var count = 0;

// 무한루프

while (true) {
	console.log(count);
	count++;
	// count가 3이면 코드 블록을 탈출한다.
	if (count === 3) break;
}

// 0 1 2
```

### `8.3.3 do...while 문`

do...while 문은 코드 블록을 먼저 실행하고 조건식을 평가한다.

- 코드 블록은 무조건 한 번 이상 실행된다.

```javascript
var count = 0;

// count가 3보다 작을 때까지 코드 블록을 계속 반복 실행한다.

do {
	console.log(count); // 0 1 2
	count++;
} while (count < 3);
```

## 8.4 break 문

break 문은 코드 블록을 탈출한다. 좀 더 정확히 표현하자면 코드 블록을 탈출하는 것이 아니라 레이블 문(식별자가 붙은 문), 반복문(for, while 등) 또는 switch 문의 코드 블록을 탈출한다.

- 레이블 문, 반복문, switch 문의 코드 블록 외에 break 문을 사용하면 SyntaxError(문법 에러)가 발생한다.

```javascript
if(true){
  break;
}

// Uncaught SyntaxError: Illegal break statement
```

```javascript
// foo라는 레이블 식별자가 붙은 레이블 문

foo: console.log("foo");
```

- 레이블 문은 프로그램의 실행 순서를 제어하는 데 사용한다.
- 사실 switch 문의 case 문과 default 문도 레이블 문이다.
- 레이블 문을 탈출하려면 break 문에 레이블 식별자를 지정한다.

```javascript
foo: {
	console.log(1);
	break foo; // foo 레이블 블록문을 탈출한다.
	console.log(2);
}

console.log("Done");
```

### 🔥 문자열에서 특정 문자의 인덱스(위치)를 검색하는 예다.

```javascript
var string = "Hello, world";
var search = "l";
var index;

// 문자열은 유사 배열이므로 for 문으로 순회할 수 있다.

for (var i = 0; i < string.length; i++) {
	// 문자열의 개별 문자가 'l'이면
	if (string[i] === "l") {
		index = i;
		break;
	}
}

console.log(index); // 2

// 메서드 사용 시 같은 동작을 한다.

console.log(string.indexOf(search)); // 2
```

## 8.5 continue 문

continue 문은 반복문의 코드 블록 실행을 현 지점에서 중단하고 반복문의 증감식으로 실행 흐름을 이동시킨다. break 문처럼 반복문을 탈출하지는 않는다.

### 🔥 문자열에서 특정 문자의 개수 세기

```javascript
var string = "Hello World";
var search = "l";
var count = 0;

// 문자열은 유사 배열이므로 for 문으로 순회할 수 있다.

for (var i = 0; i < string.length; i++) {
	// 'l'이 아니면 현 지점에서 실행을 중단하고 반복문의 증감식으로 이동한다.
	if (string[i] !== search) continue;
	count++; // continue 문이 실행되면 이 문은 실행되지 않는다.
}

console.log(count); // 3

// String.prototype.match 메서드 사용 시 같은 동작을 한다.

const regexp = new RegExp(search, "g");
console.log(string.match(regexp).length); // 3
```

위 예제의 for 문은 다음 코드와 동일하게 동작한다.

```javascript
for (var i = 0; i < string.length; i++) {
	// 'l'이면 카운트를 증가시킨다.
	if (string[i] === search) count++;
}
```

- 위와 같이 if 문 내에서 실행해야 할 코드가 한 줄이면 그냥 간단하게 for 문만 사용하는 것이 편하다.
- if 문 내에서 실행해야 할 코드가 길다면 들여쓰기가 한 단계 더 깊어지므로 continue 문을 사용하는 편이 가독성이 좋다.

```javascript
// continue 문을 사용하지 않으면 if 문 내에 코드를 작성해야 한다.

for (var i = 0; i < string.length; i++) {
	// 'l'이면 카운트를 증가시킨다.
	if (string[i] === search) {
		count++;
		// code
		// code
		// code
	}
}

// continue 문을 사용하면 if 문 밖에 코드를 작성할 수 있다.

for (var i = 0; i < string.length; i++) {
	// 'l'이 아니면 카운트를 증가시키지 않는다.
	if (string[i] !== search) continue;

	count++;
	// code
	// code
	// code
}
```

## 📔 기억하고 싶은 내용

1. 일반적으로 코드는 위에서 아래 방향으로 순차적으로 실행된다. 제어문을 사용하면 코드의 실행 흐름을 인위적으로 제어할 수 있다. 이를 통해서 개발자가 원하는 값을 도출시킬 수 있도록 할 수 있다.
2. 블록문 끝에는 세미콜론을 붙이지 않는다. 자체종결성을 가지고 있기 때문이다.
3. for 문은 반복 횟수가 명확할 때 주로 사용하고, while 문은 반복 횟수가 불명확할 때 주로 사용한다.
