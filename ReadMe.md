* [UIKit](#uikit)
    * [Live Rendering in Storyboards](#how-could-you-setup-live-rendering)
    * [Ways of specifing the layout of elements](#ways-of-specifing-the-layout-of-elements)
    * [Autolayout formula](#formula-of-autolayout)
    * [Size Classes](#size-classes)
    * [Intrinsic Content Size](#intrinsic-content-size)
    * [Frame and bounds](#whats-the-difference-between-the-frame-and-the-bounds)
    * [When bounds origin will be different form 0,0?](#when-bounds-origin-will-be-different-from-00)
    * [What do layer object represent?](#what-are-layer-object-and-what-do-they-represent)



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


## Ways of specifing the layout of elements

Here are a few common ways to specify the layout elements in a UIView:

- Using `Interface Builder`, you can add a `XIB file` to your project, layout elements within it, and then load the XIB in your application code (either automatically, based on naming conventions, or manually).
Also, using InterfaceBuilder you can create a storyboard for your application.
- You can write your own code to use NSLayoutConstraints to have elements in a view arranged by Auto Layout.

- You can create CGRects describing the exact coordinates for each element and pass them to UIView's 
```objectivec
    -(id)initWithFrame:(CGRect)frame method.
```

## Formula of Autolayout
<img src = "/Resources/Articles/Autolayout.png">

## Size Classes
A size class is a new technology used by iOS to allow you to custom your app for a given device class, based on its orientation and screen size.

There are presently four classes:
- Horizontal Regular
- Horizontal Compact
- Vertical Regular
- Vertical Compact

<img src = "/Resources/Articles/Size%20Classes.png">

## Intrinsic Content Size
The Intrinsic Content Size is one of the most powerful features you gain when you opt-in to using Auto Layout to describe your interfaces. When a view has an intrinsic content size, it is promising Auto Layout that it will have a predefined size that the engine can use to calculate and lay out its views.

<center><img src = "/Resources/Articles/Intrisic%20Content%20Size.png" width="500"></center>

## What's the difference between the frame and the bounds?
`The bounds` of an UIView is the rectangle, expressed as a location(x, y) and size (width, height) relative to its own coordinate system (0,0) `The frame` of an UIView is the rectangle, expressed as a location(x, y) and size(width, height) relative to the superview it is contained within. 

<center><img src = "/Resource/Articles/Frame-Bounds.png"></center>

## When bounds origin will be different from 0,0?

Let's take an example of `UIScrollView`:
UIScrollView's bounds.origin will not be (0, 0) when its contentOffset is not (0, 0).

# What are layer objects and what do they represent?
`Layer objects` are data objects when represents visual content. Layer objects are used by views to render their content. Custom layer objects can also be added to the interface to implement complex animations and other types of sophisticated visual effects. 