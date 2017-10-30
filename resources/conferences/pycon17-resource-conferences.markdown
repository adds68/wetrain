---
resource: true
categories: [Conferences]
title: "PyconUK"
exclude: true
---

# PyconUK

### Unsafe at any speed - Rae Knowler
- Unsafe at any speed (Book about automotive safety)
- Defaults are not bad, bad deafualts are bad 
- CKAN open data framework for python, hosts uk gov open data sites
- YAML parsers default allows arbitrary code execution, as it defaults to 
load(), instead safe_load() should be used,

### Programming Music for Performance - Ryan Kirkbridge
- Haskell live coding platform https://tidalcycles.org/
- He decided to create foxdot, his own live coding platform
- http://foxdot.org/

### Building a python frontend for HPC codes - Alice Harpool
- Wanted to implement an interface with python to some HPC libs that are written in Fortran Amrex Cortex.
- In order to write less fortran 
- f2py allows the calling of fortran in Python
- She wanted to call wrapped fortran code in python in c++
- Used python 3.6 docs to understand how to call python in C++
- Used a module called YT for plotting in  Python
- http://www.boost.org/doc/libs/1_65_1/libs/python/doc/html/tutorial/index.html

### Functional Python - Paul Will Jones
- Programming without mutations or imperitive control strcutures
- Higher class functions
- Lazy Evaluation
- Recursion
- You can optimize tail recursion in python using trampolining
- Coconut python module
- Speaker spoke very fast, so was no real deep-dives into any constructs, just general paradigms used in python.

### Pythonic code vs Performance - Lukasz Kakol
- What is profiling - CPU / Memory / I/O time
- Used Cprofiler to compare C style syntax to Python syntax for different common problems to see if python slows things down.
- Conclusion as not very conclusive

### Implenting custom containers - Claus Aichinger
- You can use a named tuple instead of a class 'namedtuple' 
- You can add __doc__ to custom container members to add descriptions about what they are used for
- __new__.__defaults__ can be used to set defaults on a custom container 
- Take a look at attr:Classes without boilerplate

### Python as a second language - Hannah Hazi
- Baby duck syndrome - your first learnt language will affect the way you learn every other language
- https://raspberrycheesecake.github.io/

### Building Quart from Flask & Asyncio - Phil Jones
- Asyncronous 'colour' problem, solved by hyper-2 http2 module in Python
- probably good to rewatch on *youtube*
- http://sans-io.readthedocs.io/

### On Big computation with Python - Russel Winder
- Don't make Python do everthing!
- We Should embrace multiple languages
- Numba - pure python
- Numpy - Cpython but slower
- Numba with @jit decorators was as fast as the D implementation
- https://www.russel.org.uk


# Day2

### Abstract Base Classes - Leonardo Giordani
- Blog (thedigitalcatonline.com)
- http://blog.thedigitalcatonline.com/blog/2016/04/03/abstract-base-classes-in-python/
- OOP programmers should be concerned with behaviour and not implementation
- Python collections module offers 'isinstance' method
- Virtual subclasses parentClass.register(childClass)
- from abc import metaABC

### Seven Deadly Wastes - jez Halfords
- Muda development system invited by toyota
- Transport, Inventory, Motion, Waiting, Over processing, Over production, Defects
- Very mangementy talk, but still quite interesting i guess
- OOPSI product stories

### Understanding natural language word vectors - Marco Bonzanini
- word2vec
- Use the surrounding words of a target word to infer meaning 
- gensim python nlp module
- marcobonzanini.com

### Automate your boilerplate
- cookie-cutter data science on github
- he build Mason, a command line tool for creating project structures from cmd

### What i learned building Forth in 64-bit assembly - David Jones
- sixity-forth drj11  (git-repo)

### Visualising environmental data with Bokeh in Python - marcus Donelly
- NOAA provides large scale open data collection
- OpenDAP is an open source data protocol/format
- Bokeh provides data analysis in python with a javascript interactive browser
- Can use CustomJS class to add custom js to bokeh plots/interfaces
- Plotly can also run in the browser

### Single malt WSGI - Simon Davy
- Talisker module on pip
- Can be used along side gunicorn/celery
- Can be used standalone 
- 

# Day 3

### Lazy sequences working hard - Thomas Guest
- wordaligned.org
- Genrators are an example of lazy containers in python, they are not actualyl running, just ready to run
- Same with Range() in python, it doesnt generate all the numbers, but it is ready to do so
- @pipe function in python

### Efficient data mangling with panda indexes - alexander hendorf
- had to stand up, no notes :(

### Learning to code for data analysis - Michel Wemelinger
- Futurelearn MOOC http://tiny.cc/lcda
- Works for the OU and built a course to teach people data science

### OOP workshop - Delegation
- Delagation ( Composition | Inheritance)
- Composition means it's composed of more than one thing
- Inheritance Is the thing, so cat is an Animal, not compaosed of Animal
- Class.__bases__ lists out inherited classes
- super() can used to access inherited class properties E.G super().name = name

# Day 4

### A trip to earth science with Python - Nikoleta Glyntasi
- Wanted to learn why earth quakes happen in her hom country (Greece)
- Quakefeed, allows you to collect data from the UCQS
- Matplotlib BaseMap Toolkit
- OBSpy allows you to analyse sysmic graphs
- @NikoletaGlyn

### MyPy the good the bad & the ugly - David Sim
- MyPy static type checker for Python
- Some issues with importing modules, still to be fixed
- Verbose class definitions
- Did find lots of bugs previously not found
- Great for running CI builds and checking for errors
- It's not fully matured yet, rapid development though

### An anble history through some of Python's history - Tony ibs
- https://github.com/tibs/python-history

#### 1994

- 1.0 Released in 1994
- He started using in 1994
- Introduced for else in 0.9.1 but no __init__()
- 1 == 1.0 in v0.9.2.0
- [-1] index for arrays was introduced in 0.9.4
- 0.9.8 intriduced struct modle for talking to C
- v1.0 buildes on many unices by using autoconf, introduced lambda
- v1.1 introduced threads, tkinter
- Guido announced as BDFL
- timsort the sorting algorithm used by Python

#### 1995

- Grail python browser released, which could run Python in the browser
- Java 1.0 was relaesed
- v1.2 released, introduced docstrings, maybe came from emacs self documenting code
- v1.3 introduced the ni module, for evaluating syntax

#### 1996

- v1.4 released, dicts were ordered and then changed back to now not-ordered

#### 1997

- v1.5
- Christian Tismer starts starship Python
- JPython started
- #!/usr/bin/env was introduced
- private variables were introduced with dunder_var

#### 1998

- Stackless python released
- Zope program was released, Pythons should have been killer app
- Zope was the first company to open source their source code

#### 1999

- v1.5.2 released
- IDLE introduced, another monty python reference
- quit and exit tell you how to exit

#### 2000
- v1.6
- Hosted on source forge
- PEPs introduced
- Alex Martelli coins "duck typing"
- Oct 2000, Python 2.0
- list comprehensions introdcued in v2
- Fredrick lung references in python


# END
