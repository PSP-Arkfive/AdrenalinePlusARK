PY = $(shell which python3)

all: _libs _adrctrl _btcnf _systemctrl _popcorn _inferno _vshctrl _kermit_idstorage _xmbctrl

_libs:
	make -C ark-dev-sdk -j

_btcnf:
	$(PY) btcnf.py build adrctrl/btcnf/psvbtjnf.txt
	$(PY) btcnf.py build adrctrl/btcnf/psvbtknf.txt
	mv adrctrl/btcnf/*.bin ../user/flash0/

_rebootex:
	make -C adrctrl/rebootex clean
	make REBOOTEXDIR=../../bootloadex -C adrctrl/rebootex

_payloadex:
# 	make -C payloadex clean
# 	make -C payloadex
# 	cp "payloadex/payloadex.bin" "../user/flash0/payloadex.bin"
# 	make -C payloadex clean

_binary:
	make -C binary clean
	make -C binary
	bin2c binary/binary.bin adrctrl/include/binary.h binary
	make -C binary clean

_adrctrl: _rebootex _binary
	make -C adrctrl clean
	make ARKSDK="../ark-dev-sdk" -C adrctrl
	cp "adrctrl/pentazemin.prx" "../user/flash0/kd/pentazemin.prx"

_systemctrl: | _libs
	make -C systemctrl clean
	make ARKSDK="../ark-dev-sdk" -C systemctrl
	psp-packer systemctrl/systemctrl.prx
	cp "systemctrl/systemctrl.prx" "../user/flash0/kd/systemctrl.prx"

_popcorn: | _libs
	make -C popcorn clean
	make ARKSDK="../ark-dev-sdk" -C popcorn
	psp-packer popcorn/popcorn.prx
	cp "popcorn/popcorn.prx" "../user/flash0/kd/popcorn.prx"

_inferno: | _libs
	make -C inferno clean
	make ARKSDK="../ark-dev-sdk" -C inferno
	psp-packer inferno/inferno.prx
	cp "inferno/inferno.prx" "../user/flash0/kd/inferno.prx"

_vshctrl: | _libs
	make -C vshctrl clean
	make ARKSDK="../ark-dev-sdk" -C vshctrl
	psp-packer vshctrl/vshctrl.prx
	cp "vshctrl/vshctrl.prx" "../user/flash0/kd/vshctrl.prx"

_kermit_idstorage: | _libs
	make -C kermit_idstorage clean
	make -C kermit_idstorage
	psp-packer kermit_idstorage/kermit_idstorage.prx
	cp "kermit_idstorage/kermit_idstorage.prx" "../user/flash0/kd/kermit_idstorage.prx"

_xmbctrl: | _libs
	make -C xmbctrl clean
	make ARKSDK="../ark-dev-sdk" -C xmbctrl
	psp-packer xmbctrl/xmbctrl.prx
	cp "xmbctrl/xmbctrl.prx" "../user/flash0/vsh/module/xmbctrl.prx"


clean:
	make -C ark-dev-sdk clean
	make -C adrctrl/rebootex clean
	make -C adrctrl clean
	make -C binary clean
	make -C systemctrl clean
	make -C popcorn clean
	make -C inferno clean
	make -C vshctrl clean
	make -C kermit_idstorage clean
	make -C xmbctrl clean
