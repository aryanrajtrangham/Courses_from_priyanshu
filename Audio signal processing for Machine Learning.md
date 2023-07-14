# Audio Signal Processing for Machine Learning  

## Applications

- Audio classification
- Speech recognition / speaker verification
- Audio denoising / audio up sampling
- Music Information Retrieval
  - Music Instrument Classification
  - Mood Classification
- etc

## Content

- Sound waves
- DAC / ADC
- Time and frequency-domain audio features (e.g., rms, spectral centroid )
- Audio transformations
  - Fourier Transforms / STFT
  - Constant-Q Transform
  - Mel Spectrograms
  - Chromograms
...

## What you’ll learn

- Get a deep understanding of audio data
- Familiarise with frequency/time-domain audio features
- Extract features from raw audio
- Recognise what audio features to use for ML applications
- Pre-process audio data for ML
- Understand (some!) math behind audio transformations
- Use librosa for your audio projects

## Sound

- Produced by vibration of an object
- Vibrations cause air molecules to oscillate
- Change in air pressure creates a wave
- **Mechanical wave**
  - Oscillation that travels through space
    - Energy travels from one point to another
    - The medium is deformed
- **Waveform**
  - Carries multifactorial information:
    - Frequency
    - Intensity
    - Timbre
  - y(t) = A *sin*(2πft + φ)
- **Periodic and aperiodic sound**
  - All Waveforms
    - Periodic
      - Simple (Single Sine waves)
      - Complex (Multiple Sine waves)
    - Aperiodic
      - Continuous (Noise)
      - Transient (Pulse)
- **Hearing Range**
  Hearing range | Range
  --------------|-------------
    Elephant    | 14 - 12000Hz
    Human       | 20 - 20000Hz
    Cats        | 48 - 75000Hz
    Dogs        | 64 - 45000Hz
    Mouse       | 1000 - 70000Hz
    Bat         | 7000 - 200000Hz
- **Pitch**
  - Logarithmic perception
  - 2 frequencies are perceived similarly if they differ by a power of 2
- **Mapping pitch to frequency**
  - F(p) = $2^{(p-69)/12}* 400$
  - F(60) = $2^{(60-69)/12}* 440$ = 261.6
  - F(p+1)/F(p) = $2^{(1/12)}$ = 1.059
- **Cents**
  - Octave divided in 1200 cents
  - 100 cents in a semitone
  - Noticeable pitch difference: 10-25 cents

## Features of Sound

- **Sound Power**
  - Rate at which energy is transferred
  - Energy per unit of time emitted by a sound source
  - Measured in watt
- **Sound Intensity**
  - Sound power per unit area
  - Measured in $W/m^{2}$

- **Thresholds**
  - Human can perceive sound with very small intensities.
  - Threshold of Hearing (TOH) = $10^{-12}*W/m^{2}$
  - Threshold of pain (TOP) = $10*W/m^{2}$

- **Intensity level**
  - Logarithmic scale
  - Measured in decibels (dB)
  - Ratio between two intensity values
  - Use an intensity of reference (IOR)
  - $dB(I) = 10*log_{10}(I/I_{TOH})$
  - $dB(I_{TOH}) = 10*log_{10}(I_{TOH}/I_{TOH}) = 0$
  - Every ~3dBs, intensity doubles.
  - Source                    | Intensity           | Intensity level | xTOH
      --------------------------|---------------------|-----------------|-------
      Threshold of hearing(TOH) | $10^{-12}$          | 0dB    |  1
      Whisper                   | $10^{-10}$          | 20dB   | $10^{2}$
      Pianissimo                | $10^{-8}$           | 40dB   | $10^{4}$
      Normal conversation       | $10^{-6}$           | 60dB   | $10^{6}$
      Fortissimo                | $10^{-2}$           | 100dB  | $10^{10}$
      Threshold of pain         |  $10$               | 130bB  | $10^{13}$
      Jet take-off              |  $10^{2}$           | 140dB  | $10^{14}$
      Instant perforation of eardrum |  $10^{4}$      | 160dB  | $10^{16}$

- ### Loudness

  - Subjective perception of sound intensity
  - Depends on duration / frequency of a sound
  - Depends on age
  - Measured in phons

- ### Equal loudness contours

    ![Sound Pressure vs Equal-loudness](https://i.pinimg.com/564x/a5/24/46/a524464ddccc0c1333c1d85d6745c979.jpg)

- ### Timbre

  - Colour of sound
  - Diff between two sounds with same intensity, frequency, duration
  - Described with words like: bright, dark, dull, harsh, warm
  - Features of Timbre
    - Timbre is multidimensional
    - Sound envelope
      - Attack - Decay - Sustain - Release Model

        ```[]
            A
          A|   A          D         S         R
          m|<------->.<------->.<------->.<-------->.
          p|        _:.        :         :          :
          l|      .  : .       :         :          :
          i|    ;    :   .     :         :          :
          t|   ;     :      ' ":""""""""":.         :
          u|  ;      :         :         : .        :
          d| ;       :         :         :   .      :
          e|.        :         :         :     ' . .:  Time
            +---------------------------------------------->
        ```

    - Harmonic content
    - Amplitude / frequency modulation

- ### Complex Sound

  - Superposition of sinusoids
  - A partial is a sinusoid used to describe a sound
  - The lowest partial is called the fundamental frequency
  - A harmonic partial is a frequency that's a multiple of the fundamental frequency
        </br> $f_{1}$ = 440,
        $f_{2}$ = 2*440 = 8880,
        $f_{3}$ = 3*440 = 1320,...
  - In harmonicity indicates a deviation from a harmonic partial

- ### Frequency modulation

  - AKA vibrato
  - Periodic variation in frequency
  - In music, used for expressive purposes

- ### Amplitude modulation

  - AKA tremolo
  - Periodic variation in amplitude
  - In music, used for expressive purposes

- ### Timbre summary

  - Multifactorial sound dimension
  - Amplitude envelop
  - Distribution of energy across partials
  - Signal modulation (frequency/amplitude)

## Audio signal

- Representation of sound
- Encodes all info we need to reproduce sound

- ### Analog Signal

  - Continuous values for time
  - Continuous values for amplitude

- ### Digital Signal

  - Sequence of discrete values
  - Data points can only take on a finite number of values

- ### Analog to digital conversion

  - Sampling
    - Locating samples
      - $t_{n} = n*T$
    - Sampling Rate
      - $s_{r} = 1/T$
      - sampling rate for CD = 44100hz
    - Nyquist frequency
      - $f_{N} = s_{r}/2$
      - Nyquist frequency for CD = 22050hz
  - Quantisation
    - Resolution = num. of bits
    - Bit depth
    - CD resolution = 16bits
    - $2^{16} = 65536$
  - Memory for 1 minute of sound
    - Sampling rate = 44100 Hz
    - Bit depth = 16 bits
        (((16 • 44,100)/10,048,576)/8)•60 = 5.49MB
  - Dynamic range
    - Difference between largest/smallest signal a system can record
    - Resolution ∝ dynamic range
  - Signal-to-quantisation-noise ratio
    - Relationship between max signal strength and quantization error
    - Correlates with dynamic range
    - $SQNR ≈ 6.02*Q$
    - $SQNR(16) ≈ 96dB$
  - Record Sound
    - Mechanical Wave (sound) -> ADC -> Digital signals
  - Produce Sound
    - Digital signals -> DAC -> Sound waves

## Types of Audio Features for ML

- ### Audio features

  - Description of sound
  - Different features capture different aspects of sound
  - Build intelligent audio systems

- ### Audio features categorization

  - Level of abstraction
    - High-level
      - Examples: instrumentation, key, chords, melody, rhythm, tempo, lyrics, genre, mood
    - Mid-level
      - Examples: pitch and beat related descriptors, such as note onsets, fluctuation patterns, MFCCs
    - Low-level
      - Examples: amplitude envelope, energy, spectral centroid, spectral flux, zero-crossing rate
  - Temporal scope
    - Instantaneous (~50ms)
    - Segment-level (seconds)
    - Global
  - Music aspect
    - Beat
    - Timbre
    - Pitch
    - Harmony
  - Signal domain
    - Time domain
      - Amplitude envelop
      - Root-mean square energy
      - Zero crossing rate
    - Frequency domain
      - Band energy ratio
      - Spectral centroid
      - Spectral flux
    - Time-frequency representation
      - Spectrogram
      - Mel-spectrogram
      - Constant-Q transform
  - ML approach
    - Traditional machine learning
      - *Amplitude envelope*
      - Root-mean square energy
      - *Zero crossing rate*
      - Band energy ratio
      - Spectral centroid
      - *Spectral flux*
      - Spectral spread
      - Spectral roll-off

      - ```[]
        Amplitude envelope       +------------------------+
        Zero Crossing rate  ====> | Tradition ML algorithm | ===> "car engine"
        Spectral flux             +------------------------+
        ```

    - Deep learning
      - Spectrogram => deep neural network => "car engine"

- ### Types of intelligent audio systems

  - DSP --------------------> rule-based systems
  - Traditional ML ---------> feature engineering
  - Deep learning ----------> automatic feature extraction

## Extraction pipeline

- ### Time-domain feature pipeline

  - Wave are converted to frames

  - ```[]
                         . .                       111
                       .     .                     110           frame 1 : sample 1  ....128
               ADC    .       .                    101 framing   frame 2 : sample 64 ....192
        Sound =====> .         .           .       100 ========> frame 3 : sample 128....256 ===> Feature computation
        wave                    .         .        011           frame 4 : sample 192....320           ⇓
                                 .       .         010             .....                             aggregation
                                  .     .          001                                           (mean, median, GMM)
                      wave          . .            000                                                  ⇓
                                                                                           feature value / vector / matrix
        GMM ----> Gaussian mixture models
    ```

- ### Frames

  - Perceivable audio chunk
    - 1 sample @44.1kHz = 0.0227ms
    - duration of 1 sample << Ear's time resolution (10ms)
  - Power of 2 num. samples
  - Typical values: 256 - 8192
    - $d_{f} = 1/s_{r}* K$
    - where
      - $d_{f}$ --> digital frequency
      - $s_{r}$ --> sampling rate
      - K --> frame size
        if $s_{r} = 44100Hz$ and $K = 512$
        then $d_{f} = 11.6ms$

- ### Frequency-domain feature pipeline

  - ```[]
                         . .                       111
                       .     .                     110           frame 1 : sample 1  ....128
               ADC    .       .                    101 framing   frame 2 : sample 64 ....192
        Sound =====> .         .           .       100 ========> frame 3 : sample 128....256 ===>  Windowing
        wave                    .         .        011           frame 4 : sample 192....320           ⇓
                                 .       .         010             .....                          Frequency graph
                                  .     .          001                                                 ⇓
                      wave          . .            000                aggregation       <===    Feature computation
                                                                    (mean, median, GMM)
                                                                           ⇓
                                                                feature value / vector / matrix
        GMM ----> Gaussian mixture models
    ```

- ### Spectral leakage

  - Processed signal isn't an integer number of periods
  - Endpoints are discontinuous
  - Discontinuities appear as high-frequency components not present in the original signal.

- ### Windowing

  - Apply windowing function to each frame
  - Eliminates samples at both ends of a frame
  - Generates a periodic signal
  - Han window: *w(k)* = 0.5•(1 - *cos(2πk/(K-1)))* , *k* ∈ Integer

    - ```[]
               1.0 _______________________________
            A      |     |     | . . |     |     |
            m  0.8 |_          .     .          _|
            p      |         .         .         |
            l  0.6 |_       .           .       _|
            i      |       .             .       |
            t  0.4 |_     .               .     _|
            u      |     .                 .     |
            d  0.2 |_   .                   .   _|
            e      |  .                       .  |
               0.0 |_____|_____|_____|_____|_____|
                   0    10    20    30    40    50
                            Sample
        ```

    - $s_{w}(k) = s(k)*w(k), k ∈ Integer$

## Time-domain audio features

- Amplitude envelop (AE)
  - Max amplitude value of all samples in a frame
  - $AE_{t} = max{k=t*k,(t+1)*K-1} s(k)$
  - Gives rough idea of loudness
  - Sensitive to outliers
  - Onset detection, music genre classification
- Root-mean-square energy (RMS)
  - RMS of all samples in a frame
  - $RMS_{t} = sqrt( (1/K)* summation {k=t•k, (t+1)*K-1} *s(k)^{2})$
  - Indicator of loudness
  - Less sensitive to outliers than AE
  - Audio segmentation, music genre classification
- Zero-crossing rate (ZCR)
  - Number of times a signal crosses the horizontal axis
  - Used in speech recognition, music info retrieval
  - $ZCR_{t} = 0.5 * summation {k=t*k, (t+1)*K-1} | sgn(s(k)) - sgn(s(k+1))|$
    - sign function :
      - s(k) > 0 --> +1
      - s(k) < 0 --> -1
      - s(k) = 0 -->  0
  - Applications
    - Recognition of percussive vs pitched sounds
    - Monophonic pitch estimation algorithm
    - Voice/unvoiced decision for speech signals
