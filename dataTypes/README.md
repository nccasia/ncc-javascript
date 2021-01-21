# Javascript DataTypes

Table of contents

1. [Array](#1-array)
2. [Object](#2-object)

# 1. Array

Mảng là cấu trúc dữ liệu đặc biệt để lưu trữ các bộ sư tập theo thứ tự.

## Declaration

Có 2 cách tạo ra 1 mảng rỗng

```javascript
let arr = new Array();
let arr = [];
```

Khai báo mảng với phần tử ban đầu

```javascript
let fruits = ["Apple", "Orange", "Plum"];
```

Các phần tử của mảng được đánh số, bắt đầu từ 0.

```javascript
let fruits = ["Apple", "Orange", "Plum"];

alert(fruits[0]); // Apple
alert(fruits[1]); // Orange
alert(fruits[2]); // Plum
```

Một mảng có thể lưu trữ các phần tử thuộc bất kỳ kiểu nào.

```javascript
// mix of values
let arr = [
  "Apple",
  { name: "John" },
  true,
  function () {
    alert("hello");
  },
];

// get the object at index 1 and then show its name
alert(arr[1].name); // John

// get the function at index 3 and run it
arr[3](); // hello
```

### Trailing comma

```javascript
let fruits = ["Apple", "Orange", "Plum"];
```

Một mảng, giống như một đối tượng, có thể kết thúc bằng ",". Kiểu **trailing comma** giúp chèn / xóa các mục dễ dàng hơn vì tất cả các dòng trở nên giống nhau.

## Methods pop/push, shift/unshift

- push: thêm một phần tử vào cuối.

```javascript
let fruits = ["Apple", "Orange"];

fruits.push("Pear");

alert(fruits); // Apple, Orange, Pear
```

- pop: thêm một phần tử vào cuối.

```javascript
let fruits = ["Apple", "Orange", "Pear"];

alert(fruits.pop()); // remove "Pear" and alert it

alert(fruits); // Apple, Orange
```

- shift: lấy một phần tử ngay từ đầu, tiến hàng đợi, để phần tử thứ 2 trở thành phần tử thứ nhất.

```javascript
let fruits = ["Apple", "Orange", "Pear"];

alert(fruits.shift()); // remove Apple and alert it

alert(fruits); // Orange, Pear
```

- unshift: thêm 1 phần tử vào đầu mảng

```javascript
let fruits = ["Apple"];

fruits.push("Orange", "Peach");
fruits.unshift("Pineapple", "Lemon");

// ["Pineapple", "Lemon", "Apple", "Orange", "Peach"]
alert(fruits);
```

**Don’t compare arrays with ==**

## Array methods

### Add/remove items

- **splice**: có dùng để chèn, xóa hoặc thay thế các phần tử

  Cú pháp:

```javascript
arr.splice(start[, deleteCount, elem1, ..., elemN])
```

```javascript
let arr = ["I", "study", "JavaScript"];

// from index 2
// delete 0
// then insert "complex" and "language"
arr.splice(2, 0, "complex", "language");

alert(arr); // "I", "study", "complex", "language", "JavaScript"
```

```javascript
let arr = ["I", "study", "JavaScript"];

arr.splice(1, 1); // from index 1 remove 1 element

alert(arr); // ["I", "JavaScript"]
```

```javascript
let arr = ["I", "study", "JavaScript", "right", "now"];

// remove 3 first elements and replace them with another
arr.splice(0, 3, "Let's", "dance");

alert(arr); // now ["Let's", "dance", "right", "now"]
```

- **slice**: Trả về 1 mảng mới tất cả các phần tử từ đầu đến cuối

  Cú pháp:

```javascript
arr.slice([start], [end]);
```

```javascript
let arr = ["t", "e", "s", "t"];

alert(arr.slice(1, 3)); // e,s (copy from 1 to 3)

alert(arr.slice(-2)); // s,t (copy from -2 till the end)
```

- **concat**: tạo một mảng mới bao gồm các giá trị từ các mảng khác và các mục bổ sung.

  Cú pháp:

```javascript
arr.concat(arg1, arg2...);
```

```javascript
let arr = [1, 2];

// create an array from: arr and [3,4]
alert(arr.concat([3, 4])); // 1,2,3,4

// create an array from: arr and [3,4] and [5,6]
alert(arr.concat([3, 4], [5, 6])); // 1,2,3,4,5,6

// create an array from: arr and [3,4], then add values 5 and 6
alert(arr.concat([3, 4], 5, 6)); // 1,2,3,4,5,6
```

### Iterate

- **forEach**: chạy một hàm cho mọi phần tử của mảng.

  Cú pháp:

```javascript
arr.forEach((item, index, array) => {
  // ... do something with item
});
```

```javascript
["Bilbo", "Gandalf", "Nazgul"].forEach((item, index, array) => {
  alert(`${item} is at index ${index} in ${array}`);
});
```

### Searching in array

- **indexOf/lastIndexOf and includes**

  `arr.indexOf (item, from)` - tìm kiếm mục bắt đầu từ chỉ mục từ và trả về chỉ mục nơi nó được tìm thấy, nếu không thì -1.

  `arr.lastIndexOf (item, from)`- giống nhau, nhưng tìm từ phải sang trái.

  `arr.includes (item, from)` - tìm kiếm item bắt đầu từ index from, trả về true nếu tìm thấy.

```javascript
let arr = [1, 0, false];

alert(arr.indexOf(0)); // 1
alert(arr.indexOf(false)); // 2
alert(arr.indexOf(null)); // -1

alert(arr.includes(1)); // true
```

- **find and findIndex**

  Cú pháp:

```javascript
let result = arr.find((item, index, array) => {
  // if true is returned, item is returned and iteration is stopped
  // for falsy scenario returns undefined
});
```

```javascript
let users = [
  { id: 1, name: "John" },
  { id: 2, name: "Pete" },
  { id: 3, name: "Mary" },
];

let user = users.find((item) => item.id == 1);

alert(user.name); // John
```

`findIndex` tương tự như find nhưng nó sẽ trả về chỉ mục nơi phần tử được tìm thấy và -1 nếu ko có kết quả nào.

- **filter**

  Cú pháp tương tự như `find`, nhưng nó trả về một mảng gồm tất cả các phần tử phù hợp:

```javascript
let results = arr.filter((item, index, array) => {
  // if true item is pushed to results and the iteration continues
  // returns empty array if nothing found
});
```

```javascript
let users = [
  { id: 1, name: "John" },
  { id: 2, name: "Pete" },
  { id: 3, name: "Mary" },
];

// returns array of the first two users
let someUsers = users.filter((item) => item.id < 3);

alert(someUsers.length); // 2
```

### Transform an array

- **map**

  Nó gọi hàm cho từng phần tử của mảng và trả về mảng kết quả. Cú pháp:

```javascript
let result = arr.map((item, index, array) => {
  // returns the new value instead of item
});
```

```javascript
let lengths = ["Bilbo", "Gandalf", "Nazgul"].map((item) => item.length);
alert(lengths); // 5,7,6
```

- **sort**

  Cú pháp:

```javascript
arr.sort((a, b) => {
  if (a > b) return 1; // if the first value is greater than the second
  if (a == b) return 0; // if values are equal
  if (a < b) return -1; // if the first value is less than the second
});
```

**Use localeCompare for strings**

```javascript
let countries = ["Österreich", "Andorra", "Vietnam"];

alert(countries.sort((a, b) => (a > b ? 1 : -1))); // Andorra, Vietnam, Österreich (wrong)

alert(countries.sort((a, b) => a.localeCompare(b))); // Andorra,Österreich,Vietnam (correct!)
```

- **reverse**

  đảo ngược thứ tự của các phần tử trong mảng

```javascript
let arr = [1, 2, 3, 4, 5];
arr.reverse();

alert(arr); // 5,4,3,2,1
```

- **split and join**

`split`: chia chuỗi thành một mảng bằng dấu phân cách đã cho.

```javascript
let names = "Bilbo, Gandalf, Nazgul";

let arr = names.split(", ");

for (let name of arr) {
  alert(`A message to ${name}.`); // A message to Bilbo  (and other names)
}
```

`join`: tạo ra chuỗi được nối bằng dấu phân cách đã cho.

```javascript
let arr = ["Bilbo", "Gandalf", "Nazgul"];

let str = arr.join(";"); // glue the array into a string using ;

alert(str); // Bilbo;Gandalf;Nazgul
```

- **reduce/reduceRight**

  được sử dụng để tính toán một giá trị duy nhất dựa trên mảng. `reduce` đi từ trái sang phải và `reduceRight` thì ngược lại.

```javascript
let value = arr.reduce(
  function (accumulator, item, index, array) {
    // ...
  },
  [initial]
);
```

```javascript
let arr = [1, 2, 3, 4, 5];

let result = arr.reduce((sum, current) => sum + current, 0);

alert(result); // 15
```

### Array.isArray

Dùng để kiểm tra `arr` có phải là mảng hay không

# 2. Object

- **keys**: Trả về 1 mảng các khóa

- **values**: Trả về 1 mảng các giá trị

- **entries**: Trả về 1 mảng mà phần tử là mảng chứa khóa và giá trị

```javascript
let user = {
  name: "John",
  age: 30,
};

Object.keys(user); // ["name", "age"]
Object.values(user); // ["John", 30]
Object.entries(user); // [ ["name","John"], ["age",30] ]
```
