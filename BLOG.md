## 2017-09-23

### Power-on

Plugged ADALM-PLUTO into my OpenSuSe desktop.

```
[ 1017.451558] usb 3-4: new high-speed USB device number 6 using xhci_hcd
[ 1023.223318] usb 3-4: new high-speed USB device number 8 using xhci_hcd
[ 1028.755081] usb 3-4: new high-speed USB device number 9 using xhci_hcd
[ 1034.650866] usb 3-4: new high-speed USB device number 11 using xhci_hcd
...
```

Well.. strange.

Reading [PLUTOSDR QUICKSTART GUIDE](https://www.rtl-sdr.com/plutosdr-quickstart-guide/)

## 2017-09-24

Still getting OTG errors:
```
[ 3416.718801] usb 3-14: new high-speed USB device number 97 using xhci_hcd
[ 3416.860322] usb 3-14: Dual-Role OTG device on non-HNP port
[ 3416.860430] usb 3-14: set a_alt_hnp_support failed: -32
[ 3417.400704] usb usb3-port14: unable to enumerate USB device
```

added rules file from here:
https://github.com/analogdevicesinc/plutosdr-fw/blob/master/scripts/53-adi-plutosdr-usb.rules

Sound OTG workaround. Connecting Pluto via simple USB HUB
```
[ 3599.044928] usb 3-13.3: new full-speed USB device number 118 using xhci_hcd
[ 3599.165320] usb 3-13.3: not running at top speed; connect to a high speed hub
[ 3599.166923] usb 3-13.3: New USB device found, idVendor=0456, idProduct=b673
[ 3599.166925] usb 3-13.3: New USB device strings: Mfr=1, Product=2, SerialNumber=3
[ 3599.166926] usb 3-13.3: Product: PlutoSDR (ADALM-PLUTO)
[ 3599.166927] usb 3-13.3: Manufacturer: Analog Devices Inc.
[ 3599.166928] usb 3-13.3: SerialNumber: xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
[ 3599.170803] usb-storage 3-13.3:1.2: USB Mass Storage device detected
[ 3599.170943] scsi host4: usb-storage 3-13.3:1.2
[ 3599.171232] cdc_acm 3-13.3:1.3: ttyACM0: USB ACM device
[ 3600.189388] scsi 4:0:0:0: Direct-Access     Linux    File-Stor Gadget 0406 PQ: 0 ANSI: 2
[ 3600.189681] sd 4:0:0:0: Attached scsi generic sg2 type 0
[ 3600.190636] sd 4:0:0:0: [sdc] 61441 512-byte logical blocks: (31.5 MB/30.0 MiB)
[ 3600.190866] sd 4:0:0:0: [sdc] Write Protect is off
[ 3600.190869] sd 4:0:0:0: [sdc] Mode Sense: 0f 00 00 00
[ 3600.191102] sd 4:0:0:0: [sdc] Write cache: enabled, read cache: enabled, doesn't support DPO or FUA
[ 3600.197575]  sdc: sdc1
[ 3600.199352] sd 4:0:0:0: [sdc] Attached SCSI removable disk
```
Ordered fast USB3 hub

## 2017-09-25

Installed USB3 HUB. Plug&Play smooth.

Trying to run GQRX with Pluto.

Have to build gr-osmosdr-gqrx/plutosdr branch https://github.com/csete/gr-osmosdr-gqrx/tree/plutosdr

Have my fork to fix errors: https://github.com/drom/gr-osmosdr-gqrx/tree/plutosdr

Drown in build / install process ... zzz

## 2017-09-26

Reading reviews:

https://www.rtl-sdr.com/adalm-pluto-sdr-unboxing-and-initial-testing/

https://wiki.analog.com/resources/tools-software/linux-software/gnuradio

Compiled: libiio, libad9361-iio, gr-iio

Can see PlutoSDR Source / Sink in GNU Radio companion

## 2017-09-27

Getting error:

```
Traceback (most recent call last):
  File "/home/drom/work/github/drom/pluto/top_block.py", line 23, in <module>
    from gnuradio import iio
ImportError: cannot import name iio
```

Trying this instruction:

https://github.com/blurbdust/gr-iio

## 2017-09-28

Still errors:
```
Traceback (most recent call last):
  File "/home/drom/work/github/drom/pluto/top_block.py", line 149, in <module>
    main()
  File "/home/drom/work/github/drom/pluto/top_block.py", line 137, in main
    tb = top_block_cls()
  File "/home/drom/work/github/drom/pluto/top_block.py", line 109, in __init__
    self.pluto_source_0 = iio.pluto_source('local:', 2400000000, 2084000, 1 - 1, 20000000, 0x8000, True, True, True, "manual", 64.0, '', True)
AttributeError: 'module' object has no attribute 'pluto_source'

```

Looking for my Pluto:

```
rom@drom:~/work/github/drom/pluto> iio_info -s
Library version: 0.10 (git tag: a826645)
Compiled with backends: local xml ip usb
Available contexts:
        0: 0456:b673 (Analog Devices Inc. PlutoSDR (ADALM-PLUTO)), serial=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx [usb:1.50.5]

```

Now I need USB support?

https://www.plutosdr.com/viewtopic.php?f=6&t=5

## 2017-09-29

Removed all gnuradio,sdr related packages installed by Yast and trying to do everything using pyBOMBS.

https://www.gnuradio.org/blog/pybombs-the-what-the-how-and-the-why/

## 2017-09-30

Stuck with compiling pyqt4
```
g++ -c -pipe -fno-strict-aliasing -O2 -fPIC -Wall -W -D_REENTRANT -DQT_WEBKIT -DQT_NO_DEBUG -DQT_GUI_LIB -DQT_CORE_LIB -DQT_SHARED -I/usr/share/qt4/mkspecs/default -I. -I/usr/include/QtCore -I/usr/include/QtGui -I/usr/include -I/usr/include/python2.7 -I../../QtCore -I. -I. -o qpycore_chimera.o qpycore_chimera.cpp                                                                                                                         
qpycore_chimera.cpp: In member function ‘void Chimera::set_flag()’:
qpycore_chimera.cpp:376:22: error: ‘pyqt4ClassTypeDef’ was not declared in this scope
         _is_flag = ((pyqt4ClassTypeDef *)_type)->qt4_flags & 0x01;
                      ^~~~~~~~~~~~~~~~~
qpycore_chimera.cpp:376:22: note: suggested alternative: ‘sipClassTypeDef’
         _is_flag = ((pyqt4ClassTypeDef *)_type)->qt4_flags & 0x01;
                      ^~~~~~~~~~~~~~~~~
                      sipClassTypeDef
qpycore_chimera.cpp:376:41: error: expected primary-expression before ‘)’ token
         _is_flag = ((pyqt4ClassTypeDef *)_type)->qt4_flags & 0x01;
                                         ^
qpycore_chimera.cpp:376:42: error: expected ‘)’ before ‘_type’
         _is_flag = ((pyqt4ClassTypeDef *)_type)->qt4_flags & 0x01;
                                          ^~~~~
make[2]: *** [Makefile:274: qpycore_chimera.o] Error 1
make[2]: Leaving directory '/home/drom/prefix/default/src/pyqt4/qpy/QtCore'
make[1]: *** [Makefile:3: all] Error 2
make[1]: Leaving directory '/home/drom/prefix/default/src/pyqt4/qpy'
make: *** [Makefile:3: all] Error 2
PyBOMBS.Packager.source - ERROR - Build failed. See output above for error messages.
PyBOMBS.Packager.source - ERROR - Problem occurred while building package pyqt4:
Build failed.
PyBOMBS.install_manager - ERROR - Error installing package pyqt4. Aborting.
```

## 2017-10-05

Stoped playing with BOMBS.
Installedd all packages from OpenSuSe / hamradio repo.
Compiled 3 analog devices packages:
 - [libiio](https://github.com/analogdevicesinc/libiio)
 - [libad9361-iio](https://github.com/analogdevicesinc/libad9361-iio)
 - [gr-iio](https://github.com/analogdevicesinc/gr-iio)*

* On `gr-iio` Used advice from: https://github.com/analogdevicesinc/gr-iio/issues/11

IT WORKS! RX and TX
