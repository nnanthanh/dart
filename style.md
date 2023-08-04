# Identifiers

Mã định danh có ba loại trong Dart.

- `UpperCamelCase` tên viết hoa chữ cái đầu tiên của mỗi từ, kể cả chữ cái đầu tiên.

- `lowerCamelCase` tên viết hoa chữ cái đầu tiên của mỗi từ, ngoại trừ chữ cái đầu tiên luôn viết thường, ngay cả khi đó là từ viết tắt.

- `lowercase_with_underscores` tên chỉ sử dụng các chữ cái viết thường, ngay cả đối với các từ viết tắt và các từ riêng biệt bằng `_`.

## Thực hiện các loại tên bằng `UpperCamelCase`

Các `class`, kiểu `enum`, `typedefs` và tham số kiểu phải viết hoa chữ cái đầu tiên của mỗi từ (kể cả từ đầu tiên) và không sử dụng dấu phân cách.

```dart
class SliderMenu { ... }

class HttpRequest { ... }

typedef Predicate<T> = bool Function(T value);

extension MyFancyList<T> on List<T> { ... }

extension SmartIterable<T> on Iterable<T> { ... }
```

## Đặt tên gói, thư mục và tệp nguồn bằng cách sử dụng `lowercase_with_underscores`

Một số hệ thống tệp không phân biệt chữ hoa chữ thường, vì vậy nhiều dự án yêu cầu tên tệp phải là
chữ thường. Sử dụng một ký tự phân tách cho phép các tên vẫn có thể đọc được ở dạng đó. Sử dụng dấu
gạch dưới làm dấu tách đảm bảo rằng tên vẫn là mã định danh Dart hợp lệ, điều này có thể hữu ích nếu
ngôn ngữ sau này hỗ trợ nhập biểu tượng.

```
my_package
└─ lib
    └─ file_system.dart
    └─ slider_menu.dart
```
## Thực hiện tiền tố nhập tên bằng cách sử dụng `lowercase_with_underscores`

```
import 'dart:math' as math;
import 'package:angular_components/angular_components.dart' as angular_components;
import 'package:js/js.dart' as js;
```
## Nên đặt tên cho các số nhận dạng khác bằng cách sử dụng `lowerCamelCase`

- Class members, top-level definitions, variables và parameters được đặt tên phải viết hoa chữ
cái đầu tiên của mỗi từ ngoại trừ từ đầu tiên và không sử dụng dấu phân cách.

```dart
var count = 3;

HttpRequest httpRequest;

void align(bool clearItems) {
// ...
}
```
## Ưu tiên sử dụng `lowerCamelCase` cho tên hằng
- Trong mã mới, sử dụng lowerCamelCasecho các biến không đổi, bao gồm cả giá trị enum.

```dart
const pi = 3.14;
const defaultTimeout = 1000;
final urlScheme = RegExp('^([a-z]+):');

class Dice {
  static final numberGenerator = Random();
}
```
##  Nên viết hoa các từ viết tắt và từ viết tắt dài hơn hai chữ cái như từ
 Các từ viết tắt viết hoa có thể khó đọc và nhiều từ viết tắt liền kề có thể dẫn đến các tên khó
hiểu. Ví dụ: đặt tên bắt đầu bằng HTTPSFTP, không có cách nào để biết liệu tên đó đề cập đến HTTPS
FTP hay HTTP SFTP.

Để tránh điều này, các từ viết tắt và từ viết tắt được viết hoa như các từ thông thường.

Ngoại lệ: Các từ viết tắt gồm hai chữ cái như IO (đầu vào/đầu ra) được viết hoa đầy đủ: IO. Mặt
khác, các từ viết tắt hai chữ cái như ID (số nhận dạng) vẫn được viết hoa như các từ thông thường:
Id.

```dart
class HttpConnection {}
class DBIOPort {}
class TVVcr {}
class MrRogers {}

var httpRequest = ...
var uiHandler = ...
var userId = ...
Id id;
```

ƯU TIÊN sử dụng _, __, v.v. cho các tham số gọi lại không được sử dụng
Đôi khi, chữ ký kiểu của hàm gọi lại yêu cầu một tham số, nhưng việc triển khai gọi lại không sử
dụng tham số. Trong trường hợp này, việc đặt tên cho tham số không sử dụng là thành ngữ _. Nếu hàm
có nhiều tham số không sử dụng, hãy sử dụng dấu gạch dưới bổ sung để tránh xung đột tên: __, ___,
v.v.

```dart
futureOfVoid.then((_) {
print('Operation complete.');
});
```

- Hướng dẫn này chỉ dành cho các chức năng ẩn danh và cục bộ . Các chức năng này thường được sử dụng
ngay lập tức trong ngữ cảnh rõ ràng tham số không sử dụng đại diện cho điều gì. Ngược lại, các khai
báo phương thức và hàm cấp cao nhất không có ngữ cảnh đó, vì vậy các tham số của chúng phải được đặt
tên sao cho rõ ràng mỗi tham số dùng để làm gì, ngay cả khi nó không được sử dụng.

## Không sử dụng dấu gạch dưới hàng đầu cho các số nhận dạng không riêng tư
Dart sử dụng dấu gạch dưới hàng đầu trong mã định danh để đánh dấu các thành viên và khai báo cấp
cao nhất là riêng tư. Điều này huấn luyện người dùng liên kết một dấu gạch dưới hàng đầu với một
trong các loại khai báo đó. Họ nhìn thấy “`_`” và nghĩ rằng “riêng tư”.

Không có khái niệm “riêng tư” cho các biến cục bộ, tham số, hàm cục bộ hoặc tiền tố thư viện. Khi
một trong số đó có tên bắt đầu bằng dấu gạch dưới, nó sẽ gửi tín hiệu khó hiểu cho người đọc. Để
tránh điều đó, không sử dụng dấu gạch dưới hàng đầu trong những tên đó.

## Không sử dụng các chữ cái tiền tố
[Ký hiệu Hungary](https://en.wikipedia.org/wiki/Hungarian_notation) và các sơ đồ khác đã xuất hiện vào thời BCPL, khi trình biên dịch không làm được gì nhiều để giúp bạn hiểu mã của mình. Bởi vì Dart có thể cho bạn biết loại, phạm vi, khả năng thay đổi và các thuộc tính khác của các khai báo của bạn, nên không có lý do gì để mã hóa các thuộc tính đó
thành tên định danh.

```dart
defaultTimeout
```

## Không đặt tên thư viện một cách rõ ràng
- Về mặt kỹ thuật, việc thêm tên vào librarychỉ thị là có thể, nhưng là một tính năng cũ và không được khuyến khích.

- Dart tạo một thẻ duy nhất cho mỗi thư viện dựa trên đường dẫn và tên tệp của nó. Các thư viện đặt
tên sẽ ghi đè URI được tạo này. Nếu không có URI, các công cụ có thể khó tìm thấy tệp thư viện chính
được đề cập hơn.

```dart
library my_library;
/// A really great test library.
@TestOn('browser')
library;
```
## Đặt hàng
- Để giữ cho phần mở đầu của tệp của bạn gọn gàng, chúng tôi có một thứ tự quy định mà các lệnh sẽ
xuất hiện. Mỗi "phần" phải được phân tách bằng một dòng trống.

## Nên đặt dart: imports before other imports

```dart
import 'dart:async';
import 'dart:html';

import 'package:bar/bar.dart';
import 'package:foo/foo.dart';
```

## Nên đặt package: imports before relative imports

```dart
import 'package:bar/bar.dart';
import 'package:foo/foo.dart';

import 'util.dart';
```
## Nên chỉ định exports trong một phần riêng biệt sau tất cả imports
Quy tắc kẻ nói dối: directives_ordering

```dart
import 'src/error.dart';
import 'src/foo_bar.dart';

export 'src/error.dart';
```

## Hãy sắp xếp các phần theo thứ tự bảng chữ cái

```dart
import 'package:bar/bar.dart';
import 'package:foo/foo.dart';

import 'foo.dart';
import 'foo/foo.dart';
```

## Formatting
- Giống như nhiều ngôn ngữ, Dart bỏ qua khoảng trắng. Tuy nhiên, con người thì không. Việc có một kiểu khoảng trắng nhất quán giúp đảm bảo rằng người đọc nhìn thấy mã giống như cách mà trình biên dịch
thực hiện.

## Nên format mã của bạn bằng cách sử dụng dart format
- Định dạng là công việc tẻ nhạt và đặc biệt tốn thời gian trong quá trình tái cấu trúc. May mắn thay,
bạn không phải lo lắng về điều đó. Chúng tôi cung cấp một trình định dạng mã tự động phức tạp được
gọi dart format làm điều đó cho bạn. Chúng tôi có một số tài liệu về các quy tắc mà nó áp dụng,
nhưng các quy tắc xử lý khoảng trắng chính thức cho Dart là bất kỳ quy tắc nào dart format tạo ra .

- Các nguyên tắc định dạng còn lại dành cho một số điều dart format không thể khắc phục cho bạn.

- Hãy xem xét việc thay đổi mã của bạn để làm cho nó thân thiện hơn với trình định dạng
Trình định dạng làm tốt nhất có thể với bất kỳ mã nào bạn ném vào nó, nhưng nó không thể hoạt động
thần kỳ. Nếu mã của bạn có số nhận dạng đặc biệt dài, biểu thức được lồng sâu, hỗn hợp các loại toán
tử khác nhau, v.v. thì đầu ra được định dạng vẫn có thể khó đọc.

- Khi điều đó xảy ra, hãy tổ chức lại hoặc đơn giản hóa mã của bạn. Xem xét việc rút ngắn tên biến cục bộ hoặc đưa một biểu thức vào một biến cục bộ mới. Nói cách khác, hãy thực hiện các loại sửa đổi tương tự như khi bạn định dạng mã bằng tay và cố gắng làm cho mã dễ đọc hơn. Hãy coi đây dart  formatlà một mối quan hệ đối tác nơi bạn làm việc cùng nhau, đôi khi lặp đi lặp lại, để tạo ra mã
đẹp.

## Tránh các dòng dài hơn 80 ký tự

- Các nghiên cứu về khả năng đọc cho thấy rằng các dòng văn bản dài sẽ khó đọc hơn vì mắt bạn phải di chuyển xa hơn khi di chuyển đến đầu dòng tiếp theo. Đây là lý do tại sao các tờ báo và tạp chí sử dụng nhiều cột văn bản.

- Nếu bạn thực sự thấy mình muốn các dòng dài hơn 80 ký tự, kinh nghiệm của chúng tôi là mã của bạn có thể quá dài dòng và có thể nhỏ gọn hơn một chút. Thủ phạm chính thường là
VeryLongCamelCaseClassNames. Hãy tự hỏi bản thân, “Mỗi từ trong tên loại đó có cho tôi biết điều gì
đó quan trọng hoặc ngăn chặn xung đột tên không?” Nếu không, hãy xem xét bỏ qua nó.

- Lưu ý rằng dart format 99% điều này là dành cho bạn, nhưng 1% cuối cùng là bạn. Nó không phân tách
chuỗi ký tự dài để vừa với 80 cột, vì vậy bạn phải thực hiện việc đó theo cách thủ công.

- Ngoại lệ: Khi một URI hoặc đường dẫn tệp xuất hiện trong một nhận xét hoặc chuỗi (thường là trong một lần nhập hoặc xuất), nó có thể giữ nguyên ngay cả khi dòng đó vượt quá 80 ký tự. Điều này giúp dễ dàng tìm kiếm các tệp nguồn cho một đường dẫn.

- Ngoại lệ: Các chuỗi nhiều dòng có thể chứa các dòng dài hơn 80 ký tự vì các dòng mới có ý nghĩa bên
trong chuỗi và việc chia các dòng thành các dòng ngắn hơn có thể làm thay đổi chương trình.

## Nên sử dụng dấu ngoặc nhọn cho tất cả các câu lệnh điều khiển luồng

- Làm như vậy sẽ tránh được vấn đề lơ lửng khác .

```dart
if (isWeekDay) {
print('Bike to work!');
} else {
print('Go dancing or read a book!');
}
```
- Ngoại lệ: Khi bạn có một if câu lệnh không có else mệnh đề nào và toàn bộ if câu lệnh nằm trên một
dòng, bạn có thể bỏ qua dấu ngoặc nhọn nếu muốn:

```dart
if (arg == null) return defaultValue;
```

- Tuy nhiên, nếu nội dung kết thúc đến dòng tiếp theo, hãy sử dụng dấu ngoặc nhọn:

```dart
if (overflowChars != other.overflowChars) {
return overflowChars < other.overflowChars;
}
if (overflowChars != other.overflowChars)
return overflowChars < other.overflowChars;
```
``````