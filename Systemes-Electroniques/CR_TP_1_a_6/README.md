# Comptes rendus TP 1 à 6

Comptes rendus des travaux pratiques de Systèmes Électroniques.

## TP n°2 : Synthèse de Filtres
### Préparation :
#### Partie 1 : Filtre passe bas de Tchébysheff (ordre 3)
1- Gabarit et Sélectivité $k$ :
  - Cahier des charges :
    - frequence de coupure (bande passante) $f_p$ = 146 Hz avec une ondulation $A_{max}$ = 1 dB;
    - frequence d'atténuation $f_a$ = 292 Hz avec une atténuation $A_{min}$ = 30 dB;
  - Calcul du facteur de selectivité $k$ : La selectivité $k$ compare la limite de la bande passante à celle de la bande coupée.
$$
    k = \frac{f_p}{f_a} = \frac{146}{292} = 0.5
    \Rightarrow
    \frac{1}{k} = \frac{f_a}{f_p} = 2
$$

2- Dénormalisation de la fonction de transfert et calcul des compasants du filtre : d'après le tableau de FPB Tchébyscheff pour n = 3
$$
T(p) = \frac{1}{(1.0058p² + 0.4970p +)(2.023p + 1)}
$$
On sait que : $$
\omega_p = 2\pi f_p = 2\pi \times 146 \approx 917.35\ \mathrm{rad/s}
$$
On pose : $p = \frac{p}{\omega_p}$

- Pour le FPB premier ordre avec $R_2$, $C_3$ avec $R_2 = 10$ $\mathrm{k}\Omega $
$$
H_1(p) = \frac{1}{1 + R_2C_3p}
$$ 
Le polynôme normalisé est $(2.023p + 1)$ et sa forme dénormalisée est : $ 1 + \frac{2.023}{\omega_p}p$
Ainsi par identification :
$$
R_2C_3 = \frac{2.023}{\omega_p}
\Rightarrow
C_3 = \frac{2.023}{R_2\omega_p}
= \frac{2.023}{10^4 \times 917.34}
\simeq 220.5\ \mathrm{nF}
$$

- Pour le Filtre de Sallen-Key avec $R_1 = R = 4.3 $ $\mathrm{k}\Omega$ et $R_2 = 10$ $\mathrm{k}\Omega$
$$
H_2(p) = \frac{1}{1 + 2RC_2p + R^2C_1C_2p^2}
$$
ce qui correspond à : $(1.0058p^2 + 0.4970p + 1)$, dénormalisation :
$$
1 + \frac{0.4970}{\omega_p}p + \frac{1.0058}{\omega_p^2}p^2
$$
Par identification : 
$$2RC_2 = \frac{0.4970}{\omega_p} \Rightarrow C_2 = \frac{0.4970}{2R\omega_p} \Rightarrow C_2 = \frac{0.4970}{4.3 \times 10^3 \times 917.34 \times 2} \simeq 63\ \mathrm{k}{\Omega}
$$
$$
R^2C_1C_2 = \frac{1.0058}{\omega_p^2} \Rightarrow C_1 = \frac{1.0058}{R^2C_2\omega_p^2} \Rightarrow C_1 = 1.026\ \mathrm {uF}
$$ 
- Calcul de la fréquence de cassure $f_0$ et l'amortissement $m$ du second ordre
  On sait que pour un FPB la forme canonique est :
$$
H(p) = \frac{A}{1 + \frac{2m}{\omega_0}p + \frac{1}{\omega_0^2}p^2}
$$
Par identification à la forme dénormalisée : 
$$
\frac{1}{\omega_0^2}
= \frac{1.0058}{\omega_p^2}
\Rightarrow
\omega_0 = \frac{\omega_p}{\sqrt{1.0058}}
\Rightarrow
\omega_0 \simeq 914.7\ \mathrm{rad/s}
$$ 
Or on sait que :
$$ \omega_0 = 2\pi f_0 \Rightarrow f_0 = \frac{\omega_0}{2\pi} \Rightarrow f_0 = 145.45\ \text{Hz}  
$$ 
Et $\frac{2m}{\omega_0} = \frac{0.4970 \omega_0}{2 \omega_p} $ On  remplace ${\omega_0}$ par son expression et on simplifie : $m = \frac{0.4970}{2 \sqrt{1.0058}} \Rightarrow m = 0.246$

### Partie 2 :Filtre passe haut de Butterworth (ordre 3)
- Cahier des charges :
  - Frequence de coupure : $f_p = 400\ Hz$
  - Fréquence d'atténuation : $f_a = 200\ Hz$

1. Calcul  de la sélectivité $k$ pour un passe haut: la bande atténuée est avant la bande passante donc:
$$
k = \frac{f_a}{f_p}
= \frac{200}{400}
= 0.5
\Rightarrow
\frac{1}{k} = \frac{1}{0.5} = 2
$$

