# Crypto Conditions
> Project for the Network Security and Cryptography course A.Y. 2022/2023 @Polimi

| Author 👨🏼‍💻 | Link 🌍 | Colaboratory 🧫 | Version 📐 | Language 🐍 | 
| :--- | :--- | :--- | :--- | :--- |
| Dario Crippa | [Paper](https://datatracker.ietf.org/doc/html/draft-thomas-crypto-conditions-04) | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/AstroWLAN/CryptoConditions/blob/main/Crypto_Conditions.ipynb) | `1.0.0` | `python` |

## Abstract 💭
Crypto conditions define a set of encoding formats and data structures used to describe conditions and fulfillments
> Method for combining signature mechanisms and hash functions to create **sophisticated signature arrangements** that can <br> self-validate based on specific conditions

These schemes are often adopted in the realm of blockchain and cryptocurrencies to create rules and standards for conducting transactions or manage smart contracts<br>
> Crypto conditions enable the **definition of requirements** that must be met before an operation or a transaction can be considered valid

Primitives like `SHA256` or signature schemes such as `Ed25519` can be used as logic gates to build intricate boolean circuits that can later be used as composite signatures<br>
> The term **circuit** refers to a set of logical and cryptographic operations that determine whether a given condition is satisfied

### Condition 🔦
A condition $C$ represents the fingerprint of a particular circuit<br>
> In most cases it is the **hash digest** of the data that represents the condition

Agents can define a condition that must be satisfied in order for a particular action or transaction to occur<br>
> Each condition **identifies a circuit** composed of one or more logic gates that will be evaluated by validating a signature or checking the digest of an hash function

 ```markdown
Condition ::= CHOICE {
    PreimageSHA256     [0]  SimpleSHA256Condition 
    PrefixSHA256       [1]  CompoundSHA256Condition
    ThresholdSHA256    [2]  CompoundSHA256Condition
    RSASHA256          [3]  SimpleSHA256Condition 
    Ed25519SHA256      [4]  SimpleSHA256Condition 
}

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
    PreimageSHA256     (0)
    PrefixSHA256       (1)
    ThresholdSHA256    (2)
    RSASHA256          (3)
    Ed25519SHA256      (4)
}
```

### Fulfillment 📦
The fulfillment $F$ represents the input given to a circuit 
> Data structure that holds the **information required** to satisfy a condition

It constitutes the cryptographic proof or evidence provided to validate the condition
> The **internal structure** depends on the crypto condition format chosen

```markdown
Fulfillment ::= CHOICE {
    preimageSha256     [0]    PreimageFulfillment
    prefixSha256       [1]    PrefixFulfillment
    thresholdSha256    [2]    ThresholdFulfillment
    rsaSha256          [3]    RsaSha256Fulfillment
    ed25519Sha256      [4]    Ed25519Sha256Fulfillment
}

# EXAMPLES

PreimageSHA256
PreimageFulfillment ::= SEQUENCE {
    preimage    OCTET STRING
}

ThresholdSHA256
ThresholdFulfillment ::= SEQUENCE {
    subfulfillments    SET of fulfillments
    subconditions      SET of conditions
}

Ed25519SHA256
Ed25519Sha256Fulfillment ::= SEQUENCE {
    publicKey    OCTET STRING (size(32))
    signature    OCTET STRING (size(64))
}
```

### Validation 🔑
A provided fulfillment is considered valid if it matches the circuit fingerprint which is another way of saying that the condition is satisfied
> It is possible to include an optional input message for evaluating the whole fulfillment


## Experiments 🧪
The linked Google Colab contains some practical experiments with various types of the crypto conditions 
