LEDka blikaj!
=============

Konečne sa dostávame k tomu zaujímavému - programovaniu hardvéru! Keďže by si v tejto fáze už mal mať nainštalovaný driver, *Python3* na počítači a aj *MicroPython* na *NodeMCU*, môžme si otvoriť vývojové prostredie pre *MicroPython* a začať programovať (či už *uPyCraft*, alebo *ESPlorer*).

Čo sa naučíme v tejto kapitole:

* základné časti dosky NodeMCU a ako naň nahrávať kód
* volanie knižnice ``machine``
* nastovanie výstupného napätia na pinoch (a tým zapínať LEDky)
* ako správne pripájať LEDky (aby nám nezhoreli)
* vytváranie premenných, *for* a *while* cykly, podmienky v kóde
* jednoduché svetelné animácie

Tieto súčiastky budeme používať:

* NodeMCU
* Breadboard + prepájacie kábliky
* LEDky a rezistory

O NodeMCU
---------

.. figure:: /_static/images/nodemcu-popisky.png
   :alt: NodeMCU


NodeMCU je relatívne malá doska s viacerými elektronickými súčiastkami. Mozgom zariadenia je mikroprocesor ``ESP8266`` (zelený obdĺžnik). Toto je miesto, kam sme nahrali *MicroPython* interpreter. Zároveň sem budeme ukladať náš kód a tu sa bude aj vykonávať. Tento mikroprocesor má v sebe vbudovanú WiFi sieťovú kartu (s anténkou - viď obrázok), takže s ním budeme môcť komunikovať aj cez internet. 

``ESP8266`` sa dá použiť aj samostane, no všetky zvyšné súciastky na NodeMCU nám zľachšujú vývoj.

Na oboch stranách sa nachádza rada *pinov* (z angl. "pin"). Každý z nich má nejakú funkciu. Niektoré slúžia na napájanie, iné na komunikáciu s ESP8266 a na niektorých vieme nastavovať výstupné napätie či čítať vstupné napätie a ťeda na ne pripájame rôzne LEDky, senzory, motorčeky, atď. Všetky piny by mali byť rovné a kolmé na rovinu dosky. (ak nie sú, skús ich **opatrne** vyrovnať)

Oproti ``ESP8266`` sa nachádza ``microUSB`` konektor, ktorým prepájame NodeMCU s počítačom. Taktiež slúži na napájanie, takže keď si dosku naprogramujeme, môžeme ju napojiť do nabíjačky od mobilu alebo do powerbanky. Napájacie napätie je 5V.

Vedľa USB konektoru sa nachádzajú dve tlačítka.
Tlačidlo ``RST`` slúži na zresetovanie dosky (nemusíš vypájať a zapájať USB kábel). Využíva sa, keď zadáš zlý príkaz a doska ti zamrzne, alebo keď chceš prerušiť nekonečný cyklus.
Stlačením lačidla ``FLASH`` pošleš impulz mikroprocesoru. Využíva sa pri nahrávaní MicroPythonu na zariadenie.

Vedľa USB konektoru sa ešte náchádza jedna dôležitá súčiastka - ``sériový prevodník``. Vďaka nemu náš počítač (so zbernicou USB) rozumie mikroprocesoru ESP8266 (ten má zas zbernicu UART). Tento prevodník môže byť v rôznych prevedeniach, najčastejšie sú to však ``CP2102`` alebo ``CH340``. Podľa typu prevodníka sme si v predchádzajúcej kapitole inštalovali driver.

Pripojenie k zariadeniu
-----------------------

Po zapojení NodeMCU k počítaču pomocou USB môžeme otvoriť IDE pre MicroPython. Tu je popísaný postup pre *uPyCraft*, no jednostlivé kroky sú veľmi podobné aj v *ESPloreri*.

1. v *Tools* -> *Board* vyberieme možnosť *esp8266*
2. v *Tools* -> *Serial* vyberieme port nášho zariadenia
3. ak sme už MicroPython na zariadenie nahradli, pri otázke *Burn Firmware* klikneme *Cancel*
4. na NodeMCU stlačíme tlačidlo ``RST`` (hneď vedľa USB konektoru) aby sme zariadenie zresetovali
5. v spodnej časti obrazovky sa nachádza interaktívna konzola z NodeMCU (anglicky *REPL*). Po zresetovaní zariadenia by sa tam mal vypísať text (aktuálna verzia MicroPythonu) a na poslednom riadku by mali byť tri zobáčiky.

.. figure:: /_static/images/uPyCraft.png
   :alt: NodeMCU

Ahoj Svet!
----------

A teraz náš prvý riadok kódu! V spodnej časti obrazovky sa nachádza *REPL* (interaktívna konzola) a ak nám zariadenie pošle nejaké informácie, vypíšu sa práve tam. V hornej časti sa nachádza priestor na písanie nášho kódu. Do tej napíš nasledujúci riadok kódu::

  print("Ahoj Svet!")

Na rozdiel od iných jazykov sa v Pythone za príkazmi nepíše bodkočiarka. Treba si ale dávať pozor, aby na začiatku riadku neboli zbytočné medzery. No a čo tento riadok kódu robí? Zavolá funkciu ``print``, ktorá vypíše argument, ktorý dastala v zátvorke, v našom prípade je to text ``Ahoj Svet!`` (úvodzovky MicroPythonu hovoria, že sa v nich nachádza textový reťazec, no nie sú súčasťou reťazca a preto sa nevypíšu). Keď sa rozhodneme, že sme s našim kódom spokojný a chceli by sme ho spustiť, stlačíme tlačidlo *DownloadAndRun* (modrá šípka). Výpis by sa mal zobraziť dole v *REPL*. 

Ako zapojiť LEDku
-----------------

Teraz si pripravíme breadboad, LEDku, zopár prepojovacích káblikov a rezistor k LEDke. Klasická LEDka má dva piny:

* kratší pin (-) je nad ním zárez v LEDke - pripájame k *zemi*, po anglicky *ground*, skratka je *GND* alebo len *G* (odborne katóda)
* dlhší pin (+) v našom prípade pripájame k *3,3 voltom*, nakoľko piny na NodeMCU majú takéto napätie (odborne anóda)

Na to, aby LEDka svietila, potrebuje byť správne zapojená (plus na plus a mínus na mínus). Ak by sme ju otočili tak by sa jej nič nestalo, len by nesvietila. Taktiež ale potebuje aj správne napätie. Napríklad klasická červená LEDka potrebuje napätie okolo 2,1V a prúd 20mA (mili ampérov - zjednodušene koľko energie potrebuje). Keďže ale NodeMCU má napätie 3,3V, musíme ho nejako unížiť, a to spravíme s rezisorom. Hodnoty rezistorov sa udávajú v *ohmoch* (vyjadruje jeho odpor). Našťastie LEDky nie sú až tak vyberavé a preto nám postačí rezistor s hodnotou medzi 70 ohmov a 1000 ohmov (čiže 1 kilo ohm). Rezistory nemajú polarity, a teda je úplne jedno, ktorých smerom ich zapojíme.

No a čo by sa stalo, ak by sme rezistor nepoužili? LEDka by sa nám veľmi rýchlo vypálila. My budeme používať iba približnú hodnotu odporu rezistoru, no pre presný výpočet pre konkrétnu LEDku (alebo LEDky) vypočítaš `na tejto stránke <http://led.linear1.org/led.wiz>`_. Správny odpor nezávisí len od LEDky, ale aj od vstupného napätia. Pre jednu LEDku potrebuješ iný rezistor ak ju napájaš s 3,3 voltami, a iný pri 5 voltovom zdroji.

Na zapojenie LEDky môžeš využiť breadboard. Nachádza sa v ňom množstvo dierok na zasúvanie či už súčiastok (NodeMCU, LEDky) alebo prepojovacích káblikov. Vrámci každej polovice *breadboardu* sa nachádzajú krátke rady spojených dierok. Zvyčajne to býva 5 spojených dierok. Keď zapojíš do jednej rady viacero káblikov, prepojíš ich tým.

.. danger::
  Vždy pre zapájaním alebo vypájaním nejakých káblikov radšej odpoj NodeMCU z počítača, aby sa náhodou nestalo, že omylom niečo vyskratuješ. Vždy pred opätovným pripojením do počítača si poriadne skontroluj svoje zapojenie! 

Zasuň svoj NodeMCU do *breadboardu* podľa schémy. Ak máš náhodou väčšiu verziu a už Ti nezostanú na bokoch voľné dierky, zapoj iba 1 polovicu NodeMCU. LEDku pripojíme tak, aby bol kratší pin prepojený s ``G`` a dlhší s ``3V``. Jedno z týchto prepojení musí byť spravené poocou rezistoru, no nezáleží na tom ktoré.

<img of led schematic here>

Ešte raz s všetko prekontroluj a môžeš zapojiť USB kábel k svojmu NodeMCU. LEDka by sa mala rozsvietiť.

Môžeš si skúsiť, čo sa stane, ak obe nožičky LEDky zapojíš k *pinu* ``G``, alebo k ``3V``. Nemusíš sa báť, ak je jedno z týchto spojení spravené pomocou rezistora, tak sa LEDke nič nestane, iba nebude v takomto zapojení svietiť.

.. poznámka::
  Aby sa dióda rozsvietila, musí byť správnym smerom pripojená na dve miesta, medzi ktorými je potenciálový rozdiel - čiže napätie. Na pine ``G`` máme 0 voltov, na pine ``3V``  máme 3,3 voltu - ich rozdiel je teda 3,3V. Čosi z tohto napätia nám ešte uberie rezistor, takže v našom prípade sú na pinoch LEDky približne 2 volty. Samotná hodnota napätie nedáva zmysel, ak sa rozprávame iba o jednom pine. Napätie je rozdiel potenciálov medzi dvoma bodmi. V elektronike väčšinou všetky napätia porovnávame vzhľadom k "zemi", čo je nula voltov. Na NodeMCU sú to piny ``G``.

Rozsvecujeme LEDku pomocou kódu
-------------------------------

Opäť odpojíme NodeMCU z USB a LEDku pozapájame podľa schémy. Kým *mínus* zostáva na ``G``, *plus* pripojíme k ``D5``.

<img of schematic LED on D5>

A prečo sme zapojili LEDku k pinu ``D5``? Pretože je jednou z tých, ktoré môžme programovať a nastavovať im výstupné napätie. Konkrétny popis pinov nájdeš tu:

.. figure:: /_static/images/nodemcu-sk.png
  :alt: NodeMCU
  :align: center
  :target: _static/download/nodemcu-sk.pdf

  :download:`Stiahni si tento NodeMCU MicroPython Ťahák (pdf)</_static/download/nodemcu-sk.pdf>`

Ak sa lepšie prizrieš do *Ťaháku*, pri pine ``D5`` je označenie *Pin(14)*. To druhé pomenovanie používa MicroPython a preto keď budeme programovať, budeme používať práve to. Tento ťahák je vždy dobré mať pri sebe, aby sme pri zapájaní vedeli, čo máme programovať.

Teraz môžme pripojiť NodeMCU a spustiť nasledujúci kód::

  from machine import Pin
  ledka = Pin(14, Pin.OUT)
  ledka.value(1)

V tomto kóde sme si najprv naimportovali z knižnice *machine* (špeciálna knižnica pre nastavovanie hardvéru na ESP8266) triedu *Pin*, ktorú odteraz môžme využívať na nastavovanie jednotlivých pinov. V druhom riadku sme si do premennej "ledka" priradili pin 14 s tým, že budeme nastavovať výstupné napätie (preto Pin.OUT). No a teraz na konci zavoláme na objekte *ledka* funkciu *value*, ktorá podľa hodnoty parametra nastaví výstupné napätie na pine. Jednotka nastaví napätie na 3,3V a 0 nastaví napätie na 0V, nič medzi tým nevieme nastaviť.


Blikáme s LEDkou
----------------

* 1 LEDka - time
* for cyklus
* While cyklus


Policajný maják
---------------

červená a modrá LEDka


Knight Rider
------------

8 LEDiek


Cvičenia navyše
----------------

Semafór
"""""""













Typickým 

.. container:: toggle

    .. container:: header

        **Ukáž riešenie**

    .. code-block:: python
       :linenos:

       from plone import api
       asdasdasdasdasd