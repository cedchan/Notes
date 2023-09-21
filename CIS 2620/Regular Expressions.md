## Definition

1. $\varepsilon$ is a regular expression
	Only the empty string matches this regex: $L(\varepsilon)=\{\varepsilon\}$

2. $\Phi$ is a regular expression
	No string matches this regex: $L(\Phi)=\emptyset$

3. For each symbol $\sigma\in \Sigma$, $\sigma$ is a regular expression
	The only string matching regex $\sigma$ is $\sigma$ itself: $L(\sigma)=\{\sigma\}$

4. If $r$ is a regular expression, so is $(r)$
	Parentheses are used only for parsing: $L((r))=L(r)$

5. If $r$ and $r'$ are regular expressions, then so is $r.r'$. 
	A string $w$ matches $r.r'$ if it can be split into $u.v$ such that $u$ matches $r$ and $v$ matches $r'$. That is, $L(r.r')=L(r).L(r')$.

>[!note]
>Usually, "." is omitted in string concatenation (e.g., $0.1=01$).

6. If $r$ and $r'$ are regular expressions, then so is $r \cup r'$. 
	A string matches $r\cup r'$ if it matches either $r$ or $r'$. That is, $L(r\cup r')=L(r)\cup L(r')$.

>[!note]
>We abbreviate the union of all $\sigma\in\Sigma$ as $\Sigma$. That is, $$\bigcup_{\sigma\in\Sigma}\sigma\rightarrow\Sigma$$
>For example, if $\Sigma=\{\text{a, b, c}\}$, we abbreviate the regular expression $(\mathrm a\cup \mathrm b \cup \mathrm c)$ as $\Sigma$.

7. If $r$ is a regular expression, then so is $r^*$.
	A string $w$ matches $r^*$ if it can be split into multiple (0 or more) parts such that each part matches $r$. That is, $L(r^*)=L(r)^*$.

### Notational Conventions

- $r^*$ means 0 or more reptitions of $r$
- $r+$ means 1 or more repetitions of $r$
- $^*$ has highest precedence, followed by $.$, followed by $\cup$

>**Examples.**
>- $\mathrm{ab}^*=\text{a.(b)}^*$
>- $\mathrm{ab\cup c=\text{(a.b)}\cup c}$
>- $\mathrm a \cup\mathrm b=\mathrm a \cup (\mathrm b)^*$

## Regular Expressions to NFAs

**Goal:** Given a regular expression $r$ construct an $\varepsilon$-NFA $M(r$) that accepts the language $L(r)$.

Construction by induction on the structure of $r$:
1. $r$ equals $\varepsilon$ ![](Pasted%20image%2020230921120836.png)
2. $r$ equals $\Phi$ ![](Pasted%20image%2020230921120927.png)
3. $r$ equals $\sigma\in\Sigma$ ![](Pasted%20image%2020230921120958.png)
4. $r$ equals $(p)$. $M(r)=M(p)$.
5. $r$ equals $r1.r2$. Build $M(r)$ from $M(r1)$ and $M(r2)$ using [concatenation construction](Constructions%20on%20Automata.md#Closure%20of%20Regular%20Languages#Concatenation%20of%20Languages). (That is, draw $\varepsilon$-transitions from accepting states of $M(r1)$ to the initial state of $M(r2)$, and make those accepting states non-accepting.) ![](Pasted%20image%2020230921121846.png) 
6. $r$ equals $r1\cup r2$. Build $M(r)$ from $M(r1)$ and $M(r2)$ by adding a new initial state. ![](Pasted%20image%2020230921121751.png)

>**Example.** Construct an NFA for $\mathrm{(a b)^*(a\cup\varepsilon)}$
>
>>[!solution]+
>>Constructing NFA for $\mathrm{a.b}$
>>![](Pasted%20image%2020230921123633.png)
>>![](Pasted%20image%2020230921123705.png)
>>Constructing $\mathrm{(a b)^*}$
>>![](Pasted%20image%2020230921124020.png)
>>Constructing $(\mathrm a\cup \varepsilon)$
>>![](Pasted%20image%2020230921124127.png)
>>![](Pasted%20image%2020230921124220.png)
>>Constructing $\mathrm{(a b)^*(a\cup\varepsilon)}$
>>![](Pasted%20image%2020230921124446.png)

### Compilation Summary

The process for compilation of a regular expression $r$ is
$$r\rightarrow \varepsilon\text{-NFA } M(r)\rightarrow\text{DFA } M'(r)$$

The number of states in $M(r)$ is about the same as the size of $r$—that is, $O(|r|)$.

Determinization using subset construction can cause the number of states to blow up, becoming $2^{|r|}$.

## Sufficiency of Operators

A proof in the textbook shows that all DFAs can also be converted into regular expressions (and therefore, these operators are sufficient).