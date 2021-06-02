# Prise en main de la carte Lolin
![](https://i.imgur.com/dkb8YUKm.jpg) <br>

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

# Début des programmes !
Pour commencer nous allons faire un simple Blink à la main : 
### Blink
    void setup(){
    pinMode(2,OUTPUT);
    }
 
    void loop(){
    digitalWrite(2,HIGH);
    delay(1000);
    digitalWrite(2,LOW);
    delay(1000);
    }   

Sur la carte Lolin la led intégré est sur le pin 2 donc avec ce programme la led en haut de la carte s'allumera. 
# Connexion au wifi 
Ce programme va permettre à la carte lolin d'établir une connexiona notre réseau wifi la led s'allumera quand la carte sera connecté au wifi pour indiqué que tout fonctionne. 
    #include <ESP8266WiFi.h>

    const char* ssid="box";
    const char* password = "mdp";

    int ledPin = 2;

    void setup() {
    
    pinMode(ledPin,OUTPUT);
    digitalWrite(ledPin,LOW);

    Serial.begin(9600);
    Serial.println();
    Serial.print("Wifi connecting to ");
    Serial.println( ssid );

    WiFi.begin(ssid,password);

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

