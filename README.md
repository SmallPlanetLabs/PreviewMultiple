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

## License

PreviewMultiple is free software distributed under the terms of the MIT license, reproduced below. PreviewMultiple may be used for any purpose, including commercial purposes, at absolutely no cost. No paperwork, no royalties, no GNU-like "copyleft" restrictions. Just download and enjoy.

Copyright (c) 2022 [Small Planet Digital, LLC](http://smallplanet.com)

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

## About Small Planet

Small Planet is a mobile agency in Brooklyn, NY that creates lovely experiences for smartphones and tablets. PreviewMultiple has made our lives a lot easier and we hope it does the same for you. You can find us at [smallplanet.com](http://smallplanet.com).

