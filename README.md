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

Sound OTG workaround. Connecting Pluto via USB HUB
