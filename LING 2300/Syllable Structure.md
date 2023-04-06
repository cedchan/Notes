
## Basic Structure

Syllables are abstract groupings of segments into larger units.

>[!definition]
>Syllables are broken into three major segments:
>1. **Onset**: Everything before the nucleus
>2. **Nucleus**: The sonority peak of the syllable (i.e., the syllabic segment, the vowel)
>3. **Coda:** Everything after the nucleus
>
>All syllables must have a nucleus, but the other parts are optional. The **rhyme/rime** is the nucleus and the coda. 

### Some Notation

- Syllable: $\sigma$
- Rhyme: R
- Onset: On
- Nucleus: Nu
- Coda: Co

>[!definition]
>**Tautosyllabic**: In the same syllable
>**Heterosyllabic**: In different syllables
>**Hiatus**: The nuclei of two syllables are adjacent, and the second syllable has no onset
>**Open syllable**: Doesn't have a coda

## Syllable Inventory

>[!definition]
>The **syllable inventory**, also known as the **syllable canon**, is the set of possible syllables in a given language.

All languages permit CV syllables
Every grammar has both the nucleus rule and the onset rule
There are also other parameters of variation

## Syllabification Algorithm

Abstractly, there is a so-called "syllabification algorithm" that can construct a syllable. The algorithm consists of five rules:
1. Nucleus Rule
2. Onset Rule
3. Coda Rule
4. Complex Onset Rule
5. Complex Coda Rule

>[!definition]
>The **core syllabification rules** are the Nucleus Rule and the Onset Rule, which appear in every language.
>
>The core syllabification rules generate the **core syllable** of the form CV, where C is a non-syllabic segment and V is the nuclear segment.

Typically, the five rules are applied in the order listed above, although this is not always the case, as discussed [later](Syllable%20Structure.md#Syllable%20Constraints#Complex%20Syllables).

### Nucleus Rule

For each segment which is a sonority maximum, inserts a rhyme constituent and associates the segment with the rhyme. Inserts a $\sigma$ constituent and associates the rhyme with the $\sigma$. 

### Onset Rule

Puts an unsyllabified segment to the left of a rhyme segment into an onset constituent and associates the onset with the $\sigma$ of the rhyme segment.

### Coda Rule

Adjoins into the rhyme an unsyllabified segment to the right of a rhyme segment.

If a language has the Coda Rule, it will always fallow the Onset Rule. This is known as **onset first**.

### Complex Onset Rule

Puts an unsyllabified segment $X$ to the left of a segment $Y$ which in an onset into that onset, provided $X$ is not more sonorous than $Y$.

This rule iterates as many times as it can.

### Complex Coda Rule

Puts an unsyllabified segment $X$ to the right of a segment $Y$ which is in a rhyme into the rhyme provided $X$ is not more sonorous than $Y$.

## Syllable Constraints

Grammars include information about how syllables can be constructed.

### Sonority Sequencing Principle

>[!theorem]
>The **Sonority Sequencing Principle** (SSP) states that a syllable may not contain a fall in sonority, followed by a rise.

There are two major corollaries of the SSP:
1. Complex onsets must rise in sonority.
2. Rhymes must fall in sonority

### Complex Syllables

- **Complex onsets**: Does the grammar have the complex onset rule?
- **Codas**: Does the grammar have the coda rule?
- **Complex codas**: Does the grammar have the complex coda rule?

Some languages have a preference for or against complex onsets—that is, some languages would rather split a complex onset into a coda of the previous word and the onset of the next. For example, [ab|ra] vs. [a|bra]. 

In languages that prefer to split up complex onsets, the [Coda Rule](Syllable%20Structure.md#Syllabification%20Algorithm#Coda%20Rule) precedes the [Complex Onset Rule](Syllable%20Structure.md#Syllabification%20Algorithm#Complex%20Onset%20Rule).

In languages that prefer to keep complex onsets, the Complex Onset Rule precedes the Coda Rule. Such languages are called **onset-maximizing**.

### Sonority Distance Requirements

If a language permits complex onsets or codas, there may be restrictions on how far apart in sonority two segments must be when they appear in the same onset or coda. For example, a stop + nasal cluster is not possible in English.

### Margin Rules

Some languages allow additional segments to be added to complex onsets or complex codas in ways that otherwise violate syllabic structure rules.

For example, the **S-Rule** in English allows an [s] to be adjoined to a complex onset containing a stop, even though there is a fall in sonority.

### Language-Specific Constraints

Some specific onset or coda clusters are not permitted in certain languages, despite otherwise following structure rules. 