# Prise en main de la carte Lolin

Cette carte n'étant pas arduino friendly elle peut s'averer plus compliqué a maitriser. Il faut avant toute chose installé un driver particulier sur notre pc pour pouvoir utiliser le port usb de notre pc.
http://www.wch-ic.com/downloads/CH341SER_EXE.html

## deuxième étape

Une fois sur notre logiciel arduino on va dans l'onglet fichier puis dans préférence et dans la ligne gestionnaire de carte supplémentaire on y rajoute cette ligne : 
http://arduino.esp8266.com/stable/package_esp8266com_index.json 

## troisième étape 

Ensuite direction l'onglet outils --> type de carte --> gestionnaire de carte et on recherche le mot "esp" qui va nous permettre d'utiliser plusieurs type de carte différentes dont celle que nous souhaitons.
La notre étant la carte NodeMcu 1.0 (ESP-12E Module)

### Vérification si tout est bien installé. 
Le type de carte devrait affiché ceci une fois notre carte choisis. <br>
![](https://i.imgur.com/l7Suz4i.jpg) <br>
Pour vérifier si nous avons le bon port COM de choisis : 
Menu Windows --> gestionnaire de périphériques --> PORT (COM et LPT) --> le driver s'appellent CH340 --> verifier si les numéro de port sont les mêmes entre le gestionnaire et arduino.
