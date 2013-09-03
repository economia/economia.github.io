---
title: "Vyznačte obsah pro tweet pomocí x-tweetable"
description: >
  Takový trik, který pomůže lidem sdílet váš obsah tak, jak si přejete, aby byl sdílený
layout: post
category: opensource
---

Sdílecí tlačítka pro nejrůznější sítě jsou už téměř standardní součástí redakčních systémů. Jenže tohle řešení má slabé místo, a tím je fakt, že nemůžete jednoduše ovlivnit, co budou lidi sdílet. Většinou je jako obsah ke sdílení použit titulek článku, a to dost často nebývá to pravé ořechové.

Naše řešení bylo inspirováno článkem [If you use WordPress, you too can have tweetable sentences like in that New York Times SNL story](http://www.niemanlab.org/2013/08/if-you-use-wordpress-you-too-can-have-tweetable-sentences-like-in-that-new-york-times-snl-story/). S troškou JavaScriptu a jQuery jsme si napsali <x-tweetable title="Jednoduchý kód, kterým můžete ovlivnit, co budou vaši čtenáři sdílet na Twitter.">plugin, který promění vyznačenou část textu na "sdílecí tlačítko" pro Twitter</x-tweetable>. Princip je prostý: V textu si pomocí [custom elementu](http://www.w3.org/TR/2013/WD-custom-elements-20130514/) &lt;x-tweetable&gt; vyznačíme pasáž, která se stane obsahem tweetu pro sdílení. Krátký skript pak z něj udělá tweetovací text.

Samozřejmě, takové řešení bude fungovat pouze v prohlížečích, které se u neznámého elementu nerozsypou. Pokud je pro vás důležité zachovat kompatibilitu a nezavádět nové tagy, můžete pro stejnou funkci využít třeba span s určitou třídou, nebo zneužít existující, ale téměř nepoužívaný tag, například &lt;ins&gt;. (Není to systémové řešení, ale někdy jsou v řetězci vytváření obsahu komponenty, které nemáte pod kontrolou, a které vám nemilosrdně vyhážou vše, co se jim zdá podezřelé, od custom elementů po třídy, a pak se lze k takové oklice uchýlit.)

Fungování pluginu vidíte na téhle stránce o kousek výše. Řešení spočívá v nahrazení obsahu elementu &lt;x-tweetable&gt; odkazem, který otevře "tweetovací okno". Patřičné [kódy jsou k dispozici na JSBinu](http://jsbin.com/UCumEZe/2/edit?html,css,js,output).

Někdy nenajdete vhodnou pasáž přímo, proto můžete do x-tweetable doplnit atribut title, jehož obsah bude použit jako "tweetovací citace".