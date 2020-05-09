Inštalácia Pythonu a MicroPythonu
=================================

Programovací jazyk Python
-------------------------

Python je veľmi populárny a všestranný programovací jazyk odporúčaný pre vyučovanie základov programovania. Práve preto postupne nahrádza iné programovacie jazyky na hodinách informatiky. Vo veľkom Python využívajú aj v Google, Dropbox, Európskej organizácii jadrového výskumu CERN, sociálnych sieťach Facebook, Pinterest a Instagram, či pri vyučovaní na prestížnej vysokej škole MIT.

Autorom jazyka Python je Guido van Rossum (prvá verzia je z 1989). V súčasnosti jazyk Python vyvíja a spravuje komunita, zastrešovaná medzinárodnou organizáciou *Python Software Foundation* (skratka *PSF*). Samotný jazyk je *open-source*.

Python je interpretovaný jazyk, a preto sa po dopísaní kódu ho neskompilujeme (ako napríklad *C* či *Pascal*) ale spustíme ho v interpreteri. Ten náš kód za chodu číta a prekladá na strojové inštukcie pre procesor. Preto je potrebné, aby sme na spustenie Python kódu mali na počítači nainštalovaný Python interpreter. (ako si vysvetlíme o schvíľu)

Odporúčame používať najnovšiu verziu **Python3** (v súčasnosti je to Python3.6). Python2 je staršia verzia Pythonu a už nie je vhodné v nej programovať. 

V čom sa Python líši snáď najviac od iných programovacích jazykov je práve komunika. Tá je tvorená profesionálmi, začiatočníkmi, učiteľmi i víkendovými programátormi a tak je veľmi rôznorodá. Po celom svete sa pravidelne organizujú konferencie *PyCon* (čiže PYthon CONference). Na Slovensku je táto konferencia organizovaná raz ročne občianskym združením *SPy* (*Slovak Python User Group*).  

Programovací jazyk MicroPython
------------------------------
MicroPython je upravená verzia Pythonu, ktorá beží aj na menej výkonných zariadeniach. Vďaka tomu vieme v MicroPythone programovať mikroelektroniku a interagovať s okolitým svetom pomocou LED diód, senzorov, bzučiakov, motorčekov, atď. Takéto zariadenia sú zároveň rádovo lacnejšie ako počítače pre klasický Python. Obrovskou výhodou je fakt, že syntax je pre obe verzie jazyka rovnaká, a tak sa učiteľom aj žiakom stačí naučiť iba jeden jazyk.

Tak ako na spustenie Python kódu na počítači potrebuje nainštalovaný interpreter, tak aj pre MicroPython kód musíme na mikroprocesom najprv nainsťalovať MicroPython interpreter. To stačí spraviť raz a následne mu budeme už len posielať naše zdrojové kódy na preklad. Raz za čas sa ale oplatí MicroPython na zariadení preinštalovať na novšiu verziu, aby sme mali vždy čo najviac funkčný interpreter.

MicroPython interpreter vymyslel Damien George v roku 2013 pre vývojovú dosku *pyboard* (s mikroprocesorom *STM32*). V súčasnosti existuje viacero verzií MicoPythonu pre rôzne mikroprocesory. My budeme používať verziu pre *ESP8266*, nakoľko tento mikroprocesor na nachádza na doskách *NodeMCU*.

.. warning::
  Jednotlivé verzie MicroPythonu pre rôzne mikroprocesory sa medzi sebou mierne líšia! Preto nie všetok MicroPython kód z internetu bude fungovať na ESP8266.

Inštalácia Pythonu
------------------

**Windows**

Z web stránky `www.python.org <http://python.org/>`_ si stiahnite verziu **Python3.5** (na konci sa bude nachádzať ešte jedno číslo, no to nás nemusí zaujímať). Dôležité je, aby sme sťahovali Python3 a nie Python2. Verziu na 64bit sťahujte iba ak máte 64 bitový operačný systém.

<img of Python.org website>

<img of PATH option>

Ďôležité je, aby sme pri inštalácii zaklikli možnosť **Add Python 3.5 to PATH**.

<img of INSTALL FOR ALL USERS>

V okne *Advanced Options* zaklikneme možnosť **for all users**.

Po ukončení inštalácie otvoríme príkazový riadok (aglicky ...), zadáme príkaz ``python`` a stlačíme Enter.

<img of console output>

Ak sa zobrazí takýto výpis ukončený troma zobáčikmi, inštalácia prebehla úspešne. Konkrétne sme otvorili REPL, ale tom si vysvetlíme neskôr.


**Linux**

Na distribúciach založených na Debiane (napr. Ubuntu) zadáme do príkazového riadka::

  sudo apt-get update
  sudo apt-get install python3 python3-pip python3-tk

Na destribúciach založených na Fedore zadáme do príkazového riadka::

  sudo dnf install python3 python3-pip python3-tk


**MacOS**

::
  
  I need help...

IDE pre Python
--------------

Monžností, v čom písať Python kód je veľa. Ja odporúčam **mu editor**, nakoľko je navhnutý pre začiatočníkov a zároveň poskytuje veľmi silné nástroje na krokovanie a debugovanie programu.

Pre inštaláciu mu editora je potrebné si otvoriť konzolu a zadať príkaz::

  pip3 install mu-editor

Na Linuxe je na začiatok príkazu potrebné pridať ``sudo``.

<img of mu editor>

*Mu editor* spúšťame tak, že v konzole zadáme príkaz ``mu``. Treba si skontrolovať, či sa nachádzame v Python3 móde. Ak nie, dole v pravo je možné zmeniť aktuálny mód.

Inštalácia driveru a prístup k zariadeniu
-----------------------------------------

Na NodeMCU sa v blízkosti USB konektora nachádza ďaľší mikročip - sériový prevodník. Vždy je na ňom napísaný jeho názov (veľmi malým písmom). Najčastejšie sa používajú tieto dva:

.. image:: /_static/images/usb_chips.png

.. note::
  Treba použiť kvalitný (a hlavne funkčný) dátový kábel! Niektoré, určené iba na nabíjanie, sú v našom prípade nepoužiteľné. Ak ti nejde pripojiť k zariadeniu, skús iný USB kábel.

**Windows**

Podľa toho, aký sériový prevodník máš, stiahni si driver pre svoj operačný systém:

* CH340
   * `Windows 7 <http://www.arduined.eu/files/CH341SER.zip>`_

   * `Windows 8 a novší <http://www.arduined.eu/files/windows8/CH341SER.zip>`_

* CP2102
   * `Windows 7 a novší <https://www.silabs.com/documents/public/software/CP210x_Windows_Drivers.zip>`_

Po úspešnej inštácii môžeš zapojiť svoje zariadenie. Následne budeš musieť ešte zistiť, k akému *portu* sa zariadenie pripojilo. Otvor si preto správcu zariadení a tam by sa malo nachádzať zariadenie s názvom totožným s názvom sériového prevodníka. Všimni si, že sa pod jeho názvom nachádaza *COM* a za tým nejaké číslo. To znamená, že driver bol dobre nainštalovaný a zariadenie sa dokázalo pripojiť.

<img of device manager here>

**Linux**

Na Linuxe nie je potrebné inštalovať žiaden driver, avšak na prístup k zariadeniu si budeš musieť nastaviť isté práva. Otvor konzolu a zadaj príkaz::

  Fedora:
  $ sudo usermod -a -G dialout,lock $(whoami)

  Debian/Ubuntu:
  $ sudo usermod -a -G dialout $(whoami)

Po tomto príkaze **je potrebné sa odhlásiť zo svojho účtu a znovu prihlásiť** (alebo rovno reštartovať počítač).

Teraz môžeš pripojiť NodeMCU do počítaču a v príkazovom riadku zadaj príkaz ``dmesg | tail``, ktorý ti vypíše niečo takéto::

   $ dmesg|tail
   [703169.886296] ch341 1-1.1:1.0: device disconnected
   [703176.972781] usb 1-1.1: new full-speed USB device number 45 using ehci-pci
   [703177.059448] usb 1-1.1: New USB device found, idVendor=1a86, idProduct=7523
   [703177.059454] usb 1-1.1: New USB device strings: Mfr=0, Product=2, SerialNumber=0
   [703177.059457] usb 1-1.1: Product: USB2.0-Serial
   [703177.060474] ch341 1-1.1:1.0: ch341-uart converter detected
   [703177.062781] usb 1-1.1: ch341-uart converter now attached to ttyUSB0

<replace code with image from console>

Ako vidíš, v poslednom riadku sa pripojilo zariadenie k ``ttyUSB0``. Keďže sa nachádza v adresári ``/dev``, jeho celá cesta ``/dev/ttyUSB0``. V tomto prípade budeme k NodeMCU pristupovať ako k ``/dev/ttyUSB0``. Posledná číslica môže byť ale aj iná (napríklad ``ttyUSB1``), alebo sa celý súbor môže nazývať trochu inak (napríklad ``/dev/ttyACM0``).

**MacOS**

Podľa toho, aký sériový prevodník máš, stiahni si driver pre MacOS:

* `CH340 <http://blog.sengotta.net/wp-content/uploads/2015/11/CH34x_Install_V1.3.zip>`_
* `CP2102 <https://www.silabs.com/documents/public/software/Mac_OSX_VCP_Driver.zip>`_

Podrobnejší návod na inštaláciu CH340 `nájdeš tu <http://www.mblock.cc/posts/run-makeblock-ch340-ch341-on-mac-os-sierra>`_ (v angličtine).


Inštalácia MicroPythonu
-----------------------

Na to, aby sme mohli programovať ESP8266 s MicroPythonom, budeme naň ešte pred tým musieť najprv nahrať MicroPython interpreter.

**Stiahnutie MicroPython firmvéru**

Najnovší MicroPython firmvér si môžeš stiahnuť na na stránke `micropython.org/download#esp8266 <http://micropython.org/download#esp8266>`_. Odporúčame najvovší (*latest*) zo sekcie *stable firmware for the ESP8266*.

**Inštalácia esptool.py**

Keď už máme stiahnutý MicroPython firmvér, na NodeMCU ho nahráme pomocou nástroja ``esptool.py``. Ten ale vyžaduje nainštalovaný *Python3* a *pip3* (tie sme inštaloval v predchádzajúcom kroku).

Do príkazového riadka zadaj::
   
   pip3 install esptool

Ak používaš Linux, budeš na začiatok príkazu musieť pridať ``sudo``.

**Nahratie firmvéru na NodeMCU**

Nástroj esptool.py sa spúšťa cez konzolu.

Teraz môžme pripojiť NodeMCU. Pred nahratím firmvéru je najlepšie vymazať ten pôvodný::

   esptool.py --port moj_port erase_flash

``moj_port`` nahraď adresou smerujúcou k zariadeniu (na Windows začína s ``COM`` a za tým číslo, na Linuxe ``/dev/ttyUSB`` a za tým číslo). Ako nájsť port zariadenia sme si ukázali v predchádzajúcej sekcii.

.. warning::
  Niekedy je potrebné pred vymazávaním starého firmvéru a nahrávaním toho nového strlačiť tlačidlo ``FLASH`` na NodeMCU (ved+la USB konektora) a držať ho počas vykonávania operácie.

Nahratie nového firmvéru::

   esptool.py --port moj_port --baud 460800 write_flash --flash_size=detect 0 moj_micropython_firmver

``moj_micropython_firmver`` nahraď názvom stiahnutého MicroPython fimvéru, ktorý bude vyzerať takto nejako: ``esp8266-2016-05-03-v1.8.bin``

IDE pre MicroPython
-------------------

.. note::
  Názov COM portu pre zariadenie sa môže zmeniť, ak zariadenie vypojíme a opäť zapojíme do PC.

Tak ako pri klasickom Pythone, aj pri MicroPythone je viacero možností, v čom písať kód a ako ho nakrávať. Momentálne pre platformu Windows odporúčame stiahnuť `uPyCraft <https://github.com/DFRobot/uPyCraft>`_ a pre Linux a MacOS zas `ESPLorer <https://esp8266.ru/esplorer/>`_. 

**uPyCraft**

uPyCraft stiahneme z `github stránky <https://github.com/DFRobot/uPyCraft>`_ (hľadajte najnovšiu verziu, napríklad uPyCraft_V0.29.exe). Kliknite na ňu a následne v pravo kliknite *Download*. Program netreba inštalovať, stačí ho iba spustiť.

**ESPlorer**

Pre spustenie ESPloreru musíme najprv stiahnúť Javu (verzia 7 alebo vyššia). Tú stiahnete `na tomto odkaze <https://java.com/en/download/>`_

Samotný ESPlorer stiahnete zo stránky `esp8266.ru/esplorer <https://esp8266.ru/esplorer/>`_

Ak ste úspešne nainštalovali JAVA, tak po dvojkliknutí na ESPlorer.jar by sa Vám program mal spustiť.
Pre Linux otvorte príkazový riadok v adresári, kde sa nachádza súbor *ESPlorer.jar* a zadajte príkaz ``java -jar ESPlorer.jar``.


**Ďaľšie možnosti**

Ďaľšou možnosťou, ako nahrávať kód na ESP8266 je program **AMPY**. Ten sa spúšťa iba cez konzolu. Návod k nemu nájdete na stránke `micropython.sk <http://micropython.sk/micropython_na_nodemcu/zaciname/nahravanie_suborov.html>`_.
