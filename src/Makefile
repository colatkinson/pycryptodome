CPPFLAGS=-DHAVE_STDINT_H -DHAVE_POSIX_MEMALIGN -DPYCRYPTO_LITTLE_ENDIAN -DHAVE_X86INTRIN_H -DUSE_SSE2 -DHAVE_UINT128
CPPFLAGS += -DSTATIC=""
CFLAGS=-Werror -Wall -O3 -g -Wno-unused-const-variable -Wconversion -Wsign-conversion # -m32 -msse2

all:: modexp ec_ws_p256 ec_ws_p384 ec_ws_p521

ec_ws_p256: ec_ws_p256.c mont.c modexp_utils.c siphash.c p256_table.c p384_table.c p521_table.c
	$(CC) $(CFLAGS) $(CPPFLAGS) -o $@ $^ -DSYS_BITS=64 -DMAIN

ec_ws_p384: ec_ws_p384.c mont.c modexp_utils.c siphash.c p256_table.c p384_table.c p521_table.c
	$(CC) $(CFLAGS) $(CPPFLAGS) -o $@ $^ -DSYS_BITS=64 -DMAIN

ec_ws_p521: ec_ws_p521.c mont.c modexp_utils.c siphash.c p256_table.c p384_table.c p521_table.c
	$(CC) $(CFLAGS) $(CPPFLAGS) -o $@ $^ -DSYS_BITS=64 -DMAIN

modexp_in: modexp.c mont.c modexp_utils.c siphash.c
	$(CC) $(CFLAGS) $(CPPFLAGS) -o $@ $^ -DSYS_BITS=64 -DMAIN

modexp: modexp.c mont.c modexp_utils.c siphash.c
	$(CC) $(CFLAGS) $(CPPFLAGS) -o $@ $^ -DSYS_BITS=64 -DPROFILE

p256_table.c: make_p256_table
	./make_p256_table > $@

p384_table.c: make_p384_table
	./make_p384_table > $@

p521_table.c: make_p521_table
	./make_p521_table > $@

make_p256_table: make_p256_table.c ec_ws.c mont.c modexp_utils.c siphash.c
	$(CC) $(CFLAGS) $(CPPFLAGS) -o $@ $^ -DSYS_BITS=64 -DMAKE_TABLE

make_p384_table: make_p384_table.c ec_ws.c mont.c modexp_utils.c siphash.c
	$(CC) $(CFLAGS) $(CPPFLAGS) -o $@ $^ -DSYS_BITS=64 -DMAKE_TABLE

make_p521_table: make_p521_table.c ec_ws.c mont.c modexp_utils.c siphash.c
	$(CC) $(CFLAGS) $(CPPFLAGS) -o $@ $^ -DSYS_BITS=64 -DMAKE_TABLE

clean::
	rm -f ec_ws_p256 ec_ws_p384 ec_ws_p521 mont.o modexp make_p256_table make_p384_table make_p521_table
