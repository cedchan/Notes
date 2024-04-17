>[!definition]
>A **language** is a set of **strings**, which are finite sequences of minimal units (words, morphemes, phonemes), with meaning.
>
>A **grammar** of a language provides the resources and methods for creating all and only the strings that are part of it.
>
>**Natural languages** are the sets of strings that native speakers deem to be part of the language.

Each part of a grammar is considered to be a discrete combinatorial system, meaning that it has well-defined discrete parts that can be combined in a rule-driven way. Grammars thus comprise a **lexicon**, the basic units, and a **syntax**, the rules.

## Lexicon

Lexicons are in their most common form like dictionaries: lists of words with meanings. But the complexity of words warrants a more detailed information system, so lexicons will contain smaller units of meaning too.

The definition of a word is a much-debated topic without consensus across linguistics, but we know that uses criteria like "spaces" isn't sufficient. A better criterion may be units that can stand freely.

>[!definition]
>**Morphemes** are the minimal units of a language with both sound and meaning.

## Right Linear Grammars

>[!definition]
>A **right linear grammar (RLG)** is a 4-tuple $\langle T,N,S,R\rangle$ where:
>- $T$ is a set of terminal symbols, including the empty string
>- $N$ is a finite set of non-terminal symbols
>- $S$ is the start symbol
>- $R$ is a set of rewrite rules of the form $A\to xB$ or $A\to x$ where $A,B\in N$ and $x\in T$.

By rewrite rules, we mean the rule allows us to replace the non-terminal symbol to the left with what comes to the right.

>**Example.**
>$G_1=\langle T,N,S,R\rangle$, with
>- $T=\{a,b\}$
>- $N=\{S,A,B\}$
>- $S$ is the start symbol
>- $R=\begin{Bmatrix}S&\to&aA\\A&\to&aA\\A&\to&bB\\B&\to&bB\\B&\to&b\end{Bmatrix}$
>
>This would accept the string $\text{aaabb}$, for example, using the path$$S\to aA\to aA\to aA\to bB\to b$$
>We can also represent strings as trees:
>![](截屏2024-03-26%20上午10.33.09.png)

>[!theorem]
>RLGs are equally expressive as regular languages.

**Proof.** We show that a language can be captured by an RLG iff it is a regular language.

($\implies$) RLG to FSA

Given $G=\langle T,N,S,R\rangle$ we can construct the equivalent FSA $D=\langle Q, \Sigma,\Delta,s,F\rangle$ with
- $Q=N\cup\{F'\}$ where $F'$ is a final state
- $\Sigma=T$
- $s=S$
- $F=\{F'\}$
- $\Delta(A,x)=\{B\mid \exists A\to xB\in R\}$
- Additionally, $F'\in\Delta(A,x)$ if $A\to x\in R$.

($\impliedby$) FSA to RLG

Given $D=\{Q,\Sigma,\delta,s,F\}$, we can construct the equivalent RLG $G=\langle T,N,S,R\rangle$ with
- $T=\Sigma$
- $N=Q$
- $S=s$
- $R_1=\{q_i\to xq_j\mid \delta(q_i,x)=q_j\}$
- $R_2=\{q_i\to x\mid \delta(q_i,x)=q_j\land q_j\in F\}$
- $R=R_1\cup R_2$
- Additionally, $S\to\varepsilon\in R$ if $s\in F$

## Context Free Grammars

RLGs are limited to rules of the form $A\to xB$ and $A\to x$, which restricts their expressivity. CFGs are a generalization of RLGs that allow for more rules.

>[!definition]
>A **context free grammar (CFG)** is a 4-tuple $C=\langle T,N,S,R\rangle$ where
>- $T$ is the set of terminal symbols
>- $N$ is the set of non-terminal symbols
>- $S$ is the start symbol
>- $R$ is a set of rewrite rules of the form $A\to\Phi$ where $\Phi$ is any sequence of terminals and non-terminals.

If $u,v,w$ are strings of terminals and non-terminals, and we have a rewrite rule $A\to w$, we say $uAv$ **yields** $uwv$. Formally,
$$uAv\Rightarrow uwv$$

If we have a sequence of strings $u_1, u_2,\dots,u_n, n\ge0$ such that $u_1\Rightarrow u_2\Rightarrow\dots\Rightarrow u_n\Rightarrow v$, we write
$$u\Rightarrow {}^*v$$

The language of a CFG is $\{w\in\Sigma^*\mid S\Rightarrow {}^*w\}$

CFGs are more expressive than RLGs and regular languages. For example, we can model $\{a^nb^n\}_{n\ge0}$, which we know is not regular, with the CFG $C=\langle T,N,S,R\rangle$,
- $T=\{a,b\}$
- $N=\{S,A\}$
- $S$ is the start symbol, and
- $R=\begin{Bmatrix}S&\to&\varepsilon\\S&\to&aAb\\A&\to&aAb\\A&\to&\varepsilon\end{Bmatrix}$.

As a visualization, see this tree:


![](截屏2024-03-26%20上午11.00.46.png)
### Pushdown Automata Model

Although vanilla FSAs can't model all CFLs, adding a simple form of memory makes them equally expressive.

>[!definition]
>A **pushdown automata (PDA)** is an FSA with an additional **pushdown stack**. 
>
>Transitions are of the form $a,b\to c$, meaning read $a$, pop $b$ from the pushdown stack, and push $c$ to the top of the stack. The special symbol $\$$ represents the bottom of the stack (so pushing $\$$ effectively resets the stack).

## Semantics
### First-Order Logic and Language

Some of the basic building blocks of formal language come by combining statements using logical operators like $\land$, $\lor$, $\lnot$, $\implies$, and $\iff$. 

>[!definition]
>For any sentences $A$ and $B$,
>1. $\lbr A\textbf{ and }B\rbr_s=\lbr A\rbr_s\land \lbr B\rbr_s$
>2. $\lbr A\textbf{ or }B\rbr_s=\lbr A\rbr_s\lor\lbr B\rbr_s$
>3. $\lbr\textbf{It-is-not-the-case-that }A\rbr_s=\lnot\lbr A\rbr_s$

## Extensions

Extensions are sets of strings or words that can be generated based on a particular word/phrase/class. For example, the extension of $\bf table$ is the set of all tables. 

These sets aren't all there is to language—it's impossible to create a set of all tables that exist in the world. Rather, it suffices to know in general what constitutes a table, from which we can generalize meaning.

It's also important to note that meaning and set membership can change over time. One common example is positions—the president may refer to person A one day, but person B another.

### Noun Phrases

The meanings of noun phrases can be represented using sets of items that fit under their category. 

**Individuals** are noun phrases that refer to any particular individual.

>**Examples.** 
>- $\sem{{\bf John}}_s$ is the individual John.
>- $\bsem{Mary}$ is the individual Mary.

**Count nouns** refer not to a particular individual, but a class of such individuals. They are modeled formally with sets.

>**Examples.** 
>- $\bsem{city}=\{x\mid x\text{ is a city}\}$
>- $\bsem{table}=\{x\mid x\text{ is a table}\}$

**Functional** or **relational nouns** represent relationships between nouns. This can be in a set-theoretic sense or a functional sense.

>**Examples.** 
>- $\bsem{mother}=\{\langle x,y\rangle\mid x\text{ is }y\text{'s mother}\}$
>- $\bsem{sister}=\{\langle x,y\rangle\mid x\text{ is }y\text{'s sister}\}$

### Verbs

**Intransitive verbs**, which don't take on an object, are simply sets of the individual that is undergoing the verb.

>**Example.** $\bsem{run}=\{x\mid x\text{ runs}\}\approx\text{the set of runners}$

**Transitive verbs** involve two individuals that are in a certain relation. They bear parallels with functional nouns. 

>**Example.** $\bsem{call}=\{\langle x, y\rangle\mid x\text{ is called by } y\}$

**Ditransitive verbs** similarly involve the relation between three individuals. 

>**Example.** $\bsem{give}=\{\langle x,y,z\rangle\mid x\text{ is given to }y\text{ by }z\}$

### Composing Meaning

>[!theorem] Principle of Compositionality
>The meaning of a composite expression is a function of the meaning of its immediate constituents and the way these constituents are put together.

The principle of compositionality seems fairly straightforward, but turns out to have a great many applications in transforming atomic elements into complex structures.

>**Example.** Intransitive verbs
>$$\bsem{Paul snores}=\begin{cases}1 & \text{if }\bsem{Paul}\in\bsem{snores}\\0&\text{o.w.} \end{cases}$$

>**Example.** Transitive verbs
>$$\bsem{Sue loves Mary}=\begin{cases}1 &\text{if }\langle\bsem{Mary},\bsem{Sue}\rangle\in \bsem{loves}\\0&\text{o.w.}\end{cases}$$
>Note that formally, $\langle\bsem{Mary},\bsem{Sue}\rangle\in \bsem{loves}$ is shorthand for 
>$$\exists x\in\bsem{Mary},y\in\bsem{Sue}\text{ s.t. }\langle x,y\rangle\in\bsem{loves}$$

In fact, we can generalize the pattern for transitive verbs as follows:
$$\lbr{\text{TV + referential term}}\rbr_s\triangleq\left\{y\mid \langle\sem{\text{referential term}}_s,y\rangle\in\sem{{\rm TV}}_s\right\}$$
>**Example.** Relational noun phrases
>With $\bsem{Sue}=s,\bsem{sister}=\{\langle x, y\rangle\mid x\text{ is } y\text{'s sister}\}$,
>$$\bsem{sister of Sue}=\{x\mid x \text{ is }s\text{'s sister}\} $$

Phrases with ditransitive verbs become a bit more complicated. Particularly, they can be decomposed into different smaller relations where we can partially fill in information. In some ways, it bears resemblance to partial function application. For example, for a function $$\textrm{give}(x,y,z)=x\text{ is given }y\text{ by }z$$we can create partial applications by filling in some values
$${\rm giveBob}(y,z)={\rm give}({\rm Bob}, y,z)=\text{Bob is given $y$ by $z$}$$
or more values ...
$${\rm giveBobWater}(z)={\rm give(Bob, Water}, z)=\text{Bob is given Water by $z$}$$
In terms of extensions, we can write the above as follows:
$$\begin{align}
\bsem{give}&=\{\langle x, y, z\rangle\mid\text{$x$ is given $y$ by $z$}\} \\
\bsem{give Bob}&=\{\langle y,z\rangle\mid \text{Bob is given $y$ by $z$}\} \\
\bsem{\textrm{[}give Bob\textrm{]} water}&=\{z\mid\text{Bob is given water by $z$}\}
\end{align}$$

In fact, we can generalize this rule.

>[!definition] Plugging Operation
>For any (binary) sub-tree $\alpha$ with daughters $\beta$ and $\gamma$, where
>1. $\sem{\beta}_s$ is an $n$-ary relation $R$ and
>2. $\sem{\gamma}_s$ is an object $x$,
>$$\begin{align}\sem{\alpha}_s\triangleq\text{set of $(n-1)$-tuples s.t. substituting $x$ as the first}\\\text{member results in a tuple in $R$}\end{align}$$

### Sentences

From the above illustrations, when we complete a (true) sentence, we'll result in a set containing the empty set. For example, 
$$\bsem{I give Bob water}=\begin{cases}\{\emptyset\} & \text{if this is true} \\\emptyset & \text{o.w.}\end{cases}$$

>[!theorem] Frege's Generalization
>The extension of a sentence $S$ is its truth value.

From this generalization, we say $\{\emptyset\}\to1$ and $\emptyset\to0$, assigning sentences extensions 1 or 0.

