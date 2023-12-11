# FFlonk verifier

A rust implementation of Polygon's FFlonk verifier for CDK prover. That's not a generic implementation but
use the specific constants from the solidity contract. The proof is 732 bytes (24 big-endian unsigned 256
bits integers) and the expected public input is 32 bytes (a big-endian unsigned 256 bits integer). To build 
the proof and public input from the raw bytes you can use the implemented `TryFrom` trait.

The solidity reference implementation from Polygon
[is in solidity](https://github.com/0xPolygonHermez/zkevm-contracts/blob/53e95f3a236d8bea87c27cb8714a5d21496a3b20/contracts/verifiers/FflonkVerifier.sol)


## Usage

```rust
use fflonk_verifier::{Proof, Public};
# use hex_literal::hex;

let data = hex!(
    r#"
    1592b15070ee070dcec2a5e1e20a020976a21df73165ae5e462aa8d8b41c5323
    2cb15a95b1fe542bfb52320223dbbd9c9637404752880456f97ae718baf60f93
    0dcf1e0d545fb4684facd1009e5bbdd63a0220a2bb57bfdabb66199b1081c11a
    016314a75659deb23bf5252d4a6eea02120c8cf951116fb88d5d8524fe1da94b
    1f924a36446ef0bee0529d5f16cebedfe4eff9c004dac713546c8b817a227e06
    181c39853bb47989464a289ec5150230b6dea91ba8f34ab05b8363a6bd3f1795
    0c676f4dac5690b05695d332b6287cb4e4c39cc40ca24545218f960528dc0823
    0ed29ae6c74ac6e7fa7ecbb16cd796b4cd4d65ce2cca0b434e97af0cc442ff96
    090c4ff97cb0d01ee2b1a6396149e407c115920bf3956009b2a3cd6832b66dfa
    2fca50be168b4ce837e93ea419b521e8cbf0c3b5b72e9d85c072e82b5f619f91
    065fa71d25e993865bf9883fcf0c91f54411b1c97ada45c3e25c0caae389c647
    0188d5441830ba5e88f1f40e9beaa8127bda5ecea61eab1f3a3830c705bfab96
    1fb344c4278f0189db466b91fd12ce63d5e9152fe1bab6d26be79bb2bc64d880
    05dc42697d566da181418c12f6355ad050c5d4f4237fbb3d9d23643c27e12ba3
    236c777c03450f05e48de21b65b2ca0df1e368609bdb94e17b88e21f13e34faf
    01c8afe9bf70777b0ff54bef8b45ab992ef240e9f267529731803e2b467359e4
    12f892b9ece35a8756ebee70d80788dfe63b0a08cd554b2a003289a477a4cf12
    23b237b76cc10a9ee7c720628e544ba46d86bdb698c25f5b59c4bd14e66e2908
    0e5d909645d14fe84ae66ac8dfdfa6e1bbb83b7ac077079a9302a63a74c5b0e0
    29047525f5135a81ad5d9f5ce772700237267e0ab908290388ee060f19a6ee0e
    303db43e2056580294a4903ad98315c70243e22a96324e6088fa9c2346e85683
    2a5e0ce958c211bce2e2979b8b78155756ec8cc3142a7b9a83909b0050b7272a
    251568ac1942b1d3da24c87a6324d05e073b22692266b4d47aa24a76bd70b176
    0ad1ac8436349d96a39d916638b6426d8b9b43e126478383ac5e6e0732d7910f
"#
);
let proof = Proof::try_from(&data).unwrap();
let pubs = hex!("2bb635ee7d9e1790de1d6ccec2d1e13dec5c4beffd75d71520107c791857c45e").into();

proof.verify(pubs).unwrap();
```
