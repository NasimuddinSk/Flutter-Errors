# InAppWebView Scroll Conflict Issue

## The Problem

The issue is with this InAppWebView code:

```dart
InAppWebView(
  initialUrlRequest: URLRequest(url: WebUri(fileUrl)),
)
```

## Why This Causes Scroll Problems

When you use EagerGestureRecognizer with InAppWebView, it creates a conflict between two scrolling systems:

1. **WebView Scrolling**: The web content inside the InAppWebView might have its own scrollable areas
2. **Flutter Widget Scrolling**: The parent Flutter widgets might also need to scroll

The EagerGestureRecognizer grabs all scroll gestures for itself, which means:
- If the web content is scrollable, users can scroll inside the web view
- But the parent Flutter widgets can't scroll when users try to scroll outside the web view
- This creates a confusing user experience where scrolling works in some places but not others

## Simple Solution

Replace EagerGestureRecognizer with a more appropriate gesture recognizer:

```dart
InAppWebView(
  initialUrlRequest: URLRequest(url: WebUri(fileUrl)),
    gestureRecognizers: {
      Factory<OneSequenceGestureRecognizer>(
        () => EagerGestureRecognizer(),
      )
  },
)
```

This allows vertical scrolling to work properly both inside the web view and with parent Flutter widgets.
