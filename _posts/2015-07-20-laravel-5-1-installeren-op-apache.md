---
layout: post
title: Laravel 5.1 installeren op Apache
comments: true
---

Voor een nieuwe klant ben ik me aan het verdiepen in Laravel, een open source web framework geschreven in PHP. Gezien u deze post leest, veronderstel ik dat u
weet wat Laravel is, waarvoor het dient en waarom u Laravel wil gaan gebruiken. Waarschijnlijk bent u daarentegen op zoek naar een uitleg over de installatie van Laravel. U bent op het goede adres.

Laten we meteen beginnen!

#Wat zijn de vereisten voor de installatie van Laravel?

* Apache web server.
* Shell SSH toegang tot de server
* Root rechten om Composer globaal te installeren (niet strikt nodig)
* Git
* PHP >= 5.5.9
* OpenSSL PHP Extensie (controleer deze met phpinfo();)
* Mbstring PHP Extensie
* Tokenizer PHP Extensie

#Installeer Composer

Composer is een integraal onderdeel van Laravel nu. Het wordt gebruikt voor het beheren van afhankelijkheden zoals externe bibliotheken die door de projecten gebruikt worden.
Het wordt ook gebruikt voor het installeren van Laravel.
Om Laravel globaal te installeren, voer je deze commando's uit:

{% highlight bash %}
curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin
ln -s /usr/local/bin/composer.phar /usr/local/bin/composer
{% endhighlight %}

De officiële Composer documentatie stelt voor om  mv composer.phar composer te doen maar als u een symbolic link gebruikt, is het veel eenvoudiger om Composer te upgraden 
(voor daarvoor {% highlight bash %}curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin{% endhighlight %} nogmaals uit).

#Installeer Laravel

Er zijn meerdere manier om Laravel te installeren maar de (voor mij toch) makkelijkste manier is deze hieronder. 
Het zal Laravel installeren in de map '/var/www/nieuwe.website' (vervang liefst nieuwe.website door iets interessanter...)

{% highlight bash %}
composer create-project laravel/laravel /var/www/nieuwe.website
{% endhighlight %}

Nadat er een heleboel tekst over je scherm zal gelopen zijn en verschillende componenten geïnstalleerd, zal er onder '/var/www/nieuwe.website'
een map 'public' bestaan. Naar deze map moeten we nu onze apache webserver wijzen om als hoofdmap te gaan gebruiken.

Maak een nieuw bestand aan onder '/etc/apache2/sites-available' en noem het nieuwe.website.conf 

Dit moet de inhoud ervan zijn:

{% highlight apache %}
<VirtualHost *:80>
ServerName nieuwe.website
DocumentRoot "/var/www/nieuwe.website/public"
<Directory "/var/www/nieuwe.website/public">
allow from all
Options +Indexes
</Directory>
</VirtualHost>
{% endhighlight %}

Nu gaan we de nieuwe website activeren en apache opnieuw starten om de nieuwe configuratie op te laden.:

{% highlight bash %}
a2ensite nieuwe.website.conf
service apache2 restart
{% endhighlight %}

#Configuratie


Er is heel wat te configureren maar daarvoor verwijs ik je naar Laravel zelf. Niettegenstaande stel ik op zijn minst volgende
zaken voor:

Zorg dat de bootstrap en cache schrijfbaar zijn door de webserver:

{% highlight bash %}
chown -R www-data:www-data /var/www/new.website.name/storage
chown -R www-data:www-data /var/www/new.website.name/bootstrap/cache
find /var/www/new.website.name/storage -type f -exec chmod ug+rw {} \;
find /var/www/new.website.name/storage -type d -exec chmod ug+rwx {} \;
find /var/www/new.website.name/bootstrap/cache -type f -exec chmod ug+rw {} \;
find /var/www/new.website.name/bootstrap/cache -type d -exec chmod ug+rwx {} \;
{% endhighlight %}

In config/app.php zet je de juiste tijdszone:
{% highlight php %}'timezone' => 'Europe/Brussels'{% endhighlight %}
En locale:
{% highlight php %}'locale' => 'nl_BE'{% endhighlight %}



