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
[ 3406.372055] usb 3-13.3: USB disconnect, device number 96
[ 3406.372147] rndis_host 3-13.3:1.0 enp0s20u13u3: unregister 'rndis_host' usb-0000:00:14.0-13.3, RNDIS device
[ 3406.427204] sd 4:0:0:0: [sdc] Synchronizing SCSI cache
[ 3406.427230] sd 4:0:0:0: [sdc] Synchronize Cache(10) failed: Result: hostbyte=DID_NO_CONNECT driverbyte=DRIVER_OK
[ 3416.718801] usb 3-14: new high-speed USB device number 97 using xhci_hcd
[ 3416.860322] usb 3-14: Dual-Role OTG device on non-HNP port
[ 3416.860430] usb 3-14: set a_alt_hnp_support failed: -32
[ 3416.978748] usb 3-14: new high-speed USB device number 98 using xhci_hcd
[ 3417.120448] usb 3-14: Dual-Role OTG device on non-HNP port
[ 3417.120563] usb 3-14: set a_alt_hnp_support failed: -32
[ 3417.238766] usb 3-14: new high-speed USB device number 99 using xhci_hcd
[ 3417.260564] usb 3-14: Dual-Role OTG device on non-HNP port
[ 3417.260680] usb 3-14: set a_alt_hnp_support failed: -32
[ 3417.378768] usb 3-14: new high-speed USB device number 100 using xhci_hcd
[ 3417.400562] usb 3-14: Dual-Role OTG device on non-HNP port
[ 3417.400680] usb 3-14: set a_alt_hnp_support failed: -32
[ 3417.400704] usb usb3-port14: unable to enumerate USB device
```

added rules file from here:
https://github.com/analogdevicesinc/plutosdr-fw/blob/master/scripts/53-adi-plutosdr-usb.rules

Sound OTG workaround. Connecting Pluto via USB HUB
