# Crypto Conditions
> Project for the Network Security and Cryptography course A.Y. 2022/2023 @Polimi

| Author 👨🏼‍💻 | Link 🌍 | Colaboratory 🧫 | Version 📐 | Language 🐍 | 
| :--- | :--- | :--- | :--- | :--- |
| Dario Crippa | [Paper](https://datatracker.ietf.org/doc/html/draft-thomas-crypto-conditions-04) | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/AstroWLAN/CryptoConditions/blob/main/Crypto_Conditions.ipynb) | `1.0.0` | `python` |

## Abstract 💭
The crypto conditions specification introduces a method to combine existing signature schemes or hashing algorithms<br>
This allows for the creation of more **complex signature arrangements** while still retaining the benefits of simpler approaches
> For example the signature is still verified using a deterministic algorithm 

These schemes are commonly used in the realm of blockchain and cryptocurrencies to establish guidelines and criteria for conducting transactions or smart contracts<br>
> In simpler terms crypto conditions allow for the specification of requirements that must be met before an operation or transaction can be considered valid

Cryptographic primitives like SHA256 or signature schemes such as ED25519 can be used as logic gates to build intricate boolean circuits that can later be used as composite signatures<br>
> Different types of crypto conditions each have different internal structures

### Condition 🔦
The condition $C$ represents the **fingerprint** of the circuit<br>
> For most condition types the fingerprint is a cryptographically secure hash of the data which defines the condition such as a public key

Users or developers define a set of conditions that need to be satisfied for a particular action or transaction to occur<br>
> A condition identifies a logical boolean circuit constructed from one or more logic gates evaluated by either validating a cryptographic signature or verifying the preimage of an hash digest

 ```markdown
SimpleSHA256Condition 
Condition ::= SEQUENCE {
    fingerprint    OCTET STRING (size(32))
    cost           INTEGER
}

CompoundSHA256Condition 
Condition ::= SEQUENCE {
    fingerprint    OCTET STRING (size(32))
    cost           INTEGER
    subtypes       ConditionTypes
}

ConditionTypes ::= BIT STRING {
    preImageSha256     (0)
    prefixSha256       (1)
    thresholdSha256    (2)
    rsaSha256          (3)
    ed25519Sha256      (4)
}
```

### Fulfillment 📦
The **fulfillment** $F$ is a data structure that represents the **circuit definition** and the minimum required logic gates with their inputs
> Circuit structure depends on the encoded cryptographic signature schemas or hash digest preimages 

It represents the cryptographic proof or evidence provided to satisfy the conditions specified in a crypto-condition

```markdown
Fulfillment ::= CHOICE {
    preimageSha256     [0]    PreimageFulfillment
    prefixSha256       [1]    PrefixFulfillment
    thresholdSha256    [2]    ThresholdFulfillment
    rsaSha256          [3]    RsaSha256Fulfillment
    ed25519Sha256      [4]    Ed25519Sha256Fulfillment
}

PreimageSHA256
PreimageFulfillment ::= SEQUENCE {
    preimage    OCTET STRING
}

ThresholdSHA256
ThresholdFulfillment ::= SEQUENCE {
    subfulfillments    SET of fulfillments
    subconditions      SET of conditions
}

ED25519SHA256
Ed25519Sha256Fulfillment ::= SEQUENCE {
    publicKey    OCTET STRING (size(32))
    signature    OCTET STRING (size(64))
}
```

### Validation 🔑
A fulfillment is considered valid when both the circuit output is `true` and the provided fulfillment matches the circuit fingerprint which is another way of saying that the condition is satisfied
> Since the evaluation of certain logic gates in the circuit requires a message as input it is possible to include an optional input message for evaluating the whole fulfillment

## Experiments 🧪
The linked Google Colab contains some practical experiments with various types of the crypto conditions 
