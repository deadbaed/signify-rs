# Signify - Ed25519 signature tool

[![crates.io](https://img.shields.io/crates/v/signify.svg?style=flat-square)](https://crates.io/crates/signify)
[![docs.rs docs](https://img.shields.io/badge/docs-latest-blue.svg?style=flat-square)](https://docs.rs/libsignify)
[![License: MIT](https://img.shields.io/github/license/badboy/signify-rs?style=flat-square)](LICENSE)
[![Build Status](https://img.shields.io/github/workflow/status/badboy/signify-rs/CI/main?style=flat-square)](https://github.com/badboy/signify-rs/actions/workflows/ci.yml)

Create cryptographic signatures for files and verify them.
This is based on [signify][], the OpenBSD tool to sign and verify signatures on files.
It is based on the [Ed25519 public-key signature system][ed25519] by Bernstein et al.

`signify-rs` verifies signatures generated by BSD signify and signs data in a format that BSD signify can verify.  
You can read more about the ideas and concepts behind `signify` in [Securing OpenBSD From Us To You](https://www.openbsd.org/papers/bsdcan-signify.html).

## Installation

```
cargo install signify
```

## Usage

Create a key pair:

```
signify -G -p pubkey -s seckey
```

Sign a file using the secret key:

```
signify -S -s seckey -m README.md
```

Verify the signature:

```
signify -V -p pubkey -m README.md
```

## Testing

Currently, there are no unit tests. :disappointed:  
But we ensure that a full cycle of generating a keypair, then signing & verifying works.
To do so:

    ./tests/full-cycle.sh

For correctness, we compare interoperability with the OpenBSD `signify`:

    ./tests/compare.sh
    

## Limitations

* ~~No embedded signatures~~
* ~~No password-protection for secret keys~~

Both things will be implemented eventually.
I also accept PRs.

## License

MIT. See [LICENSE](LICENSE).

[signify]: https://github.com/aperezdc/signify
[ed25519]: https://ed25519.cr.yp.to/
