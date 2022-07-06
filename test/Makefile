
all: out_hw.yuv out_gold.yuv
	diff -q out_gold.yuv out_hw.yuv

./decoder/bin/ldecod:
	cd ./decoder/ldecod && make

build:
	$(MAKE) -f ../build/Makefile

input.264:
	cp ./h264/720p50_parkrun_ter1-5.264 $@
	./hexfilegen.pl $@

input_size.hex: input.264
	wc input.264 | awk '{printf ("%08x\n%08x\n%08x\n%08x\n", $$3, $$3, $$3, $$3) }'  > $@

a.out: build
	bsc -sim -e mkTH ./build/*.ba

out.hex: input.264 input_size.hex a.out
	./a.out | grep "OUT" |awk "{print $$2}" > $@

out_hw.yuv: out.hex
	./dehex.pl out.hex $@

out_gold.yuv: input.264 ./decoder/bin/ldecod
	./decoder/bin/ldecod -i input.264 -o $@

clean :
	rm -rf *.cxx *.ba *.o *.h *.bi *.bo *.bsv *.log input.264 input_size.hex ./decoder/bin/ldecod build
