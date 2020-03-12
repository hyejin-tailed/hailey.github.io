---
layout: archive
date: 2020. MAR
permalink: singleton/
title : "Singleton"
tags: [iOS, Memory]

author_profile: true
header:
  image: "page_images/4-1/title.png"
---

# How to save memory avoid of unnecessary assingment.
<br><br>

# Why Did I Try This Project?

Usually apps that I have made aim to get and manage a lot of users. According these reason, apps are developed having so many global variables using memory address each!! Especially when I renovated apps which were put out to outsourcing, I got annoyed on instance called

**Global.Member != nil**
**Global.IS_PUSH_READY**

They are so indifference to use memory that each Instances' each values changed by each functions at the sametime!!!!! (on multiple threads!!)

Although it is not perfect but there are some reasons I suggest using singleton.

## Pros
- Mutable globally keeping fixed memory by using instances.
It guarantees consistent values on different threads when to share the instance during the app lifecycle. (ex. DBCP etc.)
- Whenever it accessible from any classes. (ex. Viewcontroller, interactor etc.)
- Dramatically Save loading time from second time.

## Cons
- hinder unit testing.
- sacrifice transparency for convenience.

#MyInfo
```swift
class MyInfo {
    static let sharedInstance: MyInfo = MyInfo()

    var accessToken: String = ""
    lazy var member : NMember?
    lazy var headerJson: [String: String]
  }
````

# Example
URLSession.shared
FileManager.default
UserDefaults.standard
GIDSignIn.sharedInstance()


### Reference
https://jeong-pro.tistory.com/86
https://ehdrjsdlzzzz.github.io/2018/10/28/Design-Pattern-Singleton/
