---
title: Recommended Lisp Libraries
layout: default
---

# Recommended Lisp Libraries

Some Related pages:

* [State of the Common Lisp Ecosystem](http://eudoxia.me/article/common-lisp-sotu-2015/)
* [CLiki recommended libraries](http://cliki.net/current%20recommended%20libraries). Note that
despite the name it is somewhat dated.
* [Quickdocs](http://quickdocs.org/)

## Utils

### [Alexandria](https://common-lisp.net/project/alexandria/) -- basic utilites

### [Serapeum](https://github.com/TBRSS/serapeum) -- more utilies

More utilities. Designed to compliment Alexandria.

### [Optima](https://github.com/m2ym/optima) -- Pattern Matching

### [CL-PPCRE](http://weitz.de/cl-ppcre/) -- Regular expressions

### [Iterate](https://common-lisp.net/project/iterate/) -- A better looping macro

Iterate is an alternative to `LOOP` that is more lispy, extensible, and
looks nicer.

## Compatibility layers

### [UIOP](https://common-lisp.net/project/asdf/) -- filesystem and etc.

UIOP is part of ASDF, and provides an extensive portable library for working with the file
system and operating system. As well as utilities to help with managing packages and creating
lisp images.

You can view some documentation [here](http://bimib.disco.unimib.it/people/Marco.Antoniotti/Projects/CL/HELAMBDAP/tests/asdf-uiop/docs/html/dictionary/dictionary.html).

### [Usocket](https://common-lisp.net/project/usocket/) -- sockets library

### [trivial-gray-streams](https://common-lisp.net/project/trivial-gray-streams/) -- user extensible streams

### [bordeaux-threads](https://common-lisp.net/project/bordeaux-threads/) -- threading

### [Closer to MOP](https://common-lisp.net/project/closer/closer-mop.html) -- Meta Object Protocol

## Web

### [Clack](http://clacklisp.org/) -- web application environment

Clack is a server-agnostic web application environment similar to Python's WSGI or
Ruby's Rack. I would recommend either using a web framework based on this, or using it
directly rather than using a server application such as hunchentoot or wookie directly.

For the actual server there are a few options:

* [Hunchentoot](http://weitz.de/hunchentoot/) This is probably the most popular lisp server.
If you don't have a good reason to use something else, this is a good place to start.
It is a standard threaded web server
* [Wookie](http://wookie.lyonbros.com/docs) An asynchronous lisp webserver. If you want an
async server use this.
* [Woo](https://github.com/fukamachi/woo) A newer asynchronous lisp web server. Still in beta.

### [Djula](http://mmontone.github.io/djula/) -- templating system

Based on Django templates (and similar to liquid), djula provides a flexible, modern templating
solution. I would recommend it for creating web templates. It is suitable for html, and can be used
for other formats such as json and xml as well.

### [Ningle](http://8arrow.org/ningle/) -- minamalist web framework

A very minimalist web framework built on clack. It basically just provides routing infrastructure
and request and response objects.

### [Caveman2](http://8arrow.org/caveman/) -- web framework

Built on top of ningle it provides some additional functionality, including database
support with cl-dbi, configuration, modularization, etc.


## Data structures and collections

Unfortunately there isn't a single complete collections library for
common lisp (that I know of). cl-containers and lisp-interface-library both try to be
comprehensive collection libraries... but neither is complete or well documented, and have some
weird behavior in some cases (for example an iterator over a mutable map in lisp-interface-library
destroys the underlying map). Personally, if you want functional types I would recommend Fset, if not,
I can't make a strong recommendation. With that said here are some libraries:

### [Colliflower](https://github.com/bytecurry/colliflower)

Of course I will recommend my own library: colliflower. It doesn't add any
additional collections, but it does provide a convenient way to work with collections
in a uniform way. At some point I may add integrations with other collection libraries.

### [Fset](https://github.com/slburson/fset)

Fset is a library for functional data structures implemented using weight-balanced binary trees.
It provides maps, sets, bags and sequences.

### [Lisp Interface Library](https://github.com/fare/lisp-interface-library)

A collection library that uses an interesting "interface passing style" where you pass
along an interface object that describes the semantics of the underlying data representation.

It focuses on immutable data structures, so support of mutable data structures is somewhat lacking.

There is almost no documentation other than a few tests and an article describing the interface
passing style.

### [cl-containers](https://github.com/gwkkwg/cl-containers)

Another container library. Unlike Fset and lisp-interface-library, it focuses on mutable data structures.
It uses dynamic classes to create new classes with the desired behaviour, which is kind of cool when it works,
but causes some weird edge cases.

I would recommend against using this unless you need it.
