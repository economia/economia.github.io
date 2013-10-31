---
title: "Zápisky z fronty: Volby, část serverová"
description: >
  Zpravodajství k právě proběhlým volbám byl náš dosud největší projekt. Ve špičce běžel na čtyřech serverech (tři frontendy a jeden "počítací" backend, plus jeden nefunkční stroj - o tom později) a jen za sobotní odpoledne obsloužil pár stovek tisíc pageviews (každý s desítkami požadavků). V této minisérii shrneme technologie, jaké jsme použili, a co jsme se za pochodu - nebo spíše pod intenzivní palbou - stihli naučit. První díl pojednává o tom, na jakém železe to vlastně celé běželo.
layout: post
category: obecne
---

## S Linuxem na Azure

V duchu moderních cloud řešení jsme zvolili Microsoftí Azure a nakonec jsme skončili se sestavou dvou small a dvou medium instancí (small - 1 jádro kolem 1,5 GHz, 1,7 GB RAM, medium - 2 jádra, 3,5 GB RAM). První small instance stahovala data z ČSÚ, přepočítávala je do [našeho formátu](/volebni-api/), ukládala do Redisu a generovala vizualizaci sečtených obcí. Ostatní stroje fungovaly jako frontendy - small hlavně pro mobilní uživatele na [m.ihned.cz](http://m.ihned.cz/), oba medium pro velký [ihned.cz](http://ihned.cz). Frontendy měly vždy svůj vlastní Redis, připojený jako slave k centrálnímu masteru. Takto jsme efektivně rozložili zátěž a podle potřeby mohli bezproblémově horizontálně škálovat.

Původní plán byl, že využijeme možnost servery sdružovat do jednoho *Azure Cloud Service*. Pak by se všechny servery umístily do jednoho subnetu vnitřní sítě a za jednu veřejnou, load-balanced IP. Tím pádem by veškerá autorizace k databázi spočívala v jednorázovém nastavení správné masky ve firewallu a díky Azure loadbalancingu by naše škálování bylo pro vnější uživatele zcela transparentní. A to vše na pár kliknutí v Azure Portalu. Jak říkají Angličani: *"too good to be true"*.

## Srážka s realitou

Bohužel nám během příprav nezbyl čas balancer skutečně otestovat, a tak se až během ostrého provozu ukázalo, že se příliš nesnaží různá spojení jednoho klienta předávat stejnému serveru, ale rozděluje je spíše na principu round-robin. S tím se ale vůbec nepohodl [Socket.io](http://socket.io) (resp. jeho nenastavená verze - právě pro toto použití Socket nabízí synchronizaci přes Redis...) a realtime spojení padala jak státník s virózou.

Někde kolem této chvíle nastala v našem řídícím centru panika, protože se zrovna začalo sčítat a naše připravené škálování se právě stalo nepoužitelným. A vzhledem k tomu, že připravený frontend byl za stejnou veřejnou IP, ani neexistovala cesta, jak ho rychle dostat na internet, byť mimo loadbalancing (leda na jiném portu než 80, ale to bysme zase mohli narazit na restriktivní firewally na počítačích klientů). A na vytvoření ready-to-deploy images taky do té doby nebyl čas. Při pokusu o rychlé vytvoření image z nyní stejně nepoužitelného frontendu jsme ještě narazili na další novou informaci, a sice že Azure vyžaduje před jeho vytvořením proběhnutí jakési utilitky, jejíž [manuál](http://www.windowsazure.com/en-us/manage/linux/how-to-guides/linux-agent-guide/) je na osm stran a na jeho čtení fakt nebyl čas. Až v neděli jsem se dozvěděl, že konkrétní příkaz je na jeden řádek a celá procedura vlastně není až tak nutná.

Padlo tedy rozhodnutí vytvořit další server ručně. Naštěstí toto mají Redmondští zvládnuto dobře a nainstalování Node, Redisu a jejich zběžnou konfiguraci již mám vcelku slušně zažranou v "muscle memory". Pak ještě drobné zdržení s úpravou firewallu na nový stroj z nového Cloud Service (a tím jiného IP range) a po asi čtvrthodině máme server připravený. Mezitím se chudák small instance, určená původně pouze pro mobily, zmítala pod náporem tisíců requestů za vteřinu. I přes to timeoutnula pouze párkrát, díky síťové propustnosti Azure a rychlosti Node. Balancujeme jak za krále Klacka pomocí javascriptového střídání zdrojových URL, ale funguje to. Po dalších pár minutách jsme spustili poslední, čtvrtý frontend, který zátěž definitivně srazil pod 25% CPU, od asi pětiny sečtených hlasů tedy již čtenáři viděli výsledky zcela bez komplikací. A konec dobrý, všechno dobré!

## Resumé

Jak bych tedy shrnul řešení? Mít tak půlden vývoje navíc, kdy bychom otestovali, jak funguje loadbalancing se Socket.io a připravili si image systému, pak by vše proběhlo tak, jak jsme si to plánovali. Takhle jsme sice měli pár infarktových momentů, servery (jak Azure tak Node) nás ale podržely a ve výsledku jsme byli schopni s minimálními náklady obsloužit téměř všechny požadavky. Což, pro představu, bylo za to jedno sčítací odpoledne něco přes 300GB.

(Marcel Šulek)