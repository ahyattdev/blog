---
layout: post
title:  "Observations of Apple Open Source"
---
![pmset noidle running]({{site.assets}}/apple-open-source.png)

[Apple Open Source](https://opensource.apple.com/) is a truly a strange beast. In many ways, it portrays Apple as a company that values open source and wants to give back to the community. But in many ways, it falls short of this and represents an effort to *look* like they care about Free & Open Source Software.

While Apple has added internal projects to Apple Open Source over the years, the amount of packages available on it has remained roughly the same due to deletions. Some notable removals include `launchd`, which has been excluded since the release of Mac OS X 10.10 Yosemite, and `CFNetwork`, which was removed with the release of Mac OS X 10.5 Leopard.

Perhaps the most confusing move Apple has made with Apple Open Source is with removing `CoreFoundation`. It was removed at the same time as `CFNetwork`, with the release of 10.5, but with later releases of 10.5 it was first marked as *Coming soon* (10.5.1) and then added with 10.5.2. This delayed release pattern may be interpreted as internal debate within Apple on whether to release `CoreFoundation` or not, or time taken to strip parts out of it. Once again, `CoreFoundation` was marked as *Coming soon* when the open source bits of Mac OS X 10.11 were released. This time, coming soon didn't mean one version minor later. No one knows what it means, because it has been two years since Apple made the promise that `CoreFoundation` was coming soon.

It is not as if they have forgotten, because on one occasion I emailed [opensource@apple.com](mailto:opensource@apple.com) about it and never received a response.

`CFNetwork`, unlike its friend, has never been released since it was taken away with Leopard and didn't even get a coming soon promise.

Apple has always made the Darwin kernel (`xnu`) open source, so they deserve credit for that. However, they strip out the arm related assembly code, which leaves a strange message to those who want to review it. How are people supposed to audit the kernel they use on their iPhones if Apple withholds the bits of code relevant to the iPhone?

There is also a category of projects for which Apple has released the source code but they aren't open source; meaning they lack the freedom to modify and redistribute. One of these such projects is `corecrypto`, which you aren't allowed to redistribute and must delete after 90 days of downloading. Releasing code under such licenses is very backwards and undermines the message that Apple attempted to communicate by creating Apple Open Source.

Apple Open Source largely goes under the radar of the media and many iOS and macOS developers likely don't know it exists.

If you feel motivated to reach out to Apple Open Source through the Contact Us button at the botton of the site, don't expect a response.
