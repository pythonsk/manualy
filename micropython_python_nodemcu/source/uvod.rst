Úvod
====


O tomto materiáli
-----------------
Materiál *MicroPython, Python a NodeMCU pre stredné školy I.* je určený pre začiatočníkov v Programovaní hardvéru pomocou MicroPythonu. Žiadne predchádzajúce skúsenosti s programovaním či hardvérom nie sú potrebné, všetky potrebné informácie pre prejdenie všetkých kapitol nájdete tu.


Prečo hardvér?
--------------

Dôvodov, prečo sa naučiť programovať hadvér môže byť viacero. V prvom rade je programovanie hadvéru veľká zábava a s jeho pomocou si dokážete vytvoriť množstvo zaujímavých (a i praktických) projektov či zlepšovákov. Zároveň však je dnes pri obrovskom množstve elektroniky okolo nás potrebné, aby každý mal aspoň základnú gramotnosť v tejto oblasti. Vplyv elektroniky v našich životoch sa bude iba zvyšovať, a aj práve vďaka prichádzajúcemu *Internetu vecí* (anglická skratka *IoT*).

Metodika 
--------

Rozdiel medzi jazykom Python3 (spúšťame na počítači) a jazykom MicroPython (spúšťame na mikrokoprocesoroch) si vysvetlíme v nasledujúcej kapitole, no nakoľko medzi nimi sú nejaké rozdiely a budeme pracovať s oboma, v tomto materiáli sa budeme držať nasledujúcich konvencií pri pomenovaní:

* *Python3* - verzia Pythonu pre počítač
* *MicroPython* - verzia Pythonu pre mikroprocesor (v našom prípade ESP8266)
* *Python* - platí všeobecne pre obe verzie jazyka (zväčša sa to bude týkať syntaxe, nakoľko tá je u oboch rovnaká)

Odporúčam prechádzať kapitolami a sekciami postupne, nakoľko majú logickú následnosť. V každej kapitole sa nachádzajú aj nejaké cvičenia navyše - v nich sa nachádzajú informácie navyše a zároveň slúžia na precvičenie programovania a zapájania hardvéru.

Predovšetkým vyššie kapitoly sú postavené viac na praktických projektoch. Na konci tohto materiálu sa nachádza stučný prehľad často používaných programovacích príkazov, popis k súčiastkam a zhrunutie fyzikálnej teórie (napr. k rezistorom)


Potrebné vybavenie
------------------

Väčšinu zadaní je možné prejsť s nasledovnými súčiastkami (tzv. **základný set**):

* *NodeMCU* - vývojová doska s mikroprocesorom ESP8266
* *Breadboard* - slúži na vytváranie elektrických spojení
* *Prepojovacie kábliky* - budeme ich zapájať do *breadboardu*
* *DS18B20*
* *Fotorezistor*
* *I2C Displej*
* *Neopixel LED Strip*
* *LEDky RGB aj jednofarebné*
* *Rezistory*

V cvičeniach sa nachádzajú ďaľšie súčiastky, ktoré na ne budete potrebovať, no je na Vás, ktoré cvičenia sa rozhodnete si spraviť. (Bližší popis nájdete vždy pri každom cvičení, alebo na konci tohto materiálu)


Spätná väzba
------------

Je veľmi dôležité, aby sme vedeli, či tieto materiály niekto využíva a čo Vám v nich chýba / vadí. Zároveň ak nájdete akékoľvek chyby či nejasné formulácie textov, chceme o tom počuť. 


Licencia a šírenie
------------------

Ak nie je v nejakej kapitole či sekcii napísané inak, platí otvorená licencia CC BY-SA. Tá umožňuje tento materiál voľne šíriť a modifikovať, no len s uvedením pôvodného autora a len pre nekomerčné účely.


Autori & Kontakt
----------------

Autorom tohto textu je Marek Mansell.

Kontakt: *marek.mansell@gmail.com*