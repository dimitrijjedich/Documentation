# AWS EC2 KeyPair

A key pair, consisting of a public key and a private key, is a set of security credentials that you use to prove your identity when connecting to an Amazon EC2 instance. For Linux instances, the private key allows you to securely SSH into your instance. For Windows instances, the private key is required to decrypt the administrator password, which you then use to connect to your instance.

Amazon EC2 stores the public key on your instance, and you store the private key. It's important that you store your private key in a secure place because anyone who possesses your private key can connect to your instances that use the key pair. Additionally it is not possible to retrieve the key again.

### Creating a KeyPair
You can use Amazon EC2 to create your key pairs, or you can use a third-party tool to create your key pairs, and then import them to Amazon EC2.

Amazon EC2 supports 2048-bit SSH-2 RSA keys for Linux and Windows instances. Amazon EC2 also supports ED25519 keys for Linux instances.

```bash
aws ec2 create-key-pair \
    --key-name my-key-pair \
    --key-type rsa \
    --key-format pem \
    --query "KeyMaterial" \
    --output text > my-key-pair.pem
```

`--key-name` A unique name for the key pair. Constraints: Up to 255 ASCII characters
`--key-type` Possible values: `rsa` or `ed25519` with `rsa` being the default
`--key-format` Possible values: `pem` or `ppk` with `pem` being the default
`--query` #TODO
`--output`  Possible values: `json`, `text` or `table`. The formatting style for command output.

### Describing a KeyPair
You can view the following information about your public keys that are stored in Amazon EC2: public key name, ID, key type, fingerprint, public key material, the date and time (in the UTC time zone) the key was created by Amazon EC2 (if the key was created by a third-party tool, then it's the date and time the key was imported to Amazon EC2), and any tags that are associated with the public key.

```bash
aws ec2 describe-key-pairs
```
`--key-names <value>` Allows to filter keys by name
`--key-pair-ids <value>` Allows to filter keys by id
The filter parameter are optional. Without them the output will contain all keys

### Deleting a KeyPair
```bash
aws ec2 delete-key-pair
```
To identify the key pair to delete, there are two option:
`--key-name` followed by the value
`--key-pair-id` followed by the value

### Import a KeyPair
It is possible to add a locally generated key to AWS using the following command:
```bash
aws ec2 import-key-pair --key-name "my-key" --public-key-material fileb://~/.ssh/my-key.pub
```
`--key-name` A unique name for the key pair. Constraints: Up to 255 ASCII characters
`--public-key-material` The public key. For API calls, the text must be base64-encoded. For command line tools, base64 encoding is performed for you.
