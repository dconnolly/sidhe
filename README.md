# Russh

[![Rust](https://github.com/warp-tech/russh/actions/workflows/rust.yml/badge.svg)](https://github.com/warp-tech/russh/actions/workflows/rust.yml)  <!-- ALL-CONTRIBUTORS-BADGE:START - Do not remove or modify this section -->
[![All Contributors](https://img.shields.io/badge/all_contributors-70-orange.svg?style=flat-square)](#contributors-)
<!-- ALL-CONTRIBUTORS-BADGE:END -->

Low-level Tokio SSH2 client and server implementation with opinionated crypto choices.

Examples: [simple client](russh/examples/client_exec_simple.rs), [interactive PTY client](russh/examples/client_exec_interactive.rs), [server](russh/examples/echoserver.rs), [SFTP client](russh/examples/sftp_client.rs), [SFTP server](russh/examples/sftp_server.rs).

This is a fork of [Russh](https://github.com/Eugeny/russh) by Eugeny, which was also a fork of [Thrussh](https://nest.pijul.com/pijul/thrussh) by Pierre-Étienne Meunier.

* [More panic safety](https://github.com/warp-tech/russh#safety) 
* async traits 
* `direct-tcpip` (local port forwarding)
* `forward-tcpip` (remote port forwarding) 
* `direct-streamlocal` (local UNIX socket forwarding, client only) 
* `forward-streamlocal` (remote UNIX socket forwarding) 
* Ciphers:
  * `chacha20-poly1305@openssh.com`
  * `aes128-gcm@openssh.com` 
  * `aes256-gcm@openssh.com` 
  * `aes256-ctr` 
~* `aes192-ctr`~
  * `aes128-ctr` 
~* `aes256-cbc`~
~* `aes192-cbc`~
~* `aes128-cbc`~
* Key exchanges:
  * ml-kem-only
  * hybrid x25519-mlkem
  * is there a non x25519-mlkem hybrid?  
* MACs:
  [revisit these]
  * `hmac-sha2-256` 
  * `hmac-sha2-512` 
  * `hmac-sha2-256-etm@openssh.com` 
  * `hmac-sha2-512-etm@openssh.com` 
* Host keys and public key auth:
  *  ML-DSA
  *  ML-DSA/ECDSA hybrid? Just for testing
  * `ssh-ed25519`
  * `ecdsa-sha2-nistp256` 
  * `ecdsa-sha2-nistp384` 
  * `ecdsa-sha2-nistp521` 
* Authentication methods:
  * `password`
  * `publickey`
  * `keyboard-interactive`
  * `none`
  * OpenSSH certificates 
* Dependency updates
* OpenSSH keepalive request handling 
* OpenSSH agent forwarding channels 
* OpenSSH `server-sig-algs` extension 
* PPK key format 
* Pageant support 
* `AsyncRead`/`AsyncWrite`-able channels 

## Safety

* `deny(clippy::unwrap_used)`
* `deny(clippy::expect_used)`
* `deny(clippy::indexing_slicing)`
* `deny(clippy::panic)`
* Exceptions are checked manually

### Panics

* When the Rust allocator fails to allocate memory during a CryptoVec being resized.
* When `mlock`/`munlock` fails to protect sensitive data in memory.

### Unsafe code

* `cryptovec` uses `unsafe` for faster copying, initialization and binding to native API.
