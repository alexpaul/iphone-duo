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

### Outer diplay 
<img width="925" height="1013" alt="Screenshot 2026-10-02 at 8 30 52 PM" src="https://github.com/user-attachments/assets/cce5410b-21bd-4484-ae3d-d358bfddb0e3" />

### Inner display 
<img width="925" height="1013" alt="Screenshot 2026-10-02 at 8 32 31 PM" src="https://github.com/user-attachments/assets/2d784a35-832e-40c3-bd61-76f7ea9e29f9" />


## Resources 

* [Apple: Designing for iPhone Duo (Design Guidance)](https://developer.apple.com/design/human-interface-guidelines/designing-for-iphone-duo)
* [Apple: Preparing your app for iPhone Duo (Developer Guidance)](https://developer.apple.com/documentation/technologyoverviews/preparing-your-app-for-iphone-duo)
