---
title: "Proving your Android app respects user privacy without publishing source code"
date: 2026-08-23
---

### Living in the slop era

How to prove the claim that your app doesn't send any user data?
Source code itself is not a great proof when publishing on Google Play.
Yes, you can do reproducible builds, but an average user is never going to verify this. Unless your app is popular and audited by a third party, this means nothing to normal humans. 

Also, publishing source code of the app you worked on for months or years might not be the best idea in the age of AI and slop.
What's stopping bots and agents from forking your work and spinning up their own version? Nothing.
While cloning popular open source projects won't really harm the original project, your small project might not be able to compete with clones to addition to vibe slop that is already out there.

We have to use something different to prove that our app won't send any user data to your server, some cloud or advertising platform. A method that is simple and quick to verify by anyone, even non-technical users.

On Google Play there is a section talking about privacy and how user data is processed. The problem is that this section is just a declaration.
There is no substance behind it, Google will not and can't verify this. It's just a promise and there is no reason to trust it.
So how to actually prove that the app doesn't send any data in a way anyone can verify?

### Proving privacy-first principle

How can a program share user data with whoever the developer wants? Using some kind of transportation protocol suite, like an Internet. 
You probably can see where I'm going with this:

If the app CANNOT access the internet, it can't exfiltrate any data directly, without user action. Android enforces this at the Linux kernel level. 

On Android, this can be achieved by not requesting the `INTERNET` permission in the app manifest.

```xml
<uses-permission android:name="android.permission.INTERNET" />
```

Remove that and your app cannot access the internet. [WIP - add something about other ways to exfiltrate data like bluetooth, NFC, etc. Look into:
Colluding apps (confused deputy) - App A (no INTERNET) writes data somewhere App B (has INTERNET) can read: shared external storage, a ContentProvider it exposes, an Intent with extras, or the system clipboard. This is a known Android security research topic (permission re-delegation / ICC side channels), documented in academic papers like "Soundcomber" and various ICC exfiltration studies.
]



[WIP - add a section here?? about instruction how a normal human can check permission before installing the app]

You probably want to ask: "But how my app can work without internet access? I need it for backend integration/services/api" calls!".



### Build offline first apps with alternative sync methods

We rely on the cloud apis too much - Firebase, AWS, Azure, etc., but these are not free so this is one of the reasons why so many modern apps require a subscription. I often see people promoting simple apps for note-taking, budgeting, journaling, etc., but they require a subscription to use and offline functionality is limited or not present at all. 

I really hate this trend. 

As we moved from desktop software to mobile-first apps, we should start designing our apps as offline-first. Most of us aren't building next social media or messaging apps.
In my 9-5 job as a Senior Web Developer, I mostly code in Angular, so for my hobby project, Gecko Budget, I used Capacitor native runtime to build it with Angular. I didn't feel like learning an Android native development stack just to build a simple budgeting app for myself - that would take too long. 

Capacitor offers sqlite database with jeep-sqlite plugin for web. I worked as a fullstack at some point, so I felt back at home writing SQL queries again. It's fast and a joy to work with. All the data stays on the device. 
Then I've implemented a JSON export and import solution that users can pair with their cloud storage of choice, like Nextcloud. Still no need to handle user data, they can handle it themselves. This is a real privacy-first approach to app development. GDPR-compliant 120%.

**BUT!** You still might need some data from the internet, like exchange rates.

WIP
