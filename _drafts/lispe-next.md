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

## Pathnames and File System

## OS Environment

- command line arguments
- environment variables
- run-command

## Unicode

## Concurrency

- bordeaux threads
- semaphores
- compare-and-swap/atomic operations
- timers

## Sockets

## User Defined Streams and Sequences

## Meta Object Protocol

## FFI

## Packages

- package-local nicknames
- symbol alias (multiple names for the same symbol, helps deal with conflicts)
- hierarchical packages

## Misc

- octet type ?
- unix timestamps
