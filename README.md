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
```matlab
fe = 1e4; % 10^4
te = 1/fe;
N = 5000; 
t = (0:N-1)*te; 

x = 1.2*cos(2*pi*440*t+1.2)+3*cos(2*pi*550*t)+0.6*cos(2*pi*2500*t);
plot(t,x,'.');
```
<img width="289" alt="1" src="https://user-images.githubusercontent.com/121026580/210178411-1e74a091-80dd-4a6d-81b2-47304b108bcd.png">

>Matlab ne représente pas les signaux continus. En effet il représente des séquences ou signaux échantillonnés (discrets) en fonction du temps avec te egale au rapport de 1 sur la fréquence d’échantillonnage fe et N le
nombre d’échantillons dans la séquence.

2. Calculer la TFD du signal x(t) en utilisant la commande fft, puis tracer son spectre 
en amplitude après avoir créé le vecteur f qui correspond à l'échantillonnage du signal 
dans l'espace fréquentiel. Utiliser la commande abs pour afficher le spectre 
d’amplitude.

```matlab
 f =(0:N-1)*(fe/N); 
 y = fft(x); 
 plot(f,abs(y));
```
<img width="280" alt="2 1" src="https://user-images.githubusercontent.com/121026580/210178669-53f2bf05-05ec-4e33-9075-de36339ed3b4.png">

3. Pour mieux visualiser le contenu fréquentiel du signal, utiliser la fonction fftshift, qui 
effectue un décalage circulaire centré sur zéro du spectre en amplitude obtenu par la
commande fft.


```matlab
fshift = (-N/2:N/2-1)*(fe/N);
plot(fshift,fftshift(2*abs(y)/N))
```
<img width="349" alt="3" src="https://user-images.githubusercontent.com/121026580/210179516-b60eb8ba-39a9-42a2-8658-9660a0c391d3.png">

Un bruit correspond à tout phénomène perturbateur gênant la transmission ou 
l'interprétation d'un signal. Dans les applications scientifiques, les signaux sont 
souvent corrompus par du bruit aléatoire, modifiant ainsi leurs composantes 
fréquentielles. La TFD peut traiter le bruit aléatoire et révéler les fréquences qui y 
correspond.

4. Créer un nouveau signal xnoise, en introduisant un bruit blanc gaussien dans le 
signal d’origine x(t), puis visualisez-le. Utiliser la commande randn pour générer ce 
bruit. Il est à noter qu’un bruit blanc est une réalisation d'un processus aléatoire dans 
lequel la densité spectrale de puissance est la même pour toutes les fréquences de 
la bande passante. Ce bruit suit une loi normale de moyenne 0 et d’écart type 1.

```matlab
noise = randn(size(x));
plot(noise);
title('noise');
```
<img width="317" alt="4" src="https://user-images.githubusercontent.com/121026580/210179836-7ad25eaf-6907-4c8c-8237-0f701771583d.png">

5. Utiliser la commande sound pour écouter le signal et puis le signal bruité.
```matlab
sound(x);
sound(noise);
```
La puissance du signal en fonction de la fréquence (densité spectrale de puissance)
est une métrique couramment utilisée en traitement du signal. Elle est définie comme 
étant le carré du module de la TFD, divisée par le nombre d'échantillons de fréquence. 

6. Calculez puis tracer le spectre de puissance du signal bruité centré à la fréquence 
zéro.

```matlab
f =(0:N-1)*(fe/N);
y = fft(noise);    
spectrePuissance=2.^abs(y)/N;
plot(f,spectrePuissance); 
title('spectre de puissance du signal bruité :');
```
<img width="299" alt="6" src="https://user-images.githubusercontent.com/121026580/210183928-d2f347e5-72c6-4371-a7fd-cf1eecd3c59f.png">

7. Augmenter l’intensité de bruit puis afficher le spectre. Interpréter le résultat obtenu.

## Analyse fréquentielle du chant du rorqual bleu
1. Chargez, depuis le fichier ‘bluewhale.au’, le sous-ensemble de données qui 
correspond au chant du rorqual bleu du Pacifique. En effet, les appels de rorqual bleu 
sont des sons à basse fréquence, ils sont à peine audibles pour les humains. Utiliser 
la commande audioread pour lire le fichier. Le son à récupérer correspond aux indices 
allant de 2.45e4 à 3.10e4.

```matlab
[x,fs]= audioread("bluewhale.au"); 
chant = x(2.45e4:3.10e4); 
```
2. Ecoutez ce signal en utilisant la commande sound, puis visualisez-le

```matlab
soundsc(x,fs);
```
La TFD peut être utilisée pour identifier les composantes fréquentielles de ce signal 
audio. Dans certaines applications qui traitent de grandes quantités de données avec 
fft, il est courant de redimensionner l'entrée de sorte que le nombre d'échantillons soit 
une puissance de 2. fft remplit automatiquement les données avec des zéros pour
augmenter la taille de l'échantillon. Cela peut accélérer considérablement le calcul de 
la transformation. 

3. Spécifiez une nouvelle longueur de signal qui sera une puissance de 2, puis tracer 
la densité spectrale de puissance du signal.

```matlab
N = length(chant); 
ts = 1/fs; 
t = (0:N-1)*(10*ts); 
subplot(2,1,1);
plot(t,chant);
title('bluewhale signal')
dsp_chant =  (abs(fft(chant)).^2)/N; 
f = (0:floor(N/2))*(fs/N)/10;
plot(f,dsp_chant(1:floor(N/2)+1))
title('D Spectrale de la puissance du signal')
```
<img width="310" alt="partie 2 3" src="https://user-images.githubusercontent.com/121026580/210185099-7915c110-a115-4efd-9d64-ee3daee18ac7.png">

4. Déterminer à partir du tracé, la fréquence fondamentale du gémissement de rorqual 
bleu.
