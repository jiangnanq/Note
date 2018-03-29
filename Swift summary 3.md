---
title: Summary of Swift 3
date: 2017-7-13
tags: iOS
---

# Summary of Swift development

The summary of Swift development. (Part 3)
Swift version: 3.0
Xcode version: 8.2.1

1. [Random value](#random value): Generate random value

1. <a name="random value"></a> **Random value**
    {% codeblock lang:swift %}
        let random = Int(arc4random_uniform(UInt32(mrtStations.count)))
        astation  = mrtStations[random]
    {% endcodeblock %}
