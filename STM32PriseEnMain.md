# Prise en main des cartes STM32 P-Nucleo64 WB55RG et la carte STM32 discovery.
![](https://i.imgur.com/vZxhNgB.jpg) Nucleo 
![](https://i.imgur.com/joGtdJh.jpg) Discovery 
## Première étape

Dans l'onglet Fichier --> préférences --> gestionnaire de cartes supplémentaires il faut rajouter :
https://github.com/stm32duino/BoardManagerFiles/raw/master/package_stmicroelectronics_index.json 

## Deuxième étape 

Dans l'onglet Outils --> type de cartes --> gestionnaire de cartes on recherche la marque de notre carte pour nous ce sera STM32 <br> 
![](https://i.imgur.com/4xAasgC.jpg) <br>

## Vérification 

Pour la carte P-Nucleo64 WB55RG bien pensé de vérifier les caractéristique comme sur le screen ci-dessous et le câble utilisé peux fonctionner avec la discovery mais pas la nucleo donc aussi bien verifier les câbles <br>
![](https://i.imgur.com/vFOXm7b.png) <br>

Pour la carte Discovery pareil bien vérifier les caractéristique <br>
![](https://i.imgur.com/SPAwQ02.png)

# Début des programmes ! 
Pour commencer nous allons faire un simple Blink : 
### Blink
    void setup() {
     pinMode(LED_BUILTIN, OUTPUT);
    }   

    void loop() {
    digitalWrite(LED_BUILTIN, HIGH);   
    delay(100);                       
    digitalWrite(LED_BUILTIN, LOW);    
    delay(100);                       
    }
La led qui s'allumera ce trouve proche de l'alimentation micro usb que nous utiliserons elle est facilement voyante pour la discovery pour la nucleo elle se trouve juste a cote du bouton SW3. si celle-ci ne clignote pas verifiez les paramètres au dessus.
### bouton 
    int bouton = 0; 
    void setup(){
    Serial.begin(92000);
    pinMode(2,INPUT); //Bouton
    pinMode(LED_BUILTIN, OUTPUT); //LED
    }
    void loop(){
    bouton = digitalRead(2);
    if (bouton == HIGH){
    digitalWrite(LED_BUILTIN, HIGH);  
    }else {
    digitalWrite(LED_BUILTIN, LOW);
    }
    }
### câblage
![](https://i.imgur.com/lIrhpUX.jpg) <br>

Quand le bouton branché sur le pin digital 2 est appuyé la led s'allume le temps de la pression sinon celle-ci reste éteinte. 