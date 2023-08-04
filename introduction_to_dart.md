# [Introduction to Dart](https://dart.dev/language)

### [Hello, World!](https://dart.dev/language#hello-world)

> Every app requires the top-level main() function, where execution starts.

```dart
void main() {
  print('Hello, World!');
}
```

### [Variables](https://dart.dev/language#variables)

```dart
/// String
var name = 'Voyager I';

/// int
var year = 1977;

/// double
var antennaDiameter = 3.7;

/// List
var flybyObjects = ['Jupiter', 'Saturn', 'Uranus', 'Neptune'];

/// Map
var image = {
  'tags': ['saturn'],
  'url': '//path/to/saturn.jpg'
};
```

### [Control flow statements](https://dart.dev/language#control-flow-statements)

> Dart supports the usual control flow statements:

```dart
if (year >= 2001) {
print('21st century');
} else if (year >= 1901) {
print('20th century');
}

for (final object in flybyObjects) {
print(object);
}

for (int month = 1; month <= 12; month++) {
print(month);
}

while (year < 2016) {
year += 1;
}
```

> Read more about control flow statements in Dart, including
> [break and continue](https://dart.dev/language/loops#break-and-continue),
> [switch and case](https://dart.dev/language/branches#switch-statements)
> and
> [assert](https://dart.dev/language/error-handling#assert).

### [Functions](https://dart.dev/language#functions)

> [We recommend](https://dart.dev/effective-dart/design#types)
> specifying the types of each function’s arguments and return value:

```dart
int fibonacci(int n) {
  if (n == 0 || n == 1) return n;
  return fibonacci(n - 1) + fibonacci(n - 2);
}

var result = fibonacci(20);
```

> A shorthand => (arrow) syntax is handy for functions that contain a single statement.

```dart
flybyObjects.where
(
(name) => name.contains('turn')
)
.
forEach
(
print
);
```

### [Comments](https://dart.dev/language#comments)

> Dart comments usually start with //.

```dart
// This is a normal, one-line comment.

/// This is a documentation comment, used to document libraries,
/// classes, and their members. Tools like IDEs and dartdoc treat
/// doc comments specially.

/* Comments like these are also supported. */
```

### [Imports](https://dart.dev/language#imports)

> To access APIs defined in other libraries, use import.

```dart
// Importing core libraries
import 'dart:math';

// Importing libraries from external packages
import 'package:test/test.dart';

// Importing files
import 'path/to/my_other_file.dart';
```

### [Classes](https://dart.dev/language#classes)

```dart
class Spacecraft {
  String name;
  DateTime? launchDate;

  // Read-only non-final property
  int? get launchYear => launchDate?.year;

  // Constructor, with syntactic sugar for assignment to members.
  Spacecraft(this.name, this.launchDate) {
    // Initialization code goes here.
  }

  // Named constructor that forwards to the default one.
  Spacecraft.unlaunched(String name) : this(name, null);

  // Method.
  void describe() {
    print('Spacecraft: $name');
    // Type promotion doesn't work on getters.
    var launchDate = this.launchDate;
    if (launchDate != null) {
      int years = DateTime
          .now()
          .difference(launchDate)
          .inDays ~/ 365;
      print('Launched: $launchYear ($years years ago)');
    } else {
      print('Unlaunched');
    }
  }
}
```

> You might use the Spacecraft class like this:

```dart

var voyager = Spacecraft('Voyager I', DateTime(1977, 9, 5));
voyager.describe
();

var voyager3 = Spacecraft.unlaunched('Voyager III');
voyager3.describe
();
```

### [Enums](https://dart.dev/language#enums)

> Enums are a way of enumerating a predefined set of values or instances in a way which ensures that
> there cannot be any other instances of that type.

```dart
enum PlanetType { terrestrial, gas, ice }
```

[Inheritance](https://dart.dev/language#inheritance)

> Dart has single inheritance.

```dart
class Orbiter extends Spacecraft {
  double altitude;

  Orbiter(super.name, DateTime super.launchDate, this.altitude);
}
```

### [Mixins](https://dart.dev/language#mixins)

> Mixins are a way of reusing code in multiple class hierarchies. The following is a mixin
> declaration:

```dart
mixin Piloted {
  int astronauts = 1;

  void describeCrew() {
    print('Number of astronauts: $astronauts');
  }
}
```

> To add a mixin’s capabilities to a class, just extend the class with the mixin.

```dart
class PilotedCraft extends Spacecraft with Piloted {
  // ···
}
``` 

> You can create an abstract class to be extended (or implemented) by a concrete class. Abstract
> classes can contain abstract methods (with empty bodies).

```dart
abstract class Describable {
  void describe();

  void describeWithEmphasis() {
    print('=========');
    describe();
    print('=========');
  }
}
```

### [Async](https://dart.dev/language#async)

> Avoid callback hell and make your code much more readable by using `async` and `await`.

```dart

const oneSecond = Duration(seconds: 1);
// ···
Future<void> printWithDelay(String message) async {
  await Future.delayed(oneSecond);
  print(message);
}
```

### [Exceptions](https://dart.dev/language#exceptions)

> To raise an exception, use `throw`:

```dart
if (astronauts == 0) {
throw StateError('No astronauts.');
}
```

> To catch an exception, use a `try` statement with `on` or `catch` (or both):

```dart
void divideNumbers(int a, int b) {
  try {
    // Try to divide a by b
    int result = a ~/ b;
    print("Result: $result");
  } catch (e) {
    // If there's an error, catch the exception and handle it here
    print("Error occurred: $e");
  }
}

void main() {
  divideNumbers(10, 2); // Output: Result: 5
  divideNumbers(10, 0); // Output: Error occurred: IntegerDivisionByZeroException
}

```

### [Important concepts](https://dart.dev/language#important-concepts)

> **Version note:**
> [Null safety](https://dart.dev/null-safety)
> was introduced in `Dart 2.12`. Using null safety requires a
> [language version](https://dart.dev/guides/language/evolution#language-versioning)
> of at `least 2.12`.
> * If you enable
    > [Null safety](https://dart.dev/null-safety),
    > variables can’t contain `null` unless you say they can. You can make a variable nullable by
    putting a question mark (`?`) at the end of its type. For example, a variable of type `int?`
    might be an integer, or it might be `null`. If you know that an expression never evaluates
    to `null` but Dart disagrees, you can add `!` to assert that it isn’t null (and to throw an
    exception if it is). An example: `int x = nullableButNotNullInt!`

> Unlike Java, Dart doesn't have the keywords `public`, `protected`, and `private`. If an identifier
> starts with an underscore (`_`), it’s private to its library. For details, see
> [Libraries and imports](https://dart.dev/language/libraries).

> Dart has both expressions (which have runtime values) and statements (which don’t). For example,
> the
> [conditional expression](https://dart.dev/language/operators#conditional-expressions)
> `condition` `?` `expr1` `:` `expr2` has a value of `expr1` or `expr2`. Compare that to an
> [if-else statement](https://dart.dev/language/branches#if),
> which has no value. A statement often contains one or more expressions, but an expression can’t
> directly contain a statement.

<div style="text-align: right">

July 27th, 2023

</div>
