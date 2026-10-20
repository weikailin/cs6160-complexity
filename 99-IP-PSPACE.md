---
layout: page
title: IP in PSPACE
nav_order: 999
nav_exclude: true
---


To prove that $$\text{IP} \subseteq \text{PSPACE}$$, we show that for any language $$L \in \text{IP}$$, a deterministic Turing machine can calculate the exact optimal probability of acceptance for an input $$x$$ using polynomial space.

---

### 1. Formal Setup

Let $$L \in \text{IP}$$. By definition, there exists a probabilistic polynomial-time verifier $$V$$ such that:

- **Completeness:** $$x \in L \implies \exists P, \Pr[\langle V, P \rangle(x) = 1] \ge \frac{2}{3}$$

- **Soundness:** $$x \notin L \implies \forall P^*, \Pr[\langle V, P^* \rangle(x) = 1] \le \frac{1}{3}$$


For an input $$x$$ of length $$n = \vert{}x\vert{}$$:

- The interaction consists of at most $$k(n) = \text{poly}(n)$$ rounds.

- The length of every message sent by $$V$$ or $$P$$ is bounded by $$m(n) = \text{poly}(n)$$.

- $$V$$ uses at most $$r(n) = \text{poly}(n)$$ random bits throughout the interaction.


---

### 2. Interaction as a Game Tree

The interaction protocol between $$V$$ and an optimal prover $$P^*$$ can be modeled as an expectimax game tree of depth $$2k(n)$$:

1. **Leaf Nodes (Depth $$2k(n)$$):** A complete interaction transcript $$\tau = (m_1, m_2, \dots, m_{2k})$$ together with a random string $$r \in \{0,1\}^{r(n)}$$ used by $$V$$. The leaf evaluates to $$1$$ if $$V(x, r, \tau)$$ accepts, and $$0$$ otherwise.

2. **Prover Nodes (Odd Depth):** The prover chooses a message $$m_{2j+1} \in \{0,1\}^{\le m(n)}$$ to **maximize** the probability of acceptance.
3. **Verifier Nodes (Even Depth):** The verifier chooses a random message $$m_{2j}$$ according to its internal random coins $$r$$, effectively taking the **average** (expectation) over all possible outcomes.

---

### 3. Recursive Computation of Acceptance Probability

We define a function $$W(\tau)$$ that computes the maximum probability that $$V$$ accepts $$x$$ given a partial transcript $$\tau$$:

#### **Base Case (Complete Transcript):**

For a complete transcript $$\tau = (m_1, \dots, m_{2k})$$, $$W(\tau)$$ is the fraction of verifier random strings $$r \in \{0,1\}^{r(n)}$$ consistent with $$\tau$$ for which $$V$$ accepts:


$$W(\tau) = \frac{\left\vert{} \left\{ r \in \{0,1\}^{r(n)} \;\middle\vert{}\; V(x, r, \tau) = 1 \text{ and } r \text{ is consistent with } \tau \right\} \right\vert{}}{\left\vert{} \left\{ r \in \{0,1\}^{r(n)} \;\middle\vert{}\; r \text{ is consistent with } \tau \right\} \right\vert{}}$$

#### **Prover's Turn (Transcript length is even):**

The prover chooses the message $$m \in \{0,1\}^{\le m(n)}$$ that maximizes $$W$$:


$$W(\tau) = \max_{m \in \{0,1\}^{\le m(n)}} W(\tau \circ m)$$

#### **Verifier's Turn (Transcript length is odd):**

The verifier generates message $$m$$ probabilistically based on uniform choice over applicable random coins:


$$W(\tau) = \sum_{m \in \{0,1\}^{\le m(n)}} \Pr[V \text{ outputs } m \mid \tau] \cdot W(\tau \circ m)$$

---

### 4. Space Complexity Analysis

A deterministic Turing machine $$M$$ can evaluate $$W(\emptyset)$$ (the optimal acceptance probability for input $$x$$) by performing a **Depth-First Search (DFS)** on the interaction tree:

1. **Stack Depth:** The maximum depth of the recursion stack is equal to the number of rounds, $$2k(n) = O(\text{poly}(n))$$.

2. **Stack Frame Size:** At each level $$j$$ of the recursion stack, $$M$$ needs to store:
- The current partial transcript $$\tau$$ ($$\le 2k(n) \cdot m(n) = O(\text{poly}(n))$$ bits).

- The current message candidate $$m$$ being iterated over ($$O(\text{poly}(n))$$ bits).

- A running maximum or running weighted sum ($$O(\text{poly}(n))$$ bits, since all probabilities are exact rationals with denominators bounded by $$2^{r(n)}$$).



3. **Total Space:**

$$\text{Space}(n) = \text{Depth} \times \text{Frame Size} = O(\text{poly}(n)) \times O(\text{poly}(n)) = O(\text{poly}(n))$$



---

### 5. Decision Algorithm

1. $$M$$ runs the depth-first evaluation algorithm to compute $$W(\emptyset)$$ in $$O(\text{poly}(n))$$ space.

2. If $$W(\emptyset) \ge \frac{1}{2}$$, $$M$$ accepts $$x$$; otherwise, $$M$$ rejects $$x$$.

Since $$M$$ decides $$L$$ using a polynomial amount of space, $$L \in \text{PSPACE}$$.

$$\therefore \mathbf{\text{IP} \subseteq \text{PSPACE}}$$

