---
layout: home
title: CS6160 Complexity (UVA)
nav_exclude: true
permalink: /:path/
seo:
  type: Course
  name: Complexity (Theory of Computation)
---


UVA CS 6160 Complexity (Theory of Computation)
----------------------------------------
This is the course website of CS 6160, Theory of Computation, instructed by Wei-Kai Lin. The meetings are [Mondays and Wednesdays at **2--3:15pm** Fall 2026](https://hooslist.virginia.edu/ClassSchedule/ClassHistory?subject=CS&catalogNumber=6160).
Please login to [Hoos' List](https://hooslist.virginia.edu/ClassSchedule/ClassHistory?subject=CS&catalogNumber=6160) to see the location.
This is the graduate-level course of Theory of Computation, but we focus on *Complexity* mostly.
Hence, we more often use *Complexity* in the course name for short.


## Recent Announcements

<!-- [(List of announcements)](#list-of-updates) -->

### Class 4: Time Hierachy Theorem, Oracle Machines
(Sep 7, 2026)

Jinye talked about Ladner's Theorem. 
It is a proof by diagonalization, and the theorem states that if $$\mathbf{P} \neq \mathbf{NP}$$, then there exists an NP problem that is neither in P nor NP-complete.

We then presented and proved the time hierarchy theorem, proved by Hartmanis and Stearns at 1965.
The proof can be viewed as an extension of Turing's halting problem, where many steps in the two proofs are one-to-one mapped.
The proof and statement extends to other resources, such as nondeterministic time hierarchy.
With that, we can clearly say that P is a strict subset of EXP, and similarly for other classes.
We compared the classes P, NP, EXP, and NEXP.
Deebak asked for a complete problem in NEXP, I did not know one and searched.
[Galperin-Wigderson'83](https://www.sciencedirect.com/science/article/pii/S0019995883800047) gives some languages, but I did not check whether the question is fully answered.

We continued to define oracle machines, which are Turing Machines augmented with an oracle function $$O$$.
The oracle may give the machine extra capability because computing the function $$O$$ takes no resource.
With that, we also defined oracle-aided classes, such as $$DTIME^O$$ and $$\mathbf{P}^O$$.
As pointed out by Avery and the textbook, the proofs and theorems by diagonalization, such as time hierarchy, still work after plugging in any oracle function.
That suggests that diagonalization is unuseful to prove P not equal NP, which we will discuss in the next lecture.

### Class 3: Cook-Levin, 3SAT, Classes EXP and NEXP
(Sep 2, 2026)

Deebak presented the Time Hierarchy theorem of Hartmanis and Stearns.
This is a theorem I wish I could have learned when I was a student!

We continued on the class NP with Cook-Levin Theorem, which proved that 3SAT is NP-complete.
3SAT is a useful tool to prove other problems are NP-complete through reductions, partly due to its structural simplicity, e.g., if we want to directly reduce from Circuit Satisfiability to Hamiltonian Path, the reduction would be more complicated.

Next, we looked at the classes EXP and NEXP.
They are the exponential-time counterparts of P and NP, and we have that $$\mathbf{P} \subseteq \mathbf{NP} \subseteq \mathbf{EXP} \subseteq \mathbf{NEXP}$$.
We proved that if $$\mathbf{P} = \mathbf{N}$$ then $$\mathbf{EXP} = \mathbf{NEXP}$$ using a genius technique, called *padding*.
The proof is remarkably elegant, to the point that it almost seems like cheating.

Deebak asked the question:
Do we know an example problem in NEXP?
The answer is "Yes": any problem in P or NP or EXP is certainly in NEXP, so we have many.
A refined question could be:
Do we know an example problem in NEXP but not in EXP?
The answer is "We don't know": had we found one, then EXP is not equal to NEXP, and then P is not equal to NP.@
The next refinement would be:
Do we know an example problem in NEXP but not in NP?
The answer is "Yes": by the Non-deterministic Time Hierarchy.@
Notice that it is unclear how to prove it using the *deterministic* time hierarcy of EXP: we need to find a problem in EXP but not in NP.

Nathaneal asked the question:
If EXP = NEXP, is P = NP?
I thought about it when I read the converse. I guessed it is open.
A brief search showed it open.@
More discussion is welcome.

AI Disclosure:
I used GPT in the above questions and answers marked with "@", and *the fast-mode GPT wronly insisted that PSPACE is a **strict** subset of EXP unconditionally*, but it said open with think deeper.

### Class 2: Gödel, Classes P and NP
(Aug 31, 2026)

We briefly showed Gödel's incompleteness.
The proof is adapted from [Barak's TCS book](https://introtcs.org/public/lec_09_godel.html#g%C3%B6dels-incompleteness-theorem-computational-variant); see also Section 1.5.2 of Arora-Barak, with the comment "the set of true mathematical statements is undecidable."
We continued with the complexity classes P and NP.
Following that, an important concept is the (polynomial-time) reductions between two problems; that will be bread and butter in this course.

[&#x1F4DD; Scribed notes](assets/pdf/cs6160-scribe2-aug31.pdf)

### Class 1: Syllabus, Turing Machines
(Aug 26, 2026)

We went through the [syllabus](syllabus.md).
It coveres the course goals, prerequisites, communication, and coursework.
Notice that WK updated the participation weights to 9% and 6% for presenting and scribing correspondingly.
The syllabus shall be fixed after this week.

For technical materials, we covered Turing Machines, computability, and computation time.
They serve our purposes of agreeing on a formal model of computation, on the math notations, and our communication.

[&#x1F4DD; Scribed notes](assets/pdf/cs6160-scribe1-aug26.pdf)

<!-- 
### Tentative syllabus posted
(Jan 9, 2026)

Please take a look at [the syllabus](syllabus.md) although it could change later.


## List of Updates
1. TOC
{:toc}
 -->