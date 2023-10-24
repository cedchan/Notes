## Acceptance Problem

**Problem:** Given a DFA $M$ and an input string $w$, does $M$ accept $w$?

First we need a way to encode a DFA $M$ as a string. Let $<M, w>$ be an input pair, where $<M>$ is the string encoding of $M$ and the same applies for $w$.

We can now define out language as follows:
$