# Variables
Dưới đây là ví dụ về cách tạo một biến và khởi tạo giá trị cho nó:

```dart
var name = 'Bob';
```

Biến lưu trữ các tham chiếu. Biến được gọi là `name` chứa một tham chiếu tới một đối tượng chuỗi `String` có giá trị là "Bob".

Kiểu dữ liệu của biến `name` được suy ra là `String`, nhưng bạn có thể thay đổi kiểu đó bằng cách chỉ định nó. Nếu một đối tượng không bị giới hạn bởi một kiểu duy nhất, bạn có thể chỉ định kiểu `Object` (hoặc `dynamic` nếu cần).

```dart
Object name = 'Bob';
```

Một lựa chọn khác là khai báo rõ ràng kiểu mà nó sẽ được suy ra:

```dart
String name = 'Bob';
```

## Null safety

Ngôn ngữ Dart áp dụng tính an toàn với giá trị null.

`Null safety` ngăn chặn lỗi phát sinh do việc truy cập không cố ý đến các biến được đặt là null. Lỗi này được gọi là lỗi null dereference. Lỗi null dereference xảy ra khi bạn truy cập vào một thuộc tính hoặc gọi một phương thức trên một biểu thức mà có giá trị là null. Một ngoại lệ cho quy tắc này là khi null hỗ trợ thuộc tính hoặc phương thức đó, ví dụ như `toString()` hoặc `hashCode`. Với tính an toàn với null, trình biên dịch Dart phát hiện các lỗi tiềm ẩn này vào thời điểm biên dịch.

Ví dụ, giả sử bạn muốn tìm giá trị tuyệt đối của một biến số nguyên `i`. Nếu `i` là null, việc gọi `i.abs()` sẽ gây ra một lỗi null dereference. Trong các ngôn ngữ khác, việc thử này có thể dẫn đến lỗi thời gian chạy, nhưng trình biên dịch Dart ngăn chặn những hành động này. Do đó, ứng dụng Dart không thể gây ra lỗi thời gian chạy.

`Null safety` giới thiệu ba thay đổi chính:

1. Khi bạn chỉ định một kiểu cho biến, tham số hoặc một thành phần liên quan khác, bạn có thể kiểm soát xem kiểu có cho phép giá trị null hay không. Để cho phép nullability, bạn thêm một dấu ? vào cuối khai báo kiểu.

```dart
String? name; // Kiểu có thể là null. Có thể là `null` hoặc chuỗi.
String name;   // Kiểu không thể là null. Không thể là `null` nhưng có thể là chuỗi.
```

2. Bạn phải khởi tạo biến trước khi sử dụng chúng. Các biến có khả năng là null mặc định là null, vì vậy chúng được khởi tạo theo mặc định. Dart không thiết lập giá trị khởi tạo cho các kiểu không thể là null. Nó buộc bạn phải đặt một giá trị ban đầu. Dart không cho phép bạn quan sát một biến chưa được khởi tạo. Điều này ngăn bạn truy cập vào các thuộc tính hoặc gọi phương thức trong trường hợp kiểu của người nhận có thể là null nhưng null không hỗ trợ phương thức hoặc thuộc tính được sử dụng.

3. Bạn không thể truy cập thuộc tính hoặc gọi phương thức trên biểu thức có kiểu có thể là null. Ngoại lệ tương tự được áp dụng khi đó là một thuộc tính hoặc phương thức mà null hỗ trợ như `hashCode` hoặc `toString()`.

`Null safety` biến đổi các lỗi tiềm ẩn thời gian chạy thành lỗi phân tích thời gian biên dịch. Tính an toàn với null đánh dấu một biến không phải là null khi nó đã:

- Không được khởi tạo với giá trị không phải là null.
- Gán giá trị null.

Kiểm tra này cho phép bạn sửa các lỗi này trước khi triển khai ứng dụng.

## Default value
Các biến chưa được khởi tạo có kiểu có thể là null có giá trị ban đầu là null. Thậm chí các biến có kiểu số cũng ban đầu là null, bởi vì các số giống như mọi thứ khác trong Dart là các đối tượng.

```dart
int? lineCount;
assert(lineCount == null);
```
- Dòng đầu tiên khai báo một biến `lineCount` có kiểu `int?`, tức là nó có thể có giá trị là null hoặc một số nguyên.

- Dòng thứ hai sử dụng assert để kiểm tra xem biến `lineCount` có phải là null hay không. Nếu điều kiện này sai (tức là `lineCount` không phải là null), một ngoại lệ sẽ được ném ra, làm dừng chương trình và hiển thị một thông báo lỗi tương ứng.

- Lưu ý rằng mã kiểm tra này chỉ được thực hiện trong quá trình phát triển và kiểm tra, và không ảnh hưởng đến chạy ứng dụng ở bản phát hành. Trong bản phát hành, các dòng `assert` thường được bỏ qua.

Với `null safety`, bạn phải khởi tạo giá trị của các biến không thể là null trước khi sử dụng chúng:
```dart
int lineCount = 0;
```

Bạn không cần phải khởi tạo một biến cục bộ tại chỗ nó được khai báo, nhưng bạn phải gán một giá trị cho nó trước khi sử dụng. Ví dụ, mã sau đây là hợp lệ vì Dart có thể phát hiện ra rằng `linCount` không thể là null vào thời điểm nó được chuyển cho hàm `print()`:

```dart
int lineCount;

if (weLikeToCount) {
  lineCount = countLines();
} else {
  lineCount = 0;
}

print(lineCount);
```

Các biến cấp cao nhất và biến lớp được khởi tạo theo cách lười biếng; mã khởi tạo được thực thi lần đầu tiên biến được sử dụng.

## Late variables

Trình biên dịch Dart có hai trường hợp sử dụng cho từ khóa `late`:
- Khai báo biến không thể là null được khởi tạo sau khi khai báo.
- Khởi tạo biến theo cách lười biếng.


Thông thường, phân tích luồng điều khiển của Dart có thể phát hiện khi một biến không thể là null được đặt thành giá trị không phải là null trước khi sử dụng, nhưng đôi khi phân tích thất bại. Hai trường hợp thường gặp là biến cấp cao nhất và biến thể hiện: Dart thường không thể xác định liệu chúng đã được thiết lập hay chưa.

Nếu bạn chắc chắn rằng một biến được thiết lập trước khi sử dụng, nhưng Dart không đồng ý, bạn có thể sửa lỗi bằng cách đánh dấu biến là `late`:

```dart
late String description;

void main() {
  description = 'Feijoada!';
  print(description);
}
```

Nếu bạn không khởi tạo một biến `late`, một lỗi runtime sẽ xảy ra khi biến được sử dụng.

Khi bạn đánh dấu một biến là `late` nhưng lại khởi tạo nó tại thời điểm khai báo, thì mã khởi tạo sẽ được thực thi lần đầu tiên biến được sử dụng. Việc khởi tạo lười biếng này hữu ích trong một số trường hợp:

- Biến có thể không cần thiết, và việc khởi tạo nó tốn kém.
- Bạn đang khởi tạo một biến thể hiện, và mã khởi tạo của nó cần truy cập đến `this`.

Trong ví dụ sau, nếu biến `temperature` không bao giờ được sử dụng, thì hàm `readThermometer()` tốn kém sẽ không được gọi:
```dart
// Đây là cuộc gọi duy nhất trong chương trình tới readThermometer().
late String temperature = readThermometer(); // Được khởi tạo lười biếng.
```

## Final and const

Nếu bạn không bao giờ có ý định thay đổi một biến, hãy sử dụng `final` hoặc `const`, thay vì `var` hoặc cùng với một kiểu. Một biến `final` chỉ có thể được đặt một lần; một biến `const` là hằng số thời gian biên dịch. (Các biến `const` được ngầm định `final`.)

Lưu ý: Các biến thể hiện có thể là `final` nhưng không phải là `const`.

Dưới đây là một ví dụ về cách tạo và đặt một biến `final`:

```dart
final name = 'Bob'; // Không có chú thích kiểu
final String nickname = 'Bobby';
```

Bạn không thể thay đổi giá trị của một biến final:

```dart
name = 'Alice'; // Lỗi: một biến final chỉ có thể được đặt một lần.
```

Sử dụng `const` cho các biến mà bạn muốn là hằng số thời gian biên dịch. Nếu biến `const` ở cấp lớp, hãy đánh dấu nó là `static const`. Khi bạn khai báo biến, hãy đặt giá trị thành hằng số thời gian biên dịch như số hoặc ký tự biểu tượng, biến `const` hoặc kết quả của một phép toán số học trên các số không đổi:

```dart
const bar = 1000000; // Đơn vị áp suất (dynes/cm2)
const double atm = 1.01325 * bar; // Khí quyển chuẩn
```

Từ khóa `const` không chỉ dành cho việc khai báo các biến hằng số. Bạn cũng có thể sử dụng nó để tạo các giá trị hằng số, cũng như để khai báo các trình tạo tạo các giá trị hằng số. Bất kỳ biến nào cũng có thể có giá trị hằng số.

```dart
var foo = const [];
final bar = const [];
const baz = []; // Tương đương với `const []`
```

Bạn có thể bỏ qua const khỏi biểu thức khởi tạo của một khai báo `const`, giống như đối với `baz` ở trên.

Bạn có thể thay đổi giá trị của một biến không phải cuối cùng, không phải `const`, ngay cả khi nó đã từng có giá trị const:

```dart
foo = [1, 2, 3]; // Là `const []`
```

Bạn không thể thay đổi giá trị của một biến `const`:

```dart
baz = [42]; // Lỗi: Các biến hằng số không thể được gán giá trị.
```

Bạn có thể xác định các hằng số sử dụng các kiểm tra kiểu và chuyển đổi (`is` và `as`), bộ sưu tập nếu và các toán tử lan truyền (`...` và `...?`):

```dart
const Object i = 3; // Trong đó i là một hằng số Object với giá trị int...
const list = [i as int]; // Sử dụng một chuyển đổi kiểu.
const map = {if (i is int) i: 'int'}; // Sử dụng is và bộ sưu tập if.
const set = {if (list is List<int>) ...list}; // ...và một sự lan truyền.
```

Lưu ý: Mặc dù một đối tượng `final` không thể được sửa đổi, các thuộc tính của nó có thể được sửa đổi. So sánh, một đối tượng `const` và các thuộc tính của nó không thể được sửa đổi: chúng không thay đổi.