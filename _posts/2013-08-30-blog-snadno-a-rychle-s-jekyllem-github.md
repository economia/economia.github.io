---
title: "Blog snadno a rychle s Jekyllem, GitHubem a na Windows"
description: >
  Kdyby vás někdy napadlo udělat si vlastní blog na GitHubu, tak zde najdete pár tipů.
layout: post
category: opensource
---

GitHub je opravdová sociální síť pro vývojáře. Bez GitHubu by Git byl jen verzovací systém s úchylným workflow a sadistickými volbami příkazové řádky. S GitHubem dává celé tohle snažení smysl. GitHub nabízí nejen možnost uložit si zdrojáky, navzájem je sdílet, vylepšovat a komunikovat spolu, ale pomáhá i s automatizací práce, no a v neposlední řadě i s propagací pomocí [GitHub Pages](http://pages.github.com/).

Není to nová služba, podobná možnost existovala (a snad stále ještě existuje) přímo na GitHubu, pomocí speciálně pojmenované branche, do které lze ukládat HTML soubory, ale [GitHub Pages](http://pages.github.com/) jsou o něco jednodušší, nevážou se na konkrétní repozitář, ale samy jsou repozitářem.

Když jsme se rozhodli pro blog, zkoušeli jsme různé hostované platformy. Starat se o vlastní WordPress bylo pro nás lehce "overkill", však naše potřeba je uspokojená tím, že jednou za čas napíšeme článek. Nic víc. Hostovaný WordPress či Blogger jsou sice mocné nástroje, ale pořád je tam spousta práce s nastavením a pro nás platí, že "čím jednodušší, tím lepší". 

Vrátili jsme se tedy na úplné počátky blogování a <tweetable title="Jak použít k blogování Jekyll, Github Pages a Disqus?">rozhodli se využít nějaký offline generátor stránek</tweetable>, jako býval třeba [EasyBlog](http://www.elka.cz/easyblog/), jen holt v modernějším provedení. O diskuse, které jsou hlavní důvod, proč by měl blog mít nějaký serverový background, se díky [Disqusu](http://disqus.com/) není potřeba starat. Takže nějaký generátor, který vezme z jedné strany články, z druhé šablonu, a vyplivne hotové stránky. Ty pak nahrajeme na [GitHub Pages](http://pages.github.com/), a máme hotovo.

Existuje několik podobných generátorů. Začal s tím [Jekyll](http://jekyllrb.com/), a podle jeho vzoru vzniklo několik klonů v různých jazycích. Hledali jsme, který použít, a nakonec padla volba na ten první jmenovaný. Hodně tomu napomohla i nepatrná zmínka na GitHubu, že GitHub Pages [podporují nativně Jekyll](https://help.github.com/articles/using-jekyll-with-pages).

Instalace Jekyllu nebyla úplně bezproblémová. Totiž Jekyll používá Ruby. Instalace Ruby na Windows je zatím stále trošku nepřívětivá, takže pokud se může něco pokazit a zahlásit podivnou chybu, stane se tak. Naštěstí jsme objevili [instantní řešení](http://www.madhur.co.in/blog/2013/07/20/buildportablejekyll.html) - totiž Jekyll se vším potřebným, takříkajíc v "portable verzi".

Ani to nebylo úplně perfektní. Objevily se například [problémy s UTF-8](http://joseoncode.com/2011/11/27/solving-utf-problem-with-jekyll-on-windows/) nebo s použitými moduly. Nakonec jsme to vyřešili pomocí nastavení, které skousne jak lokální instalace, tak GitHub Pages (problémy dělaly hlavně pluginy pro zpracování Markdownu). Viz náš [_config.yml](https://github.com/economia/economia.github.io/blob/master/_config.yml):

{% highlight yaml %}
markdown: kramdown
pygments: true
permalink: /:title
exclude:
- rakefile
- build.bat
{% endhighlight %}

Používáme engine Kramdown, které funguje jak pro "portable Jekyll", tak na Pages. O zvýraznění zdrojového kódu se stará [Pygments](http://pygments.org/languages/) Vyňaté soubory jsou rakefile (který řeší patch pro UTF-8) a build.bat:

{% highlight bat %}
call ..\setpath.cmd
rake build
{% endhighlight %}

Rakefile:
{% highlight ruby %}
task :build do
    puts '* Changing the codepage'
    `chcp 65001`
    puts '* Running Jekyll'
    `jekyll build`
end
{% endhighlight %}

Build.bat používáme pro zkušební sestavení blogu ve chvíli, kdy si nejsme jisti tím, jak bude výsledek vypadat. Bat se postará o správné nastavení proměnných (setpath.cmd je součástí distribuce "portable Jekyllu") a spustí rakefile. Ten nastaví správnou kódovou stránku a provede "jekyll build".

Pokud chceme napsat nový článek, tak do adresáře _posts napíšeme nový soubor v syntaxi [Markdown](http://daringfireball.net/projects/markdown/), pojmenovaný dle Jekyllovské konvence datem vydání a webovou adresou, kterou bude soubor mít. Do něj zapíšeme metainformace (titulek, perex, rubriku) a samotný text.

Publikování pak proběhne pomocí trojice git add / git commit / git push. O vlastní vykreslení se postarají [GitHub Pages](http://pages.github.com/).

Obrázky stačí umístit do adresáře a odkázat na ně - když je nezapomenete zahrnout do commitu, tak se zkopírují jak jsou na výsledné stránky.

Je to trošku jiný přístup než s hostovaným blogovacím nástrojem, je to zhruba o úroveň níž, ale na náš záměr je to dostatečné. Navíc práce s Gitem je naším denním chlebem. Navíc, proč to nepřiznat, je to i *geekovina*. Ale je to především jednoduché, rychlé a "developers-friendly".