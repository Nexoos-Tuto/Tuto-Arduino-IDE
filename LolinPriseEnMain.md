# Prise en main de la carte Lolin
![](https://i.imgur.com/dkb8YUKm.jpg) <br>

Cette carte n'étant pas arduino friendly elle peut s'averer plus compliqué à maitriser. Il faut avant tout installer un driver particulier sur notre pc pour pouvoir utiliser le port usb de notre pc.
http://www.wch-ic.com/downloads/CH341SER_EXE.html

## deuxième étape
 
Une fois sur notre logiciel arduino on va dans l'onglet fichier puis dans préférence et dans la ligne gestionnaire de carte supplémentaire on y rajoute cette ligne : 
![](https://i.imgur.com/WJhQd3I.png)
http://arduino.esp8266.com/stable/package_esp8266com_index.json 

## troisième étape 

Ensuite direction l'onglet <br> outils --> type de carte --> gestionnaire de carte <br> et on recherche le mot "esp" qui va nous permettre d'utiliser plusieurs types de cartes différentes dont celle que nous souhaitons.
La nôtre étant la carte NodeMcu 1.0 (ESP-12E Module)

### Vérification si tout est bien installé. 
Le *type de carte* devrait afficher ceci une fois notre carte choisie. <br>
![](https://i.imgur.com/l7Suz4i.jpg) <br>
Pour vérifier si nous avons le bon port COM de choisir : <br>
Menu Windows --> gestionnaire de périphériques --> PORT (COM et LPT) --> le driver s'appelle CH340 <br>
verifier si les numéros de port sont les mêmes entre le gestionnaire et arduino.

# Début des programmes !
Pour commencer nous allons faire un simple Blink à la main : 
### Blink
    void setup(){
    pinMode(2,OUTPUT); //On déclare le pin de la led. 
    }
 
    void loop(){
    digitalWrite(2,HIGH); //On va allumer la led 
    delay(1000); //pause de 1sec
    digitalWrite(2,LOW); //On éteint la LED
    delay(1000);
    }   

Sur la carte Lolin la led intégrée est sur le pin 2 donc avec ce programme la led en haut de la carte s'allumera. 
# Connexion au wifi 
Ce programme va permettre à la carte lolin d'établir une connexion à notre réseau wifi alors la led s'allumera quand la carte sera connectée au wifi pour indiquer que tout fonctionne. 
    #include <ESP8266WiFi.h>

    const char* ssid="box";
    const char* password = "mdp";

    int ledPin = 2;

    void setup() {
    
    pinMode(ledPin,OUTPUT);
    digitalWrite(ledPin,LOW);

    Serial.begin(9600); //On démarre une communication avec le moniteur série les prints seront écrit dedans.
    Serial.println();
    Serial.print("Wifi connecting to ");
    Serial.println( ssid );

    WiFi.begin(ssid,password); //On démarre la connexion wifi en se servant de L'SSID et le Password

    Serial.println();
    Serial.print("Connecting");

    while( WiFi.status() != WL_CONNECTED ){
        delay(500);
        Serial.print(".");        
    }

    digitalWrite( ledPin , HIGH);
    Serial.println();

    Serial.println("Wifi Connected Success!");
    Serial.print("NodeMCU IP Address : ");
    Serial.println(WiFi.localIP() );

    }

    void loop() {
    // put your main code here, to run repeatedly:

    }

