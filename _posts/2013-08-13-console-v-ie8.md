---
title: "Console v IE8"
description: >
  Zapomenutý console.log() dokáže napáchat pěknou paseku v IE, a co hůř - špatně se hledá!
layout: post
category: javascript
---

Znáte to - po zuřivém ladění vám zůstane někde v kódu zapomenutý ladicí výpis, známé *console.log*. Nojo, však to není nic proti ničemu, komu by to vadilo... Jenže pak vás zavolá uživatel, že mu to vůbec nefunguje!

Přijdete, koukáte - a vidíte: Má IE8. Hmmm, nějaký problém s kompatibilitou. Spustíte tedy konzoli, načtete znovu - a vida, už to jede! Tak to vidíte, asi se něco špatně načetlo, zmáčkněte F5!

Jenže pak se to stane i dalšímu, a dalšímu, a vás přestane bavit chodit od čerta k ďáblu a spouštět konzole, a začnete přemýšlet, čím to asi může být. "Špatným načtením" to není. Zmizí to, když spustíte konzoli. Aha. AHA! <tweetable title="Podivuhodnou chybu může někdy způsobit zapomenutý console.log()">On totiž IE8 nemá objekt *console*, dokud tu konzoli neotevřete!</tweetable>

Pomoc je snadná - vyházejte všechny console.log, na produkčním webu nemají co dělat.

A ti líní použijí tenhle [kousek z HTML5Boilerplate](https://github.com/h5bp/html5-boilerplate/blob/master/js/plugins.js):

{% highlight javascript %}
(function() {
    var method;
    var noop = function () {};
    var methods = [
        'assert', 'clear', 'count', 'debug', 'dir', 'dirxml', 'error',
        'exception', 'group', 'groupCollapsed', 'groupEnd', 'info', 'log',
        'markTimeline', 'profile', 'profileEnd', 'table', 'time', 'timeEnd',
        'timeStamp', 'trace', 'warn'
    ];
    var length = methods.length;
    var console = (window.console = window.console || {});

    while (length--) {
        method = methods[length];

        // Only stub undefined methods.
        if (!console[method]) {
            console[method] = noop;
        }
    }
}());
{% endhighlight %}