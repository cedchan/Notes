## Sound Production

### Phases of Sound Production

*Typically*, sound is produced with
1. **Respiration**: Expiration—producing sounds by breathing out
2. **Phonation**: Vibrate vocal folds
3. **Articulation**: Change quality of sound by shaping vocal tract

### The Vocal Organs

The trachea and lungs provide air support for sound production, while the 3 cavities—**pharyngeal, nasal,** and **oral**—change sound quality.

The **larynx** is composed of multi-layered membranes called **vocal folds**. The space between vocal folds is called the **glottis**. The **epiglottis**—which blocks off the trachea (for swallowing)—is also in the larynx. Muscles in the larynx can, for example, lengthen the larynx to raise pitch.

**Supralaryngeal articulation** occurs above the larynx, such as in the
- Pharynx
- Oral cavity
- Nasal cavity
- Tongue
- Lips
- Palate (hard/soft)
- Teeth
- Mandible (lower jaw)

The **tongue** is divided, from front to back, into 
1. Tip (apex)
2. Blade (lamina)
3. Body—front/back
4. Root

The tongue is the most **active articulator** (meaning we have a high degree of control over it). Most sounds combine movement of active articulators with **passive articulators**.

The **palate** can be divided into (from front to back)
- Alveolar ridge
- Hard palate
- Soft palate / velum (often an active articulator)
- Uvula

## Phonemes and Allophones

A **phoneme** is an abstraction of a set of sounds—**allophones**. That is, phonemes can have multiple pronunciations and are language-dependent. Phonemes are denoted by / /. 

>**Example.** The phoneme /k/ is different in *keyed* and *code*.

Allophones correspond to individual sounds in a one-to-one mapping and are language-independent. They are denoted by [ ].

With these, we have two styles of phonemic transcription:
- **Broad**: Phonemeic distinctions
- **Narrow**: All non-distinctive detail

>**Example.** *bead* vs. *bid*
>Broad: /i/ vs. /ɪ/
>Narrow: /iː/ vs. /ɪ/

Allophones are often in a **[complementary distribution](Distributions.md)**: they don't contrast with each other.

## Sound

**Sound waves** are acoustic energy transmission between a sound source and receiver. Physically, they are pressure variations over time transmitted by movements of air molecules. 

Humans can only detect a small range of pressure variation.

### Waves

**Waves** are oscillations that spread. **Longitudinal waves** vibrate parallel to the direction of wave propagation. **Transverse waves** vibrate perpendicular to the direction of the wave.

Sound waves are longitudinal and are emitted radially from a source.

Wave properties:
- **Wavelength** ($\lambda$): Distance between two successive points in the same phase
- **Frequency** ($f$): Frequency of a wave is the same as the frequency of the source
- **Period** ($T$): duration of one cycle
- **Velocity** ($V$): Propagation speed is dependent on the density and elasticity of the medium (solid > liquid > gas)

Relationships of properties:
- $V=f\lambda$
- $f=\frac{1}{T}$ (in sec)

The frequency of sound waves is related to pitch, while the amplitude is related to loudness.

### Speech Waves

It's rare that speech sounds (or really, most sounds) have simple harmonic motion, or a single frequency. Instead, they are complex waves that are the sum of multiple simple waves.

The **sawtooth waveform** is a simple waveform that bears similarity with real speech signals.

The **fundamental frequency** is 
- The lowest component frequency of a complex periodic wave
- The frequency of the longest repeating pattern

Most of the time, those two are equivalent, but not always.

Speech sounds are typically represented either on the **time domain** (typical waveforms) or the **frequency domain** (spectrum).

#### Representations of Sound

##### Waveforms
| Property | Value |
|-|-|
| x-axis|time|
| y-axis|amplitude|

##### Spectrum
| Property | Value |
|-|-|
| x-axis|frequency|
| y-axis|amplitude|

##### Spectrogram
| Property | Value |
|-|-|
| x-axis|time|
| y-axis|frequency|
| darkness |amplitude|

Each vertical "slice" of a spectrogram can be seen as the spectrum for that particular time.

### Aperiodic Sounds

**Aperiodic sounds** aren't cyclic—that is, they have no clear repeating pattern. White noise is one example of this. Its spectrum is random, but is centered on some single amplitude (with normal distribution) for all frequencies.

Other types of noise (e.g., pink noise, blue noise) have different frequency distributions.

**Transient** signals are pulses in the waveform. Their spectrums are just horizontal lines.

### Recording

Signals in the real world are **analog**—that is, continuous. But for the purposes of recordings, they must be made **discrete**.

**A/D** (analog/digital) conversion is used to record real sounds with the following:
- **Sampling**: limiting time positions
- **Quantization**: limiting the amplitude positions

A/D conversion parameters:
- **Sampling interval** ($T$): time between each sample
- **Sampling rate** ($f$): Number of samples per second

#### Choosing Parameters

The general rule is the "more is better" because it gives greater resolution to the signal. That said, real-world computational limitations would say that the minimum number of samples is preferrable. 

For a periodic sine wave, 2 samples per cycle is the minimum. Thus, we must sample at twice the desired signal frequency (**Nyquist frequency**), or perhaps a little more.

The critical information in speech signals goes up to 8 kHz, so many linguistic recordings sample at 16 kHz.

The amplitude range is divided into powers of 2. The power is called the "bit" (e.g., $2^{16}$ is 16 bits).