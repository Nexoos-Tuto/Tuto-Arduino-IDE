# MKR1000 prise en main ! <br>
![](https://i.imgur.com/YfzdXIbm.jpg)<br>
Pour bien débuter et utiliser la carte arduino MKR1000 il faut installer la bibliothèque qui permet de choisir notre carte. Pour ce faire on va dans l'onglet outils puis type de carte et gestionnaire de carte. On cherche le *nom* de notre carte puis on installe la biblithèque.
![Je suis le screen](https://i.imgur.com/pYETuny.jpg)

## Vérification 
On vérifie bien le type de carte en ayant choisi la carte MKR1000 et le port celui-ci doit afficher le nom de la carte comme ceci : 
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
Contrairement au carte UNO généralement utilisé ici la led directement branché sur la carte est sur le PIN 6 ce programme fais donc clignotait la led et nous affiche dans le moniteur série (la petite loupe en haut a droite) le mot "test" histoire de vérifier si tout fonctionne bien. 

### Capteur IR
Même pour un programme un peu plus complexe la carte réagi parfaitement bien ce programme a été fait pour la télécommande arduino fourni dans le kit de dev. Il faut bien évidemment pensé à installé la bibliothèque IRremote trouvable sur internet.

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
