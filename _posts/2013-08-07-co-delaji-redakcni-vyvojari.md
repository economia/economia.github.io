---
title: "Co dělají redakční vývojáři"
description: >
  Někdo se na Twitteru podivoval, že IHNED.cz má vývojáře. Má, a dokonce hned několik týmů. Chceme vám představit, co dělá právě ten náš.
layout: post
category: obecne
---

[IHNED.cz][ihned] má několik vývojářských týmů. Jeden se stará o přípravu šablon a integraci s redakčním systémem. Pod jejich kompetenci spadá například vývoj 
e-shopu či redesign celých webů. Druhý tým se stará o mobilní aplikaci a iOS verzi. My jsme tým redakčních vývojářů a naším úkolem je být k ruce redakci a vyvíjet 
věci podle aktuální potřeby, jejichž vývoj by byl "standardním způsobem" pomalý. A v novinách platí - buď je to rychle, nebo vůbec. Krom toho se vydáváme za hranice běžného fungování redakčních systémů a každodenní kodérskou rutinu.

Náš tým je nový, vznikl před necelými dvěma měsíci, a jedna z prvních věcí, na které jsme dělali, byla [povodňová mapa](http://data.blog.ihned.cz/c1-60046610-animace-jak-velka-voda-postupovala-ceskymi-rekami). To je typická "datažurnalistická" věc, která se skládá ze dvou částí - nejprve je třeba sehnat surová data, ideálně strojově, pak je zpracovat a vytvořit nástroj pro jejich zobrazení. Pro zobrazování podobných mapových vizualizací používáme knihovnu [Leaflet](http://leafletjs.com/). Frontend je napsaný v JavaScriptu a HTML. Stahování a zpracování dat jsme zařídili jednoduchým skriptem, napráskaným *ad hoc* v PHP.

Jen co přes nás přešly povodně, přišlo zatýkání na Úřadu vlády. (Kuriozita je, že v ten samý den jsme si pozvali [Karla Minaříka](http://karmi.cz/), aby nás proškolil v používání Gitu. Bohužel jsme v půlce školení museli začít řešit aktuální situaci.) Během několika hodin vznikly dlaždice, které vidíte na titulní straně [IHNED.cz][ihned] vpravo vedle *otvíráku*. K nim jsme si napsali i editor, který umožňoval redaktorům měnit obsah podle toho, jak se vyvíjela situace. Vzhledem k tomu, že náš redakční systém není zrovna pružný, tak jsme zvolili současný způsob, tj. nezávislý IFRAME.

Během krize měly dlaždice víc pater, pak se snížily, ale jako formát zůstaly. V těchto dnech pracujeme na jejich redesignu a rozšíření pro více typů informací, protože se ukázalo, i z ohlasů čtenářů, že jde o oblíbený formát. Zejména videokomentáře si čtenáři pochvalují a volali po zpřístupnění [archivu](http://dialog.ihned.cz/videokomentare/).

Při krizi jsme dělali i [mapu vztahů](http://data.blog.ihned.cz/c1-60105930-kdo-co-a-s-kym-sit-vztahu-ktera-ukoncila-politickou-drahu-petra-necase). Vizualizace zajišťuje knihovna [D3](http://d3js.org/) a data jsou uložena v tabulce v Google Docs. Původně jsme pro čtení dat z těchto tabulek používali JS knihovnu, ale časem se ukázalo, že se jedná o velmi pohodlný způsob publikace dat, tak jsme napsali nejprve vlastní proxy, která se proměnila v komplexní službu, jež nám umožňuje načíst data z tabulek v GDocs a transformovat je na nějaký použitelný formát (JSON, JSONP). Dnes vyšla ["stojednička"](http://zpravy.ihned.cz/politika/c1-60386340-grafika-hlasy-proti-rusnokovi) - vizualizace je jednoduchá a využívá opět zdrojové tabulky v Google Docs, podobně jako další tabulky v článcích. Z týchž tabulek čerpají informace i další naše vizualizace - třeba [Zemanova vláda](http://ihned.cz/zemanovavlada) nebo [Mapa moci](http://ihned.cz/mapamoci).

Asi největší práci dalo zpracování [dojezdové mapy MHD](http://ihned.cz/mhd). Samotný zobrazovací engine není příliš složitý; problém byl s množstvím dat. V Praze je okolo 3000 zastávek MHD. My jsme měli k dispozici jízdní řády pro jednotlivé zastávky - tedy to, co vidíte na zastávce vylepené ve vitrínce. Z těchto údajů jsme museli propočítat, jak dlouho vám bude trvat cesta z jedné každé stanice do všech ostatních. A to všechno několikrát - pro špičku, pro prázdniny, pro provoz mimo špičku. Totéž pro loňský rok. Kolega Marcel odhaduje, že se jednalo o víc než 3 miliony výpočtů. Tohle počítat na lokálních počítačích je vyložený nesmysl, který by i na našich výkonných strojích trval několik měsíců, takže jsme využili sílu cloudu a nasadili paralelní výpočet na stovce virtuálních počítačů u Amazonu.

Pro [mapu kriminality](http://data.blog.ihned.cz/c1-60335790-zizkovu-a-libni-zdaleka-se-vyhni-kde-se-v-praze-nejvic-krade-znasilnuje-a-loupi) jsme zase potřebovali zjistit souřadnice policejních okrsků. Policie ČR nám sice poskytla data o tom, které adresy patří pod kterou služebnu, ale geografické zaměření bylo na nás. Z ČÚZK jsme získali informace o všech zaměřených adresních místech v ČR, kterými jsme nakrmili databázi, a pak jsme pro všechny policejní okrsky zjišťovali, jaké domy pod něj spadají a jaké mají souřadnice. O týden později jsme si to zopakovali i pro Brno, kde jsme měli situaci veselejší o to, že některé ulice nejsou ani zaměřené. U jiných jsou hranice okrsků popsány stylem: "Ulice Vondráčkova, čísla 1, 3, 7 a 11", "Ulice Veverkova kromě čísel 5, 7 a 9" nebo "Ulice Kosmonautů, pouze sudá čísla".

Právě teď čekáme na zahájení hlasování v PSP ČR o důvěře Rusnokově vládě. V tomto hlasování máme pokusné želízko v ohni - live ukazatel aktuálního stavu. Navenek je poměrně nenápadný, uvnitř jej ale pohání [Socket.io](http://socket.io/), který dokáže v reálném čase komunikovat se skriptem ve vašem prohlížeči. Výsledek uvidíte na titulní stránce [IHNED.cz][ihned] po dobu hlasování.

To jsou tedy věci, které připravil a zveřejnil náš tým - tým redakčních vývojářů IHNEDu. *Stay tuned*, budeme se těšit.

[ihned]: http://ihned.cz "Zpravodajský server Hospodářských novin"