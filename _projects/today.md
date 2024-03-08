---
layout: page
title: Todoapp.Today
description: Plan today, prepare tomorrow.
img: assets/img/today.png
importance: 1
category: side-projects
giscus_comments: true
---

They say that every engineer has to build a To-Do app in their life.

[Today](https://sphere-arrest-659920.framer.app/) is my implementation of a To-Do app, designed by my former colleague and ping pong office rival, [Julian Panzer](https://julianpanzer.com/). It is available exclusively for macOS users and it resides discreetly on the menu bar, always within reach. It is optimized for being used entirely with the keyboard, for pro users like us ;)

While currently available only for macOS, we might make an iOS companion app with some more time in the future.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/today-macos.png" title="Today for macOS" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    With a minimalist setup, focused on simplicity and efficiency, the app is fully navigatable with the keyboard.
</div>

#### SwiftUI 

Today is my first app developed using SwiftUI!

Working with SwiftUI was a lot of fun, it facilitated rapid layout creation and made it extremely easy to build a responsive user interface through state observation. However, as anticipated, certain UI intricacies fell short in comparison to AppKit/UIKit. For example, something as simple as setting the background of a TextField to be transparent [didn't work if such TextField was inside a List]((https://stackoverflow.com/questions/78035722/transparent-textfield-inside-macos-swiftui-list)). 

You can try this yourself and observe that the clear background of the TextField inside a list is not respected:

```swift
import SwiftUI

struct ContentView: View {
    @State private var items = ["Item 1", "Item 2"]

    var body: some View {
        VStack {
            List {
                ForEach(items.indices, id: \.self) { index in
                    TextField("Inside list", text: $items[index])
                        .textFieldStyle(.plain)
                        .background(Color.clear) // NOT respected
                        .padding()
                }.background(.blue)
            }
            .frame(width: 300, height: 200)
         TextField("Outside list", text: $items[0])
            .textFieldStyle(.plain)
            .background(Color.clear) // Respected
            .padding()
        }.background(.green)
        .padding()
    }
}
```
<div class="caption">
    An example of SwifUI having some limitations on styling a UI element.
</div>

##### Keyboard integration

Keyboard control is the main differentatior for Today and implementing it was fairly easy. The idea is to add an invisible view as the background of the parent content view, such as:

```swift
  var body: some View { contentView.background(KeyEventHandling()) }
```

The transparent `KeyEventHandling` NSView intercepts all keyboard events and broadcast them using the notifiation center, so that multiple views in the code base can intercept the events and react accordingly:

```swift
struct KeyEventHandling: NSViewRepresentable {
  func makeNSView(context: Context) -> NSView {
    DispatchQueue.main.async {
      KeyView.shared.window?.makeFirstResponder(KeyView.shared)
    }
    return KeyView.shared
  }
  
  func updateNSView(_ nsView: NSView, context: Context) {}
}

class KeyView: NSView {
  static let shared = KeyView()
  override var acceptsFirstResponder: Bool { true }
  override func keyDown(with event: NSEvent) {
    switch event.keyCode {
    // For a list of mapping between keyCodes and keys check this out: https://eastmanreference.com/complete-list-of-applescript-key-codes
    case 53:
      NotificationCenter.default.post(Notification(name: .escKeyPressed))
    case 76, 36:
      NotificationCenter.default.post(Notification(name: .enterKeyPressed))
    case 126:
      NotificationCenter.default.post(Notification(name: .upKeyPressed))
    // etc...
    }
  }
}
```

##### Focusing a TextField programmatically

One of the biggest challenge was fine-tuning TextField interactions, specifically setting it on focus after certain events like arrow navigation or shortcuts. I ended up writing a custom Text Field solution using AppKit, inspired by [this article](https://serialcoder.dev/text-tutorials/macos-tutorials/macos-programming-implementing-a-focusable-text-field-in-swiftui/).

Then I created a central coordinator to broadcast keyboard events, using the notification center, something as simple as:

```swift
func attemptToFocusTextField() {
  NotificationCenter.default.post(name: .shouldFocusAddItem, object: nil)
}
```

Many places in the app can attempt to focus the TextField. For example, when opening the Popover using a shortcut (implemented using [Hotkey](https://github.com/soffes/HotKey/)), the TextField should be focused so that the user can type a new ToDo right away without using the mouse.

Finally, the TextField implementation can react when receiving such notification and update its internal focus state:

```swift
    CustomTextFieldImplementation() // not showing for brevity
      .onReceive(.shouldFocusAddItem) { _ in
        DispatchQueue.main.async {
          self.shouldFocus = true // A @State variable that controls the focus
          // When focusing the text field, we don't want any ToDo items to be selected or in editing mode
          viewState.currentSelectedItem = nil
          viewState.currentEditedItem = nil
        }
      }
```

#### Popovers on macOS

Another challenge was generally working with a [popover window](https://developer.apple.com/design/human-interface-guidelines/popovers) in the menu bar on macOS. A popover is "a transient view that appears above other content when people click or tap a control or interactive area". Popovers are more niche and less documented than standard windows. This [Popover](https://github.com/iSapozhnik/Popover) library is a great entry point to creating and customizing Popovers on macOS, I recommend it as it simplifies most of the interactions that you will probably need to work with.

For example, creating a transparent padding between the main view containing the ToDos and the help view proved challenging, as it requires the popover view to be transparent, which is not supported "out of the box".

<div class="row">
    <div class="col-sm d-flex justify-content-center">
        {% include figure.liquid loading="eager" path="assets/img/popover-help.png" title="Today with help view" class="img-fluid rounded" width="300" height="auto" %}
    </div>
</div>

[comment]: # (TODO: add download button)