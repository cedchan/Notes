
## Gestalt Psychology

Gestalt psychology believes that people construct all perception and abstract thoughts from smaller components of complex systems. A central idea is that the whole is greater than the sum of its parts.

Gestalt psychology finds its roots in three closely interrelated theories: [atomism](Perception.md#Gestalt%20Psychology#Atomism), sensationalism, and associationism. 

### Atomism

**Atomism**, which also known as **elementalism**, is the view that all knowledge is built from simple, elementary constituents. 

In a sense, DSP itself is based on atomism. 

### Sensationalism

**Sensationalism** posits that the simplest constituents (so-called atoms of thought) are elementary sense impressions.

### Associationism

**Associationism** suggests that complex ideas are constructed by association of simpler ideas.

### Deep Learning

Deep learning itself seems to be an application of Gestalt psychology.

## Gestalt Effects

### Phoneme Restoration Effect

When a segment in some speech signal is replaced by some noise burst, then played back to people, they (1) reconstruct the replaced phoneme automatically, and (2) are inaccurate in identifying where the burst occurred, tending toward phrase boundaries.

### Auditory Streaming Effect

When multiple notes are played together (e.g., two violins playing a melody and a harmony), humans are typically able to separate out the different parts. 

## Latent Semantic Analysis

**Latent Semantic Analysis (LSA)** is an NLP technique for comparing the semantic content of two documents. Word counts of each lexical item are represented as rows and columns in a matrix.

Then, singular value decomposition is used to maintain structural similarity while reducing dimensions. Then, cosine similarity is used to compare columns.

The issue with LSA in its original form was that associated words would not show up as such in this sort of historgramming of word counts. 

## Word Embeddings

In the simplest of forms, word embeddings represent words as vectors of numbers, which can be used to geometrically compare words semantically, syntactically, etc.

### Applying to Sound

Models like wav2vec represent do a similar kind of analysis on audio by representing a certain clip of audio though an inventory of learned units.