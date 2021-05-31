---
title: LILYGO TTGO LoRa32 V2.1
summary: 30.5.2021 LILYGO TTGO LoRa32 V2.1
authors:
    - Harry Karvonen
    - Pispalan IT
date: 2021-05-30
template: no_toc.html
---

# 30.5.2021 LILYGO TTGO LoRa32 V2.1_1.6
`Harry Karvonen, Pispalan IT`

Tutkin saatuja radio-moduuleja ja ne ovat näköjään tasan samoja kuin
aasialaisen valmistajan LILYGO radio-moduuli TTGO LoRa32 V2.1_1.6. Tuotesivun
[LILYGO TTGO LoRa32
V2.1_1.6](http://www.lilygo.cn/prod_view.aspx?TypeId=50003&Id=1270&FId=t3:50003:3)
dokumentaation perusteella oletan, että kyseessä on tismalleen sama
radio-moduuli.

Sivulta löytyy kaksi ohjelma projektia liittyen radio-moduuliin
[LilyGO/ESP32-Paxcounter](https://github.com/LilyGO/ESP32-Paxcounter) ja
[Xinyuan-LilyGo/TTGO-LoRa-Series](https://github.com/Xinyuan-LilyGo/TTGO-LoRa-Series).
Molemmat ohjelmat ovat tarjolla GitHubissa. Ensimmäinen näistä ohjelmista
näyttäisi olevan ladattu jo valmiiksi radio-moduuleihin.
Moduuliin ladattu ohjelma on forkattu
[cyberman54/ESP32-Paxcounter](https://github.com/cyberman54/ESP32-Paxcounter)
projektista. Viime viikolla saadun ulostulon perusteella on tuo LILYGOn
versio, joka on ladattu laitteeseen.

Radio-moduuli koostuu
[ESP32-PICO-D4](https://www.espressif.com/sites/default/files/documentation/esp32-pico-d4_datasheet_en.pdf)
-mikro-ohjaimesta ja [Semtech
SX1276](https://www.semtech.com/products/wireless-rf/lora-core/sx1276)
radiosta. Myöhemmin tähän tutustutaan tarkemmin. Nyt riittää, että
kokonaisuutta tarkastellaan valmiiden ohjelmien näkökulmasta. Tulen käyttämään
valmiita ohjelmia radio-moduulin kanssa säästääkseni aikaa ja todetakseni miten
kokonaisuus toimii.

## Radio-moduulin tekniset tiedot
Tiedot löytyvät [valmistajan
sivuilta](http://www.lilygo.cn/prod_view.aspx?TypeId=50003&Id=1270&FId=t3:50003:3)
ja yhteenveto kerätty tähän:

- Käyttöjännite (Working voltage): 1.8~3.7v
- Virta (Acceptable current): 10~14mA
- Lähetys virta (Transmit current):
     - 120mA@+20dBm
     - 90mA@+17dBm
     - 29mA@+13dBm
- Käyttötaajuus (Operating frequency): 433MHz/868MHz/915MHz
- Lähetysteho (Transmit power): +20dBm
- Vastaanottoherkkyys (Receive sensitivity):
     - -139dBm@LoRa & 62.5Khz & SF=12 & 146bps
     - -136dBm@LoRa & 125Khz & SF=12 & 293bps
     - -118dBm@LoRa & 125Khz & SF=6 & 9380bps
     - -123dBm@FSK & 5Khz & 1.2Kbps
- Taajuusvirhe (Frequency error): +/-15KHz
- FIFO koko (FIFO space): 64Byte
- Lähetysnopeus (Data rate):
     - 1.2K~300Kbps@FSK
     - 0.018K~37.5Kbps@LoRa         
- Modulaatiot (Modulation Mode): FSK, GFSK, MSK, GMSK, LoRa TM, OOK
- Liityntä (Interface form): SPI
- Nukkumis virta (Sleep current):
     - 0.2uA@SLEEP
     - 1.5uA@IDLE
- Käyttölämpötila (Operating temperature): -40℃- +85℃
- Digitaalinen RSSI funktio (Digital RSSI function)
- Automaattinen taajuus korjaus (Automatic frequency correction)
- Automaattinen vahvistuksen säätö (Automatic gain control)
- Nopea herätys ja taajuus vaihtelu (Fast wake-up and frequency hopping)
- Konfiguroitava paketin käsittely (Highly configurable data packet handler)
- Antenni (SMA Antenna): TP4054

## Paxcounter

Paxcounter on radio-moduuliin ladattu ohjelma, joka kuuntelee WiFi ja Bluetooth
laitteiden lähetyksiä. Näistä laitteiden määristä arvioidaan paljonko ihmisiä
on lähistöllä. Tulos näytetään näytöllä ja lähetetään LoRaWAN lähetyksenä.

## TTGO-LoRa-Series / ReceiverBin

Nopeasti tutkittuna tällä ohjelmalla pystyy kuuntelemaan LoRaWAN lähetyksiä.
Saadut paketit todennäköisesti tulostetaan sarjaporttiin.  Tämän päättelin
[lähdekoodin
(LoRaReceiver.ino)](https://github.com/sandeepmistry/arduino-LoRa/blob/master/examples/LoRaReceiver/LoRaReceiver.ino)
perusteella, joka löytyy projektista, josta TTGP-LoRa-Series on riippuvainen
