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


### Class 18: TQBF in IP
(Oct 28, 2026)

Wish introduced PCP Theorem, where PCP stands for Probabilistic Checkable Proofs and is conceptually related to IP. 
The PCP theorem states that we have an efficient reduction from any NP problem to the Approximate SAT problem (a promise problem).
As a corollary, Approximate SAT (or MaxSAT) is as hard as solving the standard SAT (as a decision problem).
Notice that the corollary is perhaps unsurprising;
However, the efficient reduction is surprising.

We continued and finished the protocol and the proof of TQBF is in IP, which proved that IP = PSPACE.
An issue raised and resolved in the textbook is the *polynomial degree* of the arithmetized QBF.
We apply linearization operators to "replace" high-degree variables to degree 1.
The resulting linearized polynomial is short in the number of coefficients, so that the prover-to-verifier messages, i.e., the polynomials, are short.
Another issue raised by Nathan and Zhizhen is that the *values* and the polynomial coefficients of the linearization remains double exponential in magnitude.
That is too large: The prover cannot send a polynomial with huge coefficients even the degree is low!

I left the issue with saying that "choosing a random prime of $$\poly(n)$$ bits works with high probability."
Searching with Gemini, I found it in [Shamir's 1992 paper](https://dl.acm.org/doi/pdf/10.1145/146585.146609), quoted below.

> THEOREM 4. Let $$B$$ be a closed QBF of size $$n$$. Then there exists a prime $$p$$ of
> length polynomial in $$n$$ such that $$A \neq O \mod p$$ if $$B$$ is true.
> 
> ...
> 
> This prime can be chosen by the prover P and sent to the verifier V
> (along with a written proof of primality) as the first step of the interactive
> proof, since even an infinitely powerful cheating prover cannot find such a
> prime if $$A = 0$$. 

The point is that there is a good prime $$p$$ that preserves completeness (with probability 1) when the statement is true:
The prover finds $$p$$ that does not divide the value $$K \neq 0$$ in the statement and then sends both $$p$$ and $$K' = K \mod p$$ to the verifier.
The verifier just need to ensure that $$p$$ is indeed prime, which can be efficiently proved (see below if needed), and that $$K' \neq 0$$ and thus $$K \neq 0$$, which does not need the exponentially long string $$K$$.
Shamir claims *perfect* completeness.
Notice that whether $$K$$ is a multiple of $$p$$ matters only when we arithmetize the QBF in the very beginning of the protocol.
All subsequent statements (i.e., the recursive ones) are all already $$\mod p$$ statements and exact equality, not over the integers, not just $$> 0$$.
Hence, for a *true* TQBF statement, in an intermediate round of the protocol, the verifier may ask the prover to prove that $$g'(a_1,a_2,a_3) = 0 \mod p$$ for some $$g'$$ and some random $$a_1,a_2,a_3 \in GF(p)$$, which still achieves perfect completeness.

To prove $$p$$ is indeed prime, there are many ways.
We can use the result that PRIMES is a problem in NP, which is nontrivial and requires some algebra.
Alternatively, it is straightforward to see that PRIMES is in coNP because COMPOSITES is in NP.
Then, we can reduce PRIMES to $$\mathit{\#SAT_D}$$ because TAUTOLOGY and thus $$\mathit{\#SAT_D}$$ is coNP-hard.
That gives an interactive proof of PRIMES.


### Class 17: \#SATD in IP
(Oct 26, 2026)

Zhizhen introduced the class AM (for Arthur-Merlin), which is a subset of IP but restricts the verifier-to-prover messages to public random coins.
Zhizhen also showed an AM protocol for the GNI problem, which needs a subprotocol to prove set sizes, which we will cover later.

We briefly argued that $$\mathbf{BPL} \subseteq \mathbf{P}$$.
I would like to stress that, a PTM $$M$$ that solves a problem in BPL may not halt in polynomial time, and we must construct another (deterministic) TM $$M'$$ to solve the problem.
$$M'$$ computes on the configuration graph of $$M$$ in a way similar to some Markov decision process.

We then finished the sumcheck proof for $$\mathit{\#SAT_D}$$.
Wish asked a good question:
The verifier may ask the prover to prove $$\sum_{b_2, \dots, b_n \in \bit} g(a, b_2, \dots, b_n) = s(a)$$ for many distinct random $$a$$.
Would that catch all cheating provers?
The result is yes, but the recursion grow exponentially in $$n$$, too much.
Shiyu asked another good question:
Can we have the verifier send all the random challenges $$a \gets GF(p)$$ in one round instead of recursing interactively (so that the number of rounds is reduced to two)?
The answer is no, when $$a$$ is known in advance, the prover can easily find $$s$$ such that satisfies the sumcheck and at the same time makes the recursive statement of $$s(a)$$ true.

### Class 16: Arithmetization and \#SATD
(Oct 21, 2026)

We finished Quiz 1 today.
It is good to see our progress :)

We continued with the class IP.
Recall that we proved that IP is in PSPACE last time.
Given that, although IP is defined without any computable prover, for any language in IP, we know that the language can be decided by a prover instantiated by a TM in PSPACE.
That probably makes IP easier to think about.

We next aim to prove that PSPACE is in IP, a surprising result by Shamir. 
We began with the warmup problem $$\mathit{\#SAT_D}$$, which states that a 3-CNF $$\phi$$ has exactly $$K$$ satisfying assignments.
Notice that $$\mathit{\#SAT_D}$$ is a decision problem and a generalization of the TAUTOLOGY problem.
We showed the arithmetization of boolean formulas and then a *sumcheck* protocol for polynomials.
It is cool as the arithmetization is a one-to-one mapping between boolean formulas and polynomials, but then we evaluate polynomials on non-binary values.

We will finish the theorem next week. 


### Class 15: Interactive Proofs, Graph Non-Isomorphism
(Oct 19, 2026)

We commented on the BPP-completeness and BPTIME hierarchy and wrapped up the chapter.

The next new chapter is on the languages that can be proved by *Interactive Proofs*.
Recall that by Gödel's incompleteness, we can only prove a restricted set of statement, i.e., classes of languages.
Still, the class can be a large set.

We defined the class of *deterministic* interactive proofs, $$\mathbf{dIP}$$, that are efficiently verifiable (deterministically).
Unsurprisingly, $$\mathbf{dIP} = \mathbf{NP}$$.
That says interaction does not help proving statements.
That is different from our human experiences in learning math proofs!
Let's still be interactive---as the following $$\mathbf{IP}$$ class suggests, interaction is powerful.

Relaxing the verifier to be a probabilistic Turing Machine, we defined the class $$\mathbf{IP}$$.
Also, notice that throughout the chapter of interactive proofs, we consider the prover to be any function, which can even be incomputable, e.g., solve a halting problem.
We illustrated the example of Graph Non-Isomorphism problem (GNI), and we proved that GNI is in IP.
Because GNI is unlikely in NP, IP is probably a strict superset of NP.

We proved that $$\mathbf{IP} \subseteq \mathbf{PSPACE}$$ by showing $$\mathbf{IP} \subseteq \mathbf{NPSPACE}$$ and then applying Savitch's Theorem.
Another [proof by Gemini is copied here](99-IP-PSPACE.md), which gives a deterministic PSPACE algorithm that is longer in description.
This is the first step toward proving $$\mathbf{IP} = \mathbf{PSPACE}$$.
We will prove the second direction later.



### Class 14: Sipser–Gács–Lautemann Theorem, RL, BPL
(Oct 14, 2026)

Andrew introduced promise problems and their corresponding complexity classes.

We proved Sipser–Gács–Lautemann Theorem, using a probabilistic method.
In general, probabilistic methods proves the existence of a combinatorial object that satisfies some properties.
It is extremely useful, and as in this proof, the probability boils down to counting, but the probability is much more comprehensible than counting.
The existential property gives the existential quantifier needed in the class $$\mathbf{\Sigma_2^p}$$.

Jinye asked that if we can find the strings $$u_1,\dots,u_k$$ in $$\exists u_1,\dots,u_k \forall r, \bigvee_i (M(x; u_i \oplus r) = 1)$$.
Notice that such strings may depend on $$x$$.
If we could find them in polynomial time, then we could prove $$\mathbf{BPP} \subseteq \mathbf{coNP}$$, which is an open question.
Deebak asked if we can find low Hamming weight $$u_1,\dots,u_k$$.
I think it is possible but need calculation, and it is an interesting question.
If we could reduce the number of randomness to a small number, e.g., logarithmic, then derandomization could be easier.

We introduced randomized logarithmic-space problems and their classes RL and BPL.
It is interesting to see that undirected connectivity $$\mathit{UPATH} \in \mathbf{RL}$$.



### Class 13: BPP vs Other Classes
(Oct 12, 2026)

Deebak talked about UniqueSAT.

We talked the conjecture that BPP is not more powerful than P.
That is, given randomness, we probably still do not solve more problems in polynomial time.
Notice that some problems, such as Polynomial Identity Test, can be in P, but we just haven't yet found the efficient and deterministic algorithm.

Adleman's Theorem states that $$\mathbf{BPP} \subseteq \mathbf{P/poly}$$.
Its proof is a simple amplification of probability and then a counting argument.
An unlikely hypothesis could be that $$\mathit{SAT}\in\mathbf{BPP}$$.
If the hypothsis is true, by Adleman's Theorem and then by Karp-Lipton Theorem, the polynomial hierarchy collapses to $$\mathbf{\Sigma_2}$$.
If we do not believe in the collapse, then we cannot solve SAT in BPP.
Similarly, Sipser–Gács–Lautemann Theorem states that $$\mathbf{BPP} \subseteq \mathbf{\Sigma_2 \cap \Pi_2}$$.


### Class 12: Probabilistic Turing Machines, BPP, RP, ZPP
(Oct 7, 2026)

We introduced Probabilistic Turing Machines (PTM), which are TMs that use an unbiased random bit at each step.
Then, we showed the Polynomial Identity Test (PIT) problem, which is an example that can be solved efficiently with a randomized algorithm, or PTM.
We do not (yet) know a deterministic algorithm that solves PIT in polynomial time.
Thus, it seems that PIT and other similar problems are showing that randomness is a powerful resource and speeds up algorithms.
However, we stress that there is no proof.
Also, many people in the area believe that randomness *does not* give extra power to algorithms.
That is, we might be able to prove that for an entire class $$S$$ of problems that are efficiently solveable using PTMs, we can solve all problems in $$S$$ efficiently using deterministic TMs.
This is called *derandomization* and will be discussed later in this course. 

As raised by many students in this class, we need to define when or what's called a PTM *solves* a problem.
The first and perhaps more intuitive definition is $$\mathsf{BPTIME}$$ and $$\mathsf{BPP}$$.
It requires that the PTM outpus the same as the language w.p. $$\ge 2/3$$, for all positive and negative instances.
The probability is over the choices of the random coins.
The second is one-sided, called $$\mathsf{RTIME}$$ and $$\mathsf{RP}$$, which are similar to $$\mathsf{BPP}$$ but additionally require that all negative instances are correct w.p. 1.
All above requires the PTM to halt in a specific time $$T(n)$$ in (all) worst cases.
The third, called $$\mathsf{ZTIME}$$ and $$\mathsf{ZPP}$$, only requires the PTM to halt in time $$T(n)$$ *in expectation*, but the answer must be correct w.p. 1 when halting for all instances.
Notice that in this class, my slides and writing sometimes wrongly said ZP, which should be ZPP.

[&#x1F4DD; Scribed notes](assets/pdf/cs6160-scribe12-oct7.pdf)



### Older Updates and Notes

* [1. Time, Space, Alternation, Circuits](1-timespace.md)


<!-- 
### Tentative syllabus posted
(Jan 9, 2026)

Please take a look at [the syllabus](syllabus.md) although it could change later.
 -->


## List of Updates
1. TOC
{:toc}
