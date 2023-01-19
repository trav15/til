# Key Management Service (KMS)

**KMS custom key store** feature combines the controls provided by AWS CloudHSM with the integration and ease of use of AWS KMS. *You can configure your own CloudHSM cluster and authorize AWS KMS to use it as a dedicated key store for your keys rather than the default AWS KMS key store*. When you create keys in AWS KMS you can choose to generate the key material in your CloudHSM cluster. CMKs that are generated in your custom key store never leave the HSMs in the CloudHSM cluster in plaintext and all AWS KMS operations that use those keys are only performed in your HSMs.

A **key policy** is a resource policy for an AWS KMS key. Key policies are the primary way to control access to KMS keys. Every KMS key must have exactly one key policy. The statements in the key policy determine who has permission to use the KMS key and how they can use it. You can also use IAM policies and grants to control access to the KMS key, but every KMS key must have a key policy.

Unless the key policy explicitly allows it, you cannot use IAM policies to allow access to a KMS key. Without permission from the key policy, IAM policies that allow permissions have no effect. (You can use an IAM policy to deny permission to a KMS key without permission from a key policy.) *The default key policy enables IAM policies*. To enable IAM policies in your key policy, add the policy statement described [here](https://docs.aws.amazon.com/kms/latest/developerguide/key-policy-default.html#key-policy-default-allow-root-enable-iam).

## Envelope Encryption

Your data is protected when you encrypt it, but you have to protect your encryption key. One strategy is to encrypt it. Envelope encryption is the practice of encrypting plaintext data with a data key and then encrypting the data key under another key.

You can even encrypt the data encryption key under another encryption key and encrypt that encryption key under another encryption key. But, eventually, ***one key must remain in plaintext so you can decrypt the keys and your data. This top-level plaintext key-encryption key is known as the master key.***

### Protecting data keys

When you encrypt a data key, you don’t have to worry about storing the encrypted data key, because the data key is inherently protected by encryption. You can safely store the encrypted data key alongside the encrypted data.

### Encrypting the same data under multiple master keys

Encryption operations can be time-consuming, particularly when the data being encrypted are large objects. Instead of re-encrypting raw data multiple times with different keys, you can re-encrypt only the data keys that protect the raw data.

### Combining the strengths of multiple algorithms

In general, symmetric key algorithms are faster and produce smaller ciphertexts than public-key algorithms. But public-key algorithms provide inherent separation of roles and easier key management. Envelope encryption lets you combine the strengths of each strategy.

To perform envelope encryption using KMS keys, you must first generate a data key using your KMS key and use its plaintext version to encrypt data.


## *Resources*

- [Tutorials Dojo KMS Cheat Sheet](https://tutorialsdojo.com/aws-key-management-service-aws-kms/)