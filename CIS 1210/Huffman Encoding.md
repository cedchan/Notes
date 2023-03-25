## Encoding

Characters are encoded as binary strings. Thus, if you have $b$ bits, you can create $2^b$ combinations, or characters. Conversely, you need $\lceil\lg n\rceil$ bits to encode $n$ characters. For 26 letters and a space, that's 5 bits. ASCII uses 8.

But some characters are used more frequently then others. This is the crux of Huffman encoding.

>[!idea]
The idea behind Huffman encoding is that frequent characters use fewer bits than other characters.

But there's ambiguity: What if a smaller encoding is the prefix of a larger one? We need our encodings to be **prefix free**

>[!definition]
>A **prefix code** for a set of $S$ letters is a function $\gamma$ that maps each letter $x\in S$ to some binary sequence, such that for any distinct $x, y\in S$, $\gamma(x)$ isn't a prefix of $\gamma(y)$.

With a prefix code, we easily encode text by converting each letter $x$ to $\gamma(x)$. To decode, we scan left to right, and since we know no sequence is a prefix of another, as soon as we hit a match (i.e., a sequence in the range of $\gamma$), we can replace the sequence with the letter. 

>[!definition]
>An **optimal prefix code** is as efficient as possible. That is, given $S$ and the frequencies for each letter in $S$, it minimizes the average bits per letter $\text{ABL}(\gamma)=\sum\limits_{x\in S}f_x\cdot|\gamma(X)|$, where $f_x$ is the frequency of letter $x$.

## Prefix Codes as Trees

>[!lemma]
>Suppose the letters of our alphabet are leaves in a binary tree. Then, we say that we can encode each letter as a path from the root to the leaf, where each left edge is 0 and each right edge is 1. This encoding is a prefix code.

Thus, the number of bits of each letter is its depth in the tree, and the ABL is similarly the average depth of each letter, multiplied by that letter's frequency.
$$
\text{ABL}(T)=\sum_{x\in S}f_x\cdot\text{depth}_T(x)
$$

>[!lemma]
>The binary tree corresponding to an optimal prefix code is full.

*Proof:* If it were not full, we could place the lone child (i.e., the one with out a sibling, since the tree isn't full) where the parent is and achieve a shorter encoding.

## Huffman's Algorithm

>[!lemma]
>There is an optimal prefix code corresponding to tree $T*$ where the two lowest frequency letters are assigned to leaves that are siblings in $T*$.

*Proof:* If we are given $T*$, the tree structure of $T$, but not the character-to-leaf mappings, we can construct a valid $T$ by adding leaves in decreasing order of depth. Then, the highest frequency letters will have the greatest depth. It follows that the order of leaves at a certain depth doesn't matter, and since $T$ is full, we conclude that some ordering has the lowest two frequency letters are siblings in some $T*$. 

A [priority queue](Heaps.md#Priority%20Queues) implementation of Huffman:

```
Huffman(S):
	Let Q be a priority queue with S as values and frequencies as keys

	for i = 1 to n do
		Allocate a new node w
		y = extractMin(Q)
		z = extractMin(Q)
		w.left = y
		w.right = z
		f_w = f_y + f_z
		insert(Q, z)

	return extractMin(Q) // root of the tree
```

### Correctness

We do proof by induction.

**Hypothesis:** Huffman works on $T'$, the result of Huffman on $S'=(S\setminus\{y,z\})\cup\{w\}$.

>[!lemma]
>With $T, T'$ from above, $\text{ABL}(T)=\text{ABL}(T)-f_w$.

**Step:** Assume for contradiction that $T$ is not optimal, but $Z$ is. This means that $\text{ABL}(Z)<\text{ABL}(T)$. By lemmas above, we assume $Z$ has $y, z$ as siblings. If we delete $y, z$ and replace them with $w$ to create $Z'$, we have $\text{ABL}(Z')=\text{ABL}(Z)-f_w$. 

But this means $\text{ABL}(Z')<\text{ABL}(T')$ (subtract $f_w$ from both sides of original inequality), contradictin gthat $T'$ is optimal.

### Runtime

We must, for each letter, find the min and operate on it. Implementing Huffman with a binary priority queue, we can [extract the min](Heaps.md#Heap%20Extract%20Maximum) in $O(\lg n)$ time, and [construct the heap](Heaps.md#Building%20a%20Heap) in $O(n)$ time. Thus, we have total runtime $O(n\lg n)$. 