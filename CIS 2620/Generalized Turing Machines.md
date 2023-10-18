## Two-Tape Turing Machines

In a two-tape TM, there are two tapes, both potentially unbounded on the right side. There are two read/write heads that can move independently. A single transition depends on the current state and the contents of the two tapes, then updates the state and updates/moves both tapes.

>**Example.** Create a two-tape TM to check if a string is a palindrome.
>
>In our single-tape solution, we had to go back and forth for each symbol, leading to around $n^2$ complexity. Here we can get the complexity to be linear by copying the first tape to the second, then having one head at the front and one at the back.

>[!definition]
>A 2-tape TM $M$ has
>- States $Q$
>- Initial state $q_0$
>- Accepting state $q_a$
>- Rejecting state $q_r$
>- Tape alphabet $\Gamma$
>- Input alphabet $\Sigma$
>- Blank symbol $\_$
>- Transition function $\delta:Q\times\Gamma\times\Gamma\rightarrow Q\times\Gamma\times\{\text{L, R}\}\times\Gamma\times\{\text{L, R}\}$
>The rules for accepting/rejecting are the same as a single-tape TM.

### Two-Tape to Single-Tape

**Goal:** Systematically convert a 2-tape TM $M$ into a single-tape TM $M'$ such that on every input $w$, $M$ accepts, rejects, or goes in infinite loop exactly when $M'$ accepts, rejects, or goes in infinite loop, respectively.

Note by this goal that $M$ is halting iff $M'$ is halting, and $L(M)=L(M')$.

Intuitively, we want to combine our two tapes into a single tape. We can mark the beginning of a new "tape" with $\#$, and put an $\mathrm x$ before the cell that each head was at.

The state of $M'$ contains the state of $M$ and the contents of the two current cells.

E.g.,
![](Pasted%20image%2020231017122313.png)
becomes
![](Pasted%20image%2020231017122356.png)

This means initially, the input $w$ is `# x w # x`.

Transitions are as follows: The state transition is the same in both $M$ and $M'$. Then to simulate the heads, we must scan through the entire tape and move the $\mathrm x$'s either left or right. Finally, the true "head" goes back to the initial position on the far left side of the tape.

In the case that one of the tapes of $M$ is expanded, $M'$ may have to shift everything over by one.

>[!note]
>We can expand this to any number of tapes.

## Two-Way Infinite Tape

In a two-way infinite TM, the tape can extend on both sides an unbounded amount. Since there is no left-most end, the head points to the first symbol of the input initially.

## Nondeterministic Turing Machines (NTM)

NTMs are similar in concept with [NFAs](Nondeterministic%20Finite%20Automata.md), but with some crucial differences.

For NTMs, we must define a new transition function $\Delta:Q\times\Gamma\rightarrow 2^{Q\times\Gamma\times\{\text{L, R}\}}$

To simplify, let's assume $\Delta(q, \gamma)$ always contains 2 choices. We can then specify them as
$$\begin{gather}
\delta_0:Q\times\Gamma\rightarrow Q\times\gamma\times\{\text{L, R}\}\\
\delta_1:Q\times\Gamma\rightarrow Q\times\gamma\times\{\text{L, R}\}
\end{gather}$$

On an input $w$, an NTM $N$ initializes with the configuration $(\varepsilon, q_0, w)$. Like with NFAs, $w$ is accepted if some execution is accepting, and rejected if all executions are finite and rejecting.

The problem with just exploring all possibilities (branches of the execution tree) is that TMs can be non-terminating, so we might get stuck in one branch and never find the accepting branch.

The solution is that we should try all execution paths in a breadth-first manner. 

Note the key difference with NFAs: the tape and head are changing between executions, so we can't just store a set of all possible states.

### NTM to 3-Tape TM

We can turn our nondeterministic NTM into a deterministic 3-tape TM, with
- Tape 1: The original input w (never updated)  
- Tape 2: Used as a work tape to simulate M’ (initially all blanks)
- Tape 3: Binary counter encoding execution path (initially 0)

That is, we copy the input on tape 1 to tape 2 for each execution and run it, then track what executions we're on with tape 3. Specifically on tape 3, a 0 indicates to use $\delta_0$ while a 1 indicates to use $\delta_1$. 

To track accepting or rejecting states, we have the state of $M'$ contain a bit $b$ with values in $\{0, 1\}$, initialized at $1$.

$$\begin{align}
\hline
&\text{Tape 1} \leftarrow w \\
&\text{Tape 2} \leftarrow \varepsilon\\
&\text{Tape 3}\leftarrow 0 \\
&\text{\bf repeat}: \\
&\quad\text{Copy Tape 1 to Tape 2} \\
&\quad\text{Set state of $M$ to $q_0$ and Head 2 to left-most cell of Tape 2} \\
&\quad\text{{\bf while} Tape 3 reads 0 or 1:} \\
&\quad\text{\quad {\bf using} $\delta_0$ if Tape 3 reads 0 and $\delta_1$ if it reads 1:} \\
&\quad\text{\quad\quad Update state of $M$, current cell of Tape 2, and move Head 2} \\
&\quad\text{\quad Move Head 3 one to the right} \\
&\quad\text{} \\
&\quad\text{// Decide whether to accept or reject} \\
&\quad\text{{\bf if} state of } M=q_a \textbf{ then:} \\
&\quad\quad\text{Accept} \\
&\quad\text{{\bf else if} state of } M\neq q_r \textbf{ then:} \\
&\quad\quad b\leftarrow 0 \\
&\quad\text{{\bf else}:} \\
&\quad\quad\text{{\bf if} Tape 3 contains only 1s and $b=1$ {\bf then}} \\
&\quad\quad\quad\text{Stop and reject} \\
&\quad\quad\textbf{else} \\
&\quad\quad\quad b\leftarrow 1 \\
\\
&\quad\text{Add 1 to Tape 3, treating it as a binary number}\\
&\quad\text{Tape 2}\leftarrow\varepsilon
\\\hline
\end{align}$$

Again, the NTM doesn't change decidability, but it causes an "exponential" slow-down. This is the central problem of P vs. NP.