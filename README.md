# PreviewMultiple

A simple way to preview SwiftUI content in multiple ways.

## Usage:

The simplest way to use PreviewMultiple is to wrap the content in an existing PreviewProvider in `PreviewMultiple { ... }` as shown below. This will cause the previewed content to be repeated three times, once for a large iPhone, a middle-sized iPhone, and a small iPod Touch. For development of an iPhone-only app, this will provide a reasonable starting set of devices for testing UI layouts.

```swift
    struct CoolView_Previews: PreviewProvider {
        static var previews: some View {
            PreviewMultiple {
                Text("Cool SwiftUI stuff here")
            }
        }
    }
```

Multiple combinations of device types have been created to provide more flexibility in testing. For example. `.lightDarkiPhoneBig` shows the previewed content on the largest iPhone in both light and dark modes. This can be combined with `.lightDarkiPhoneSmall` with Swift Array addition to show the previewed content in four modes simultaneously.

```swift
    struct CoolView_Previews: PreviewProvider {
        static var previews: some View {
            PreviewMultiple(devices: .lightDarkiPhoneBig + .lightDarkiPhoneSmall) {
                Text("Cool SwiftUI stuff here")
            }
        }
    }
```

The property `devices` provided to `PreviewMultiple` is an Array of `PreviewConfiguration` values. This struct defines the specifics of what will be used for a preview instance and includes:

 * deviceModel: PreviewDeviceName
 * colorScheme: ColorScheme - .light or .dark 
 * orientation: InterfaceOrientation - .portrait, .portraitUpsideDown, .landscapeLeft, .landscapeRight (only suported on iOS 15 and macOS 12)
 * sizeCategory: ContentSizeCategory - .extraSmall through .accessibilityExtraExtraExtraLarge

You can create your own PreviewCombination static vars in an extension to make combos that best help you see what is important to you. 

```swift
extension  {
    public static let importantCombo: PreviewCombination = [
        PreviewConfiguration(.iPhone13ProMax, orientation: .landscapeRight),
        PreviewConfiguration(.iPhone13ProMax, orientation: .portraitUpsideDown),
        PreviewConfiguration(.iPhone13Mini, scheme: .dark, orientation: .landscapeLeft),
        PreviewConfiguration(.iPadMini4, sizeCategory: .accessibilityMedium),
        PreviewConfiguration(.watch7_41mm),
        PreviewConfiguration(.iPadAir_4th),
    ]
}
```
