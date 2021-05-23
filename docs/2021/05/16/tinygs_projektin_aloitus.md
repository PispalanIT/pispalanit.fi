# 16.5.2021 TinyGS projektin aloitus

Moro, olen päättänyt aloitta uuden projektin liittyen satelliitteihin,
kuunneltuani [Wappuradiota](https://wappuradio.fi). Myös uutisissa oli asiasta
ja kyseessä on UPM:n valmistama puinen satelliitti [WISA
WOODSAT](https://www.wisaplywood.com/fi/campaigns/wisawoodsat/).  Tutkittuani
asiaa totesin ettei vielä ole liian myöhäistä rakentaa laitteistoa, jolla
saadaan napattua satelliitin lähettämiä selfieitä.

## Sateliitin lähetyksen kuuntelu

Satelliitti lähettää ottamansa selfien radiolla maahan, jossa satelliitin maa-
asema vastaanottaa lähetyksen. Käytetty radiotaajuuskaista on tiedotteiden
mukaan radioamatöörien käyttämällä taajuuskaistalla. Aluksi oletin että tätä
varten tarvitsee rakentaa oma radio-vastaanotin. Tämä osoittautui kuitenkin
paljon yksinkertaisemmaksi. WISA WOODSAT on rakennettu
[CubeSat-standardin](https://fi.wikipedia.org/wiki/CubeSat) mukaan. Lisää voi
lukea https://www.cubesat.org/.

Satelliittien maa-asemaa varten on luotu projekti
[TinyGS](https://www.cubesat.org/). Tuettuja laitteita oli muutamia ja
halvimmat radiot olivat muutaman kympin luokkaa.  Lista tuetuista laitteista
löytyy [TinyGS GitHub:sta](https://github.com/G4lile0/tinyGS#hardware).

## Radion hankinta

Kävin läpi TinyGS:n listaamat radiot ja suurin osa oli saatavilla Kiinasta.
Onnekseni myös muutama radio löytyi Saksan Amazonista.

Valitsin radion sen mukaan mitä oli saatavilla EU-alueelta ja mikä oli halvin.
Päädyin valitsemaan TTGO LoRa32 radion versio V1 tai V2, se selviää myöhemmin.
Tätä radiota myytiin DollaTek LoRa32 V2.1 nimellä.

Radiot ovat fiksattu tietylle ISM-kaistalle ja monen arvonnan jälkeen päädyin
kokeilemaan 433MHz taajuus-alueelle määritettyä versiota. Voi olla että WISA
WOODSAT käyttää esimerksiksi 136 MHz taajuu-aluetta. Tämä täytyy vielä
myöhemmin selvittää.

Lopullinen tilaus tässä vaiheessa oli kaksi [DollaTek LoRa32 V2.1 433MHz
radiota](https://www.amazon.de/-/en/gp/product/B07RXSKPBX/).
