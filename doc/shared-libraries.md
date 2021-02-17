Shared Libraries
================

## spiffcoinconsensus

The purpose of this library is to make the verification functionality that is critical to Bitcoin's consensus available to other applications, e.g. to language bindings.

### API

The interface is defined in the C header `spiffcoinconsensus.h` located in `src/script/spiffcoinconsensus.h`.

#### Version

`spiffcoinconsensus_version` returns an `unsigned int` with the API version *(currently `1`)*.

#### Script Validation

`spiffcoinconsensus_verify_script` returns an `int` with the status of the verification. It will be `1` if the input script correctly spends the previous output `scriptPubKey`.

##### Parameters
- `const unsigned char *scriptPubKey` - The previous output script that encumbers spending.
- `unsigned int scriptPubKeyLen` - The number of bytes for the `scriptPubKey`.
- `const unsigned char *txTo` - The transaction with the input that is spending the previous output.
- `unsigned int txToLen` - The number of bytes for the `txTo`.
- `unsigned int nIn` - The index of the input in `txTo` that spends the `scriptPubKey`.
- `unsigned int flags` - The script validation flags *(see below)*.
- `spiffcoinconsensus_error* err` - Will have the error/success code for the operation *(see below)*.

##### Script Flags
- `spiffcoinconsensus_SCRIPT_FLAGS_VERIFY_NONE`
- `spiffcoinconsensus_SCRIPT_FLAGS_VERIFY_P2SH` - Evaluate P2SH ([BIP16](https://github.com/spiffcoin/bips/blob/master/bip-0016.mediawiki)) subscripts
- `spiffcoinconsensus_SCRIPT_FLAGS_VERIFY_DERSIG` - Enforce strict DER ([BIP66](https://github.com/spiffcoin/bips/blob/master/bip-0066.mediawiki)) compliance
- `spiffcoinconsensus_SCRIPT_FLAGS_VERIFY_NULLDUMMY` - Enforce NULLDUMMY ([BIP147](https://github.com/spiffcoin/bips/blob/master/bip-0147.mediawiki))
- `spiffcoinconsensus_SCRIPT_FLAGS_VERIFY_CHECKLOCKTIMEVERIFY` - Enable CHECKLOCKTIMEVERIFY ([BIP65](https://github.com/spiffcoin/bips/blob/master/bip-0065.mediawiki))
- `spiffcoinconsensus_SCRIPT_FLAGS_VERIFY_CHECKSEQUENCEVERIFY` - Enable CHECKSEQUENCEVERIFY ([BIP112](https://github.com/spiffcoin/bips/blob/master/bip-0112.mediawiki))
- `spiffcoinconsensus_SCRIPT_FLAGS_VERIFY_WITNESS` - Enable WITNESS ([BIP141](https://github.com/spiffcoin/bips/blob/master/bip-0141.mediawiki))

##### Errors
- `spiffcoinconsensus_ERR_OK` - No errors with input parameters *(see the return value of `spiffcoinconsensus_verify_script` for the verification status)*
- `spiffcoinconsensus_ERR_TX_INDEX` - An invalid index for `txTo`
- `spiffcoinconsensus_ERR_TX_SIZE_MISMATCH` - `txToLen` did not match with the size of `txTo`
- `spiffcoinconsensus_ERR_DESERIALIZE` - An error deserializing `txTo`
- `spiffcoinconsensus_ERR_AMOUNT_REQUIRED` - Input amount is required if WITNESS is used
- `spiffcoinconsensus_ERR_INVALID_FLAGS` - Script verification `flags` are invalid (i.e. not part of the libconsensus interface)

### Example Implementations
- [NBitcoin](https://github.com/MetacoSA/NBitcoin/blob/5e1055cd7c4186dee4227c344af8892aea54faec/NBitcoin/Script.cs#L979-#L1031) (.NET Bindings)
- [node-libspiffcoinconsensus](https://github.com/bitpay/node-libspiffcoinconsensus) (Node.js Bindings)
- [java-libspiffcoinconsensus](https://github.com/dexX7/java-libspiffcoinconsensus) (Java Bindings)
- [spiffcoinconsensus-php](https://github.com/Bit-Wasp/spiffcoinconsensus-php) (PHP Bindings)
