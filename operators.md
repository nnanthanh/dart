# Operators

Dart hỗ trợ các toán tử được hiển thị trong bảng sau. Bảng cho thấy sự liên kết của toán tử và mức
độ ưu tiên của toán tử Dart từ cao xuống thấp. Bạn có thể triển khai nhiều toán tử này dưới dạng
thành viên của lớp.

| Description              | Operator                                                                | Associativity |    |    |
|:-------------------------|:------------------------------------------------------------------------|:--------------|:---|:---|
| unary postfix            | `expr++`    `expr--`    `()`    `[]`    `?[]`    `.`    `?.`    `!`     | None          |    |    |
| unary prefix             | `-expr`    `!expr`    `~expr`    `++expr`    `--expr`      `await expr` | None          |    |    |
| multiplicative           | `*`   `/`    `%` `~/`                                                   | Left          |    |    |
| additive                 | `+`    `-`                                                              | Left          |    |    |
| shift                    | `<<`    `>>`    `>>>`                                                   | Left          |    |    |
| shift                    | `<<`   `>>`    `>>>`                                                    | Left          |    |    |
| bitwise AND              | &                                                                       | Left          |    |    |
| bitwise XOR              | ^                                                                       | Left          |    |    |
| bitwise OR               | \                                                                       | Left          |    |    |
| relational and type test | `>=`    `>`    `<=`    `<`    `as`    `is`    `is!`                     | None          |    |    |
| equality                 | `==`    `!=`                                                            | None          |    |    |
| logical AND              | `&&`                                                                    | Left          |    |    |
| logical OR               | \|                                                                       | Left          |    |    |
| if null                  | ??                                                                      | Left          |    |    |
| conditional              | `expr1` `?` `expr2` `:` `expr3`                                         | Right         |    |    |
| cascade                  | `..`    `?..`                                                           | Left          |    |    |
| assignment               | `=`    `*=`    `/=`   `+=`   `-=`   `&=`   `^=`   `etc.`                | Left          |    |    |
Khi bạn sử dụng toán tử, bạn tạo ra các biểu thức. Dưới đây là một số ví dụ về biểu thức toán tử:

```dart
a++
a + b
a = b
a == b
c ? a : b
a is T
```

## Operator precedence example

Trong bảng toán tử, mỗi toán tử có thứ tự ưu tiên cao hơn các toán tử ở các hàng tiếp theo. Ví dụ,
toán tử nhân `%` có thứ tự ưu tiên cao hơn toán tử bằng `=`, thứ tự ưu tiên cao hơn toán tử AND
logic `&&`. Điều đó có nghĩa là hai dòng mã sau đây sẽ thực thi theo cùng một cách:

```dart
// Dấu ngoặc giúp tăng tính đọc hiểu.
if ((n % i == 0) && (d % i == 0)) ...

// Khó đọc hơn, nhưng tương đương.
if (n % i == 0 && d % i == 0)
...
```

## Arithmetic operators

Trong Dart, hỗ trợ các toán tử số học thông thường, như được thể hiện trong bảng dưới đây.

| Operator | Meaning                                                                  |
|:---------|:-------------------------------------------------------------------------|
| +        | Add                                                                      |
| -        | Subtract                                                                 |
| -expr    | Unary minus, also known as negation (reverse the sign of the expression) |
| *        | Multiply                                                                 |
| /        | Divide                                                                   |
| ~/       | Divide, returning an integer result                                      |
| %        | Get the remainder of an integer division (modulo)                        |
| +        | Add                                                                      |
| +        | Add                                                                      |
| +        | Add                                                                      |
| +        | Add                                                                      |

Example:

```dart
assert(2 + 3 == 5);
assert(2 - 3 == -1);
assert(2 * 3 == 6);
assert(5 / 2 == 2.5); // Result is a double
assert(5 ~/ 2 == 2); // Result is an int
assert(5 % 2 == 1); // Remainder

assert('5/2 = ${5 ~/ 2} r ${5 % 2}' == '5/2 = 2 r 1');
```

| Operator | Meaning                                     |
|:---------|:--------------------------------------------|
| ++var    | var = var + 1 (expression value is var + 1) |
| var++    | var = var + 1 (expression value is var)     |
| --var    | var = var - 1 (expression value is var - 1) |
| var--    | var = var - 1 (expression value is var)     |

Example:

```dart
int a;
int b;

a = 0;
b = ++
a; // Increment a before b gets its value.
assert(a == b); // 1 == 1

a = 0;
b = a++; // Increment a after b gets its value.
assert(a != b); // 1 != 0

a = 0;
b = --a; // Decrement a before b gets its value.
assert(a == b); // -1 == -1

a = 0;
b = a--; // Decrement a after b gets its value.
assert(a != b); // -1 != 0
```

## Equality and relational operators

| Operator | Meaning                     |
|:---------|:----------------------------|
| `==`     | Equal; see discussion below |
| `!=`     | Not equal                   |
| `>`      | Greater than                |
| `<`      | Less than                   |
| `>=`     | Greater than or equal to    |
| `<=`     | Less than or equal to       |

Để kiểm tra xem hai đối tượng x và y đại diện cho cùng một thứ hay không, hãy sử dụng toán
tử `==`. (Trong trường hợp hiếm hoi bạn cần biết liệu hai đối tượng có phải là cùng một đối tượng
hay không, hãy sử dụng hàm `identical()` thay thế.) Đây là cách toán tử `==` hoạt động:

Nếu x hoặc y là null, trả về `true` nếu cả hai đều là null và `false` nếu chỉ một trong hai là null.
Trả về kết quả của việc gọi phương thức `==` trên x với đối số y. (Đúng vậy, các toán tử như `==` là
các phương thức được gọi trên toán hạng đầu tiên của chúng.

Dưới đây là một ví dụ về cách sử dụng từng toán tử bằng nhau và quan hệ:

```dart
assert(2 == 2);
assert(2 != 3);
assert(3 > 2);
assert(2 < 3);
assert(3 >= 3);
assert(2 <= 3);
```

## Type test operators

Các toán tử `as`, `is` và `is!` rất hữu ích để kiểm tra kiểu tại runtime.

| Operator | Meaning                                            |
|:---------|:---------------------------------------------------|
| as       | Typecast (also used to specify library prefixes)   |
| is       | True if the object has the specified type          |
| is!      | True if the object doesn’t have the specified type |

Kết quả của `obj` `is` `T` là true nếu `obj` triển khai giao diện được chỉ định bởi `T`. Ví dụ: `obj` `is` `Object?` luôn đúng.

Sử dụng toán tử as để chuyển đổi một đối tượng thành một kiểu cụ thể nếu và chỉ khi bạn chắc chắn rằng đối tượng có kiểu đó. Ví dụ đầu tiên:

```dart
(employee as Person).firstName = 'Bob';
```

Nếu bạn không chắc chắn rằng đối tượng có kiểu T, thì hãy sử dụng is T để kiểm tra kiểu trước khi sử dụng đối tượng. Ví dụ thứ 2:

```dart
if (employee is Person) {
  // Kiểm tra kiểu
  employee.firstName = 'Bob';
}
```

Lưu ý: Mã không tương đương. Nếu employee là null hoặc không phải là Person, thì ví dụ đầu tiên sẽ ném ra một ngoại lệ; ví dụ thứ hai không làm gì cả.

## Assignment operators

Như bạn đã thấy, bạn có thể gán giá trị bằng toán tử `=`. Để chỉ gán nếu biến được gán là null, hãy sử dụng toán tử `??=`.

```dart
// Gán giá trị cho a
a = value;
// Gán giá trị cho b nếu b là null; nếu không, b vẫn giữ nguyên
b ??= value;
```

Các toán tử gán kết hợp như `+=` kết hợp một phép toán với một phép gán.

|     |     |     |      |     |
|:----|:----|:----|:-----|:----|
| =   | *=  | %=  | >>>= | ^=  |
| +=  | /=  | <<= | &=   | \   |= |
| -=  | ~/= | >>= |      |     |

Dưới đây là cách thức hoạt động của các toán tử gán hợp chất:

|                       | Compound assignment | Equivalent expression |
|:----------------------|:--------------------|:----------------------|
| For an operator `op`: | a op= b             | a = a op b            |
| Example:              | a += b              | a = a + b             |

Ví dụ sau đây sử dụng các toán tử gán và gán hợp chất:

```dart
var a = 2; // Gán sử dụng =
a *= 3; // Gán và nhân: a = a * 3
assert(a == 6);
```

## Logical operators

Bạn có thể đảo ngược hoặc kết hợp các biểu thức boolean bằng cách sử dụng các toán tử logic.

| Operator | Meaning                                                                  |
|:---------|:-------------------------------------------------------------------------|
| !expr    | inverts the following expression (changes false to true, and vice versa) |
| \|\|        |logical OR|
| &&       | logical AND                                                              |

Ví dụ sau đây sử dụng các toán tử logic:

```dart
if (!done && (col == 0 || col == 3)) {
  // ...Làm gì đó...
}
```

## Bitwise and shift operators

Bạn có thể thao tác trên các bit riêng lẻ của các số trong Dart. Thông thường, bạn sẽ sử dụng các toán tử bitwise và shift này với các số nguyên.

| Operator | Meaning                                               |
|:---------|:------------------------------------------------------|
| &        | AND                                                   |
| \|                                                       |OR|
| ^        | XOR                                                   |
| ~expr    | Unary bitwise complement (0s become 1s; 1s become 0s) |
| <<       | Shift left                                            |
| >>       | Shift right                                           |
| >>>      | Unsigned shift right                                  |

Ví dụ sau đây sử dụng các toán tử bitwise và shift:

```dart
final value = 0x22;
final bitmask = 0x0f;

assert((value & bitmask) == 0x02); // AND
assert((value & ~bitmask) == 0x20); // AND NOT
assert((value | bitmask) == 0x2f); // OR
assert((value ^ bitmask) == 0x2d); // XOR

assert((value << 4) == 0x220); // Shift left
assert((value >> 4) == 0x02); // Shift right

// Ví dụ dịch sang phải cho kết quả khác nhau trên web
// vì giá trị toán hạng thay đổi khi được ẩn danh thành 32 bit:
assert((-value >> 4) == -0x03);

assert((value >>> 4) == 0x02); // Shift right không dấu
assert((-value >>> 4) > 0); // Shift right không dấu
```

Lưu ý về phiên bản: Toán tử >>> (được gọi là shift ba hoặc shift không dấu) yêu cầu phiên bản ngôn ngữ ít nhất là 2.14.

## Conditional expressions

Dart có hai toán tử cho phép bạn đánh giá các biểu thức một cách súc tích có thể được sử dụng nếu không thì cần có các câu lệnh if-else:

`condition` `?` `expr1` `:` `expr2`

Nếu `condition` là true, thì evaluate `expr1` (và trả về giá trị của nó); nếu không, evaluate và trả về giá trị của `expr2`.

`expr1` `??` `expr2`

Nếu `expr1` không phải là null, thì trả về giá trị của nó; nếu không, evaluate và trả về giá trị của `expr2`.

Khi bạn cần gán một giá trị dựa trên biểu thức boolean, hãy xem xét sử dụng `?` và `:`.

```dart
var visibility = isPublic ? 'public' : 'private';
```

Nếu biểu thức boolean kiểm tra null, hãy xem xét sử dụng `??`.

```dart
String playerName(String? name) => name ?? 'Guest';
```

Ví dụ trước đó có thể được viết ít nhất hai cách khác, nhưng không súc tích như vậy:

```dart
// Phiên bản dài hơn một chút sử dụng toán tử ?:.
String playerName(String? name) => name != null ? name : 'Guest';

// Phiên bản rất dài sử dụng câu lệnh if-else.
String playerName(String? name) {
if (name != null) {
return name;
} else {
return 'Guest';
}
}
```

## Cascade notation

Cascade (`..`, `?..`) cho phép bạn thực hiện một chuỗi các thao tác trên cùng một đối tượng. Ngoài việc truy cập các thành viên thể hiện, bạn cũng có thể gọi các phương thức thể hiện trên cùng một đối tượng. Điều này thường giúp bạn tiết kiệm bước tạo biến tạm thời và cho phép bạn viết mã mượt mà hơn.

Hãy xem xét đoạn mã sau:

```dart
var paint = Paint()
  ..color = Colors.black
  ..strokeCap = StrokeCap.round
  ..strokeWidth = 5.0;
```

Hàm tạo, `Paint()`, trả về một đối tượng `Paint`. Mã sau khi sử dụng cú pháp cascade hoạt động trên đối tượng này, bỏ qua bất kỳ giá trị nào có thể được trả về.

Ví dụ trước là tương đương với mã sau:

```dart
var paint = Paint();
paint.color = Colors.black;
paint.strokeCap = StrokeCap.round;
paint.strokeWidth = 5.0;
```

Nếu đối tượng mà cascade hoạt động có thể là null, thì hãy sử dụng cascade null-shorting (`?..`) cho thao tác đầu tiên. Bắt đầu bằng `?..` đảm bảo rằng không có thao tác cascade nào được thực hiện trên đối tượng null đó.

```dart
querySelector('#confirm') // Get an object.
  ?..text = 'Confirm' // Use its members.
  ..classes.add('important')
  ..onClick.listen((e) => window.alert('Confirmed!'))
  ..scrollIntoView()
```
Phiên bản ghi chú: Cú pháp `?..` yêu cầu phiên bản ngôn ngữ tối thiểu là 2.12.

Mã trước đó tương đương với mã sau:

```dart
var button = querySelector('#confirm');
button?.text = 'Confirm';
button?.classes.add('important');
button?.onClick.listen((e) => window.alert('Confirmed!'));
button?.scrollIntoView();
```

Bạn cũng có thể lồng các cascade vào nhau. Ví dụ:

```dart
final addressBook = (AddressBookBuilder()
      ..name = 'jenny'
      ..email = 'jenny@example.com'
      ..phone = (PhoneNumberBuilder()
            ..number = '415-555-0100'
            ..label = 'home')
          .build())
    .build();
```

Hãy cẩn thận khi xây dựng cascade trên một hàm trả về một đối tượng thực sự. Ví dụ, đoạn mã sau sẽ thất bại:

```dart
var sb = StringBuffer();
sb.write('foo')
  ..write('bar'); // Lỗi: phương thức 'write' không được định nghĩa cho 'void'.
```

sb.write() trả về void và bạn không thể xây dựng cascade trên void.

Lưu ý: Nghiêm ngặt mà nói, ký hiệu "double dot" cho cascade không phải là một toán tử. Đó chỉ là một phần của cú pháp Dart.

## Other operators

Bạn đã thấy hầu hết các toán tử còn lại trong các ví dụ khác:

| Operator | Name                          | Meaning                                                                                                                                                                                                                      |
|:---------|:------------------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `()`     | Ứng dụng hàm                  | Đại diện cho một cuộc gọi hàm                                                                                                                                                                                                |
| `[]`     | Truy cập chỉ mục              | Đại diện cho một cuộc gọi đến toán tử `[]` có thể ghi đè; ví dụ: `fooList[1]` truyền int `1` cho `fooList` để truy cập phần tử ở vị trí `1`                                                                                  |
| `?[]`    | Truy cập chỉ mục có điều kiện | Giống như `[]`, nhưng toán hạng bên trái có thể là null; ví dụ: `fooList?[1]` truyền int `1` cho `fooList` để truy cập phần tử ở vị trí 1 trừ khi `fooList` là null (trong trường hợp này, biểu thức sẽ đánh giá thành null) |
|      `.`                                                                                                                                                                                                                                                                 |Truy cập thành viên|Tham chiếu đến thuộc tính của một biểu thức; ví dụ: `foo.bar` chọn thuộc tính `bar` từ biểu thức `foo`|
|`?.` |Truy cập thành viên có điều kiện|Giống như `.`, nhưng toán hạng bên trái có thể là null; ví dụ: `foo?.bar` chọn thuộc tính `bar` từ biểu thức `foo` trừ khi foo là null (trong trường hợp này, giá trị của `foo?.bar` là null)|
|`!`|	Toán tử khẳng định null|Chuyển đổi một biểu thức thành kiểu không phải null cơ bản của nó, ném một ngoại lệ runtime nếu việc chuyển đổi không thành công; ví dụ: `foo!.bar` khẳng định `foo` không phải là null và chọn thuộc tính `bar`, trừ khi `foo` là null trong trường hợp đó, một ngoại lệ thời gian chạy sẽ được ném|
