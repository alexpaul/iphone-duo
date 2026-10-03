# iPhone Duo

> Apple: Build your app to resize

<img width="1480" height="832" alt="platforms-designing-for-iphone-intro~dark@2x" src="https://github.com/user-attachments/assets/550ddb0e-a6bd-4f3f-88b2-ff06188126b5" />

## Terminology 

* [Device Hub](https://developer.apple.com/documentation/xcode/device-hub)
* Device poses
* Size classes
* [Layout](https://developer.apple.com/design/human-interface-guidelines/layout)
* Layout margins
* [Safe area insets](https://developer.apple.com/documentation/swiftui/geometryproxy/safeareainsets)
* [Dynamic layouts](https://developer.apple.com/design/human-interface-guidelines/designing-for-iphone-duo#Dynamic-layouts)
* [Vertical controls](https://developer.apple.com/design/human-interface-guidelines/designing-for-iphone-duo#Vertical-controls)
* Display
  * Outer display
  * Inner display
* Hinge
* [Reserved regions](https://developer.apple.com/design/human-interface-guidelines/designing-for-iphone-duo#Reserved-regions)
  * Outer camera region
  * Inner camera region
  * Folding region
  * See [ReservedRegion](https://developer.apple.com/documentation/swiftui/reservedregion) API
* Split Views
* [Arrangement views](https://developer.apple.com/design/human-interface-guidelines/designing-for-iphone-duo#Arrangement-views)
  * Split arrangement
  * Overlay arrangement
  * See [ArrangementView](https://developer.apple.com/documentation/swiftui/arrangementview) API

## Poses

* Closed
* Open
* Laptop
* Book
* Tent

[Resource](https://mastodon.social/@stroughtonsmith/117314500271565893) for Xcode 27.1 to enable 3D preset viewing in the device hub.
```
defaults write ~/Library/Containers/com.apple.dt.Devices/Data/Library/Preferences/com.apple.dt.Devices com.apple.dt.coredevicepop.useInternalV68ActionBar -bool true
```

## Safe Area Insets on iPhone Duo

### Outer display 
<img width="925" height="1013" alt="Screenshot 2026-10-02 at 8 30 52 PM" src="https://github.com/user-attachments/assets/cce5410b-21bd-4484-ae3d-d358bfddb0e3" />

### Inner display 
<img width="925" height="1013" alt="Screenshot 2026-10-02 at 8 32 31 PM" src="https://github.com/user-attachments/assets/2d784a35-832e-40c3-bd61-76f7ea9e29f9" />

## Split view on iPhone Duo 

### Outer display 
<img width="925" height="1013" alt="Screenshot 2026-10-02 at 9 41 21 PM" src="https://github.com/user-attachments/assets/719a998e-f486-4baa-bbda-1784311d6492" />

### Inner display 
<img width="925" height="1013" alt="Screenshot 2026-10-02 at 9 41 45 PM" src="https://github.com/user-attachments/assets/f33e589c-fdc9-4121-b35d-a4e7848afe30" />

### Book pose (Notice how the content moves away from the folded region)
<img width="925" height="1013" alt="Screenshot 2026-10-02 at 9 43 31 PM" src="https://github.com/user-attachments/assets/37be074a-5ed9-4777-9202-af808c826e56" />

## Arrangement views 

### ⚠️ Available in iOS 27.1+
<img width="933" height="171" alt="Screenshot 2026-10-02 at 9 57 43 PM" src="https://github.com/user-attachments/assets/80bd6dec-b0d3-42e8-85b4-10e0d0a214a9" />

### Using `if #available` 
```swift
if #available(anyAppleOS 27.1, *) {
    ArrangementView {
        Color(.yellow)
    } secondary: {
        Color(.green)
    }
    .arrangementViewStyle(.split) // .automatic, .overlay, .split
} else {
    // Fallback on earlier versions
    Text("Sorry no ArrangementView for you")
}
```

### Outer display 
<img width="925" height="1013" alt="Screenshot 2026-10-02 at 10 09 12 PM" src="https://github.com/user-attachments/assets/13eee1d4-36b9-4582-8218-9ae6e284310d" />

### Inner display 
<img width="925" height="1013" alt="Screenshot 2026-10-02 at 10 09 24 PM" src="https://github.com/user-attachments/assets/dd64e56b-320b-4a2d-8e55-650ff27db91c" />

### Book pose (Notice how the content moves away from the folded region)
<img width="925" height="1013" alt="Screenshot 2026-10-02 at 10 09 37 PM" src="https://github.com/user-attachments/assets/0802191d-21f3-483d-b9a1-02b50305bca9" />

### Outer display (`.overlay` style)
<img width="925" height="1013" alt="Screenshot 2026-10-03 at 4 40 53 PM" src="https://github.com/user-attachments/assets/1e6859da-116b-4201-a789-5425bc881131" />

### Inner display (`.overlay` style)
<img width="925" height="1013" alt="Screenshot 2026-10-03 at 4 41 01 PM" src="https://github.com/user-attachments/assets/1a8646a6-e2c4-4cbd-9155-039016d2781e" />

### Book pose (`.overlay` style)
We can use `.overlayArrangementEdge(.leading)` to decide that the player control moves to the `.leading` edge when in Book pose 

```swift
ArrangementView {
    // Primary: controls that sit on top of the content
    PlayerControlsView()
        .overlayArrangementEdge(.leading)   // or .trailing
} secondary: {
    // Secondary: full-bleed content underneath
    VideoSurfaceView()
}
.arrangementViewStyle(.overlay)
```

<img width="925" height="1013" alt="Screenshot 2026-10-03 at 4 41 09 PM" src="https://github.com/user-attachments/assets/be4aa65e-080d-4fdb-ac4a-5d5ac6cea777" />


## Resources 

* [Apple: Designing for iPhone Duo (Design Guidance)](https://developer.apple.com/design/human-interface-guidelines/designing-for-iphone-duo)
* [Apple: Preparing your app for iPhone Duo (Developer Guidance)](https://developer.apple.com/documentation/technologyoverviews/preparing-your-app-for-iphone-duo)
