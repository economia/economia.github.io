---
title: "Vývojářský blog?"
description: >
  Ano, čtete dobře, další vývojářský blog. Tentokrát od lidí, co dělají
  redakční technologie v IHNED.cz.
layout: post
category: obecne
---

Tak určitě, není to žádná převratná myšlenka, vždyť jich je dvanáct do tuctu.
Proč tedy další? A kdo vůbec jsme?

Jsme lidi, co připravují v Economii nejrůznější speciály a redakční nástroje pro [IHNED.cz][ihned]. Ne, naší starostí
není redakční systém, my se nestaráne ani o sociální sítě ani o moderaci komentářů. Naši práci uvidíte především na
nestandardních "pikoškách", jako je třeba [Mapa moci](http://ihned.cz/mapamoci) nebo [Zemanova vláda](http://ihned.cz/zemanovavlada).

Naše práce je specifická tím, že děláme "rychloobrátkové zboží". Nemáme na každou věc týdny času. Většina vizualizací vzniká v řádu několika málo dnů, kdy je potřeba všechno připravit, napsat a publikovat. Výsledek musí být funkční a pochopitelný, ale nemusí být naprosto perfektní, stačí *good enough*. Primárním cílem naší práce je *exekuce* - tedy dotáhnout věc do konce a publikovat ji. Na druhou stranu nás nemusí pálit dlouhodobé rozvíjení jedné služby...

Takový styl práce má svoje specifika. Věci musí být jednoduché, rychle napsané, i za cenu hacků, ale na druhou stranu musí být znovupoužitelné, takže pokud možno univerzální. Když máme možnost něco "napráskat" rychle v nějaké knihovně, tak to uděláme, i když to nebude stoprocentní - ale pokud si máme vybrat mezi vypiplaným řešením, které budeme psát dva týdny, a funkčním řešením, co máme za dva dny venku, bereme vždy to druhé.

Při práci používáme především JavaScript a jeho knihovny. [jQuery](http://jquery.com/), [D3](http://d3js.org/), [Leaflet](http://leafletjs.com/), to je náš denní chleba. K tomu třeba [Twitter Bootstrap](http://twitter.github.io/bootstrap/). Sledujeme samozřejmě novinky v oboru - poslední věc, na kterou jsme se koukali, je [Bower](http://bower.io/). Místo JavaScriptu někteří používají [LiveScript](http://livescript.net/), čisté CSS nahrazují [Stylusem](http://learnboost.github.io/stylus/)... Testujeme v [qUnit](http://qunitjs.com/) a používáme [Live Reload](http://livereload.com/). Verzujeme Gitem a používáme k tomu GitHub a BitBucket.

Na serverech používáme taky různé technologie. Něco v Pythonu, něco v PHP, kolegové "dataři" mají na své experimenty v jazyce R spuštěný Shiny server... Před tím vším jsou předsazené proxy na nginx. Databáze je jednak klasická MySQL, ale na některé věci se nám víc hodí [Redis]() nebo [neo4j](http://www.neo4j.org/).

Většina z nás píše v [Sublime Text 2](sublimetext.com), který jsme si *vytunili* pár pluginy, což by mohlo být téma na příští zápisek.

O čem tady budeme psát? O věcech, na které jsme přišli při práci, o zajímavých technologiích, které jsme objevili, o nápadech, co šly okolo, a v neposlední řadě o našich vlastních knihovnách, které nám vzniknou pod rukama a které dáme ven k použití (pod nějakou BSD-like licencí, nebojte se GPL).

<x-tweetable title="Vývojáři z redakce IHNED.cz mají vlastní blog">Doufám, že to bude i pro vás zajímavé čtení.</x-tweetable>


[ihned]: http://ihned.cz "Zpravodajský server Hospodářských novin"