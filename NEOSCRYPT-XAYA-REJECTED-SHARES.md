# NeoScrypt-Xaya rejected shares diagnosis

The canonical SpaceXpanse `neoscrypt-xaya` implementation exposes `void neoscrypt(const unsigned char *input, unsigned char *output)` and hard-codes an 80-byte input. It runs FastKDF-BLAKE2s, ChaCha SMix, Salsa SMix, XORs both streams, then final FastKDF. That matches nsgminer profile `0x80000620` in the CPU hash core.

If shares are rejected while the GPU finds nonces, the most likely issue is **work/header byte order or nonce insertion**, not the NeoScrypt core. This export separates the Xaya OpenCL file and binary cache to prevent stale normal-NeoScrypt binaries.

Validation steps:

1. Delete existing `.bin` OpenCL cache files before testing.
2. Run with `--neoscrypt-xaya`, not `--neoscrypt`.
3. Confirm logs show kernel `neoscrypt-xaya`.
4. If shares remain invalid, instrument CPU-vs-GPU by hashing the exact 80-byte header for one GPU-found nonce through `scanhash_neoscrypt_xaya`; if CPU rejects the GPU nonce, the OpenCL result/target compare path is wrong. If CPU accepts but pool rejects, submit byte order / nonce endian is wrong.

The four-stage ccminer-style kernel cannot be dropped into this branch because nsgminer creates only one OpenCL kernel named `search` and allocates only `CLbuffer0`, `outputBuffer`, and `padbuffer8`.
