# NeoScrypt-Xaya working-fix notes

This tree fixes the rejected-share path for `--neoscrypt-xaya`.

The important point is that Xaya does not need a different NeoScrypt math core inside nsgminer.  The canonical Xaya implementation hashes exactly 80 bytes with NeoScrypt parameters N=128, r=2, p=1, password=salt=input.  The rejected shares came from the host-side serialization boundary: nsgminer was assembling Xaya stratum work with the normal NeoScrypt byte-order path and submitting the nonce in the normal NeoScrypt byte order.

Main changes:

1. `miner.c`: Xaya stratum work generation now follows ccminer's `ALGO_XAYA` layout:
   - version: little-endian decode
   - previous hash: little-endian decode
   - merkle root: byte-preserving word layout equivalent to ccminer's `swab32(be32dec(...))`
   - ntime: little-endian decode
   - nbits: little-endian decode
   - 80-byte NeoScrypt padding words preserved

2. `miner.c`: Xaya stratum submission now sends the nonce in little-endian form, like ccminer's default/ALGO_XAYA submit path.  The old code submitted `htobe32(nonce)` for Xaya, which submits the byte-reversed nonce.

3. `miner.c`: Xaya stratum difficulty now gets the same 65536 divisor used by ccminer for `ALGO_XAYA`, `ALGO_NEOSCRYPT`, and `ALGO_SCRYPT`.

4. `miner.c` and `util.c`: OpenCL nonce recheck now uses a full 256-bit little-endian target check instead of only the high 64 bits.  `fulltest_le` also no longer uses an unsigned countdown loop.

5. `ocl.c`: `--neoscrypt-xaya` loads `neoscrypt-xaya.cl` and caches it as `neoscrypt-xaya`, avoiding stale normal NeoScrypt `.bin` reuse.

6. `driver-opencl.c`: OpenCL intensity and displayed kernel name now treat Xaya as a NeoScrypt-family OpenCL workload.

Build:

```sh
find . -name '*.bin' -delete
./autogen.sh
CFLAGS="-O2" ./configure --enable-opencl --enable-neoscrypt-xaya
make
```

Run:

```sh
./nsgminer --neoscrypt-xaya --verbose -o stratum+tcp://POOL:PORT -u USER -p PASS
```

Expected startup evidence:

```text
Loading NeoScrypt-Xaya OpenCL kernel: neoscrypt-xaya.cl
```

Do not rename `neoscrypt-xaya.cl` to `neoscrypt.cl` with this tree.  The loader is patched to load the dedicated file.
