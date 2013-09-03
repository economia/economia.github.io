---
title: "Tuníme Sublime Text 2"
description: >
  Nejen samými kool věcmi, spouštěním serverů a pokřikováním v newsroomu je živ redakční vývojář. Čas od času musíme taky sednout a věnovat se té poctivé kodéřině. Každý vývojář si nastaví své vývojové prostředí tak, aby mu vyhovovalo, stejně jako si každý koloťuk omotá kladívko vlastní sadou umolousaných leukoplastí. My používáme, až na výjimky, výborný textový editor Sublime Text 2, který jsme si potunili sadou pluginů.
layout: post
category: sublime
---

[Sublime Text 2](http://www.sublimetext.com/) je, věřte nebo ne, opravdu nejlepší textový editor pro vývojáře a kodéry. Rychlý, lehký a snadno upravitelný pomocí obří sady pluginů. Pokud jste zvyklí pracovat s IDE (Borland Pascal... ehm... tedy... Visual Studio, NetBeans, Eclipse, WebStorm, ...), bude vám Sublime připadat strohý, ale ten, kdo si až dosud vystačil s (výborným) PSPadem, může shledat Sublime zajímavým.

Po instalaci je potřeba nainstalovat jako úplně první věc [Package Manager](https://sublime.wbond.net/installation#st2). Ten pak řídí stahování a instalaci dalších pluginů. Stačí stisknout Ctrl+Shift+P, napsat "Install packages", a pak už jen vybírat. <x-tweetable title="Pár tipů na pluginy pro Sublime Text 2">Co jsme si nainstalovali my?</x-tweetable>


##Theme - Nil

Barevné schéma ve světlé i tmavé mutaci

##Alignment

Dokáže zarovnat víc řádků pod sebou nejen podle prvního znaku, ale třeba tak, aby byly zarovnané znaky "="

##All Autocomplete

Automatické doplňování textu ze všech otevřených souborů

##Clipboard History

Pokud někdy kopírujete text, tak vám tenhle plugin ušetří mnohé hledání a "odkopírovávání" obsahu.

##DataConverter

Pomůže s převodem CSV souborů do různých jiných formátů

#DocBlockr

Usnadňuje psaní dokumentace v syntaxi PHPDoc, JSDoc apod. Hodí se, když pak pracujete třeba s [Daux.io](http://daux.io/)

##Emmet

Dříve ZenCoding. Urychlí psaní HTML a CSS

##EncodingHelper

Může se to zdát absurdní, ale i v roce 2013 stále existují weby, které nepoužívají kódování UTF-8. Třeba ten náš. Snažíme se používat UTF kde to jde, ale někdy musíme sáhnout i do oblastí, kde je stále Windows-1250. A pak potřebujeme EncodingHelper.

##Expand Selection to Quotes

Pomůže vybrat text v uvozovkách

##Git

Snazší integrace s Gitem. Marcel doporučuje následující nastavení:
    { "keys": ["ctrl+'", "ctrl+c"], "command": "git_commit"},
    { "keys": ["ctrl+'", "ctrl+a"], "command": "git_add_choice"},
    { "keys": ["ctrl+'", "ctrl+p"], "command": "git_push"},
    { "keys": ["ctrl+'", "ctrl+q"], "command": "git_quick_commit"},

##GitGutter

Ukazuje v postranním proužku provedené změny proti poslednímu commitu

##LiveReload

Soubor uložíte - a automaticky se v prohlížeči obnoví.

##Origami

Pomáhá s prací ve více panelech

##Pretty JSON

Pokud pracujete, jako my, často s formátem JSON, oceníte formátování přes Ctrl+Alt+J

##SFTP

Automaticky kopíruje změněné soubory na server přes (S)FTP/SCP

##SublimeCodeIntel

Inteligentní doplňování kódů

##SublimeOnSaveBuild

Při uložení provede build (u nás nejčastěji minifikaci skriptů a jejich překlad z LiveScriptu do JS)

##YUI compressor

Nejjednodušší způsob, jak minifikovat skripty a styly.