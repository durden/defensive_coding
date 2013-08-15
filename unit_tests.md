# Unit tests

- Not just for Test Driven Development
- Old bugs have tendency to come back
- Re-factoring insurance
- Release early, find bugs, write tests, repeat

# Presenter notes

- Hard to get manager buy-in b/c it takes longer usually up-front

--------------------------------------------------

# Unit test benefits

- Improves documentation of bug fix
- Answer [5 Ws](http://en.wikipedia.org/wiki/Five_Ws)
    - http://en.wikipedia.org/wiki/Five_Ws
- Future-proof code against duplicate bugs

# Presenter notes

- Think executable documentation!
- Document how you tested it, what the bug scenario was
- Good unit test is best doc for weird bug fix
    - test will include comments, data to re-create bug, steps for scenario
- Refactoring has a tendency to allow old bugs to creep in

--------------------------------------------------

# Unit test downsides

- Hard to run
- Not usually located close to real code
- Some environments hard to duplicate
- False positives

# Presenter notes

- Doctests are nice b/c they are right there with code but can be ugly
    - Problems for documentation generators like sphinx?

--------------------------------------------------

# Unit test tools

- Pytest
- Nose
- doctests
- Travis CI

# Presenter notes

- Tools to help mitigate the hard to run aspect of tests
