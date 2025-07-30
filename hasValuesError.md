
# Flutter Calendar Carousel Error

## Error Message

You can copy the error message below to search for solutions:

```
/C:/Users/Developer-10/AppData/Local/Pub/Cache/hosted/pub.dev/flutter_calendar_carousel-2.4.1/lib/classes/event.dart:33:23: Error: The method 'hashValues' isn't defined for the class 'Event'.
 - 'Event' is from 'package:flutter_calendar_carousel/classes/event.dart' ('/C:/Users/Developer-10/AppData/Local/Pub/Cache/hosted/pub.dev/flutter_calendar_carousel-2.4.1/lib/classes/event.dart').
Try correcting the name to the name of an existing method, or defining a method named 'hashValues'.
  int get hashCode => hashValues(date, description, location, title, icon, id);
                      ^^^^^^^^^^
Target kernel_snapshot_program failed: Exception
```

## Solution

To fix this error, replace the `hashValues` method with `Object.hash`. Copy the code below:

```dart
@override
int get hashCode => Object.hash(date, description, location, title, icon, id);
```

## Explanation

The `hashValues` method was deprecated in Flutter and replaced with `Object.hash`. This change is required to resolve the compilation error in newer versions of Flutter.

## How to Apply the Fix

1. Locate the file with the error: `event.dart`
2. Find the `hashCode` getter method
3. Replace the existing implementation with the solution code above
4. Save the file and recompile your Flutter project
