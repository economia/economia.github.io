---
title: "Volební API"
description: >
  Jiná média ukazují výsledky sčítání ve své vizualizaci. My vám dáme kromě vizualizace i zdrojová data online!
layout: post
category: obecne
---

Od začátku oddělení redakčního vývoje se snažíme vše, co vyprodukujeme, taky [zveřejňovat](https://github.com/economia) pod otevřenou licencí. S blížícími se volbami programujeme kalkulačku průběžných výsledků, která vychází z dat zveřejňovaných ČSÚ na volby.cz. I tu najdete mezi našimi projekty - viz [Volební moduly](https://github.com/economia/volebni-moduly). Abyste ji však nemuseli zprovozňovat sami, spustíme před volbami veřejné API s již spočítanými výsledky. Konkrétní datum spuštění a finální endpointy včas oznámíme na [našem twitteru](https://twitter.com/vyvojIHNED), zatím pro vás máme specifikaci a ukázkové výstupy na základě dat z voleb 2010.

AKTUALIZOVÁNO:

API nabízí tři datasety - [parties](http://economia-node2.cloudapp.net/api/parties), [candidates](http://economia-node2.cloudapp.net/api/candidates) a [country](http://economia-node2.cloudapp.net/api/country). Obsahují seznam stran a jejich výsledků, seznam již zvolených kandidátů a průběžné výsledky sčítání. Viz [popis](http://datasklad.ihned.cz/volebni-api/).

Co použitím našeho API získáte nad strojově čitelnými daty z Volby.cz? Především to je průběžný výpočet složení sněmovny včetně preferenčních hlasů, které ČSÚ zveřejní až po sečtení všech výsledků. Také máme k dispozici "mediální" server ČSÚ, který je oddělený od veřejného, takže i pokud volby.cz "spadnou", naše API bude fungovat dál.

Výstup je ve formátu JSON. Počet požadavků na API nemá předem daná omezení, pokud nejste významný internetový portál, tak váš provoz naše technika ustojí. Budeme však monitorovat IP a HTTP referer, vyhrazujeme si právo v případě potřeby váš přístup omezit. Naše data také můžete předávat pomocí vlastní proxy, v takovém případě by neměl vůbec nastat problém, zvlášť pokud využijete HTTP If-Modified-Since, který budeme aktivně sledovat a odpovídat HTTP 304 Not Modified. V takovém případě nemáme problém ani s pollingem 1 request za sekundu. 