# Audio Signal Processing for Machine Learning  

## Applications
- Audio classification
- Speech recognition / speaker verification
- Audio denoising / audio upsampling
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
- Preprocess audio data for ML
- Understand (some!) math behind audio transformations 
- Use librosa for your audio projects

## Sound
- Produced by vibration of an object
- Vibrations cause air molecules to oscillate
- Change in air pressure creates a wave
- ### Mechanical wave
    - Oscillation that travels through space
    - Energy travels from one point to another
    - The medium is deformed
- ### Waveform
    - Carries multifactorial information:
        - Frequency 
        - Intensity
        - Timbre
    - y(t) = A *sin*(2πft + φ)
- ### Periodic and aperiodic sound
    - All Waveforms
        - Periodic
            - Simple (Single Sinewavess)
            - Complex (Multiple Sinewaves)
        - Aperiodic
            - Continous (Noise)
            - Transient (Pulse)
- ### Hearing Range
    Hearing range | Range
    --------------|-------------
    Elephant    | 14 - 12000Hz
    Human       | 20 - 20000Hz
    Cats        | 48 - 75000Hz
    Dogs        | 64 - 45000Hz
    Mouse       | 1000 - 70000Hz
    Bat         | 7000 - 200000Hz
- ### Pitch
    - Logarithmic perception
    - 2 frequencies are perceived similarly if they differ by a power of 2
- ### Mapping pitch to frequency
    - F(p) = 2<sup>(p-69)/12</sup> x 400
    - F(60) = 2<sup>(60-69)/12</sup> x 440 = 261.6
    - F(p+1)/F(p) = 2<sup>(1/12)</sup> = 1.059
- ### Cents
    - Octave divided in 1200 cents
    - 100 cents in a semitone
    - Noticeable pitch difference: 10-25 cents

## Features of Sound
- ### Sound Power
    - Rate at which energy is trasferred
    - Energy per unit of time emmited by a sound source
    - Measured in watt
- ### Sound Intensity
    - Sound power per unit area
    - Measured in W/m<sup>2</sup>
- ### Thresholds
    - Human can perceive sound with very small intensities.
    - Threshold of Hearing (TOH) = 10<sup>-12</sup>W/m<sup>2</sup>
    - Threshold of pain (TOP) = 10•W/m<sup>2</sup>
- ### Intensity level
    - Logarithmic scale
    - Measured in decibels (dB)
    - Ratio between two intensity values
    - Use an intensity of reference (IOR)
    - *dB(I)* = 10•*log<sub>10</sub>(I/I<sub>TOH</sub>)*
    - *dB(I<sub>TOH</sub>)* = 10•*log<sub>10</sub>(I<sub>TOH</sub>/I<sub>TOH</sub>)* = 0
    - Every ~3dBs, intensity doubles.
    - Source                    | Intensity           | Intensity level | xTOH
      --------------------------|---------------------|-----------------|-------
      Threshold of hearing(TOH) | 10<sup>-12</sup>    | 0dB    |  1
      Whisper                   | 10<sup>-10</sup>    | 20dB   | 10<sup>2</sup>
      Pianissimo                | 10<sup>-8</sup>     | 40dB   | 10<sup>4</sup>
      Normal conversation       | 10<sup>-6</sup>     | 60dB   | 10<sup>6</sup>
      Fortissimo                | 10<sup>-2</sup>     | 100dB  | 10<sup>10</sup>
      Threshold of pain         | 10<sup></sup>       | 130bB  | 10<sup>13</sup>
      Jet take-off              | 10<sup>2</sup>      | 140dB  | 10<sup>14</sup>
      Instant perforation of eardrum | 10<sup>4</sup> | 160dB  | 10<sup>16</sup>
- ### Loudness
    - Subjective perception of sound intensity
    - Depends on duration / frequency of a sound
    - Depends on age
    - Measured in phons
- ### Equal loudness contours
    <pre>
        <img style="background-color: black" height="400px" width="auto" src="https://canadianaudiologist.ca/wp-content/uploads/2016/03/Figure-1-3.png" /></pre>

- ### Timbre
    - Colour of sound
    - Diff between two sounds with same intensity, frequency, duration
    - Described with words like: bright, dark, dull, harsh, warm
    - Features of Timbre
        - Timbre is multidimensional
        - Sound envelope
            - Attack - Decay - Sustain - Release Model
            <br><pre font-family="Cascadia Code">
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
            </pre>
        - Harmonic content
        - Amplitude / frequency modulation
- ### Complex Sound
    - Superposition of sinusoids
    - A partial is a sinusoid used to describe a sound
    - The lowest partial is called the fundamental frequency
    - A harmonic partial is a frequency that's a multiple of the fundamental frequency
        <br> *f<sub>1</sub>* = 440,
        *f<sub>2</sub>* = 2•440 = 8880,
        *f<sub>3</sub>* = 3•440 = 1320,...
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
