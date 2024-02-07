>[!idea]
>Recall the [lower bound](Deterministic%20Finite%20Automata%20(DFA).md#A%20Lower%20Bound%20on%20the%20States) on the number of states a DFA must have: the cardinality of a set of distinguishable strings.
>
>Then, if we can show such a set of infinite size exists, the DFA cannot be finite.

>**Example.** $A=\{w\mid\mathrm{count}(w, \mathrm a)=\mathrm{count}(w, \mathrm b)\}$
>
>Consider $S=\{\varepsilon, \text{ a, aa, aaa, ...}\}=\{\mathrm a^k\mid k\geq 0\}$
>$|S|=\infty$, and each element is pairwise distinguishable. Consider 2 strings $\mathrm a^i, \mathrm a^j, i\neq j$. Adding the suffix $\mathrm b^i$ will distinguish them. Thus, no finite number of states will suffice.

>[!theorem]
>Iff there exists an infinite set $S$ of pairwise distinguishable (w.r.t. $A$) string, then $A$ is not regular.

>**Example.** $A=\{w.w \mid w \in \{\text{a, b}\}^*\}=\{\varepsilon,\text{ aa, bb, abab, aaaa, baba, bbbb, ...}\}$
>
>A string $w$ belongs in $A$ if $w$ can be split into two identical halves.
>
>Consider $S=\{\varepsilon, \text{ a, aa, aaa, ...}\}=\{\mathrm a^k\mid k\geq 0\}$. $|S|=\infty$
>
>$S$ contains pairwise distinguishable strings. Consider two strings $\mathrm a^i, \mathrm a^j, i\neq j$. $\mathrm a^i.\mathrm a^i$ can be split into 2 identical halves, so it's in $A$. $\mathrm a^j.\mathrm a^i$. This doesn't work if $i, j$ are both even.
>
>Instead use the suffix $\mathrm{ba}^i\mathrm b$. 


>**Example.** $\Sigma=\{\mathrm a\}, A=\{w\mid\text{length of }w\text{ is a perfect square}\}$
>$A=\{\varepsilon, \mathrm{a, a^4, a^9, ...}\}$
>
>Let $S=\{\varepsilon,\mathrm{a,aa,aaa,...}\}$. Consider 2 strings $\mathrm a^i, \mathrm a^j, i<j$. 
>
>Let our suffix be $\mathrm a^p, p=\mathrm a^{j^2-i}$. Since $j>i, p\geq0$. $i+p=j^2$, a perfect square. Further, $j+p=j^2+(j-i)>j^2$. The next square is $(j+1)^2=j^2+2j+1$ and since $j-1<j^2+2j+1$, $j+p$ can't be a perfect square.