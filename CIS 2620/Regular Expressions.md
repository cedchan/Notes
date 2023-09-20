## Iteration: Kleene* Operation

>[!definition]
>$$A^*=\{w\mid w \text{ can be split into multiple parts s.t. each part is in }A\}$$

That is, $A^*$ is repeated concatenation, starting at $\varepsilon$.

>**Example.** $A=\{w\mid \mathrm{count}(w, \mathrm a)=2\}$ What is $A^*$?
>
>>[!solution]+
>>$A^*=\{w\mid w=\varepsilon \lor w \text{ contains a positive even number of a's}\}$

>**Example.** $\{w\mid w \text{ consists of 0 or more b's followed by a}\}, \Sigma=\{\text{a, b, c}\}$. What is $A^*$?
>
>>[!solution]+
>>$A^*=\{w\mid w \text{ doesn't contain any c and doesn't end with b}\}$

## Definition

1. $\varepsilon$ is a regular expression
	Only the empty string matches this regex: $L(\varepsilon)=\{\varepsilon\}$

2. $\phi$ is a regular expression
	No string matches this regex: $L(\phi)=\emptyset$

3. For each symbol $\sigma\in \Sigma$, $\sigma$ is a regular expression
	The only string matching regex $\sigma$ is $\sigma$ itself: $L(\sigma)=\{\sigma\}$

4. If $r$ is a regular expression, so is $(r)$
	Parentheses are used only for parsing: $L((r))=L(r)$

>[!error]


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

