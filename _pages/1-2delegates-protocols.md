---
layout: archive
date: 2019. FEB
permalink: delegates-protocols/
title : "Delegates and Protocols"
tags: [iOS, object-oriented]

author_profile: true
header:
  image: "page_images/2/2-0.jpg"
---

# Pass Data Between Viewcontrollers in Object-Oriented Programming

<br><br>

# Why Did I Try This Project?

There are many ways to pass data between ViewControllers.
By the way, for object-oriented programming, there is an attractive way that Swift and C# have called "Delegates".
Java has a similar way called "Interface".

# Three ways to pass data between ViewControllers.
1. NotificationCenter: Loaded by FirstViewController.
2. Callbacks: Loaded by SecondViewController.
3. Delegation: The act of giving responsibility to another. This needs protocol.

### Protocol
- A protocol is a common means for unrelated objects to communicate with each other
- A protocol defines a blueprint of methods, properties, and other requirements that suit a particular task or piece of functionality.
java: interface


# How to Implement

## 1. Create Protocol
{% include figure image_path="page_images/2/2-1.jpg" alt="this is a placeholder image" caption="" %}

## 2. Create a delegate property  
{% include figure image_path="page_images/2/2-3.jpg" alt="this is a placeholder image" caption="" %}

## 3.Conform to the protocol (add functionality)
{% include figure image_path="page_images/2/2-2.jpg" alt="this is a placeholder image" caption="" %}


### Reference
- youtube: Passing Data with Delegates/Protocols (iOS, Xcode 9, Swift 4)

{% include group-by-array collection=site.post field="tags" %}

{% for tag in group names %}
  {% assign posts = group_items[forloop.index0] %}
  <h2 id="{{ tag | slugify }} class="archive_subtitle">{{ tag }}</h2>
  {% for post in posts %}
    {% include archive-single.html %}
  {% endfor %}
{% endfor%}
