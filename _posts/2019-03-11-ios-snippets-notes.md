---
title: "iOS Snippets & Notes"
published: true
---

## ISO8601 Date Formatter with backwards support

```swift
extension Date {
    init?(iso8601 string:String) {
        if #available(iOS 11.0, *) {
            let formatter = ISO8601DateFormatter()
            formatter.formatOptions = [.withInternetDateTime]
            if let value = formatter.date(from: string) {
                self = value
                return
            }
            formatter.formatOptions = [.withInternetDateTime, .withFractionalSeconds]
            if let value = formatter.date(from: string) {
                self = value
                return
            }
            return nil
        } else {
            let formatter = DateFormatter()
            formatter.locale = Locale(identifier: "en_US_POSIX")
            formatter.dateFormat = "yyyy-MM-dd'T'HH:mm:ssZZZZZ"
            if let value = formatter.date(from: string) {
                self = value
                return
            }
            formatter.dateFormat = "yyyy-MM-dd'T'HH:mm:ss.SSSZZZZZ"
            if let value = formatter.date(from: string) {
                self = value
                return
            }
            return nil
        }
    }
    var iso8601:String {
        get {
            if #available(iOS 10.0, *) {
                let formatter = ISO8601DateFormatter()
                formatter.formatOptions = [.withInternetDateTime]
                return formatter.string(from: self)
            } else {
                let dateFormatter = DateFormatter()
                dateFormatter.locale = Locale(identifier: "en_US_POSIX")
                dateFormatter.dateFormat = "yyyy-MM-dd'T'HH:mm:ssZZZZZ"
                return dateFormatter.string(from: self)
            }
        }
    }
}
```

## Scroll up tableview after keyboard active + Get keyboard height

> Just Use [IQKeyboardManager](https://github.com/hackiftekhar/IQKeyboardManager)

In viewDidLoad

```swift
NotificationCenter.default.addObserver(forName: NSNotification.Name.UIKeyboardWillShow, object: nil, queue: nil) { (notification) in
    if let keyboardFrame = notification.userInfo?[UIKeyboardFrameEndUserInfoKey] as? NSValue {
        let keyboardRectangle = keyboardFrame.cgRectValue
        let contentInset = UIEdgeInsetsMake(0.0, 0.0, keyboardRectangle.height, 0.0)
        self.tableView.contentInset = contentInset
        self.tableView.scrollIndicatorInsets = contentInset
    }
}
NotificationCenter.default.addObserver(forName: NSNotification.Name.UIKeyboardWillHide, object: nil, queue: nil) { (notification) in
    self.tableView.contentInset = .zero
    self.tableView.scrollIndicatorInsets = .zero
}
```

In cell, add handler for text did begin edit, then call

```swift
self.tableView.scrollToRow(at: indexPath, at: .none, animated: false)
```

## UIColor vs Storyboard color difference

Since iOS 10 UIColor defaults to use sRGB profile, should use that in storyboard color picker as well

## Textview scroll to bottom

```swift
private func scrollToBottom() {
    self.textView.scrollRangeToVisible(NSMakeRange(self.textView.text.count - 1, 0))
}
```
