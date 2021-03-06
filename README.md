# station-meteo

 -- Projet linux embarqué --

GAURIER Florian
JADOULT Thibault
WITT Isaac-Andreï
DRILLON Mathieu

#### Partie GPIO :

Pour cette partie, nous nous sommes aidé de la documentation sysfs: en modifiant le pin 11 de la rpi3 en mode OUT et en modifiant sa valeur, on peut faire passer la led branché en série à ce pin de l'état éteint à l'état allumé.
Par la suite, nous nous sommes servi des packages python déjà présent sur la rpi3 pour la controler. Taper python sur son terminal permet d'ouvrir une console python:

>>> import RPi.GPIO as GPIO --> On importe la bibliothèque RPI.GPIO

>>> GPIO.setmode(GPIO.BCM) --> On choisit le mode entre BOARD (11) et BCM(17)
	
>>> GPIO.setup(17, GPIO.OUT) -->On passe en mode sorti pour envoyer une commande
	
>>> GPIO.output(17, o) --> o=1 pour allumer / o=0 pour éteindre
	
>>> GPIO.cleanup() --> On réinitialise les pins GPIO

Pour finir, en utilisant le code Python proposer dans la partie et en jouant avec les valeurs a et b (fréquence et duty cycle), on peut faire en sorte de modifier l'intensité de la led.
>>> p = GPIO.PWM(11, a) --> mode BOARD
>>> p.start(b)

#### Partie BME280 :

Pour tester le bme et récupérer les information, nous avons réutilisé le fichier `linux_userspace.c` présent dans le dossier `examples`.<br>
Une fois qu'il n'y a plus eu de problème, les donnée reçus ne changaient pas et que le problème venait de la fonction `stream_sensor_data_forced_mode`.<br> 
Après moulte éffort pour corrigé ceci, nous décidâmes de changer de fonction, nous utilison maintenant la fonction `stream_sensor_data_normal_mode` , trouver dans le README du driver.<br>
Nous avons dû implémenter une ligne pour qu'elle fonctionne, que voici `int8_t stream_sensor_data_normal_mode(struct bme280_dev *dev);` à la ligne 140, et changer la fonction `delay_ms` par `delay_us`, en prenant en compte aussi qu'il fallait ajouter ceci `uint32_t req_delay;` comme pour l'ancienne version.

#### Partie I2C et BME280 :
Une fois qu'on pouvait allumé la led et reçevoir les donnée du capteur, il suffisait juste de combiné les éléments ensemble.
Pour ce faire nous  nous somme aider de ce [site](https://www.ics.com/blog/gpio-programming-using-sysfs-interface) qui donnais déjà du code en C++ pour communiqué avec le port GPIO.
