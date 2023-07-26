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
      Aircrack-ng   | DaveGrahl  | John the ripper
      --------------|------------|-----------------
      Cain and Abel | Hashcat    | Rainbowcrack
      Crack         | Hydra      | Ophcrack
    - To prevent brute force attack on login/sign up pages `captcha` are used.
      -`Captcha` is a contrived acronym for "Completely Automated Public Turing test to tell Computers are Human Apart"
