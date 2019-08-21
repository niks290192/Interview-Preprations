* [UIKit](#uikit)
    * [Live Rendering in Storyboards](#how-could-you-setup-live-rendering)


# UIKit

## How could you setup Live Rendering?
With `@IBInspectable` and `@IBDesignable`, its possible to build a custom interface for confugring your custom controls and have them rendered in real-time while designing your project.

`@IBInspectible` properties provide new access to an old feature:
user-defined runtime attributes. Currently accessible from the identity inspector, these attributes have been available since before Interface Builder was integrated into Xcode. They provide a powerful mechanism for configuring any key-value coded property of an instance in a NIB, XIB, or storyboard.

Built-in Cocoa types can also be extended to have inspectable properties beyond the ones already in Interface Builder's attribute inspector. If you like rounded corners, you'll love this UIView extension:

```swift
extension UIView {
    @IBInspectable var cornerRadius: CGFloat {
        get {
            return layer.cornerRadius
        }

        set {
            layer.cornerRadius = newValue
            layer.masksToBounds = newValue > 0
        }
    }
}
```

The attribute `@IBDesignable` lets Interface Builder perform live updates on a particular view.
This allows seeing how your custom views will appear without building and running your app after each change.

To mark a custom view as `IBDesignable`, prefix the class name with `@IBDesignable` (or the IB_DESIGNABLE macro in Objective-C). Your initializers, layout, and drawing methods will be used to render your custom view right on the canvas:

```swift
@IBDesignable
class MyCustomView: UIView {
    ...
}
```