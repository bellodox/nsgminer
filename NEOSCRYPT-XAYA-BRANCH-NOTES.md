# NeoScrypt-Xaya branch notes

This branch exports a dedicated `neoscrypt-xaya.cl` while preserving nsgminer's existing OpenCL ABI: one kernel named `search` with arguments `(block header, output, scratchpad, target)`.

The canonical Xaya difference used by this source tree is not a separate hash core. CPU verification calls `neoscrypt(..., 0x80000620)`, same as standard NeoScrypt, but the Xaya path keeps the 80-byte block header little-endian. Therefore the GPU kernel is intentionally a monolithic NeoScrypt kernel; Xaya-specific correctness is provided by host-side work/header byte-order handling and by loading a separate kernel file/cache when `--neoscrypt-xaya` is active.

Changed files:

- `ocl.c`: loads `neoscrypt-xaya.cl` and uses `neoscrypt-xaya` binary cache name when `opt_neoscrypt_xaya` is set.
- `driver-opencl.c`: reports kernel name as `neoscrypt-xaya` for the Xaya mode.
- `neoscrypt-xaya.cl`: dedicated OpenCL kernel file compatible with nsgminer.

Build example:

```sh
./autogen.sh
CFLAGS="-O2" ./configure --enable-opencl --enable-neoscrypt-xaya
make
```

Run example:

```sh
./nsgminer --neoscrypt-xaya -o stratum+tcp://POOL:PORT -u USER -p PASS
```

Validation: accepted shares against a Xaya pool/node are the final proof. Rejected shares with identical CPU validation usually indicate host-side work construction/byte-order issues, not the CL file.
