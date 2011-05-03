all: ebin clean driver
	erlc -o ebin src/hash_ring.erl

ebin:
	mkdir -p ebin

driver:
	gcc -o ebin/hash_ring_drv.so src/hash_ring_drv.c ../../hash_ring.c ../../sha1.c ../../sort.c -I../../ -I/usr/local/lib/erlang/usr/include -m32 -shared -undefined suppress -flat_namespace
	
test: driver
	erlc  -DTEST -o ebin src/hash_ring.erl
	erl -pa ebin -noshell -noinput -eval 'eunit:test(hash_ring, [verbose]).' -s init stop
	
clean:
	rm -rf ebin/*