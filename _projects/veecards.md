---
layout: page
title: Veecards
description: Bring your contacts to life.
img: assets/img/veecards.png
importance: 1
category: work
related_publications: false
---

During my first startup adventure – in Italy between 2013-2016 at [Code Atlas SRL](https://www.codeatlas.it) – we designed and built [Veecards](http://www.veecards.com): an app to improve contacts' management.

Watch an intro video:

<div align="left" style="position: relative;">
    <a href="https://www.youtube.com/watch?v=66d7-8nEstM">
        <img src="https://img.youtube.com/vi/66d7-8nEstM/maxresdefault.jpg" style="width:100%;">
        <div style="position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%);">
            <svg xmlns="http://www.w3.org/2000/svg" width="100" height="100" viewBox="0 0 24 24">
                <path fill="#ffffff" d="M3 22v-20l18 10-18 10z"/>
            </svg>
        </div>
    </a>
</div>

<br/>
The main idea of Veecards is to reverse the responsibility and effort to maintain your address book with correct and fresh data: instead of keeping all your contacts up-to-date, you would only have to focus on your own.
<br/>
<br/>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/why_veecards.png" title="Why Veecards" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/veecards_idea.png" title="Veecards idea" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/veecards_nfc.png" title="Veecards NFC" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    By creating virtual business cards and distributing them to categorized groups of contacts such as Friends, Family, and Acquaintances, you could update your email address on Veecards, ensuring that everyone in your network receives the update instantly and effortlessly integrates it into their address books.
</div>

#### From Concept to Launch: navigating the startup journey

Creating a product from the ground up, alongside a small team of three, presents a unique set of challenges distinct from those encountered within established companies.

In Code Atlas, each of us brought technical expertise to the table as co-founders, yet we found ourselves navigating diverse responsibilities. From conceptualizing the product to determining feature priorities, collaborating with an external agency on UI/UX design, and orchestrating a successful launch, every aspect demanded our attention.
For the technical implementation, we had to architect the backend, build the Android and iOS mobile apps and the infrastructure to update users' address books in real time with CardDav and push notifications.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/code-atlas-office.png" title="Startup office" class="img-fluid rounded z-depth-1" height="200" %}
    </div>
</div>

We successfully developed an app that closely aligned with our initial vision, boasting functionality and design elements that were modern for the time. Despite our efforts, the product struggled to find its niche in the market.

The journey was an invaluable learning opportunity, providing me with exposure to the intricacies of the startup ecosystem and the process of bringing an app from conception to the final users on the app stores.

##### Contributions

I built the iOS app with UIKit in Objective-C. The app included authentication, virtual business card managament, push notifications and an integration with the address book API to synchronize the received that directly on the phone.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/veecards-banner.png" title="Veecards on iOS" class="img-fluid rounded z-depth-1" height="400" %}
    </div>
</div>

With the other co-founders, I also worked on the backend, which was built in Java on top of (what at the time was called) "Google App Engine" and included a [CardDAV](https://en.wikipedia.org/wiki/CardDAV) server to share and update contacts.
