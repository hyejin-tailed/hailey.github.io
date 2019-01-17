---
layout: archive
date: 2019. JAN
permalink: memory-leak/
title : "Memory Leaks"
tags: [iOS, Memory]

author_profile: true
header:
  image: "page_images/1-0.jpg"
---

## H2 Memory Problems and Types of Debugging


# H1 Why Did I Try This Project?

Usually at a start-up company,  it is important to develop certain functions as soon as possible and then fix it to a stable state.
Since this is nature of work, I’m always searching for new functions that I never knew about and then applying them to my projects.
Yes, the most important thing is stability. So i prefer usually to use “strong” variable  to prevent crash.


#H1 Debugging
See? It was just simple segue between profile tab in main.async thread using Grand Central Dispatch.


{% include figure image_path="page_images/1-0.jpg" alt="this is a placeholder image" caption="This is a figure caption." %}


#H1 Memory Problems


## H2  Check 1. Types
1.  Value Types : Intances keep a unique copy of thier data.  - String, Int, Bool, Array, Dictionary, struct, enum,
2. Reference Types : Instances share a single copy of the data - class (0x0…)


## H2  Check 2. Retain Cycle
1. retain: continue to hold on to, not let go.
2. cycle: to go back and forth or around in a circle. both intences reference to each other.



## H2  Check 3. Make a Order
1. identify who the child is.
2. make the child have a weak or unowned reference to parent - a weak or unowned reference does not increase the Reference Count (not tracked)


## H2  Check 4.
-parent - child? : optional var (not let)
-may or may not exist (optional)
-wll not exist if parent is removed from memory
-will not increase reference count
-will be mutated (changed) to nil once there are no reference to it (var, not let)


### H3 weak?
parent - child : optional var (not let)
-parent - child!
-references always have a value.
-will never be nil once set.


### H3 unowend?
not optional


## H2 Check5. Capture List
: Closures are self-contained blocks of functionality that passed around and used in your code.
-Closures are reference type.
-Captured variable also strong reference type in Closures.
-Use a Capture List to  change variables to weak or unowned.


# H1 I Tried, However Faced an Issues.
I tried to make @IBOutlet var  to @IBOutlet weak var , but my project is consisted of MVVM pattern so using segue with storyboard occured a problem not to draw cells.


# H1 Conpensate the Defect
So I should change all @IBOutlet weak var to strong.


# H1 Result


### H3 Reference
- youtube: Mark Moeykens Memory 1 - Value Types vs Reference Types (iOS, Xcode 9, Swift 4)






{% include group-by-array collection=site.post field="tags" %}

{% for tag in group names %}
  {% assign posts = group_items[forloop.index0] %}
  <h2 id="{{ tag | slugify }} class="archive_subtitle">{{ tag }}</h2>
  {% for post in posts %}
    {% include archive-single.html %}
  {% endfor %}
{% endfor%}
