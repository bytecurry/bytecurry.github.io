---

layout: post
title: Proposed changes for a new Common Lisp Standard
tags: lisp

---

The ANSI Common Lisp standard was pubished in 1994. That was 21 years ago (in 2015). A lot has
changed since then, and in my opinion there are several non-standard features that most implementations provide that should be standardized, as well as some other improvements. This
post is a catalog of things I would like to see standardized in a new lisp standard.

Some argue that Common Lisp doesn't need a new standard because it is powerful enough that new
features can be added through libraries and user code. To some extent this is true, and for many of the things in this post there are compatibility libraries. But for most them them libraries must
either be compatibility layers over implementation specific features, or use FFI, which is itself
not standardized. And for some, the change is more fundamental. Also, compatibility libraries
have the problem that need to be maintained for every lisp implementation, which isn't always feasible, it would be much better if there is a standard that the implementations are responsible for following.

This is by no means a technical proposal for a standard. It is more of a wish-list of what I would
like to see in a new standard, if it was ever created.

## Pathnames and File System

Most lispers would agree that Common Lisp pathnames are overly complex and a pain to use.
The lisp pathname system is antiquated and a relic of when there were many more ways to represent filenames, but now there are really only two: Unix filenames and Windows filenames (there are probably obscure operating systems that use other filename systems, but they are certainly not
widely used). Lisp pathnames are overspecified in some ways and underspecified in others. I would
like pathnames to be simplified. Here is a list of things I would like to see:

- Remove logical pathnames, they are rarely used, and difficult to use portably
- Remove the pathname host and version, they don't mean anything on modern implementations
- Provide functions to convert to and from _native_ namestrings and pathnames. Maybe this just means requiring the namestring functions to return the native namestrings. But the fact that in the current standard there is no way to portably get a pathname from a OS filename, or get the OS filename from a pathname is frankly ridiculous.

## OS Environment

Beyond opening files and listing directory contents, ANSI lisp doesn't specify any
other interaction with the operating system. At a very minimum the following should be
standardized:

- The ability to read any command line arguments passed to the program
- A way to read and write environment variables
- A way to run external commands in the system, and control stdin and stdout. Something similar
to `popen` in C.
- A portable function to end the program with an exit code

Additionally, the following would be nice, but not necessary:

- Access to the current user and group id and/or names
- A function to create a temporary file
- Functions to change and get the current working directory

## Unicode

The ANSI standard makes no mentions of Unicode and has very little specification around character
representation or encoding. I would like the following to be standardized:

- A required external-format of `:utf-8`
- Require that char-code and code-char _must_ use take and return the Unicode code point.
- Reader `#\` syntax for numeric character literals, using Unicode code points (for example something like `#\x1234` which expands
to `(code-char #x1234)`).

Notice that none of these require that the implementation actually support full Unicode range,
only that for the characters it does support it is Unicode aware (and can encode/decode UTF-8,
which is a pretty standard encoding).

## Concurrency

Concurrency is a major part of modern applications, but the ANSI lisp says not a word about it.
However, there is a proposed standard and compatibility library in the form of
[Bordeaux Threads](https://trac.common-lisp.net/bordeaux-threads/wiki/ApiDocumentation).

In the case of a new lisp standard I would expect the Bordeaux Threads standard to be part of it.
But Bordeaux Threads is somewhat minimalist, and I would also like it if the following
concurrency primitives were included:

- Atomic operations and/or compare-and-swap semantics
- Timers, such as SBCL's make-timer and friends.
- Semaphores

## Sockets

In 1994 the internet was only used by a few. Now it is critical for many applications
(and certainly for web applications). Every implementation I know of has support for sockets.
Unfortunately, their interfaces for using sockets vary widely. There is also
[usocket](https://common-lisp.net/project/usocket/) which provides a portability layer.

A new lisp standard should definitely standardize socket usage, and possibly specify
local domain (unix) sockets as well.

## User Defined Streams and Sequences

In the ANSI Lisp standard there is no mechanism to create user-defined
streams or sequences. Even before the ANSI standard was standardized there was a
proposed standard for user defined streams in the form of [Gray Streams](http://www.cliki.net/gray%20streams).
Allegro proposed an alternative in the form of [Simple Streams](http://franz.com/support/documentation/current/doc/streams.htm).

Personally, I like simple streams better, but gray streams are more widely implemented by implementations, have a
compatibility library ([trivial-gray-streams](https://github.com/trivial-gray-streams/trivial-gray-streams)), and are
thus used in libraries. But one or both of those standards should be part of any future lisp standard.

In the case of user defined sequences, the only implementation I know of that provides such a mechanism is SBCL.
There was also a [talk](http://www.doc.gold.ac.uk/~mas01cr/talks/2007-04-03%20Cambridge/ilc-talk.pdf) given about it.
I think that user-defined sequences are generally useful and would like to see them standardized (and implemented).

## Meta Object Protocol

## FFI

## Packages

- package-local nicknames
- symbol alias (multiple names for the same symbol, helps deal with conflicts)
- hierarchical packages

## Garbage Collection

- weak hash tables
- finalizers
- force garbage collection
- trivial-garbage

## Misc

- octet type ?
- unix timestamps
- octets-to-string and string-to-octets
- octet buffer streams
- estensable test/hashing for hast-tables
