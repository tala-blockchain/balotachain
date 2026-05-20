# tala-crypto

Canonical Rust cryptography for Tala and BalotaChain lives here. The crate is
organized around ristretto255 group operations, Merlin transcripts for
Fiat-Shamir transforms, threshold ElGamal, DKG, commitments, Benaloh challenge
helpers, and NIZK proof modules.

The implementation treats constant-time behavior as part of the public contract:
secret-dependent branches, secret-dependent memory access, and early exits on
secret values are not allowed.

