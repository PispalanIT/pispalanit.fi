---
title: Platformio
summary: 16.8.2021 Platformio
authors:
    - Harry Karvonen
    - Pispalan IT
date: 2021-08-16
template: no_toc.html
---

# 16.8.2021 Platformio
`Harry Karvonen, Pispalan IT`

Tänään tutustuin TinyGS ohjelman kääntämiseen ja lataamiseen ESP32
mikro-ohjaimelle. Projektin kehittäjät suosittelevat
[Platformio](https://platformio.org/):n käyttämistä ja päätin tutustua miten
tämä toimii. Platformio on Python:lla toteutettu käännösympäristö, joka
huolehtii kirjastojen hakemisesta, koodin kääntämisestä ja binäärin
lataamisesta mikro-ohjaimelle. Tarkempia tietoja osoitteesta
[https://docs.platformio.org/en/latest/](https://docs.platformio.org/en/latest/).

Ennen tähän Platformioon tutustumista yritin esptool.py:tä käyttäen ladata
binäärin mutta törmäsin ongelmaan, että ohjelma mitä latasin, ei ollut
kokonainen levykuva flash-muistista vaan vain osa. Tämän lisäksi olisin
tarvinnut kolme muuta binääripakettia. Totesin että tietoa ei ollut nopeasti
saatavilla, niin päätin kunnioittaa kehittäjien ohjetta ja käyttää
Platformiota.

Asennus on suoraviivainen ja tein sen pip:llä aikaisemmin pystyttämääni esptool Python-virtuaali-ympäristöön.

```bash
$ pip install platformio
# ...
$ platformio --version
PlatformIO Core, version 5.1.1
# tai
$ pio --version
PlatformIO Core, version 5.1.1
```

Seuraavaksi noudin TinyGS-projektin lähdekoodin Github:sta.
```bash
$ git clone https://github.com/G4lile0/tinyGS.git
...
$ cd tinyGS
```

Varsinainen ohjelman kääntäminen tapahtuu tinyGS-hakemistossa kutsumalla Platformiota. Hakemistossa on platformio.ini-tiedosto, joka määrittää kääntämisen vipuja ja muita tietoja.

```bash
$ platformio run
```

Tässä menee jonkin aikaa, koska Platformio hakee puuttuvat kirjastot ja tämän jälkeen tekee käännöstyön. Tämän vaiheen jälkeen voi tarkastella mitä binääritiedostoja muodostui. Nämä löytyvät .pio/build/heltec_wihi_lora_32-hakemiston alta.

```bash
$ ls .pio/build/heltec_wifi_lora_32/
firmware.bin      lib0af  lib330  lib471  lib694  lib9d4  libb17  libec2                 libFrameworkArduinoVariant.a
firmware.elf      lib0cb  lib3d3  lib4b3  lib6e1  liba2a  libd27  libf08                 partitions.bin
FrameworkArduino  lib2d5  lib40f  lib4e7  lib98a  liba5b  libe11  libFrameworkArduino.a  src
```

Ohjelman lataaminen mikro-ohjaimeen tapahtuu antamalla run-komennolle vipu -t upload. Käyttetty vipu --upload-port on valinnainen ja sitä ei tarvitse antaa, jos koneessa on vain yksi mirko-ohjain kytkettynä.

```
$ platformio run -t upload --upload-port /dev/ttyACM0 
Processing heltec_wifi_lora_32 (platform: espressif32; board: heltec_wifi_lora_32; framework: arduino)
----------------------------------------------------------------------------------------------------------------------
Tool Manager: Installing platformio/tool-mkspiffs @ ~2.230.0
Tool Manager: tool-mkspiffs @ 2.230.0 has been installed!
Verbose mode can be enabled via `-v, --verbose` option
CONFIGURATION: https://docs.platformio.org/page/boards/espressif32/heltec_wifi_lora_32.html
PLATFORM: Espressif 32 (3.3.1) > Heltec WiFi LoRa 32
HARDWARE: ESP32 240MHz, 320KB RAM, 4MB Flash
DEBUG: Current (esp-prog) External (esp-prog, iot-bus-jtag, jlink, minimodule, olimex-arm-usb-ocd, olimex-arm-usb-ocd-h, olimex-arm-usb-tiny-h, olimex-jtag-tiny, tumpa)
PACKAGES: 
 - framework-arduinoespressif32 3.10006.210326 (1.0.6) 
 - tool-esptoolpy 1.30100.210531 (3.1.0) 
 - tool-mkspiffs 2.230.0 (2.30) 
 - toolchain-xtensa32 2.50200.97 (5.2.0)
Converting tinyGS.ino
LDF: Library Dependency Finder -> http://bit.ly/configure-pio-ldf
LDF Modes: Finder ~ chain, Compatibility ~ soft
Found 34 compatible libraries
Scanning dependencies...
Dependency Graph
|-- <ArduinoOTA> 1.0
|   |-- <Update> 1.0
|   |-- <WiFi> 1.0
|   |-- <ESPmDNS> 1.0
|   |   |-- <WiFi> 1.0
|-- <ESPmDNS> 1.0
|   |-- <WiFi> 1.0
|-- <Update> 1.0
|-- <ArduinoJson> 6.17.2
|-- <IotWebConf> 3.0.1
|   |-- <DNSServer> 1.1.0
|   |   |-- <WiFi> 1.0
|   |-- <WebServer> 1.0
|   |   |-- <WiFi> 1.0
|   |   |-- <FS> 1.0
|   |-- <WiFi> 1.0
|   |-- <EEPROM> 1.0.3
|   |-- <ESPmDNS> 1.0
|   |   |-- <WiFi> 1.0
|   |-- <Update> 1.0
|-- <Wire> 1.0.1
|-- <ESP8266 and ESP32 OLED driver for SSD1306 displays> 4.2.0
|   |-- <Wire> 1.0.1
|   |-- <SPI> 1.0
|-- <PubSubClient> 2.8
|-- <WiFi> 1.0
|-- <WiFiClientSecure> 1.0
|   |-- <WiFi> 1.0
|-- <HTTPClient> 1.2
|   |-- <WiFi> 1.0
|   |-- <WiFiClientSecure> 1.0
|   |   |-- <WiFi> 1.0
|-- <HTTPUpdate> 1.3
|   |-- <HTTPClient> 1.2
|   |   |-- <WiFi> 1.0
|   |   |-- <WiFiClientSecure> 1.0
|   |   |   |-- <WiFi> 1.0
|   |-- <Update> 1.0
|   |-- <WiFi> 1.0
|-- <RadioLib> 4.2.0
|   |-- <SPI> 1.0
|-- <ESPNtpClient> 0.2.5
|   |-- <WiFi> 1.0
|   |-- <Ticker> 1.1
Building in release mode
Compiling .pio/build/heltec_wifi_lora_32/src/tinyGS.ino.cpp.o
In file included from tinyGS/src/Radio/Radio.h:27:0,
                 from /home/kayttaja/tinygs/tinyGS/tinyGS/tinyGS.ino:76:
lib/RadioLib/src/RadioLib.h:50:4: warning: #warning "God mode active, I hope it was intentional. Buckle up, lads." [-Wcpp]
   #warning "God mode active, I hope it was intentional. Buckle up, lads."
    ^
Retrieving maximum program size .pio/build/heltec_wifi_lora_32/firmware.elf
Checking size .pio/build/heltec_wifi_lora_32/firmware.elf
Advanced Memory Usage is available via "PlatformIO Home > Project Inspect"
RAM:   [==        ]  17.0% (used 55672 bytes from 327680 bytes)
Flash: [========= ]  93.8% (used 1229068 bytes from 1310720 bytes)
Configuring upload protocol...
AVAILABLE: esp-prog, espota, esptool, iot-bus-jtag, jlink, minimodule, olimex-arm-usb-ocd, olimex-arm-usb-ocd-h, olimex-arm-usb-tiny-h, olimex-jtag-tiny, tumpa
CURRENT: upload_protocol = esptool
Looking for upload port...
Use manually specified: /dev/ttyACM0
Uploading .pio/build/heltec_wifi_lora_32/firmware.bin
esptool.py v3.1
Serial port /dev/ttyACM0
Connecting.....
Chip is ESP32-PICO-D4 (revision 1)
Features: WiFi, BT, Dual Core, 240MHz, Embedded Flash, VRef calibration in efuse, Coding Scheme None
Crystal is 40MHz
MAC: 98:cd:ac:f3:d7:3c
Uploading stub...
Running stub...
Stub running...
Changing baud rate to 921600
Changed.
Configuring flash size...
Auto-detected Flash size: 4MB
Flash will be erased from 0x00001000 to 0x00005fff...
Flash will be erased from 0x00008000 to 0x00008fff...
Flash will be erased from 0x0000e000 to 0x0000ffff...
Flash will be erased from 0x00010000 to 0x0013cfff...
Compressed 17104 bytes to 11191...
Writing at 0x00001000... (100 %)
Wrote 17104 bytes (11191 compressed) at 0x00001000 in 0.4 seconds (effective 377.7 kbit/s)...
Hash of data verified.
Compressed 3072 bytes to 128...
Writing at 0x00008000... (100 %)
Wrote 3072 bytes (128 compressed) at 0x00008000 in 0.0 seconds (effective 568.0 kbit/s)...
Hash of data verified.
Compressed 8192 bytes to 47...
Writing at 0x0000e000... (100 %)
Wrote 8192 bytes (47 compressed) at 0x0000e000 in 0.1 seconds (effective 740.1 kbit/s)...
Hash of data verified.
Compressed 1229168 bytes to 697353...
Writing at 0x00010000... (2 %)
...
Writing at 0x0013856e... (100 %)
Wrote 1229168 bytes (697353 compressed) at 0x00010000 in 11.2 seconds (effective 881.4 kbit/s)...
Hash of data verified.

Leaving...
Hard resetting via RTS pin...
============================================ [SUCCESS] Took 22.94 seconds ============================================
```

Latauksen valmistuttua saadaan mikro-ohjaimen näytölle eloa. Seuraan lisää [ohjeita](https://github.com/G4lile0/tinyGS/wiki/Ground-Station-configuration) ja saan yhteyden mikro-ohjaimeen WLAN-yhteydellä. Teen alustavat asetukset. Vielä puuttuu [MQTT](https://en.wikipedia.org/wiki/MQTT)-palvelimen käyttäjätunnus ja salasana. Siksi kommentoin mqtt.loop() pois loop():sta. MQTT-tunnusten luominen on nopeaa ja helppoa. Ei vaadi ihmiskontatkia vaan onnistuu TinyGS Personal Bot:n avulla Telegrammia käyttäen.

Flashasin vielä toisen laitteen ja kokeilin testipaketin lähettämistä paketeissa tulleilla antenneilla ja onnistunut lähetys saatiin aikaiseksi. Seuraavaksi on tarkoitus tutkia antenni vaihtoehtoja.
