# Cryptography and Network Security

## Syllabus

1. Introduction to Cryptography
2. Mathematical Background - Abstract Algebra & Number Theory
3. Block Ciphers
4. Public Key Cryptography
5. Cryptographic Hash functions and Digital Signatures
6. Security Practices and System Security
7. Email, IP and Web Security

## Introduction to Cryptography

### CIA Tried

![cia_triad](/images/cia_triad.svg)

- CIA Triad
  - Confidentiality
    - Example : Account information
  - Integrity
    - Example : Patient's information
  - Availability
    - Example : Authentication service
  </br></br>Additional
    - Authenticity
    - Accountability

- `Computer Security` - The protection afforded to an automated information system in order to attain applicable objectives of preserving the integrity, availability and confidentiality of information system resources (include hardware software, firmware information/ data and telecommunications).

Threats and Attack (RFC 2828)

- `Threat`: A potential for violation of security, which exists when there is a circumstance, capability, action or an event that could breach security and cause harm. That is a threat Is it possible danger that might exploit a vulnerability.
- `Attack`: An assault on system security that drives from an intelligence read that is an intelligent act that is deliberately attempt (especially in the sense of a method or technique) to evade security services and violate the security policy of a system.

### OSI security architecture

- `Security Attack` : Action that compromises the security of an individual or an organization.
  - `Passive Attacks` : Attempts to learn or make use of information from the system.
    - Does not affect system resources.
    - Eavesdropping or monitoring of transmissions.
    - Goal: Obtain information that is being transmitted.
    - Types:
      - Release of message contents
      - Traffic Analysis
  - `Active attack` : Active attacks involve some modification of the data stream or the creation of a false stream.
    - Subdivide into four categories.
      1. Masquerade : Pretending to be someone else.
      2. Replay : Capture from source and later replay to destination.
      3. Modification of messages : Capture from source and modifies the messages.
      4. Denial of Service (DoS) : Denies data from the server.
  - Passive attack vs Active Attack
    - Passive Attack
      - Hard to Detect
      - Neither sender nor receiver is aware of the attack
      - Encryption prevents the success of the passive attacks
      - More emphasis is on prevention than detection.
    - Active Attack
      - Hard to Prevent
      - Difficult to prevent - Physical, software and network vulnerabilities.
      - Detect and recover from any disruption or delays.
      - If the detection has a deterrent effect, it may also contribute to prevention.
- `Security Mechanism` : Detect, prevent, or recover from a security attack.
  - `Specific security mechanisms`
    - `Encipherment`
    - `Digital Signature`
    - `Access Control`
    - `Data Integrity`
    - `Authentication Exchange`
    - `Traffic Padding`
    - `Routing Control`
    - `Notarization` : Deployment of trusted 3rd party authority.
  - `Pervasive security mechanism`
    - `Trusted Functionality`
    - `Security Label`
    - `Event Detection`
    - `Security Audit Trail`
    - `Security Recovery`
- `Security Service` : The processing or communication service that is provided by a system to give a specific kind of protection to system resources, security services, implement security policies and are implemented by security mechanism.
  - `Authentication` : The process of verifying a user or device before allowing access to a system or resources
    - Peer entity authentication : The process of verifying that a peer entity in an association is as claimed.
    - Data origin authentication : Also known as message authentication, data origin authentication is an assurance that the source of the information is indeed verified.
  - `Access control` : Access control is a data security process that enables organizations to manage who is authorized to access corporate data and resources.
  - `Data confidentiality` : The protection of data from unauthorized access and disclosure.
  - `Data Integrity` : The overall accuracy, completeness, and consistency of data.
  - `Non repudiation` : The assurance that someone cannot deny the validity of data.

### Model for Network Security

![model_ns_1](/images/model_ns_1.png)

- Design an algorithm
- Generate the secret information
- Develop methods for distribution and sharing of information
- Specify a protocol

![model_ns_2](/images/model_ns_2.png)

### Cryptography

![model_crypt](/images/encryption.png)

- The art or science encompassing the principles and methods of transforming an intelligible message into that is unintelligible and then re-transforming that message back to its original form.
- Types of Cryptography
  - Symmetric Cryptography (Private Key Cryptography) : Same key are used for both encryption and decryption.
  - Asymmetric Cryptography (Public Key Cryptography) : Different key are used for both encryption and decryption.
- Encryption schemes
  - Unconditionally secure
  - Computationally secure
- Key Terms
  - `Plaintext` : Any useful data used, which can be easily understood manually or through softwares.
  - `Ciphertext` : Encrypted  plain text is called ciphertext.
  - `Cipher` (Encryption Algorithm) : It convert plaintext to ciphertext.
  - `Key` : The most important data used to encrypt and decrypt the plain text.
  - `Cryptanalysis` (code breaking) : To know the text being transmitted using hit and trial of algorithm.
  - `Cryptology` : Cryptography + Cryptanalysis

### Attacks

- General approaches to attack conventional schemes
  - `Cryptanalysis attacks` : Based on info know to the cryptanalyst

     Types of cryptanalytic attacks | Known to cryptanalyst
    --------------------------------|------------------------
     Ciphertext Only   |- Encryption Algorithm </br>- Ciphertext
     Known Plain text  |- Encryption Algorithm </br>- Ciphertext </br>- One or more PT-CT pairs formed with secret key
     Chosen plaintext  |- Encryption Algorithm </br>- Ciphertext </br>- PT message chosen by cryptanalyst, together with its CT generated with the secret key
     Chosen Ciphertext |- Encryption Algorithm </br>- Ciphertext </br>- CT chosen by cryptanalysis, together with its corresponding decrypted PT generated with secret key
     Chosen text       |- Chosen Plaintext and Chosen Ciphertext
    - Most difficult - Cipher text only (when not even encryption algorithm is known)
  - `Brute-force attack` : A brute force attack is a hacking method that uses trial and error to crack passwords, login credentials, and encryption keys.
    - Trying every possible key.
    - Until an intelligible translation of the ciphertext into plaintext is obtained
    - Guessing
    - Exhaustive key search.
    - Software Tools that can perform brute-force attack.
    - Examples :
      Aircrack-ng   | DaveGrahl  | John the ripper
      --------------|------------|-----------------
      Cain and Abel | Hashcat    | Rainbowcrack
      Crack         | Hydra      | Ophcrack
    - To prevent brute force attack on login/sign up pages `captcha` are used.
      -`Captcha` is a contrived acronym for "Completely Automated Public Turing test to tell Computers are Human Apart"

### Classical Encryption Techniques

1. Substitution Technique
   - Letters are replaced by other letters or symbols
   - Example :
      a | b | c | d | e | f | g | h | i | j | k | l | m
     ---|---|---|---|---|---|---|---|---|---|---|---|----
      n | o | p | q | r | s | t | u | v | w | x | y | z

      Lets assume, ${a → M, b → X, x → Z, g → A}$
      </br>Plain text : bag
      </br>Ciphertext : XMA
2. Transposition Technique
   - Applying some sort of permutation on the plaintext letters.
   - Plaintext : Science
   - Ciphertext : Siencce, Csience, etc.

 Substitution                | Transposition
-----------------------------|---------------------------
 Caesar Cipher               | Rail Fence
 Monoalphabetic Cipher       | Raw Column Transposition
 Playfair Cipher             |
 Hill Cipher                 |
 Polyalphabetic Cipher       |
 One-Time Pad                |

### Shift Cipher

- Letters are replaced by other letters or symbols.
- The earlier known and simplest method used by Julius Caesar.
- Replacing each letter of the alphabet with the letter standing three places further down the alphabet.
- Example :
  0 | 01| 02| 03| 04| 05| 06| 07| 08| 09| 10| 11| 12
  --|---|---|---|---|---|---|---|---|---|---|---|----
  a | b | c | d | e | f | g | h | i | j | k | l | m

  13| 14| 15| 16| 17| 18| 19| 20| 21| 22| 23| 24| 25
  --|---|---|---|---|---|---|---|---|---|---|---|----
  n | o | p | q | r | s | t | u | v | w | x | y | z

- Algorithm :
  For each plaintext letter 'p', substitute the ciphertext letter 'C':
  - ${C = E (p,k) mod 26 = (p + k) mod 26}$
  - ${p = D (C,k) mod 26 = (C - k) mod 26}$
- Example :
  Fo k = 4
  plaintext : linux
  Ciphertext :  pmryb

- Shift Cipher with key = 3 is called Caesar Cipher
- Example :
  For k = 3 (caesar cipher)
  plaintext : academy
  Ciphertext : dfdghpb

- Pros                  | Cons
  ----------------------|----------------------------
  Simple                | The encryption & decryption algorithm are known.
  Easy to implement     | There're only 25 keys to try (Vulnerable to brute-force attack)
  _                     | The language of plaintext is known & easily recognizable.

### Monoalphabetic Cipher

- **Permutation** : A permutation of a finite set of elements 'S' is an ordered sequence of all elements of 'S', with each element appearing exactly once.
  - For example S = { a, b, c }
  - There are six permutations of S: abc, acb, bac, bca, cab, cba.
- The `cipher` line can be any **permutation** of the 26 alphabetic characters.
- This would seem to eliminate brute-force techniques for cryptanalysis.
- A single cipher alphabet (mapping from plain alphabet to cipher alphabet) is used per message.
- English language - Nature of plain text is known.
- Example:
  - plain text - Work
  - Cipher text - Eptl
- Pros                  | Cons
  ----------------------|----------------------------
  Better security than Caesar Cipher | Monoalphabetic ciphers are easy to break because they reflect the frequency data of the original alphabet.
  A countermeasure is to provide multiple substitutes known as homophones, for a single letter | Prone to guessing attack using the English letter frequency of occurrence of letters.

### Playfair Cipher

- Aka Playfair square or Wheatstone-Playfair cipher.
- Manual symmetric encryption technique.
- The first literal Digram substitution cipher.
- Invented in 1854 by Charles Wheatstone.
- Bore the name of Lord Playfair for promoting its use.
- Multiple letter encryption cipher.
- 5 x 5 matrix constructed using a keyword (Example: Monarchy)
   M | O | N | A | R
  ---|---|---|---|---
   C | H | Y | B | D
   E | F | G |I/J| K
   L | P | Q | S | T
   U | V | W | X | Z
- Rules for encryption using Playfair Cipher
  - Digrams
  - Repeating Letters - Filled letter.
  - Same Column | ${↓}$ | Wrap around.
  - Same Row | ${→}$ | Wrap around.
  - Rectangle | ${⇋}$ | Swap
- Example :
  1. Plaintext : attack
     - Digrams : at ta ck
        at | ta | ck
        ---|----|----
        rs | sr | de
     - Cipher text : rssrde

  2. Plaintext : mosque
     - Diagram : mo sq ue
        mo | sq | ue
        ---|----|----
        on | ts | ml
     - Cipher text : ontsml

  3. Plaintext : balloon
     - Digram : ba ll oo n → ba lx lo on (x is filler character)
       ba | lx | lo | on
       ---|----|----|----
       ib | su | pm | na
     - Cipher text : ibsupmna → ibspmna (ignoring filler character)

### Hill Cipher

- Multi-letter cipher
- Developed by Lester Hill 1929.
- Encrypts a group of letters: digraph, trigraph or polygraph.
- Hill Algorithm
  - This can be expressed as :
    - ${C = E(K,p) = P }$ x ${ K mod 26}$
    - ${P = D(K,C) = C }$ x ${ K^{-1} mod 26 = P}$ x ${ K }$ x ${ K^{-1} mod 26}$
  - ${(C_{1} C_{2} C_{3}) = (P_{1} P_{2} P_{3}) \left(\begin{array}{cc} K_{11} & K_{12} & K_{13}\\ K_{21} & K_{22} & K_{23} \\ K_{31} & K_{32} & K_{33}\end{array}\right) mod 26 ← Encryption}$
  
    - ${C_{1} = (P_{1}K_{11} + P_{2}K_{21} + P_{3}K_{31}) mod 26}$
    - ${C_{2} = (P_{1}K_{12} + P_{2}K_{22} + P_{3}K_{32}) mod 26}$
    - ${C_{3} = (P_{1}K_{13} + P_{2}K_{23} + P_{3}K_{33}) mod 26}$
  - Example :
    - Plaintext : pay more money
    - The alphabets are transformed into corresponding numbers in alphabets, then the encryption takes place.
    - Cipher text : rrlmwbkaspdh
