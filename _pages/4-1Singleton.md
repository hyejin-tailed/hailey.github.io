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

```swift
Global.Member != nil
Global.IS_PUSH_READY
````

They are so indifference to use memory that each Instances' each values changed by each functions at the sametime!!!!! (on multiple threads!!)

Although it is not perfect but there are some reasons I suggest using singleton.

# Example
URLSession.shared
FileManager.default
UserDefaults.standard
GIDSignIn.sharedInstance()


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
    lazy var header: [String: String]
  }
````

The Reason why I used **lazy var** is header is up to accessToken.

```swift
lazy var header: [String: String] {
    var defaultHeader = ["Language": Util.myLanguage()]
    if accessToken == "" {
        defaultHeader["Auth"] = "\(accessToken)"
    } else {
        defaultHeader["Auth"] = "notMember"
    }
    return defaultHeader
}
````

Let's complete

```swift
struct NMember : Codable{
    var memberId: Int
    var email: Int
    var langCode: String
}

class MyInfo {
    static let sharedInstance: MyInfo = MyInfo()

    var accessToken: String = ""
    lazy var member : NMember? = nil
    lazy var header: [String: String] = {
        var defaultHeader = ["Content-Type":"application/json;charset=UTF-8",
                             "Accept-Language": "ko"]
        if accessToken == "" {
            defaultHeader["Auth"] = "notMember"
        } else {
            defaultHeader["Auth"] = "\(self.accessToken)"
        }
        print("accessToken = \(accessToken) header = \(defaultHeader)")

        return defaultHeader
    }()

    private init() {
    }

    func setMyInfo(_ member: NMember) {
        self.member = member
    }

    func setToken(token : String){
        accessToken = token
    }
}

func login(){
    MyInfo.sharedInstance.setToken(token: "login!")
    print("login header = \(MyInfo.sharedInstance.header)")

}

login()
````

```
accessToken = login! header = ["Content-Type": "application/json;charset=UTF-8", "Accept-Language": "ko", "Auth": "login!"]
login header = ["Content-Type": "application/json;charset=UTF-8", "Accept-Language": "ko", "Auth": "login!"]

````

#lazy var
**MyInfo** will be initiated when accessToken is preserved by APIs.

**var** invokes when the instance is initiated.
So, nobody doesn't know which variable of them is going to be invoked by order.
But at least, I want to set order with accessToken and header.
**var accessToken** will be invoked when the instance is initiated.
After that, **var defaultHeader** will be invoked.




### Reference
https://jeong-pro.tistory.com/86
https://ehdrjsdlzzzz.github.io/2018/10/28/Design-Pattern-Singleton/
https://medium.com/@abhimuralidharan/lazy-var-in-ios-swift-96c75cb8a13a
