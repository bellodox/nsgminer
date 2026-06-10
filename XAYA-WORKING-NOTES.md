NeoScrypt-Xaya working-code patch

This tree forces a separate neoscrypt-xaya.cl load and patches Xaya stratum header assembly to the ccminer/Xaya byte order: version/prevhash/ntime/nbits little-endian decoded, merkle words byte-preserved via be32toh on the generated merkle root, and submit nonce little-endian. It also applies the 65536 difficulty divisor for Xaya.

Verify before build:
  grep -R "XAYA-KERNEL-PROOF" -n ocl.c
  grep -R "opt_neoscrypt_xaya" -n miner.c ocl.c driver-opencl.c

Build:
  find . -name "*.bin" -delete
  ./autogen.sh
  CFLAGS="-O2" ./configure --enable-opencl --enable-neoscrypt-xaya
  make

Run the local binary explicitly:
  ./nsgminer --neoscrypt-xaya --verbose -o stratum+tcp://POOL:PORT -u USER -p PASS
