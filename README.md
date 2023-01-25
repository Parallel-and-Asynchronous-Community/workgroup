# Parallel and Asynchronous Community workgroup
This is a collection of resources for people using and work on implementing and working with parallel and asynchronous code.

# Table of questions

|Question|Why this question|
|--- | --- |
|What is the unit of schedulable code?|Some systems are actor based, some green threads, fibers, coroutines, lightweight threads, processes, promises, events or threads|
|Is there special language keywords?|Async/await keywords|
|How is the unit of schedulable code scheduled?|An indepth explanation how |
|Is it cooperative, preemptive or other?|Some languages are preempted and are descheduled by an outside process such as the operating system or a scheduler or scheduler thread |
|What is the interaction with the type system?|Some langauges use type system to enforce safety|
|How is asychrony represented?|How can you schedule multiple tasks at the same time?|
|How does parallelism, asychrony interact with garbage collection or memory management|There is usually interactions between asychronous elements due to change of ownership of resources between independently scheduled execution units.|
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

## Scheduling

Hey, welcome! A high-level overview of the scheduler is this:

There's are N threads running code. Each thread has its own queue, and there's a global queue. Threads run the following steps in a loop:

1. Process all jobs from the thread-local queue
2. Steal a number of jobs from another queue
3. Steal a number of jobs from the global queue
4. Go to sleep

The initial process is scheduled onto the global queue and thus picked up by a random thread. Newly spawned processes are stored in the thread-local queue. If there are sleeping threads, one is woken up.

Thread-local queues have a fixed size, and new processes are scheduled onto the global queue if the local queue is full.

Processes run for a fixed amount of time using reductions. This is just a simple counter: it starts at X, and the process suspends when it reaches zero. Currently the only thing that results in a reduction is a method call, which reduces by 1, but this may change in the future.

For sockets we use non-blocking IO. If a socket would block we use epoll/kqueue/etc to poll for readiness in a separate OS thread, rescheduling the process if the socket is ready.

For files and other forms of IO that don't support non-blocking IO, we essentially mark the thread as "blocked". When this happens, a backup thread is woken up and takes over work. When the blocked thread unblocks, it reschedules the process onto the global queue and the thread becomes a backup thread. The default thread count is N regular threads and N * 4 backup threads, where N is the number of CPU cores.
[21:16]
Things are being moved around a bit as part of the work on the native compiler, so code wise it's best to look at the native-compiler branch. The scheduler code lives in https://gitlab.com/inko-lang/inko/-/tree/native-compiler/vm/src/scheduler


# Golang

From golang's documentation: https://go.dev/doc/

"The Go programming language is an open source project to make programmers more productive.

Go is expressive, concise, clean, and efficient. Its concurrency mechanisms make it easy to write programs that get the most out of multicore and networked machines, while its novel type system enables flexible and modular program construction. Go compiles quickly to machine code yet has the convenience of garbage collection and the power of run-time reflection. It's a fast, statically typed, compiled language that feels like a dynamically typed, interpreted language."

# Erlang

From Erlang website: https://www.erlang.org/

"What is Erlang?
Erlang is a programming language used to build massively scalable soft real-time systems with requirements on high availability. Some of its uses are in telecoms, banking, e-commerce, computer telephony and instant messaging. Erlang's runtime system has built-in support for concurrency, distribution and fault tolerance.

What is OTP?
OTP is set of Erlang libraries and design principles providing middle-ware to develop these systems. It includes its own distributed database, applications to interface towards other languages, debugging and release handling tools."

# Javascript

From MDN Javascript page: https://developer.mozilla.org/en-US/docs/Web/javascript

"JavaScript (JS) is a lightweight, interpreted, or just-in-time compiled programming language with first-class functions. While it is most well-known as the scripting language for Web pages, many non-browser environments also use it, such as Node.js, Apache CouchDB and Adobe Acrobat. JavaScript is a prototype-based, multi-paradigm, single-threaded, dynamic language, supporting object-oriented, imperative, and declarative (e.g. functional programming) styles.

JavaScript's dynamic capabilities include runtime object construction, variable parameter lists, function variables, dynamic script creation (via eval), object introspection (via for...in and Object utilities), and source-code recovery (JavaScript functions store their source text and can be retrieved through toString())."

# Futhark

From Futhark's website: https://futhark-lang.org/

"Futhark is a small programming language designed to be compiled to efficient parallel code. It is a statically typed, data-parallel, and purely functional array language in the ML family, and comes with a heavily optimising ahead-of-time compiler that presently generates either GPU code via CUDA and OpenCL, or multi-threaded CPU code."
