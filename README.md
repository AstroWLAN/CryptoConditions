# Crypto Conditions
> Project for the Network Security and Cryptography course A.Y. 2022/2023 @Polimi

| Author 👨🏼‍💻 | Link 🌍 | Colaboratory 🧫 | Version 📐 | Language 🐍 | 
| :--- | :--- | :--- | :--- | :--- |
| Dario Crippa | [Paper](https://datatracker.ietf.org/doc/html/draft-thomas-crypto-conditions-04) | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/AstroWLAN/CryptoConditions/blob/main/Crypto_Conditions.ipynb) | `1.0.0` | `python` |

## Abstract 💭
The Crypto Conditions specification introduces a way to combine existing signature schemes or hashing algorithms in order to create a more robust signing system while still retaining the benefits of a simpler approach
> In particular a deterministic algorithm to verify the signature still exists

Existing cryptographic primitives like SHA256 or signature schemes such as ED25519 can be used as logic gates to build intricate boolean circuits that can later be used as composite signatures

### Fulfillment 📦
The fulfillment $F$ represents the **circuit definition** and the minimum required logic gates with their inputs
> For most condition types the fingerprint is a cryptographically secure hash of the data which defines the condition such as a public key


```markdown
PreimageSHA256 
Fulfillment ::= SEQUENCE {
    preimage             OCTET STRING
}

ThresholdSHA256
Fulfillment ::= SEQUENCE {
    subfulfillments      SET of fulfillments
    subconditions        SET of conditions
}

ED25519 SHA256
Fulfillment ::= SEQUENCE {
    publicKey            OCTET STRING (size(32))
    signature            OCTET STRING (size(64))
}
```

### Condition 🔦
The condition $C$ represents the **fingerprint** of the circuit and includes some metadata like the cost of the Crypto Condition format
> For most condition types the fingerprint is a cryptographically secure hash of the data which defines the condition such as a public key


```markdown
SimpleCondition Condition ::= {
    fingerprint    OCTET STRING (size(32))
    cost           INTEGER
}

CompoundCondition Condition ::= {
    fingerprint    OCTET STRING (size(32))
    cost           INTEGER
    subtypes       ConditionTypes
}
```
