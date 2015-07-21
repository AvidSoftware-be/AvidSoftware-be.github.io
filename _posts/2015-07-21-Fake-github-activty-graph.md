---
layout: post
title: Fake Github activity graph howto
comments: true
---

Op Github zie je op je profiel een grafiek staan van je activiteit. Met een beetje creativiteit en wat git kennis, zou je die grafiek kunnen manipuleren dacht ik zo.

![Github Graph](/public/GithubGraph.png "Github Graph")

Als je volgende commando's uitvoert op een 'nix terminal, zal je een commit maken in een repo die eigenlijk geen commit is. Het zal wel geregistreerd worden
in de grafiek:
{% highlight bash %}
GIT_AUTHOR_DATE='2014-10-25T00:01'
GIT_COMMITTER_DATE='2014-10-25T00:01'
git commit --allow-empty -m 'Graph Data 2014-10-25T00:01'
{% endhighlight %}

Dus, als je veel tijd hebt zou je een script kunnen maken die een commit (of meerdere voor een donkere kleur) maakt in een gegeven week.

Zo bouw je een 'tekening' op.

Maar het kan nog sneller en beter. Wat als je gewoon een tekening kon tekenen en op basis daarvan een script genereren?

Dat kan.

[Laurence Gellert](http://www.laurencegellert.com), een developer uit Portland, Oregon USA, deed dat. Je kan de tool vinden op:

[http://www.laurencegellert.com/software/github-graph-builder/](http://www.laurencegellert.com/software/github-graph-builder/)

Laat je even weten als je er iets mooi mee gemaakt hebt?

Kijk ook even op [mijn profiel](https://github.com/AvidSoftware-be) om mijn werkje te zien.