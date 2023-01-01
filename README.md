# TS- TP1- Analyse spectrale d’un signal transformée de Fourier discrète 
## Objectifs
- Représentation de signaux et applications de la transformée de Fourier discrète (TFD) sous Matlab. 
- Evaluation de l’intérêt du passage du domaine temporel au domaine fréquentiel dans l’analyse et l’interprétation des signaux physiques réels
>Commentaires : Il est à remarquer que ce TP traite en principe des signaux continus. 
Or, l'utilisation de Matlab suppose l'échantillonnage du signal. Il faudra donc être 
vigilant par rapport aux différences de traitement entre le temps continu et le temps 
discret.

>Tracé des figures : toutes les figures devront être tracées avec les axes et les légendes des axes appropriés.

>Travail demandé : un script Matlab commenté contenant le travail réalisé et des
commentaires sur ce que vous avez compris et pas compris, ou sur ce qui vous a 
semblé intéressant ou pas, bref tout commentaire pertinent sur le TP.
## Représentation temporelle et fréquentielle 
- Considérons un signal périodique x(t) constitué d’une somme de trois sinusoïdes de 
fréquences 440Hz, 550Hz, 2500Hz. 
𝐱(𝐭) = 𝟏.𝟐𝐜𝐨𝐬(𝟐𝐩𝐢𝟒𝟒𝟎𝐭 + 𝟏.𝟐) + 𝟑𝐜𝐨𝐬(𝟐𝐩𝐢𝟓𝟓𝟎𝐭) + 𝟎. 𝟔𝐜𝐨𝐬(𝟐𝐩𝐢𝟐𝟓𝟎𝟎𝐭)
1. Tracer le signal x(t). Fréquence d’échantillonnage : fe = 10000Hz, Intervalle : 
Nombre d’échantillons : N = 5000.
