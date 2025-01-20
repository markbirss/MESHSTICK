# MESHSTICK
diy CH341 USB-TO-SPI SX1262 LoRa Meshstick that you can have manufactured or part assembled and finish by just adding the USB 2.0 connector, Waveshare SX1262 TXCO Core LoRa module and SMA anntenna connection

Waveshare SX1262 TXCO Core module is on the back side of the board.

More vesions being evaluated are SX1280, 1W eByte E22, wio sx1262, LR1110 and LR1121

Verion 1 did not have the 24C02 I2C flash chip that is being used to store a unique serial number for the device. 

The 2 pin jumper is populated when you want to program the flash chip.
(IMSProg is used in the example bellow)

![image](https://github.com/user-attachments/assets/aaa8b17d-667d-4d9b-8514-47ea46e0fc33)

```
5312cc00861a12550403000000000000
32303030303031360000000000000000
4d455348535449434b20505752442042
59204d45534854415354494300000000
```
Remove the jumper for normal use (once the 24C02 flash is programmed)

Confirm that your unique iSerial is actually ready from the device (with jumper removed)
e.g using lsusb

```
lsusb | grep CH341
Bus 001 Device 016: ID 1a86:5512 QinHeng Electronics CH341 in EPP/MEM/I2C mode, EPP/I2C adapter
```

**Use the device numder 016 above for -s**
```
lsusb -s 016 -v|grep -i iserial
  iSerial                 3 20000016
```

# **DISCLAIMER**

# Use of these GERBER, BOM and CPL are at your own risk

**BOARD VERSIONS**

V2 (2 layer board)

![image](https://github.com/user-attachments/assets/500f8c9d-ebc8-4c9a-9d1d-d4be7684a38d)

v2.zip (includes GERBER, BOM and CPL)

V3 (4 layer board)

![image](https://github.com/user-attachments/assets/18aa3d66-34e6-4053-8227-9289ae9c23d5)

v3.zip (includes GERBER, BOM and CPL)

V4 (4 layer board)
Adds I2C header

![image](https://github.com/user-attachments/assets/228740ff-ed01-44a1-b398-000f16365175)

v4.zip (includes GERBER, BOM and CPL)

**Use Case**

You want to add a Meshtastic Powered Meshstick to your Raspberry Pi or Desktop Computer running Ubuntu 24.04/ Debian 12/ Fedora or Steam Deck to use Meshtasticd (linux-native)

arm64/armf/x86-64

**yaml.conf**

https://github.com/meshtastic/firmware/blob/master/bin/config.d/lora-meshstick-1262.yaml

**More instrctions to follow soon**

Support my work and considder
**buy me a coffee**
https://buymeacoffee.com/mark.birss
