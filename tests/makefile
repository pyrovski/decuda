nvcc=/usr/local/cuda2.3/bin/nvcc
ptxas=/usr/local/cuda2.3/bin/ptxas
ptx=float1.ptx float2.ptx test10.ptx test11.ptx test12.ptx test13.ptx test14.ptx test15.ptx test16.ptx test17.ptx test18.ptx test19.ptx test20.ptx test22.ptx test23.ptx test24a.ptx test24b.ptx test24c.ptx test24.ptx test25a.ptx test25b.ptx test25.ptx test26.ptx test29.ptx test2.ptx test30.ptx test31.ptx test32.ptx test33.ptx test34.ptx test35.ptx test36.ptx test39.ptx test3.ptx test40.ptx test42_8.ptx test42.ptx test44.ptx test4.ptx test5b.ptx test5.ptx test6.ptx test7.ptx test8_16.ptx test8b.ptx test8.ptx test8r.ptx test9.ptx test.ptx

cubinO1=$(ptx:.ptx=.O1.cubin)
cubinO2=$(ptx:.ptx=.O2.cubin)
cubin=$(cubinO1) $(cubinO2)

decuda=$(cubin:.cubin=.decuda)
nv50dis=$(cubin:.cubin=.nv50dis)
cuobjdump=$(cubin:.cubin=.cuobjdump)

dis=$(decuda) $(nv50dis) $(cuobjdump)

all: $(dis) 

%.ptx:%.cu
	$(nvcc) $^ -o $@ -ptx

%.O1.cubin:%.ptx
	$(ptxas) -O1 -o $@ $^

%.O2.cubin:%.ptx
	$(ptxas) -O2 -o $@ $^

%.decuda:%.cubin
	decuda.py -o $@ $^

%.nv50dis:%.cubin
	cat $^ | nv50dis -n > $@

%.cuobjdump:%.cubin
	cuobjdump -sass $^ > $@

clean:
	rm -f $(ptx) $(dis) $(cubin)
