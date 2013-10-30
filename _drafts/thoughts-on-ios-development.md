---
title: My thoughts on iOS development
layout: default
permalink: development
---

I've been developing iOS apps for almost 4 years. In my first company, I'm very
lucky to be involved in the Labelbox[^1] project and implement it from stratch.
The core function has been developed under two weeks. 

I was also responsible for revamping Steply and 潮品 (pronounced as "Chao Pin" in
Chinese), both of them are instagram-like photography social network. They were 
heavily image based and there was a slight lag whenever a new photo is being rendered into
the feed view. I wasn't pleased with the results and struggle to elimate the tiny lag, and
later I found a solution and have been merged into one of the popular
opensource image downloading project [rs/SDWebImage]



[Labelbox]:https://itunes.apple.com/hk/app/labelbox/id417694704?mt=8
[rs/SDWebImage]:https://github.com/rs/SDWebImage
[^1]: Labelbox is a photography utility app that adds "labels" to photos with user specified text and style. Today it remains one of the most notable in-house product for the company. While I implemented most of UI part and adding label gestures, the label market was added after I left the company. You can download [Labelbox] from the app store.
