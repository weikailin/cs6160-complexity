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

[(List of announcements)](#list-of-updates)


### Class 9: Alternating Turing Machine, Fortnow's Theorem
(Sep 23, 2026)

Avery talked about the non-uniform class P/poly and presented Karp-Lipton Theorem.
Karp-Lipton shows that if $$\mathbf{NP} \subseteq \mathbf{P}/poly$$, then the polynomial hierarchy collapses to $$\Sigma_2^p$$.
Notice that in the proof, we replaced a quantified boolean formula by a boolean circuit (without quantification), which is in general a step we have when proving the polynomial hierarchy collapses.

We introduced alternating Turing machines and their execution.
It is probably easier to see the classes using the "witness" definition, but it is also a good practice to define the machines directly.
With that, we proved Fortnow's Theorem.
It is an unconditional impossibility and says that SAT cannot be solved when restricting to $$O(n^{1.1})$$ time and $$O(n^{0.1})$$ space.
Notice that if we restrict only time or only space, the problem remains open.
Fortnow's Theorem is surprisingly proved (by a sequence of reductions) through $$\Sigma_2\mathbf{TIME}$$, showing an application of alternating TM.
See also [this note from Sudan's course](https://people.seas.harvard.edu/~madhusudan/MIT/ST07/scribe/lect08.pdf).

### Class 8: Williams' Theorem, Tree Evaluation Problem
(Sep 21, 2026)

Nathan presented polynomial hierarchy.
They are natural extensions of P, NP, and coNP.
A natural problem to remember is ExactIndepSet, which gives $$(G, k)$$ and asks whether largest independent set on the graph $$G$$ is exactly $$k$$ vertices.
While we do not know if ExactIndepSet is in NP or coNP, ExactIndepSet is in the next class of polynomial hierarchy.
The polynomial hierarchy is also a natural restriction of QBF.

We then stated and proved Williams' Theorem.
That is, any problem solvable in time $$T(n)$$ can be solved in space $$O(\sqrt{T \log T})$$.
Our proof is the simpler but weaker version, which proved space  $$O(\sqrt{T} (\log T)^{3/2})$$.
We also briefly mentioned the key idea of Cook-Mertz tree-evaluation algorithm.
The technique of Cook-Mertz uses a storage that is filled with some other data, but the other data is modified and recovered in the end of the subroutine.
"Using data-occupied" space while recover the data in the end of computation is developed recently and termed "catalytic" algorithms, as catalysts in chemical reactions.

The entire proof of Williams, including Cook-Mertz, is based on elementary algebra and Turing machines.
It is highly recommended to read.


### Class 7: Savitch's Theorem, Complement Classes, NL = coNL
(Sep 16, 2026)

We reviewed PSPACE-completeness by comparing the QBF problem with two-player games.
We also remarked that the proof of QBF to be PSPACE-complete generalizes in Savitch's Theorem, which states that $$\mathbf{NSPACE}(S(n)) = \mathbf{SPACE}(S(n)^2)$$.

We then introduced the complement of a complexity class.
That gives many classes we do not know how to compare: while coP = P, we do not know if coNP equals NP.
Namely, for many problems in coNP, it is unclear how to prove them in NP because we do not know the NP witness.
More generally, DTIME(T(n)) = coDTIME(T(n)), but NTIME(T(n)) vs coNTIME(T(n)) is unclear.
Similarly, we have SPACE(S(n)) = coSPACE(S(n)).
However, surprisingly, NSPACE(S(n)) = coNSPACE(S(n)).
This is proved through $$NotPATH \in \mathbf{NL}$$ using a carefully designed witness/certificate, where NotPATH(G, s, t) is the decision problem that outputs 'Yes' if there is no s-t path in the graph G.


### Class 6: Quantified Boolean Formula is PSPACE-Complete
(Sep 14, 2026)

Andrew talked about the Tree Evaluation Problem of S. Cook et al. (ACM Trans. Comput. Theory, 2012).
It is the essential tool in the work of Williams (STOC, 2025).
Williams proved that any problem solveable by a multi-tape Turing machine in time $$T(n)$$ can also be solved in space $$\sqrt{T(n) \log T(n)}$$, a huge success in complexity and algorithms!
See the beautiful paper and video recordings of Williams:
- Paper: https://arxiv.org/pdf/2502.17779
- Video at IAS: https://youtu.be/1qwDO5ulUFs
- Video at TCS+: https://youtu.be/tM9ekW6FAS8

We defined Quantified Boolean Formula (QBF) and showed that it is PSPACE-complete to decide whether a QBF is true.
As for NP-completeness, the more challenging step is to reduce from any PSPACE problem to a QBF in polynomial time.
Notice that the reduction efficiently uses time by alternating the exist and for-all quantifiers.
This is consistent with the special cases: had the reduction used only the exist quantifier, the result would be SAT, which is intuitively easier than PSPACE.

(&#x1F4DD; no scribed notes.)

### Class 5: Limits of Diagonalization, SPACE and NSPACE, PSPACE
(Sep 9, 2026)

Zhizhen talked about SPACE and NSPACE classes and their relation to DTIME classes.
An important observation is that when space is bounded, the number of Turing-Machine configurations is bounded, and that imply many results.
Namely, we have $$\mathbf{NSPACE}(s(n)) \subseteq \mathbf{DTIME}(2^{O(s)})$$.

We finished P vs NP with the limitation of diagonalization, which is roughly equivalent to proofs that uses TMs in a black-box way.
We argued that there is no black-box proof showing P not equal to NP, but we still do not know to non-black-box prove it.
Next, we continued with clarifying the definition of NSPACE, and we discussed how to define a configuration so that it is easier to solve $$\mathbf{NSPACE}(s(n))$$ using $$\mathbf{DTIME}(2^{O(s)})$$.
We ended with defining PSPACE and PSPACE-completeness.

[&#x1F4DD; Scribed notes](assets/pdf/cs6160-scribe5-sep9.pdf)


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

[&#x1F4DD; Scribed notes](assets/pdf/cs6160-scribe4-sep7.pdf)

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
A brief search showed it open.
More discussion is welcome.

AI Disclosure:
I used GPT in the above questions and answers marked with "@", and *the fast-mode GPT wronly insisted that PSPACE is a **strict** subset of EXP unconditionally*, but it said open with think deeper.

[&#x1F4DD; Scribed notes](assets/pdf/cs6160-scribe3-sep2.pdf)


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
 -->


## List of Updates
1. TOC
{:toc}
