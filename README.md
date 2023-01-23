# workgroup
This is a collection of resources for people implementing and working with parallel and asynchronous code.

# Table of questions

Question|Why this question|
|--- | --- | ---|
What is the unit of schedulable code?|Some systems are actor based, some green threads, fibers, coroutines, lightweight threads, processes or threads|
How is the unit of schedulable code scheduled?|An indepth explanation how |
Is it cooperative, preemptive or other?|Some languages are preempted and are descheduled by an outside process such as the operating system or a scheduler or scheduler thread |
What is the interaction with the type system?|Some langauges use type system to enforce safety|
How is asychrony represented?|How can you schedule multiple tasks at the same time?|

# Pony Lang

From Pony Lang's website: https://www.ponylang.io/

"Pony is an open-source, object-oriented, actor-model, capabilities-secure, high-performance programming language."

# Inko

From Inko's website: https://inko-lang.org/


"
A language for building concurrent software with confidence
Inko makes it easy to build concurrent software, without having to worry about unpredictable performance, unexpected runtime errors, race conditions, and type errors.

Inko features deterministic automatic memory management, move semantics, static typing, type-safe concurrency, efficient error handling, and more.

Inko supports 64-bits Linux, macOS and Windows, and installing Inko is quick and easy."

# Golang

From golang's documentation: https://go.dev/doc/

"The Go programming language is an open source project to make programmers more productive.

Go is expressive, concise, clean, and efficient. Its concurrency mechanisms make it easy to write programs that get the most out of multicore and networked machines, while its novel type system enables flexible and modular program construction. Go compiles quickly to machine code yet has the convenience of garbage collection and the power of run-time reflection. It's a fast, statically typed, compiled language that feels like a dynamically typed, interpreted language."
