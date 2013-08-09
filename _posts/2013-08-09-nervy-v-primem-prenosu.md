---
title: "Nervy v přímém přenosu"
description: >
  Ve středu proběhlo hlasování o důvěře vlády, a my jsme pro tu příležitost připravili na titulní stránku měřidlo. Co ho pohánělo?
layout: post
category: obecne
---

Ukazatel aktuálního stavu hlasování byl momentální nápad našeho šéfeditora. Hlavní vtip byl v tom, že měl ukazovat výsledek v reálném čase, bez nutnosti obnovovat stránku. Slíbili jsme, že se podíváme, co můžeme udělat...

Bylo jasné, že s AJAXem nevystačíme a že bude potřeba použít nějaké websockety či podobnou technologii. Použili jsme knihovnu [Socket.io](http://socket.io/), která dokáže jako fallback k websocketům použít jiné metody, třeba comet nebo přinejhorším AJAXový heartbeat. Navíc nabízí velmi jednoduché rozhraní pro příjem zpráv, jejich vysílání i "broadcast", tedy vyslání všem naslouchajícím.

![Měřák](/images/rusnok.jpg)

Bylo tedy jasné, že na serveru poběží Node.js, který pomocí [Socket.io](http://socket.io/) obslouží připojené čtenáře a bude jim posílat data o aktuálním stavu hlasování. Na klientu bude vizualizace, která se připojí k Node serveru a zobrazí ukazatel. Rozhraní bylo poměrně jednoduché - natáčení ručičky pomocí CSS transformací, jednoduchá logika, která zajišťovala chvění ručičky, a vlastní mechanismus, zajišťující připojení na server.

Aby měl server co vysílat čtenářům, musel ho někdo krmit daty - k tomu sloužila jednoduchá HTML stránka se seznamem poslanců a tlačítky PRO - PROTI - ZDRŽEL SE - CHYBÍ. Tahle stránka se připojovala taky na server a posílala data o stavu hlasování; server pak jen zajistil vysílání ("broadcasting").

A co se stane v případě, že se člověk, který kliká na tlačítko, uklikne? Když přeslechne, jak poslanec hlasoval? Co se stane, když spadne server? Druhý pokus nemáme. Na celou akci máme pár minut, a pak bude po všem. Takže jsme určili dva "plniče", kteří seděli u stránky se seznamem poslanců. Jejich seznamy byly synchronizované (zase přes websocketí server). Logicky jsme použili i dva servery - "plnící" stránky posílaly svoje zprávy na oba servery, klienti se náhodně připojili na jeden ze dvou serverů. Pokud se spojení zaseklo, klient zkusil automaticky po nějakém čase druhý server.

Nejprve jsme spustili (v pondělí odpoledne) jeden server a na chvíli na domovskou stránku nasadili kód, který otestoval spojení. Vše fungovalo bez problémů. Ze serveru jsme vytvořili image a připravili se, že jej naklonujeme. Mezitím probíhalo ladění designu měřidla.

V úterý jsme otestovali plnění dat a jejich následnou vizualizaci v podobě "kostiček". Stál jsem v newsroomu, četl seznam poslanců a říkal jsem "Pro návrh - proti návrhu" stále dokola.

V úterý v podvečer jsme měli hotový design a spustili jsme druhý server ze stejné šablony.

Ve středu ráno jsme zjistili, že server stále ještě startuje. Nahlásili jsme problém na hotline, a tam zjistili, že se image nevytvořila správně. Nainstalovali jsme tedy druhý server "na zelené louce", nastavili potřebný software, nahráli skripty a sledovali přenos ze sněmovny. 

Když bylo jasné, že se hlasovat během dopoledne nebude, zkusili jsme celý systém ještě jednou. Znovu jsem stál, četl jména poslanců, říkal za každým "Pro návrh" a "Proti návrhu" a všichni okolo sledovali, jestli se ručička hýbe i na mobilech, tabletech a jiných prohlížečích. Pokus dopadl velmi dobře, od stisknutí hlasovacího tlačítka do započítání hlasu uplynuly řádově desetiny sekundy.

A pak jsme čekali. A čekali. A čekali. Připravení na okamžik, až se "přistoupí k hlasování". V ten okamžik jsme nahodili měřidlo na titulní stránku a první klienti se začali připojovat.

Ukazatel počtu připojených klientů uspokojivě rostl, ale lehce podezřelé bylo, že rostl nerovnoměrně - zhruba v poměru 2:5. Když na serveru 1 bylo 400 lidí, na serveru 2 jich bylo 1000. A pak se server 2 zhroutil. Newsroomem obcházelo strašidlo infarktu: *Proč, proč, co se děje?* U mnohých klientů se ručička zastavila. Každá sekunda trvala celou věčnost. Automatika po deseti sekundách začala přepojovat uživatele na první server, takže se postupně ukazatele zase rozjely, ale server 2 stále ležel. Příčina? Zapomenutý *ulimit*, který způsobil zahlcení systémových zdrojů. Na serveru 1 byl nastavený, bohužel neproběhlo klonování a při ruční instalaci serveru 2 jsme na to zapomněli jako na smrt. 

Po odhalení příčiny jsme server okamžitě nahodili a hlasování dojelo už bez problémů. Po odhlasování jsme vzali data (pole s 200 hodnotami), spojili je se jmény poslanců, které připravila redakce, a vydali "kostičky".

![Kostičky](/images/rusnokostky.jpg)

Ve špičce jsme měli připojeno 1600 uživatelů najednou. Nakonec to, díky politickým zákulisním hrám, nebyla tak jednoznačná záležitost, jak jsme si představovali, takže sledování ručičky bylo docela dramatické. Systém zvládl i výpadek jednoho serveru, což je dobrá zpráva. (Ano, víme, byla to školácká chyba, ale komu se nikdy taková nestala, ať první hodí monitorem!) Pro příště víme, že to zvládneme, a taky že nesmíme zapomenout na ulimit!

Pro zájemce [zdroják ke stažení](/dl/rusnometr.zip)

[ihned]: http://ihned.cz "Zpravodajský server Hospodářských novin"