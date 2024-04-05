---
layout: page
title: Backend UI
description: A hybrid approach@SoundCloud
img: assets/img/bdui-cover.png
importance: 1
category: work
giscus_comments: true
---

Throughout my tenure at SoundCloud, I've witnessed numerous projects, but none was as successful as engineering a new home screen powered by a dynamic **Backend Driven UI**.
Managing the layout of the screen from the backend was an innovative approach that reshaped the way we rendered user interfaces in the app, resulting in more flexibility and a substantial improvement of development iteration speed.

### Mobile UI: the classic approach

When building User Interfaces for mobile apps, the process typically involves designing and implementing the UI components directly within the mobile application codebase. The data shown on screen is usually fetched from a backend server or other data sources via API calls. The UI elements are statically pre-built on the app, to be populated with the fetched data. These components are designed and structured to ensure optimal user experience for the type of data the needs to be presented on screen. Additionally, user interactions and navigation are programmed to facilitate transitions between different screens and functionalities within the app.

<div class="row" style="background-color: white; display: flex; justify-content: center;">
    {% include figure.liquid loading="eager" path="assets/img/bduiclassicui.png" title="Classic UI" class="img-fluid rounded" %}
</div>
<div class="caption">
    A classic approach to show a list of articles on a mobile app UI.
</div>

### Backend driven UI

In a backend driven UI approach, the user interface layout and content presentation are controlled by the server rather than being hard-coded into the app. The API response of the backend, in addition to the data, contains instructions on how to render it. The UI elements must be already defined on the client, but their appearance can be changed dynamically based on the received instructions. The degree of customization that the UI elements support is the most important design decision when following this approach.

In this example, the backend returns a `type` field that controls the style of the cell used by the app to show its content.

<div class="row" style="background-color: white; display: flex; justify-content: center;">
    {% include figure.liquid loading="eager" path="assets/img/bduibdui.png" title="Backend Driven UI" class="img-fluid rounded" %}
</div>
<div class="caption">
    A backend driven approach: the "type" field determines how the app renders the cell.
</div>

### A hybrid approach

Backend Driven UI can be approached in different ways and the key is deciding how much control should the backend have on the UI. More flexibility comes with more challenges and unpredictable behaviors.

If traditional mobile UI is the simplest but less flexible approach, the [Hub framework](https://github.com/spotify/HubFramework) developed at Spotify is biased towards customization and, at the end of the spectrum, a web browser gives maximum flexibility for the highest cost.

<div class="row" style="background-color: white; display: flex; justify-content: center;">
    {% include figure.liquid loading="eager" path="assets/img/bdui-compromise" title="BDUI compromise" class="img-fluid rounded" %}
</div>
<div class="caption">
    The spectrum of Backend Driven UI
</div>

In this project, we followed a hybrid approach, blending the flexibility of traditional frontend development with the dynamic control afforded by backend systems. In my experience, the sweet spot is somewhere in the middle: you can predefine a comprehensive set of UI elements to form the building blocks of your interfaces (hardcoded in the clients) and gave *some* control over them from the backend. For example, you can have a few "generic" cells with layout elements like labels and image views that can be filled by the backend, but there is usually no need to be able to customize details that don't change often, like a label's Font.

When a hybrid backend driven UI approach is well implemented, building a new page in your app is a matter of using the existing UI catalog (this works with a [design system](https://www.figma.com/blog/design-systems-101-what-is-a-design-system/)) to define the layout and just send that from the backend with its data.

### The advantages of a Backend driven UI

While not entirely unrestricted, our system allowed for significant flexibility in design, empowering us to change the layout of the screen without doing work on the mobile app. The aspect I appreciated the most was giving full control of the layout of the screen to product designers, to test UI changes without necessitating engineering work.

The Backend Driven UI solution also facilitated rapid experimentation and fast pace A/B testing, decoupling us from the constraints of traditional app store release cycles. With the backend driving the UI, we could swiftly iterate on designs, introduce changes and gather user feedback in near real-time.

### The challenges

Of course, such an approach was not without its challenges. We encountered the difficult task of ensuring future-proofing while maintaining backwards compatibility, a delicate balancing act that demanded meticulous planning and execution. When encountering scenarios such as an old client receiving instructions to display a UI element that isn't defined in its bundle, a robust approach involves implementing versioning and establishing a reliable fallback system. For instance, if the application receives instructions to display an element it doesn't recognize, it should gracefully render the same data on a designated fallback element.

Additionally, when dealing with a dynamic layout, thorough testing of all possible combinations is essential. Leveraging UI tests can significantly contribute to identifying and addressing any potential issues that may arise.

### Talk

I had the pleasure to talk more in detail about Backend Driven UI at the mobOS conference in Cluj and Cocoaheads in Berlin, [you can find the slides here!](https://www.slideshare.net/andreacipriani357/backend-driven-ui-on-mobile-apps).

<div class="row">
    {% include figure.liquid loading="eager" path="assets/img/bdui-mobos" title="BDUI mobOS" class="img-fluid rounded z-depth-1" %}
</div>
<div class="caption">
    Backend Driven UI at the mobOS conference in Cluj
</div>