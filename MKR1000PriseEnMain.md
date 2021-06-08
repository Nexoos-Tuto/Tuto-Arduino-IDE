# MKR1000 prise en main ! <br>
![](https://i.imgur.com/YfzdXIbm.jpg)<br>
Pour bien débuter et utiliser la carte arduino MKR1000 il faut installer la bibliothèque qui permet de détecter notre carte. Pour ce faire on va dans l'onglet *outils* puis *type de carte* et *gestionnaire de carte*. On cherche le *nom* de notre carte puis on installe la bibliothèque.
![Je suis le screen](https://i.imgur.com/pYETuny.jpg)

## Vérification 
Pour vérifier le type de carte, nous allons nous rendre dans l'onglet *outils* puis *type de carte* qui doit donc avoir un affichage comme ceci : <br>
![Imgur](https://i.imgur.com/54ZN6AQm.png)

# Début des programmes ! 
Pour commencer nous allons faire un simple Blink à la main : 
### Blink
    void setup(){
    pinMode(6,OUTPUT);
    Serial.begin(9600);
    }
 
    void loop(){
    digitalWrite(6,HIGH);
    delay(1000);
    digitalWrite(6,LOW);
    delay(1000);
    Serial.println("test");
    }

Ici la led qui est directement branchée sur la carte, sur le PIN 6(contrairement aux autres Arduino).Ce  programme fait clignoter la led et nous affiche dans le moniteur série (la petite loupe en haut à droite) le mot "test" histoire de vérifier si tout fonctionne bien.

### Capteur IR
Même pour un programme un peu plus complexe la carte réagit parfaitement bien ce programme a été fait pour la télécommande arduino fournie dans le kit de dev. Il faut bien évidemment penser à installer la bibliothèque IRremote trouvable sur internet si elle ne se trouve pas directement dans le logiciel arduino. Si non https://www.arduinolibraries.info/libraries/i-rremote à ajouter ici dans le logiciel : <br> 

![](https://i.imgur.com/c62LS01.png)

<br> Ce code étant fait pour la télécommande du kit il ne marchera pas avec une autre. pour faire fonctionner notre télécomande il faut avant tout réceptionner la première valeur que la télécommande envoie comme par exemple ma touche 0 la valeur renvoyé était FF6897 étant de l'héxadécimal on le note avec 0x devant et on peut dire à l'arduino que SI on reçoit FF6897 alors ça correspond à la touche 0 (à faire pour chaque touche).

    #include <IRremote.h>

    const char IR = 12;
    IRrecv recepteur(IR);
    decode_results messageRecu ;
    void setup(){
      Serial.begin(9600);
      recepteur.enableIRIn();
    }
    void loop(){

    if (recepteur.decode(&messageRecu))
    {
      if (messageRecu.value == 0xFF6897) {
        Serial.println("la touche 0");
      }
      if (messageRecu.value == 0xFF30CF) {
        Serial.println("la touche 1");
    }
    else if (messageRecu.value == 0xFF18E7 ) {
      Serial.println("la touche 2");
    }
    else if (messageRecu.value == 0xFF7A85 ) {
      Serial.println("la touche 3");
    }
    else if (messageRecu.value == 0xFF10EF ) {
      Serial.println("la touche 4");
    }
    else if (messageRecu.value == 0xFF38C7 ) {
      Serial.println("la touche 5");
    }
    else if (messageRecu.value == 0xFF5AA5 ) {
      Serial.println("la touche 6");
    }
    else if (messageRecu.value == 0xFF42BD ) {
      Serial.println("la touche 7");
    }
    else if (messageRecu.value == 0xFF4AB5 ) {
      Serial.println("la touche 8");
    }
    else if (messageRecu.value == 0xFF52AD ) {
      Serial.println("la touche 9");
    }
    else if (messageRecu.value == 0xFFE01F ) {
      Serial.println("la touche -");
    }
    else if (messageRecu.value == 0xFFA857 ) {
      Serial.println("la touche +");
    }
    else if (messageRecu.value == 0xFF906F ) {
      Serial.println("la touche eq");
    }
    else if (messageRecu.value == 0xFF22DD ) {
      Serial.println("la touche |<<");
    }
    else if (messageRecu.value == 0xFF02FD ) {
      Serial.println("la touche >>|");
    }
    else if (messageRecu.value == 0xFFC23D ) {
      Serial.println("la touche >||");
    }
    else if (messageRecu.value == 0xFFA25D ) {
      Serial.println("la touche CH-");
    }
    else if (messageRecu.value == 0xFF629D ) {
      Serial.println("la touche CH");
    }
    else if (messageRecu.value == 0xFFE21D ) {
      Serial.println("la touche CH+");
    }
    else if (messageRecu.value == 0xFF9867 ) {
      Serial.println("la touche 100+");
    }
    else if (messageRecu.value == 0xFFB04F ) {
      Serial.println("la touche 200+");
    }
    recepteur.resume();
    }
    delay(1);
    }
# Connexion au wifi 

Pour ce faire nous allons utiliser un programme qui nous connecte à notre réseau et qui vérifie toute les 10s la connexion  :

    #include <WiFi101.h> //bibliotheque Wifi101
    #include "infos_wifi.h" //fichier secret 

    char ssid[] = SECRET_SSID;        // nom de la box
    char pass[] = SECRET_PASS;        // mot de passe de la box
    int status = WL_IDLE_STATUS;     // status de la wifi (en attendant qu'il se connecte)

    void setup() {
    Serial.begin(9600);  //initialise le moniteur série
    while (!Serial);     //indique si le port de série spécifié est prêt.

    // tant qu'il essaye de se connecter à la box
    while (status != WL_CONNECTED) { //status essaye de se connecter
        Serial.print("En attente de la connexion à: ");
        Serial.println(ssid);
        // infos pour se connecter
        status = WiFi.begin(ssid, pass); //

        // attend 10s avant de se connecter
        delay(10000);
    }

    // si on est connecté ::
    Serial.println("Connecté à la Box");
    
    Serial.println("----------------------------------------");
    printData();
    Serial.println("----------------------------------------");
    }

    void loop() {
    // verifie connexion toutes les 10s
    delay(10000);
    printData();
    Serial.println("----------------------------------------");
    }

    void printData() {
    Serial.println("Infos Carte Arduino:");
    // affiche adresse IP
    IPAddress ip = WiFi.localIP();
    Serial.print("IP Address: ");
    Serial.println(ip);

    Serial.println();
    Serial.println("Infos Box:");
    Serial.print("SSID: ");
    Serial.println(WiFi.SSID());

    // affiche le RSSI
    long rssi = WiFi.RSSI();
    Serial.print("signal strength (RSSI):");
    Serial.println(rssi);

    //type de chiffrement 
    byte encryption = WiFi.encryptionType();
    Serial.print("Encryption Type:");
    Serial.println(encryption, HEX);
    Serial.println();
    }

Le fichier infos_wifi.h est une fichier secret contenant deux lignes pour proteger nos identifiants si quelqu'un recupère notre code :

    #define SECRET_SSID " "
    #define SECRET_PASS " "
