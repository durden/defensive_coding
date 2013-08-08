## Bugs: Can't code without them, so code against them!

Talk for PyTexas 2013 on concepts of coding defensively

### Abstract proposal

There are a lot of approaches and philosophies to prevent bugs in software, but
the truth is they are unavoidable in complex, modern systems.  So, what's a
developer to do?  Code in a style that tries to alert and test for the bugs
when they happen instead of feeling like a failure when you can't prevent the
unavoidable.

Wikipedia defines this style of programming as 'defensive programming,' and the
idea is code in a way that expects software to be misused and have bugs.  This
talk will explore this general concept and how to add bits of this style of
development to you Python code with the following:
    - Asserts
    - Logging
    - Unit tests

The presentation requires [landslide](https://github.com/adamzap/landslide)
to view.  This can be installed via pip and the included `requirements.txt`
file (`pip install -r requirements.txt`).

#### Live presentation slides

You can view a live version of the presentation
[here](http://durden.github.com/defensive_coding).
