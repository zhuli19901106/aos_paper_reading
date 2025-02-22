# The Scalable Commutativity Rule: Designing Scalable Software for Multicore Processors
##Authored jointly by MIT and Havard, Doi:10.1145/2517349.2522712  

####Student Name: Zhu Li
####Student ID: 2015210959
####Major: Computer Science, Tsinghua University
####Organization: Institute of High Performance Computing
####Instructor: Prof. Jiwu Shu

## What is the paper discussing?
The paper talks about the scalablity, but not just an implementation issue, but even before implementation.

It introduces a rule, "Whenever interface operations commute, they can be implemented in a way that scales."

By this rule, the paper claims that the system can be **designed to be** scalable, more than just **implemented to be** so.

To illustrate their idea, the research group devised a tool named **COMMUTER**, that automatically generates tests that verifies the scalability of high-level design of interfaces.

## What are some key ideas?
Scalability evaluation on large applications usually involves high pressure, various workload, multiple cores. When problems arises, they're usually distributed among different workloads, which exhibit different type of bottlenecks.

Developers tend to resolve the issue by one-at-a-time debugging and fixing, thus making it too late to find a scalable solution.

Should the verification be executed during an earlier phase, e.g. the designing of software interfaces, things would've be different.

### Related Work:
This section talks about prior work that is related to the commutativity rule.

1. **Thinking about scalability**: Roughly, if a shared memory system is **disjoint-access-parallel**, those processes scale linearly. Even the contention of a single cache-line 
2. **Commutativity**: Previous work approximated commutativity by **being conflict-free**. While the ideas shared similarity, research was directly by different initiatives. Former researchers aimed at **safety of concurrent execution**, whereas this paper focuses on **scalability** issues.
3. **Test case generation**: Concolic testing, symbolic execution and conflict coverage.

### The Scalable Commutativity Rule:
This section provides the reader with a modelling view of the rule.

1. **Actions**: An action is either **an invocation or a response**.
2. **Commutativity**: A set of operations commutes in some context when the specification is **indifferent to the execution order** of that set.
3. **Implementations**: An implementation m is a function in S × I → S × R.
4. **Formalized proof**: The detail is hard to understand, I believe it's due to the formal language itself, with a bunch of arcane symbols.

### Designing Commutative Interfaces:
This section demonstrates the **interface-level reasoning** enabled by the rule.

1. **Decompose compound operations**: Sometimes conflict occurs during an unnecessary part of an operation, which can be removed without losing the functionality.
2. **Embrace specification non-determinism**: Overly deterministic design may result in poort scalability, such as the "lowest available file descriptor" in POSIX.
3. **Permit weak ordering**: Strict ordering often involves locking and synchronization.
4. **Release resources asynchronously**: Many POSIX operations have global effects that must be visible before the operation returns. But when an operation releases resources, **the need for an global effect to be spread all over the system** is not as strict. (A bit tricky to understand)

### The COMMUTER:
To put it simply, the paper designed such a tool to show their research has potential for **real-world applications**.

With an automated tool that generates test cases from manually defined constraints, developers of large projects might be able to find a solution for **scalable interface-level design**.

### Finding Scalability Opportunities:
- How many test cases does COMMUTER generate, and what do they test?
- How good are current implementations of the POSIX interface? Do the test cases generated by COMMUTER find cases where current implementations don’t scale?
- What techniques are necessary to achieve scalability for cases where current file and virtual memory systems do not scale?
- What situations might be too difficult or impractical
to make scale, despite being commutative?

Read the section to find the answer.

### Performance Evaluation:
It did well, really well.

The performance of the system **scales linearly up to 48 cores**. But nobody knows if it will persist at 96 cores, not even the author himself.

## What about the conclusion?
This paper introduced the idea of **commutative rule**, illustrated it with rigorous proof, implemented it with the **COMMUTER** toolkit and applied it on sv6.

It proivides new insights to developers, especially for those developers of a large software projects, that requires excellent **multicore scalability**.

## What are your thoughts?
Tip of an iceberg. The work done behind this best paper is vast indeed.
