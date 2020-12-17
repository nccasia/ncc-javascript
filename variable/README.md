# Javascript Variable

Table of contents

1. [`var`, `let` and `const`](#1-var-let-and-const)
2. [reference vs primitive value](#2-reference-primitive)

Biến trong JavaScript được nhập lỏng lẻo, có nghĩa là, các biến có thể giữ giá trị với bất kỳ loại dữ liệu nào.

## 1. `var`, `let` and `const`

## 1.1 var

### Scope: function/locally scoped or globally scoped

Khi được khai báo trong function, `var` sẽ có scope là **function/locally scoped**, ngoài ra sẽ có scope **globally scoped**.

Đặc biệt, biến `var` còn có thêm tính chất **hoisting**: nghĩa là dù khai báo ở đâu thì biến đều sẽ được đem lên đầu scope trước khi code được thực hiện.

Ví dụ:

```javascript
console.log(greeting);
var greeting = "say hello";
```

sẽ được biên dịch là:

```javascript
var greeting;
console.log(greeting); // greeting is undefined
greeting = "say hello";
```

### Can be updated and re-declared

```javascript
var greeting = "hey hi";

if (true) {
  var greeting = "say Hello instead";
}

console.log(greeting); //"say Hello instead"
```

Vì thỏa điều kiện `if` nên `greeting` khi này sẽ tái khai báo(**re-declare**) và có giá trị là `"say Hello instead"` và sẽ vẫn giữ nguyên giá trị này sau khi thoát ra khỏi block `if`.

Nếu code của ta lên đến hàng trăm, nghìn dòng code, hoặc chúng ta cũng không biết được giá trị của biến liệu có bị thay đổi ở đoạn code nào sẽ dẫn đến việc khó khăn khi debug.

Để giải quyết vấn đề trên thì ES6 cung cấp cho chúng ta thêm 2 cách khác để khai báo biến bao gồm `let` và `const`.

## 1.2 let

### Scope: block scoped

Biến được khai báo bởi `let` có phạm vi trong block. Block là một đoạn code đc giới hạn bởi hai dấu ngoặc nhọn `{}` (curly braces).

```javascript
if (true) {
  let greeting = "say Hi";
  console.log(greeting); // "say Hi"
}

console.log(greeting); // Uncaught ReferenceError: greeting is not defined
```

### Can be updated but not re-declared

Biến khai báo bới let có thể được update nhưng không thể được khái báo lại.

```javascript
let greeting = "say Hi";
greeting = "say Hello instead";
```

```javascript
let greeting = "say Hi";
let greeting = "say Hello instead"; // Uncaught SyntaxError: Identifier 'greeting' has already been declared
```

## 1.3 const

Tương tự với `let`, `const` cũng có scope là **block scoped** và **hoisting**

Với biến có type là **primitive** (bao gồm string, number, boolean, null, và undefined) thì chúng ta sẽ không thể tái khai báo hay cập nhật giá trị mới để thay thế cho giá trị trước đó của biến.

```javascript
const greeting = "say Hi";
greeting = "say Hello instead"; // error : Assignment to constant variable.

const greeting = "say Hi";
const greeting = "say Hello instead"; // error : Identifier 'greeting' has already been declared
```

Với biến có type là **reference** (bao gồm object, array, và function) thì tuy không thể tái khai báo hay cập nhật giá trị của biến nhưng chúng ta vẫn có thể cập nhật giá trị cho thuộc tính của biến đó.

```javascript
const greeting = {
  message: "Hello",
  number: "five",
};

greeting.message = "say Hello instead";
console.log(greeting); // {message:"say Hello instead",number:"five"}
```

## 2. `reference` vs `primitive` value
