---
title: "Volební API"
description: >
  Ano, čtete dobře, další vývojářský blog. Tentokrát od lidí, co dělají
  redakční technologie v IHNED.cz.
layout: post
category: obecne
---

Od začátku oddělení redakčního vývoje se snažíme vše, co vyprodukujeme, taky [zveřejňovat](https://github.com/economia) pod otevřenou licencí. S blížícími se volbami programujeme kalkulačku průběžných výsledků, která vychází z dat zveřejňovaných ČSÚ na volby.cz. I tu najdete mezi našimi projekty - viz [Volební moduly](https://github.com/economia/volebni-moduly). Abyste ji však nemuseli zprovozňovat sami, spustíme před volbami veřejné API s již spočítanými výsledky. Konkrétní datum spuštění a finální endpointy včas oznámíme na [našem twitteru](https://twitter.com/vyvojIHNED), zatím pro vás máme specifikaci a ukázkové výstupy na základě dat z voleb 2010.

<iframe src="http://datasklad.ihned.cz/volebni-api/" width="790" height="650" frameborder="0"></iframe>

Co použitím našeho API získáte nad strojově čitelnými daty z Volby.cz? Především to bude průběžný výpočet složení sněmovny včetně preferenčních hlasů, které ČSÚ zveřejní až po sečtení všech výsledků. Také budeme mít k dispozici "mediální" server ČSÚ, který je oddělený od veřejného, takže i pokud volby.cz "spadnou", naše API bude fungovat dál.

Výstup bude ve formátu JSON, pokud byste chtěli JSONP, napište nám a pošleme parametry pro získání tohoto formátu. Počet požadavků na API nemá předem daná omezení, pokud nejste významný internetový portál, tak váš provoz naše technika ustojí. Budeme však monitorovat IP a HTTP referer, vyhrazujeme si právo v případě potřeby váš přístup omezit. Naše data také můžete předávat pomocí vlastní proxy, v takovém případě by neměl vůbec nastat problém, zvlášť pokud využijete HTTP If-Modified-Since, který budeme aktivně sledovat a odpovídat HTTP 304 Not Modified. V takovém případě nemáme problém ani s pollingem 1 request za sekundu. Pro realtime data však pravděpodobně připravíme WebSocketový endpoint pomocí Socket.io, který také včas zveřejníme.