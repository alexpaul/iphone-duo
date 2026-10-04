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
  * [DeviceHinge](https://developer.apple.com/documentation/swiftui/devicehinge)
  * [DeviceHinge.Status](https://developer.apple.com/documentation/swiftui/devicehinge/status-swift.struct)
  * `onHingeChange`
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

> Apple: People hold iPhone Duo and set it down in a number of ways: partially folded like a book, placed down on a surface, or standing on its edges.

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

> Apple: By default, the SwiftUI layout system sizes and positions views to avoid certain safe areas.

### Outer display 
<img width="925" height="1013" alt="Screenshot 2026-10-02 at 8 30 52 PM" src="https://github.com/user-attachments/assets/cce5410b-21bd-4484-ae3d-d358bfddb0e3" />

### Inner display 
<img width="925" height="1013" alt="Screenshot 2026-10-02 at 8 32 31 PM" src="https://github.com/user-attachments/assets/2d784a35-832e-40c3-bd61-76f7ea9e29f9" />

## Split view on iPhone Duo 

> Apple: On iPhone Duo, a split view expands on the inner display and collapses to a single pane on the outer display, the same way it adapts between regular and compact environments on other iPhone devices. When built with standard components, split views adapt to reserved regions automatically, adjusting width and margins to adapt to the fold.

### Outer display 
<img width="925" height="1013" alt="Screenshot 2026-10-02 at 9 41 21 PM" src="https://github.com/user-attachments/assets/719a998e-f486-4baa-bbda-1784311d6492" />

### Inner display 
<img width="925" height="1013" alt="Screenshot 2026-10-02 at 9 41 45 PM" src="https://github.com/user-attachments/assets/f33e589c-fdc9-4121-b35d-a4e7848afe30" />

### Book pose (Notice how the content moves away from the folded region)
<img width="925" height="1013" alt="Screenshot 2026-10-02 at 9 43 31 PM" src="https://github.com/user-attachments/assets/37be074a-5ed9-4777-9202-af808c826e56" />

## Arrangement views 

> [Apple](https://developer.apple.com/design/human-interface-guidelines/designing-for-iphone-duo#Arrangement-views): An arrangement view is a layout container that holds two views inside it — a primary view and a secondary view — and dynamically organizes them based on display size, orientation, and reserved regions.

### ⚠️ Available in iOS 27.1+
<img width="933" height="171" alt="Screenshot 2026-10-02 at 9 57 43 PM" src="https://github.com/user-attachments/assets/80bd6dec-b0d3-42e8-85b4-10e0d0a214a9" />

### Using `if #available` 
```swift
if #available(iOS 27.1, *) {
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

## Hinge

> Apple: A hinge provides its angle along with a status determined by the system based on the current angle and device orientation. You use this type with the `View/onHingeChange(_:)` modifier.

Try? it out 

```swift
import SwiftUI

@available(iOS 27.1, *)
struct HingeView: View {
    @State private var hinge: DeviceHinge?

    var body: some View {
        Group {
            if let hinge {
                VStack {
                    Text(statusTitle(for: hinge.status))
                        .font(.largeTitle)
                        .foregroundStyle(statusColor(for: hinge.status))
                    Text("\(Int(hinge.angle.degrees))°")
                        .monospaced()
                        .font(.title2)
                        .foregroundStyle(statusColor(for: hinge.status))
                }
            } else {
                ContentUnavailableView(
                    "Hinge Unavailable",
                    systemImage: "rectangle.split.2x1",
                    description: Text("Fold or unfold the device to report the hinge angle.")
                )
            }
        }
        .onHingeChange { _, newContext in
            hinge = newContext.hinge
        }
    }

    private func statusColor(for status: DeviceHinge.Status) -> Color {
        switch status {
        case .closed: .gray
        case .partiallyOpen: .orange
        case .fullyOpen: .green
        default: .secondary
        }
    }

    private func statusTitle(for status: DeviceHinge.Status) -> String {
        switch status {
        case .closed: "iPhone Duo closed"
        case .partiallyOpen: "iPhone Duo partially open"
        case .fullyOpen: "iPhone Duo fully open"
        default: "Unknown"
        }
    }
}

struct HingeSimpleDemo: View {
    var body: some View {
        if #available(iOS 27.1, *) {
            HingeView()
        } else {
            Text("DeviceHinge requires a newer OS")
        }
    }
}

#Preview {
    HingeSimpleDemo()
}
```

### Outer display 
<img width="925" height="1013" alt="Screenshot 2026-10-03 at 7 26 23 PM" src="https://github.com/user-attachments/assets/2d540cd7-cd0a-44a4-8368-94f239383244" />

### Inner display 
<img width="925" height="1013" alt="Screenshot 2026-10-03 at 7 26 32 PM" src="https://github.com/user-attachments/assets/ed758229-e163-4513-88ea-670d02d06620" />

### Book pose
<img width="925" height="1013" alt="Screenshot 2026-10-03 at 7 26 42 PM" src="https://github.com/user-attachments/assets/951c57b7-db67-4aed-a251-9f965e7117dd" />


## Resources 

* [Apple: iPhone Duo (Resources includes videos)](https://developer.apple.com/iphone-duo/)
* [Apple: Designing for iPhone Duo (Design Guidance)](https://developer.apple.com/design/human-interface-guidelines/designing-for-iphone-duo)
* [Apple: Preparing your app for iPhone Duo (Developer Guidance)](https://developer.apple.com/documentation/technologyoverviews/preparing-your-app-for-iphone-duo)
