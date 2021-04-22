# station-meteo

 -- Projet linux embarqué --

JADOULT Thibault
WITT Isaac-Andreï

Partie GPIO :

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

Partie I2C et BME280 :
