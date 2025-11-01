# MESHSTICK

If you are self assembling the board you can view the interactive BOM here below

iBOM

BOARD | iBOM url  |
|:--|:--|
| V4 | [https://markbirss.github.io/MESHSTICK/](https://markbirss.github.io/MESHSTICK/) |

![image](https://github.com/user-attachments/assets/4bb72821-e60b-422d-a0fc-4dbff11431b2)

diy CH341 USB-TO-SPI SX1262 LoRa Meshstick that you can have manufactured or part assembled and finish by just adding the USB 2.0 connector, Waveshare SX1262 TXCO Core LoRa module and SMA anntenna connector

Waveshare SX1262 TXCO Core module is on the back side of the board.

More versions being evaluated are SX1280, 1W eByte E22, wio sx1262, LR1110 and LR1121

Version 1 did not have the 24C02 I2C flash chip that is being used to store a unique serial number for the device. 

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

**Use the device number 016 above for -s**
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

**Use Case**

You want to add a Meshtastic Powered Meshstick to your Raspberry Pi, OpenWRT Router or Desktop Computer running Ubuntu 24.04/ Debian 12/ Fedora or Steam Deck to use Meshtasticd (linux-native)

arm64/armf/x86-64 and all OpenWRT architecture packages are available

![image](https://github.com/user-attachments/assets/151a8aec-32f0-4b41-8105-572d234cb666)
![image](https://github.com/user-attachments/assets/6efbec43-0d96-4e8c-8f79-3fa06c425427)

**blacklist spi-ch341 kernel driver**

add to /etc/modprobe.d/blacklist.conf
```
# Meshstick
blacklist spi-ch341
```

**yaml.conf**
source

```
Lora:
  Module: sx1262
  CS: 0
  IRQ: 6
  Reset: 2
  Busy: 4
  spidev: ch341
  DIO2_AS_RF_SWITCH: true
  DIO3_TCXO_VOLTAGE: true
#  USB_Serialnum: 12345678
  USB_PID: 0x5512
  USB_VID: 0x1A86
```

**UPDATE** [2025-03-08]

If you have installed meshtasticd package, you will first need to stop the meshtasticd service to run mui
```
sudo systemctl stop meshtasticd
sudo systemctl disable meshtasticd
```

Support for 2.6.x MUI 

**UPDATE** [2025-04-27]
OS Image - Mesh Hessen Raspberry Pi Image - (Contributed by @Do3MLA, Manuel)

https://drive.google.com/file/d/1g-4EMshe5GP99uXz_K4nthUIZ1fj3jOa/view

Mesh Hessen Raspberry Pi Image Changelog:

Meshsens (updated)

Meshtastic CLI (updated)

Meshtasticd Native Linux 2.6.4 including MUI version 2.6.6

(Prepared for the MeshStick)


For other HATs or dongles, you will need to adjust the Meshtasticd settings.

The image is ready to use.

Download with Chrome

Extract with 7zip

Flash with Belena Etcher


There are two startup scripts on the desktop: one for using the MeshStick via the MUI window, and one for using it via Android.


Or build native-tft mui yourself

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
source bin/activate
pip3 install platformio
```

Raspbian Dependancies
```
sudo apt install -y libusb-1.0-0-dev libgpiod-dev libyaml-dev libyaml-cpp-dev libbluetooth-dev libxkbcommon-dev libinput-dev libi2c-dev
```

Build and run native-tft (MUI) - 2.6.x
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


**More updates to follow soon**

**UPDATE** [2025-04-02]

# Cheaper and quicker DIY Meshstick (PiggyStick)

Important Note: Remember to move the voltage jumpers to 3V3


![image](https://github.com/user-attachments/assets/8447c0ef-48c2-4a3a-8f65-9710fe350646)

![image](https://github.com/user-attachments/assets/ba8dde8e-d778-48b7-8717-97aba98dad13)

PiggyStick wio-sx1262 [2025-04-11]
![shaking-butt-happy](https://github.com/user-attachments/assets/6f96dfdf-dcf0-4438-88c8-5b1fe6b49747)
![20250411_161830](https://github.com/user-attachments/assets/83d1bad5-e82d-47c6-bb95-1d577eed0287)

PiggyStick LR1121 E80-900M2213S 868/915 and 2.4Ghz Dual LoRa Radio Module (only one radio use at a time) [2025-04-14]
![image](https://github.com/user-attachments/assets/edca2a78-8112-4522-918f-78f406324169)



![image](https://github.com/user-attachments/assets/06b78362-9d90-469c-9e22-1c8ab6588830)

if I2c flash is really needed connect other side - but after flashing the eeeprom you will need to cut pin1 of ch341

![image](https://github.com/user-attachments/assets/fc274006-4af6-4214-8e79-fc62ec63ac2d)

https://www.aliexpress.com/item/1005005400942525.html

https://www.aliexpress.com/item/1005005305349454.html


**UPDATE** [2025-05-05]


Piggystick also works mounted in front with a flipped pcb (you can even swap radio modules out )

![image](https://github.com/user-attachments/assets/c78452f4-b839-4c28-ae2a-e11569d04324)

Newer editions of the CH341B dongles are also supported and working as expected

![image](https://github.com/user-attachments/assets/c92588c4-53c1-4f07-a105-9fc976a735bc)



Trademarks

Meshtastic® is a registered trademark of Meshtastic LLC
https://meshtastic.org/docs/legal/licensing-and-trademark/


Pine64 is a registered trademark of https://pine64.com/ - Pine Store ltd. 

Support my work and consider **buying  me a coffee**

https://buymeacoffee.com/mark.birss
