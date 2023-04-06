
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

## "Loudness Predicts Prominence"

It's been known for some time that pyschological "prominence" of sounds is not equivalent to the quantitative measures for them that are used. For example: Pitch is psychological while $f_0$ is physical. Loudness is psychological while amplitude is physical.

"Loudness Predicts Prominence: Fundamental Frequency Lends Little," a study in 2005, showed that [TK] . 

They took measures of loudness, aperiodicity, spectral slope, $f_0$, and a running measure of duration, which were transformed into coefficients for Legndre polynomials and classified to reproduce human prominence judgements.

The coefficients are used as a feature vector that is fed into a quadratic discriminant forest classifier. 

### Measures of Loudness

Broadly, they measure loudness by weighting energy of the signal sometimes. Specifically, they use 0.7 octave frequency bins on the spectral power density derived from an $L=50$ ms wide, $1+\cos\frac{2\pi(t-t_c)}{L}$ window. 

#### Bark Scale

The **Bark scale** is a pyschoacoustical scale that seeks to measure loudness. The idea is that equal distances along the scale correspond to equal perceptual distance. Above 500 Hz, it is roughly logarithmic, while below 500 Hz it becomes increasingly linear.

### Aperiodicity

### Spectral Slope

### Fundamental Frequency

$f_0$

### Running Measure of Duration

The idea is that you're integrating amplitude differences with an exponential decay. So as you move away from a point in time, if the spectrum isn't changing, you do exponential decay until your integration meets a threshold. But if the spectrum is changing, then the integration will increase more rapidly. 