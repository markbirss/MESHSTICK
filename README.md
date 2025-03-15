# MESHSTICK
![image](https://github.com/user-attachments/assets/82dec8c3-5a28-477a-bc55-12dd8e2373ae)


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

Confirm that your unique iSerial is actually read from the device (with jumper removed)
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

Adds I2C header for connecting more I2C devices in the furture

![image](https://github.com/user-attachments/assets/228740ff-ed01-44a1-b398-000f16365175)

v4.zip (includes GERBER, BOM and CPL)


# **JLBPCB Gerber view (online)**
https://jlcpcb.com/RGE

# **SMA Connector**
**LCSC #C9900018296**
Alternative parts number available from Mouser or DigiKey

EMPCB.SMAFSTJ.B.HT
https://www.digikey.co.za/en/products/detail/taoglas-limited/EMPCB-SMAFSTJ-B-HT/3522337

Other possible candidates

LCSC Part # C496550

or

https://jlcpcb.com/partdetail/cntitle-SMAKHD9/C20415780

**Use Case**

You want to add a Meshtastic Powered Meshstick to your Raspberry Pi, OpenWRT Router or Desktop Computer running Ubuntu 24.04/ Debian 12/ Fedora or Steam Deck to use Meshtasticd (linux-native)

arm64/armf/x86-64 and all OpenWRT architecture packages are available

![image](https://github.com/user-attachments/assets/151a8aec-32f0-4b41-8105-572d234cb666)
![image](https://github.com/user-attachments/assets/6efbec43-0d96-4e8c-8f79-3fa06c425427)

**yaml.conf**
source

https://github.com/meshtastic/firmware/blob/master/bin/config.d/lora-meshstick-1262.yaml

```
Lora:
  Module: sx1262
  CS: 0
  IRQ: 6
  Reset: 2
  Busy: 4
  spidev: ch341
  DIO3_TCXO_VOLTAGE: true
#  USB_Serialnum: 12345678
  USB_PID: 0x5512
  USB_VID: 0x1A86
```

**UPDATE** [2025-03-08]

Support for 2.6.x MUI 

https://meshtastic.org/docs/software/meshtastic-ui/

sudo nano /etc/meshtasticd/config.d/x11.yaml
```
Display:
  Panel: X11
  Width: 480
  Height: 480
```

Platformio python install
```
sudo apt -y install python3-full python3-virtualenv
virtualenv .
soruce bin/activate
pip3 install platformio
```

Build native-tft (MUI) - 2.6.1
```
git clone https://github.com/meshtastic/firmware
cd firmware/
git submodule update --init --recursive --remote;
pio run -e native-tft
.pio/build/native-tft/program
```

![image](https://github.com/user-attachments/assets/9a7b7d22-bf03-4470-ad59-0469376bb167)

![image](https://github.com/user-attachments/assets/51092e6c-ce0c-4932-8e86-414b0caec46c)


**TESTING**

Various developers including myself have already received and tested the early version 1 of the Meshstick devices.


**More instrctions to follow soon**

Support my work and considder **buying  me a coffee**

https://buymeacoffee.com/mark.birss
