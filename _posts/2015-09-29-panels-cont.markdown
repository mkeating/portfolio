---
layout: post
title:  "Panels continued, and Library"
date:   2015-09-29
categories: devlog
---

I've continued the design of panels by including 2 attributes: origin and terminal. Origin == true will mean that a panel is the first panel of a new story. Terminal will default to false for now; I included it in case I want users to be able to 'kill' a storyline and prevent any future branches from that panel. At the moment it feels unnecessarily stifling so I won't implement it, but the object attribute is there if needed.
Designing panels this way allows me to avoid having any sort of Story object at all. Stories are simply defined by their origin panel. Specific storylines are created by climbing backwards up the chain of parents from a given panel.
Here's how the panel object looks currently:
<pre><code>

  Panels.insert({
            title: title,
            text: text,
            createdAt: new Date(),
            createdBy: Meteor.userId(),
            origin: true,
            terminal: false,
          });

</code></pre>
    
I've got panel creation up and running, but still have to work out how a newly created panel will inherit the id of its parent. I should have this wrapped up in the next day or so.
Another bit I've worked on is having a Library view; at the moment it's just a listing of all panels where origin == true. This is where users can browse stories rather than starting their own, and I'll be refining it and allowing search, sorting by various tags, etc.