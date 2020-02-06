


# Tổng hợp câu hỏi phỏng vấn Javascript về Front-end lẫn Back-end 
![enter image description here](https://i.imgur.com/9P7ipCX.png)
Các câu hỏi bên dưới chủ yếu về Javascript bao gồm cả Front-end lẫn Back-end. Rất mong sẽ giúp ích cho các bạn trong quá trình ôn luyện Javascript cũng như chuẩn bị phỏng vấn .

Nếu thích hãy để lại cho mình **1 STAR** nhé . Nếu bạn nào có câu hỏi hay và muốn đóng góp để repository này ngày càng chất lượng đừng ngần ngại **Create Pull Request** để đăng câu mới nhé ! 

# Người đóng góp :

 - [@quangpl](https://github.com/quangpl) 

## Câu 1. Sự khác biệt giữa `undefined` và ` not defined` trong JavaScript

### Câu trả lời

Trong JavaScript nếu bạn  sử dụng một biến không tồn tại và chưa được khai báo, thì JavaScript sẽ đưa ra một lỗi  `var name is not defined` và các  lệnh sẽ ngừng thực thi sau đó. Nhưng nếu bạn sử dụng `typeof undeclared_variable` thì nó sẽ trả về `undefined`.

Tiếp theo, hãy hiểu sự khác biệt giữa khai báo và định nghĩa.

`var x` là một khai báo vì bạn chưa xác định giá trị của nó, nhưng bạn đang khai báo sự tồn tại của nó và nhu cầu cấp phát bộ nhớ cho chính nó

```javascript
var x; // khai báo x
console.log (x); // kết quả : undefined
```

`var x = 1` bao gồm cả khai báo và định nghĩa (chúng ta cũng có thể nói rằng chúng ta đang thực hiện khởi tạo), Ở đây xảy ra 2 việc là khai báo và gán giá trị cho biến x . Trong JavaScript, mọi khai báo biến và khai báo hàm đều được đưa lên đầu phạm vi hiện tại của nó sau đó mới được sử dụng và thuật ngữ này gọi là  `hoising`.

Một biến có thể được khai báo nhưng không được xác định giá trị . Và dĩ nhiên giá trị của nó là  `undefined`.

```javascript
var x; // khai báo biến x 
typeof x === 'undefined'; // kết quả : true 
```

Một biến có thể không được khai báo cũng không được định nghĩa. Khi chúng ta  tham chiếu đên biến đó thì kết quả sẽ là `undefined`.

```
console.log (y); // Kết quả:  ReferenceError: y is not defined
```

### Tham khảo :
[http://stackoverflow.com/questions/20822022/javascript-variable-definition-declaration](http://stackoverflow.com/questions/20822022/javascript-variable-definition-declaration)


## Câu 2. Với giá trị nào của `x` thì kết quả của các câu lệnh sau không giống nhau?


```javascript
//  if( x <= 100 ) {...}
//  if( !(x > 100) ) {...}
```
### Câu trả lời

`NaN <= 100` là` false` và` NaN> 100` cũng là` false`, vì vậy nếu
giá trị của `x` là `NaN`, các câu lệnh không giống nhau.

Điều tương tự cũng xảy ra với bất kỳ giá trị nào của x khi trả về  **NaN**, ví dụ: `undefined`,` [1,2,5] `,` {a: 22} `, v.v.

Đây là lý do tại sao bạn cần chú ý khi  xử lý các biến . `NaN` có thể bằng nhau, nhỏ hơn hoặc nhiều hơn bất kỳ giá trị số nào khác, vì vậy cách tốt nhất để kiểm tra xem giá trị đó có phải là `NaN` hay không, là sử dụng hàm ` isNaN () `.

## Câu  3. Hạn chế của việc khai báo hàm  trực tiếp bằng các đối tượng JavaScript là gì?

### Câu trả lời

Một trong những nhược điểm của việc khai báo các hàm trực tiếp bằng các đối tượng JavaScript là chúng quản lý bộ nhớ rất kém . Song song đó, một bản sao mới của hàm được tạo cho mỗi phiên bản của một đối tượng (biến). Hãy xem ví dụ bên dưới :

```javascript
var Employee = function (name, company, salary) {
  this.name = name || "";       
  this.company = company || "";
  this.salary = salary || 5000;

  // Tạo một hàm/phương thức mới bằng cách này :
  this.formatSalary = function () {
      return "$ " + this.salary;
  };
};

// Chúng ta cũng có thể tạo hàm/phương thức mới bằng prototype:
Employee.prototype.formatSalary2 = function() {
    return "$ " + this.salary;
}

// Tạo mới các đối tượng với các đối tượng khác nhau 
var emp1 = new Employee('Yuri Garagin', 'Company 1', 1000000);
var emp2 = new Employee('Dinesh Gupta', 'Company 2', 1039999);
var emp3 = new Employee('Erich Fromm', 'Company 3', 1299483);
```

Ở đây, mỗi biến đối tượng `emp1`,` emp2`, `emp3` có bản sao riêng của phương thức` formatSalary`. Tuy nhiên, `formatSalary2` sẽ chỉ được thêm một lần vào một đối tượng `Employee.prototype`.

## Câu  4. Thế nào là closure trong javascript? bạn có thể cho một ví dụ?

### Câu trả lời

Closure là một hàm được định nghĩa bên trong một hàm khác (được gọi là hàm cha) và có quyền truy cập vào biến được khai báo và định nghĩa trong phạm vi hàm cha.

Closure có quyền truy cập vào biến trong ba phạm vi:
- Biến được khai báo trong phạm vi của chính mình
- Biến được khai báo trong phạm vi hàm cha
- Biến toàn cục 

```javascript
var globalVar = "abc";


(function outerFunction (outerArg) { // bắt đầu phạm vi của  outerFunction
  // Biến bên trong phạm vi của outerFunction  
  var outerFuncVar = 'x';    
  //  Hàm close tự gọi 
  (function innerFunction (innerArg) { // bắt đầu phạm vi của innerFunction
    // Biến được khai báo và định nghĩa bên trong pham vi của innerFunction 
    var innerFuncVar = "y";
    console.log(         
      "outerArg = " + outerArg + "\n" +
      "outerFuncVar = " + outerFuncVar + "\n" +
      "innerArg = " + innerArg + "\n" +
      "innerFuncVar = " + innerFuncVar + "\n" +
      "globalVar = " + globalVar);
  //kết thúc phạm vi của  innerFunction
  })(5); // Truyền tham số 5 
// kết thúc phạm vi của  outerFunction
})(7); //Truyền tham số 7
```


innerFunction là một Closure được định nghĩa bên trong outerFunction và có quyền truy cập vào tất cả các biến được khai báo và định nghĩa trong phạm vi hàm cha. Ngoài chức năng này thì Closure có quyền truy cập vào biến toàn cục .


## Câu 5. Viết hàm `mul` để được kết quả như bên dưới 

`` `javascript
console.log (mul (2) (3) (4)); // kết quả: 24
console.log (mul (4) (3) (4)); // kết quả: 48
`` `
### Câu trả lời

Dưới đây là code để giải đề trên : 
```javascript
function mul (x) {
  return function (y) { // hàm ẩn danh 
    return function (z) { // hàm ẩn danh 
      return x * y * z;
    };
  };
}
```

Ở đây, hàm `mul`  nhận đối số thứ nhất và trả về hàm ẩn danh nhận tham số thứ hai và trả về hàm ẩn danh nhận tham số thứ ba và trả về phép nhân của các đối số được truyền liên tiếp

Trong hàm Javascript được định nghĩa bên trong có quyền truy cập vào biến hàm ngoài và hàm là đối tượng lớp đầu tiên để nó cũng có thể được trả về bởi hàm và được truyền dưới dạng đối số trong hàm khác.
Một số điểm cần lưu ý : 
- Hàm là một hình thức khác của loại Đối tượng
- Một hàm có thể có các thuộc tính và có một liên kết trả về hàm constructor của nó
- Một hàm có thể được lưu trữ dưới dạng biến
- Một hàm có thể được truyền dưới dạng tham số cho hàm khác
- Một hàm  có thể được trả về từ một hàm  khác

## Câu 6. Làm thế nào để làm trống một mảng trong JavaScript?
Ví dụ:

```javascript
var arrayList =  ['a', 'b', 'c', 'd', 'e', 'f'];
```

Làm thế nào chúng ta có thể làm trống mảng trên?

### Câu trả lời
Chúng ta hãy thử qua các cách sau đây 

#### Cách 1

```
javascript
arrayList = [];
```

Đoạn mã trên sẽ làm cho biến ArrayList thành một mảng trống mới. Cách này được khuyến nghị nếu bạn không có **tham chiếu đến mảng ban đầu** Ví dụ:

```javascript
var arrayList = ['a', 'b', 'c', 'd', 'e', 'f']; // Tạo mảng 
var anotherArrayList = arrayList;  // Tham chiếu đến arrayList từ một biến khác 
arrayList = []; // Làm trống mảng đó 
console.log(anotherArrayList); // Kết quả  ['a', 'b', 'c', 'd', 'e', 'f']
```

#### Cách 2

```javascript
arrayList.length = 0;
```
Code trên sẽ xóa mảng hiện có bằng cách đặt độ dài của nó thành 0. Cách làm này  cũng sẽ cập nhật tất cả các biến tham chiếu trỏ đến mảng ban đầu.

Ví dụ:

`` `javascript
var arrayList = ['a', 'b', 'c', 'd', 'e', 'f']; // Tạo mảng 
var anotherArrayList = arrayList;  // Tham chiếu đến  arrayList từ một biến khác 
arrayList.length = 0; // Làm rỗng mảng 
console.log(anotherArrayList); // Kết quả :  []
`` `


#### Cách 3

```javascript
while(arrayList.length) {
  arrayList.pop();
}
```

Cách mình vừa  thực hiện cũng có thể làm trống mảng. Nhưng không nên sử dụng thường xuyên. 

## Câu 7 . Kết quả của đoạn code sau đây?


```javascript
var output = (function(x) {
  delete x;
  return x;
})(0);

console.log(output);
```

### Câu trả lời

Đoạn mã trên sẽ xuất ra `0` . Toán tử `delete` được sử dụng để xóa một thuộc tính khỏi một đối tượng. Ở đây `x` không phải là một đối tượng, nó là ** biến cục bộ **. Toán tử `delete` không ảnh hưởng đến các biến cục bộ.



## Câu 8. Kết quả của đoạn code sau đây ?


```javascript
var x = 1;
var output = (function() {
  delete x;
  return x;
})();

console.log(output);
```
### Câu trả lời

Đoạn mã trên sẽ xuất ra `1` . Toán tử `delete` được sử dụng để xóa một thuộc tính khỏi một đối tượng. Ở đây `x` không phải là một đối tượng, nó là ** biến toàn cục ** thuộc loại` number`.


## Câu 9. Kết quả của đoạn code sau đây ?


```javascript
var x = { foo : 1};
var output = (function() {
  delete x.foo;
  return x.foo;
})();

console.log(output);
```
### Câu trả lời

Đoạn mã trên sẽ xuất ra `undefined` .  Toán tử `delete` được sử dụng để xóa một thuộc tính khỏi một đối tượng. Ở đây `x` là một đối tượng có foo là một thuộc tính và từ một  hàm IIFE, mình  đang xóa thuộc tính`foo` của đối tượng` x` và sau khi xóa, mình đang tham chiếu thuộc tính đã xóa **foo**  nên kết quả sẽ là `undefined`.

## Câu 10.  Kết quả của đoạn code sau đây ?

```javascript

var Employee = {
  company: 'xyz'
}
var emp1 = Object.create(Employee);
delete emp1.company
console.log(emp1.company);
```

### Câu trả lời
Đoạn mã trên sẽ xuất ra `xyz` . Ở đây, đối tượng `emp1` có company là  **prototype**, xóa toán tử không xóa thuộc tính **prototype**

Đối tượng `emp1` không có ** company** làm thuộc tính  của mình. bạn có thể kiểm tra bằng cách  `console.log (emp1.hasOwnProperty ('company')); // Kết quả : false` Tuy nhiên, chúng ta có thể xóa thuộc tính **company** khỏi đối tượng `Employee` bằng cách sử dụng `delete Employee.company` hoặc chúng ta cũng có thể xóa khỏi đối tượng `emp1` bằng cách sử dụng thuộc tính `__proto__`  và  `delete emp1.__proto__.company`.


## Câu 11. `undefined x 1` trong JavaScript là gì?

```javascript
var trees = ["redwood", "bay", "cedar", "oak", "maple"];
delete trees[3];
```

### Câu trả lời
  - Khi bạn chạy code trên và `console.log(trees);` và bạn sẽ nhận được kết quả `["redwood", "bay", "cedar", undefined × 1, "maple"]`
  - Trong các phiên bản gần đây của Chrome, bạn sẽ thấy từ  `empty` thay vì  `undefined x 1`
  - Khi bạn chạy  trên trình duyệt Firefox thì bạn sẽ nhận được kết quả   `["redwood", "bay", "cedar", undefined, "maple"]`
  
Rõ ràng, Chrome có cách hiển thị  cho các index chưa được khởi tạo trong các mảng. Tuy nhiên, khi bạn kiểm tra  `trees[3] === undefined` trong bất kỳ trình duyệt nào, bạn sẽ nhận được kết quả là ` true`. Rõ ràng `undefined x 1` đại diện cho các phần tử hay index chưa được khởi tạo.


  
## Câu 12. Kết quả của đoạn code bên dưới là gì?

```javascript
var trees = ["xyz", "xxxx", "test", "ryan", "apple"];
delete trees[3];
console.log(trees.length);
```
### Câu trả lời  
Kết qủa của đoạn code bên trên là `5`. Khi chúng ta sử dụng toán tử `delete` để xoá mảng các phần tử , thì độ dài mảng sẽ không ảnh hưởng. Điều này luôn đúng nếu bạn dùng `delete` cho từng phần tử của mảng.

Bởi vì khi ta dùng toán tử `delete` để xoá các phần tử của mảng thì các phần từ đó sẽ được chuyển thành `undefined x 1` nên độ dài mảng không thay đổi là tất nhiên . Còn `undefined x 1` là gì, mời xem 
  
## Câu 13. Kết quả của đoạn code bên dưới là gì?

```javascript
var bar = true;
console.log(bar + 0);   
console.log(bar + "xyz");  
console.log(bar + true);  
console.log(bar + false);
```
### Câu trả lời

Kết quả của đoạn code sẽ là `1, "truexyz", 2, 1` , bởi vì ta có quy luật sau : 
  - Số + Số  -> Phép cộng 
  - Biến Boolean + Số  -> Phép cộng 
  - Biến Boolean + Biến Boolean --> Phép cộng 
  - Số + Chuỗi  ->  Phép nối chuỗi 
  - Chuỗi + Biến Boolean  ->  Phép nối chuỗi 
  - Chuỗi + Chuỗi   ->  Phép nối chuỗi 


  
## Câu 14. Kết quả của đoạn code bên dưới là gì?

```javascript
var z = 1, y = z = typeof y;
console.log(y);
```
### Câu trả lời


Kết quả của code bên trên sẽ là  `"undefined"` .Theo như quy luật toán tử kết hợp với mức độ ưu tiên như nhau. Quy luật của toán tử gán là `Phải sang trái ` nên `typeof y` sẽ được xem xét đầu tiên và giá trị hiện tại của nó là  `"undefined"` và gán cho  `z`  sau đó gán cho `y` nên ta được kết quả như trên. 
Code sẽ được thực hiện theo thứ tự bên dưới 
```javascript
var z;
z = 1;
var y;
z = typeof y;
y = z;


  
## Câu 15. Kết quả của đoạn code bên dưới là gì?

  
```javascript
// NFE (Named Function Expression)
var foo = function bar() { return 12; };
typeof bar();
```

### Câu trả lời

 Kết quả sẽ là `Reference Error`. Để khắc phục lỗi trên ta sẽ thực hiện như sau : 

**Cách 1**
```javascript
var bar = function() { return 12; };
typeof bar();
```

**Cách 2**

```javascript
function bar() { return 12; };
typeof bar();
```

Định nghĩa hàm chỉ có thể có một biến tham chiếu đó  là tên hàm , Ở Cách 1 `bar` tham chiếu đến một  `anonymous function` và trong Cách 2 chúng ta có định nghĩa `bar` là một tên hàm 

```javascript
var foo = function bar() {
  // foo is visible here
  // bar is visible here
  console.log(typeof bar()); // Works here :)
};
// foo is visible here
// bar is undefined here
```

**CẬP NHẬT MỖI TUẦN - NHỚ STAR ĐỂ THEO DÕI CÂU HỎI MỚI NHÉ** 


