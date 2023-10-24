## Linear Model

The **linear model**, which is what we've studied thus far, views phonology as a linear sequence of segments—sort of like beads on a string. 

Each segment is simply represented as a feature matrix of characteristics of the segment.

## Non-Linear Model

**Non-linear models**, also knows as **hierarchical**, have a tier-based system where segments are grouped into different parts. 

For example, consider the tree-like structure of syllable structure that we've looked at before. Clearly, there are multiple "lines." Images of these sorts of models are called **charts** sometimes.

There are typically two major tiers that constitute the model: the timing tier and the melodic tier. The **timing tier** expresses length. The **melodic tier** consists of the traditional feature matrix we've seen.

## X-Slots

The **timing tier**, the first tier, expresses length. It consists of units called **X-slots**, which represent relative duration. If one segment is length X, then a longer segment in the word might have durration XX or XXX. 

So what's the difference between a segment of length XX and that same segment but of length X, repeated twice? When there's a single segment, any change to that segment will apply to its entirety, whereas a repeated segment might have the first segment be affected while the second remains the same.

**Geminate inalterability** is a phenomenon where a single segment of multiple timing units (X-slots) are immune to changes the same segment with a single timing unit would undergo. 

### Obligatory Contour Principle (OCP)

Countours are obligatory on the melodic tier. We cannot have adjacent elements be the same, if not separated by some sort of pattern. The same idea can be applied to other features in linguistics, suhc as length.

### Stability Effect

There can be effect that only affects a certain tier of the hierarchy.

An association line is marked by dashed line. Two small cross represent a deleted association line.

### Compensatory Lengthening

**Compensatory lengthening** is where a segment deletes and an adjacent segmet becomes longer. The lengthed segment "compensates" for the deletion.

### Deletion

Notice that segments of length 0 are not pronounced, so segment deletion can also be seen as "de-linking" timing units with their melodic tier. 

The question then becomes, what happens to the empty time unit? One option is that the preceding segment **spreads** to the empty space. (Again, this can be represented witha  dashed line.)

## Moraic Theory

**Moraic theory** states that long segments must appear in the rhyme. Onsets are weightless in Moraic theory.  

Similar to X-slots, lengths of segments can be represented by different symbols. Here, there are light, heavy, and superheavy segments called moras ($\mu$). 
- **Light:** A short vowel
- **Heavy:** A short vowel followed by a consonant *or* a long vowel
- **Superheavy:** A long vowel followed by a consonant

Stressed segments must be heavy.

### Underlying Forms

Short vowels have a mora, and long vowels have two.

Short consonants don't have a mora underlyingly, but may be given one from being in the coda. Long consonants do have moras. Thus, if a consonant has a mora, it is likely either in the coda or is geminate.

### Syllabification Rules

Moraic theory interacts in a specific way with the [syllabification rules](Syllable%20Structure.md#Syllabification%20Algorithm).

#### Nucleus Rule

Projects $\sigma$ from the leftmost mora attached to each sonority peak. To **project** is to insert $\sigma$ to the $\sigma$-tier and attach it to the leftmost mora.

#### Onset Rule

Adjoin an unsyllabified segment to the onset of a syllable that contains a syllabified segment.

#### Coda Rule

The Coda Rule is split into two parts: weight by position and coda formation.

In **weight by position**, a mora is projected from any unsyllabified segment immediately to the right of a moraic syllabified segment.

Then in **coda formation**, an unsyllabified mora is adjoined to the syllable of a syllabified mora to its immediate left. 

### Syllabic Prespecification

Some irregulars can't be derived entirely from syllabic rules. In these cases, we may sometimes have to **prespecify** the some parts of the syllable structure in the UR.

Prespecification is typically used to encode unpredictable properties in URs.

Note that irregulars are typically exceptional in only some small detail, rather than the entire word.

### Consequences of Multi-Tiered Representations

One argument for multi-tiered representations are **stability effects**: elements on one tier can be deleted without necessarily delting the elements they are associated with on another tier.

Further, elements on one tier can be linked to one, multiple, or no elements on another tier. **Floating** or **unassociated** elements (i.e., not linked with any element on another tier) have no phonetic realization. They are notated with an apostrophe or by surrounded by a circle. 

