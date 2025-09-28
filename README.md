# DDE
Dynamic Dictionary Encryption

Project: Implementation of a dynamic dictionary-based message encryption system with multi-tokens and dictionary updates after each message.
Date: 2025.28.09

---

## Description

Dynamic Dictionary Encryption (DDE) is a method for encoding messages that combines:

* **Local dynamic dictionary**
  Each word, character, or phrase has one or more fixed-length tokens. The dictionary resides **only in RAM** and is never transmitted.

* **Multi-tokens for randomness**
  A single dictionary entry can have multiple tokens. When encoding, a random token is selected, making repeated messages unique.

* **Dynamic dictionary updates**
  After sending each message, the dictionary is updated — new tokens are added, old tokens are shuffled or replaced — to prevent repetition in token streams.

* **Fixed token length**
  All tokens have the same length, hiding the structure of the text and preventing leakage of word or phrase lengths.

* **Message compression**
  Frequently used words and phrases are replaced by short tokens, reducing the volume of transmitted data.

* **Optional cryptographic encryption**
  The token stream can be further encrypted using AES or ChaCha20 for additional security.

---

## How It Works

1. Split the original message into words/phrases.
2. For each dictionary entry, select a random token from its set of possible tokens (multi-token).
3. Replace the entries with tokens → forming the encoded token stream.
4. Send the token stream to the recipient.
5. After sending, update the local dictionary (add new tokens, shuffle existing ones).
6. The recipient uses their local dictionary to decode the token stream back into the original message.

---

## Example

Original message:

```
hello, how are you?
```

Dictionary:

```
"hello" → [8sd1gnht, q7f2k1l9]  
"how are you?" → [x7kp0dnl, j3v9s1rt]
```

Encoding:

```
"hello, how are you?" → "q7f2k1l9 j3v9s1rt"
```

After sending, the dictionary is updated — new tokens are generated for subsequent messages.

---

## How It Works (Diagram)

Original Message → Tokenization → Multi-Token Selection → Encoded Stream → Send → Recipient Decoding → Dictionary Update

---

## Features

* Fully local dictionary storage → high security.
* Dynamic dictionary updates → every message is unique.
* Multi-tokens → statistical analysis of token streams is useless.
* Fixed token length → hides text structure.
* Message compression and reduced data transmission size.

---

## Use Cases

- Secure local chat applications
- Encrypted IoT messaging
- Compressed communication for low-bandwidth networks
- Educational demonstration of dynamic encryption concepts

---

## License

This project is released under the **MIT License** — free to use, modify, and distribute with attribution.

---
