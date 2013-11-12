---
title: "Zápisky z fronty: Volby, část softwarová"
description: >
  Kvůli volbám jsme si naprogramovali řadu užitečných utilit. Spousta se jich zase čtyři roky nebude hodit, ale pár kousků je přeci jen univerzálnějších. Nyní konečně bylo trochu času projít repozitáře, dopsat readme a dát je k dispozici světu.
layout: post
category: obecne
---

Kvůli volbám jsme si naprogramovali řadu užitečných utilit. Spousta se jich zase čtyři roky nebude hodit, ale pár kousků je přeci jen univerzálnějších. Nyní konečně bylo trochu času projít repozitáře, dopsat readme a dát je k dispozici světu (nadpisy vedou na příslušné repozitáře).

## [Volební moduly](https://github.com/economia/volebni-moduly)

Kolekce skriptů pro stažení volebních výsledků ze serveru [ČSÚ](http://volby.cz/opendata/opendata.htm), výpočet rozdělení mandátů stranám a rozdělení stranických mandátů kandidátům (včetně preferenčních hlasů). Jako bonus také indikuje nejslabší mandát - takový, který může strana nejsnáze ztratit. To je vždy poslední mandát v každém kraji - kandidát jej může ztratit pokud ho překoná další v pořadí ze stejného kraje, pokud o mandát přijde celý kraj (při přepočítání rozdělení) nebo když nějaká strana nově překoná 5% kvórum.

## [Vizualizace výsledků](https://github.com/economia/volby-2013)

Generátor SVG, který byl podkladem pro naše [volební mapy](http://data.blog.ihned.cz/c1-61086960-jak-se-zmenila-politicka-mapa-republiky-vysledky-snemovnich-voleb-v-kazde-obci-od-roku-1996-do-vcerejska). Pokud vás zajímá, jestli někde volili Pravý Blok nebo kde Okamura porazil Babiše, určitě se mrkněte.

## [SVG Mapper](https://github.com/economia/svg-mapper)

Převodník SVG obrázku na mapové podklady použitelné jako vrstva v Leafletu nebo Google Maps. Díky němu jsme převedli vizualizaci výsledků (což bylo 9MB velké SVG, jehož vykreslení trvá i na výkonném PC 5-10 vteřin) na stovky mapových dlaždic různé úrovně přiblížení, které jdou zobrazit za pár stovek milisekund a kilobajtů. Protože nám přišel jako užitečný pro komunitu i za hranicemi naší republiky, je k němu zpracován poměrně podrobný manuál v angličtině.

## [Package & Response](https://gist.github.com/veproza/7433985)

[Minule jsem psal](/zapisky-z-fronty) o zátěži, kterou naše servery ustály. Kromě extrémně rychlé architektury Node na tom nesla svůj podíl naše in-memory cache, Package. Využili jsme specifika zpravodajského webu, totiž že drtivá většina požadovaného obsahu (daleko přes 99%) je představuje pouze pár kilobajtů dat a tak jsme si tato data vždy připravili, gzipovali a až do jejich invalidace je servírovali všem, kdo si o ně řekli. Jak vypadala naše již druhá implementace této metody (první byla u Hatecloudu) se můžete podívat v [Gistu](https://gist.github.com/veproza/7433985). Zároveň tam najdete i třídu zastřešující pár convenience metod pro HTTP request, se kterou Package spolupracuje.

*Marcel Šulek*
