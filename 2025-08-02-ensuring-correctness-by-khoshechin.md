# Study Notes — *Ensuring Correctness in Distributed Systems*
**Seminar:** Mohammad Hossein Khoshechin (MPI-SWS) — 2 Aug 2025  
**Author:** Sara Mohammadi Mohammadi — personal study notes 

---

## Summary (abstract)
This seminar explains the classic practical problems in concurrent/distributed systems with details of how the mathematical tools reason about them.
Including refined descriptions for each of the *Formal Methods* : transition systems, temporal logics (LTL), automata, and model checking. 
My notes are focused on the first half of the seminar, and i will update it soon after gaining deeper perspective on the rest.
---

## 1. Concurrent vs Distributed programs 
- **Concurrent program**: multiple threads/processes on the same machine that may share memory.  
  **Challenge:** nondeterministic interleavings (a bug might happen in a specific rare interleaving) ⇒ race conditions, deadlocks, starvation (when a processer is continuously behind a resource and never gets to proceed)
- **Distributed program**: independent processes on different machines that talk via messages over network.  
  **Challenge:** no shared memory; must handle message delays, partitions, and partial failures.

**Classic examples**
- *Producer–Consumer* (bounded buffer, semaphores) — shows why synchronization (locks/semaphores) is needed.
- *Chain replication* — replicas are chained; updates go to the head and flow to the tail; reads go to the tail for strong consistency.
  Replicas are linearly chained. Head and Tail replicas are in contact with clients. Update req is sent to the head 
REQ UPDATE from the client => head replica: updates locally and forwards => next replica in chain:... => … => tail replica: updates locally and reports back an ACK <= … <= head receives ACK <= REP ACK to the client
(ensures durability)
REQ READ => always sent to the tail (ensures consistency) : REP QUERY back to the client

---

## 2. Formal methods 
- **Formal specification**: write the system in a precise mathematical language (no ambiguity).
- **Formal verification**: prove the implementation satisfies the spec.
  - **Deductive verification**: write proofs/invariants (Coq, Isabelle/HOL, etc.).
  - **Model checking**: exhaustively analyze state space; produces counterexamples (SPIN, NuSMV, TLA+, IVY, …).

**Refinement & synthesis**  
  Powerful techniques to bridge between high-level design and low-level implementation:
	Refinement: start with a high-level simplified math model and conquer it step by step to reach an executable program


---

## 3. Transition systems 
- Label states with atomic propositions; traces = sequences of labels (observable behavior).
- `Post(s)` / `Pre(s)` — direct successors / predecessors.
- Reachability (terminal states have an empty Post)
- Trace(P)={trace(p) | p \in P} => like context-free grammar
---

## 4. Concurrency by interleaving
Compose two transition systems by interleaving their transitions and show by pairs.

**Guarded Command Language (GCL)** — Dijkstra’s style: great for modeling nondeterministic programs; semantics given as a small-step transition relation over configurations `<command, state>`.

**Example algorithm:** Peterson’s mutual exclusion as two concurrent GCL processes; model as `TS(P1) ∥ TS(P2)`.
<img width="838" height="502" alt="image" src="https://github.com/user-attachments/assets/d57bb722-5872-4a23-97af-9dba1846ed64" />


---

## 5. Linear Temporal Logic (LTL) — specify behaviors over time
- Syntax: propositions `a`, boolean ops, and temporal ops `⃝` (next), `U` (until).  
- Common derived ops: `♢φ` (eventually φ), `□φ` (always φ).
- Used to express safety (nothing bad ever happens) and liveness (something good eventually happens).

**Model checking with LTL:** reduce an LTL formula to a Büchi automaton and check the product of the system and the automaton for emptiness (no violating run).

---

## 6. Automata-theoretic model checking (high level)
1. Translate `¬φ` to a Büchi automaton `A¬φ`.  
2. Build system automaton `ATS` (captures traces).  
3. Product `ATS × A¬φ` accepts precisely traces violating `φ`.  
4. Check emptiness (SCC / nested DFS). If nonempty → counterexample.

Complexity: exponential in formula size (but many practical heuristics exist).

---

## 7. Practical verification techniques
- **Concrete enumerative**: bread-and-butter BFS/DFS of reachable states until you find a bad state.
- **Backward reachability**: compute predecessors from bad states (`Pre*`) and intersect with initial states.
- **Symbolic model checking**: encode sets of states and transitions as logical formulas (BDDs or SAT); use SAT solvers for bounded model checking (BMC).
- **Monitors**: turn temporal properties into state invariants by composing the system with a monitor automaton (reduces liveness to safety in some frameworks).

---

## 8. The state-explosion problem & remedies
- State space grows exponentially with variables and number of components.
- Strategies: symbolic representations, abstraction/refinement, partial-order reductions, compositional reasoning, and heuristics (IC3/PDR, BMC).

---

## References & further reading
- Seminar slides — M.H. Khoshechin, MPI-SWS (Aug 2, 2025).  
- Tools: Coq, Isabelle/HOL, SPIN, NuSMV, TLA+, IVY, PRISM 
