
**Problem:** Given a problem $A$, decide if it is (1) decidable, (2) recognizable but undecidable, or (3) unrecognizable.

**Upper bound techniques:**
- To show $A$ is decidable, find a halting TM/program for it
- To show $A$ is recognizable, find a TM/program that accepts it

How to show A is undecidable or unrecognizable:
- Use of closure properties
- Technique of problem reduction

## Combining Two Recognizers

>[!theorem]
>If a language $A$ and its complement $A^\complement$ are both recognizable, then both must be decidable.

Suppose $A$ and $A^\complement$ to be recognizable. Then there is a TM $M$ for $A$ and another TM $M'$ for $A^\complement$. 

To get a halting TM for $A$, we can run $M$ and $M'$ in parallel. Specifically, first copy the input string to both tapes, then repeat the following:
1. Execute one transition of $M$ on Tape 1;
 2. If $M$ stops and accepts, stop and accept;
 3. Execute one transition of $M’$ on Tape 2;
 4. If $M’$ stops and accepts, stop and reject


