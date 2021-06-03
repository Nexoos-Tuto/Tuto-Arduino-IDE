# Prise en main des cartes STM32 P-Nucleo64 WB55RG et la carte STM32 discovery.
![](https://i.imgur.com/vZxhNgBm.jpg) Nucleo 
![](https://i.imgur.com/joGtdJhm.jpg) Discovery 
## Première étape

Dans l'onglet Fichier --> préférences --> gestionnaire de cartes supplémentaires il faut rajouter :
https://github.com/stm32duino/BoardManagerFiles/raw/master/package_stmicroelectronics_index.json 

## Deuxième étape 
 
Dans l'onglet <br> Outils --> type de cartes --> gestionnaire de cartes <br> on recherche la marque de notre carte pour nous ce sera STM32 <br> 
![](https://i.imgur.com/4xAasgC.jpg) <br>

## Vérification 

Pour la carte P-Nucleo64 WB55RG il faudrait bien pensé de vérifier les caractéristiques comme sur l'image ci-dessous. Le câble utilisé peux fonctionner avec la discovery mais pas la nucleo donc aussi il faut pensé bien verifier les câbles <br>
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
La led se situe proche de l'alimentation micro usb pour la discovery tandis pour le nucléo se trouve juste a cote du bouton SW3. si celle-ci ne clignote pas verifiez les paramètres au dessus.
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
![](https://i.imgur.com/lIrhpUXm.jpg) <br>

Quand le bouton branché sur le pin digital 2 est appuyé "alors" la led s'allume durant le temps de la pression du bouton sinon celle-ci restera éteinte 