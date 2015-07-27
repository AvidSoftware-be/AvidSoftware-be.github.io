---
layout: post
title: XDEBUG doen werken op Laravel Homestead met phpStorm
comments: true
---

phpStorm van Jetbrains, gecombineerd met XDEBUG is een enorm krachtige combinatie om op zoek te gaan naar fouten in een php applicatie of een bestaande applicatie
 te onderzoeken op de werking.
 
Om het aan de praat te krijgen met Laravel op een Homestead vm moet je wat handig zijn.

Hieronder leg ik je uit hoe je dit aan de praat krijgt.

#Homestead instellen
Gelukkig is XDebug al werkende op de standaard homestead vm. We moeten hier dus niet veel aan doen. Als tip wil ik wel meegeven dat het interessant is
om de timeout van nginx op 600 seconden te zetten. Anders krijg je tijdens een lange debugsessie soms een timeout (504 error).

#phpStorm instellen
1. open je project in phpStorm
2. open de 'preferences'
3. navigeer naar `Languages & Frameworks`, `PHP`, `Servers`.
4. Maak een nieuwe server aan., volg even mee hieronder:
    ![Server aanmaken](/public/phpstormserversinstellen.gif "Server aanmaken")
    Je moet dus het vinkje `Use path mappings` aan zetten en de mapping maken tussen de vagrant/homestead mapstructuur en de structuur op je mac. 
5. open het menu `Run` en kies `Edit configurations`
    Geef het een naam en kies de server die je hierboven hebt gemaakt.
    
-> Happy debugging!    






