# Comptes rendus TP 1 à 6

Comptes rendus des travaux pratiques de Systèmes Électroniques.

## TP n°2 : Synthèse de filtres

### Préparation

## Partie 1 : Filtre passe-bas de Tchébycheff (ordre 3)

### 1. Gabarit et facteur de sélectivité \(k\)

**Cahier des charges :**

- Fréquence de coupure de la bande passante : \(f_p=146\,\mathrm{Hz}\), avec une ondulation maximale \(A_{\max}=1\,\mathrm{dB}\).
- Fréquence d'atténuation : \(f_a=292\,\mathrm{Hz}\), avec une atténuation minimale \(A_{\min}=30\,\mathrm{dB}\).

La sélectivité \(k\) compare la limite de la bande passante à celle de la bande atténuée.

$$
k=\frac{f_p}{f_a}
=\frac{146}{292}=0.5
$$

$$
\boxed{k=0.5\qquad\text{et}\qquad\frac{1}{k}=2}
$$

### 2. Dénormalisation de la fonction de transfert et calcul des composants

D'après le tableau du filtre passe-bas de Tchébycheff d'ordre 3, la fonction de transfert normalisée est :

$$
T(p)=\frac{1}{(1.0058p^2+0.4970p+1)(2.023p+1)}
$$

La pulsation de référence est :

$$
\omega_p=2\pi f_p
=2\pi\times146
$$

$$
\boxed{\omega_p\simeq917.35\,\mathrm{rad/s}}
$$

Pour dénormaliser la fonction de transfert, on effectue le remplacement :

$$
p\longleftarrow\frac{p}{\omega_p}
$$

#### a) Filtre passe-bas passif du premier ordre

Le filtre est constitué de \(R_2=10\,\mathrm{k}\Omega\) et de \(C_3\).

Sa fonction de transfert est :

$$
H_1(p)=\frac{1}{1+R_2C_3p}
$$

Après dénormalisation, le facteur du premier ordre devient :

$$
1+\frac{2.023}{\omega_p}p
$$

Par identification :

$$
R_2C_3=\frac{2.023}{\omega_p}
$$

$$
C_3=\frac{2.023}{R_2\omega_p}
=\frac{2.023}{10^4\times917.35}
$$

$$
\boxed{C_3\simeq220.5\,\mathrm{nF}}
$$

#### b) Filtre passe-bas actif de Sallen-Key du second ordre

On utilise \(R=4.3\,\mathrm{k}\Omega\), avec \(R_1=R\) dans le montage considéré.

La fonction de transfert est :

$$
H_2(p)=
\frac{1}{1+2RC_2p+R^2C_1C_2p^2}
$$

Le polynôme dénormalisé est :

$$
1+\frac{0.4970}{\omega_p}p
+\frac{1.0058}{\omega_p^2}p^2
$$

Par identification du coefficient de \(p\) :

$$
2RC_2=\frac{0.4970}{\omega_p}
$$

$$
C_2=\frac{0.4970}{2R\omega_p}
$$

$$
C_2=\frac{0.4970}{2\times4.3\times10^3\times917.35}
$$

$$
\boxed{C_2\simeq63.0\,\mathrm{nF}}
$$

Par identification du coefficient de \(p^2\) :

$$
R^2C_1C_2=\frac{1.0058}{\omega_p^2}
$$

$$
C_1=\frac{1.0058}{R^2C_2\omega_p^2}
$$

En utilisant les valeurs non arrondies de \(C_2\) et de \(\omega_p\), on obtient :

$$
\boxed{C_1\simeq1.026\,\mathrm{\mu F}}
$$

#### c) Fréquence propre \(f_0\) et coefficient d'amortissement \(m\)

La forme canonique du filtre du second ordre est :

$$
H(p)=\frac{A}{1+\frac{2m}{\omega_0}p+\frac{1}{\omega_0^2}p^2}
$$

Par identification du coefficient de \(p^2\) :

$$
\frac{1}{\omega_0^2}
=\frac{1.0058}{\omega_p^2}
$$

Donc :

$$
\omega_0=\frac{\omega_p}{\sqrt{1.0058}}
$$

$$
\boxed{\omega_0\simeq914.7\,\mathrm{rad/s}}
$$

Sachant que \(\omega_0=2\pi f_0\), on obtient :

$$
f_0=\frac{\omega_0}{2\pi}
=\frac{914.7}{2\pi}
$$

$$
\boxed{f_0\simeq145.58\,\mathrm{Hz}}
$$

Par identification du coefficient de \(p\) :

$$
\frac{2m}{\omega_0}=\frac{0.4970}{\omega_p}
$$

D'où :

$$
m=\frac{0.4970\,\omega_0}{2\omega_p}
$$

En remplaçant \(\omega_0\) par son expression :

$$
m=\frac{0.4970}{2\sqrt{1.0058}}
$$

$$
\boxed{m\simeq0.248}
$$

---

## Partie 2 : Filtre passe-haut de Butterworth (ordre 3)

### 1. Cahier des charges et facteur de sélectivité

Les données sont :

- Fréquence de coupure de la bande passante : \(f_p=400\,\mathrm{Hz}\).
- Fréquence d'atténuation : \(f_a=200\,\mathrm{Hz}\).

Pour un filtre passe-haut, la bande atténuée se situe en dessous de la bande passante. On définit donc :

$$
k=\frac{f_a}{f_p}
=\frac{200}{400}=0.5
$$

$$
\boxed{k=0.5\qquad\text{et}\qquad\frac{1}{k}=2}
$$

### 2. Vérification de l'ordre du filtre

Pour un filtre de Butterworth, l'ordre minimal vérifie :

$$
n\geq
\frac{\log_{10}\left(10^{A_{\min}/10}-1\right)}
{2\log_{10}\left(f_p/f_a\right)}
$$

En reprenant \(A_{\min}=13\,\mathrm{dB}\), valeur utilisée dans le calcul initial :

$$
n\geq
\frac{\log_{10}\left(10^{13/10}-1\right)}
{2\log_{10}(400/200)}
$$

$$
n\geq2.12
$$

L'ordre doit être un entier supérieur ou égal à cette valeur. On choisit donc :

$$
\boxed{n=3}
$$


### 3. Dénormalisation de la fonction de transfert et calcul des composants

Les capacités données sont :

$$
C_1=C=220\,\mathrm{nF}
\qquad;\qquad
C_2=100\,\mathrm{nF}
$$

Pour un filtre passe-haut de Butterworth d'ordre 3, la fonction de transfert normalisée s'écrit :

$$
T(p)=
\frac{1}
{\left(\frac{1}{p^2}+\frac{1}{p}+1\right)
\left(\frac{1}{p}+1\right)}
$$

La pulsation de coupure est :

$$
\omega_p=2\pi f_p
=2\pi\times400
$$

$$
\boxed{\omega_p\simeq2513.27\,\mathrm{rad/s}}
$$

En effectuant la dénormalisation \(p\longleftarrow p/\omega_p\), on obtient :

$$
H(p)=
\frac{1}
{\left[
\left(\frac{\omega_p}{p}\right)^2+
\frac{\omega_p}{p}+1
\right]
\left(\frac{\omega_p}{p}+1\right)}
$$

Posons :

$$
D_1=
\left(\frac{\omega_p}{p}\right)^2+
\frac{\omega_p}{p}+1
$$

$$
D_2=\frac{\omega_p}{p}+1
$$

Pour le second ordre :

$$
D_1=\frac{\omega_p^2+\omega_pp+p^2}{p^2}
$$

Ainsi :

$$
\frac{1}{D_1}
=\frac{p^2/\omega_p^2}
{1+\frac{p}{\omega_p}+\frac{p^2}{\omega_p^2}}
$$

Il s'agit d'un filtre passe-haut actif du second ordre de Sallen-Key.

Pour le premier ordre :

$$
D_2=\frac{\omega_p+p}{p}
$$

Donc :

$$
\frac{1}{D_2}
=\frac{p/\omega_p}{1+\frac{p}{\omega_p}}
$$

Il s'agit d'un filtre passe-haut passif du premier ordre.

La fonction de transfert totale est alors :

$$
H(p)=
\frac{p^2/\omega_p^2}
{1+\frac{p}{\omega_p}+\frac{p^2}{\omega_p^2}}
\times
\frac{p/\omega_p}{1+\frac{p}{\omega_p}}
$$

#### a) Calcul de \(R_3\) pour le filtre passe-haut du premier ordre

La fonction de transfert du premier ordre est :

$$
H_1(p)=\frac{R_3C_2p}{1+R_3C_2p}
$$

Par identification :

$$
R_3C_2=\frac{1}{\omega_p}
$$

Donc :

$$
R_3=\frac{1}{C_2\omega_p}
$$

$$
R_3=\frac{1}{100\times10^{-9}\times2513.27}
$$

$$
\boxed{R_3\simeq3.98\,\mathrm{k}\Omega}
$$

#### b) Calcul de \(R_1\) et \(R_2\) pour le filtre passe-haut de Sallen-Key

La fonction de transfert du second ordre est :

$$
H_2(p)=
\frac{R_1R_2C^2p^2}
{1+2R_1Cp+R_1R_2C^2p^2}
$$

Par identification du coefficient de \(p\) :

$$
2R_1C=\frac{1}{\omega_p}
$$

D'où :

$$
R_1=\frac{1}{2C\omega_p}
$$

$$
R_1=
\frac{1}{2\times220\times10^{-9}\times2513.27}
$$

$$
\boxed{R_1\simeq904.3\,\Omega}
$$

Par identification du coefficient de \(p^2\) :

$$
R_1R_2C^2=\frac{1}{\omega_p^2}
$$

D'où :

$$
R_2=\frac{1}{R_1C^2\omega_p^2}
$$

En utilisant \(R_1=1/(2C\omega_p)\), on peut simplifier :

$$
R_2=\frac{2}{C\omega_p}
$$

$$
R_2=\frac{2}{220\times10^{-9}\times2513.27}
$$

$$
\boxed{R_2\simeq3.62\,\mathrm{k}\Omega}
$$

### 4. Fréquence propre \(f_0\) et coefficient d'amortissement \(m\)

La pulsation propre du second ordre est :

$$
\omega_0=\frac{1}{C\sqrt{R_1R_2}}
$$

Or, d'après l'identification précédente :

$$
R_1R_2C^2=\frac{1}{\omega_p^2}
$$

Ainsi :

$$
\omega_0=\omega_p
$$

$$
\boxed{\omega_0\simeq2513.27\,\mathrm{rad/s}}
$$

La fréquence propre vaut :

$$
f_0=\frac{\omega_0}{2\pi}
$$

$$
\boxed{f_0\simeq400\,\mathrm{Hz}}
$$

Par identification du coefficient de \(p\) :

$$
\frac{2m}{\omega_0}=2R_1C
$$

D'où :

$$
m=R_1C\omega_0
$$

En remplaçant \(\omega_0\) par son expression :

$$
m=R_1C\frac{1}{C\sqrt{R_1R_2}}
$$

On simplifie \(C\) :

$$
m=\frac{R_1}{\sqrt{R_1R_2}}
$$

En écrivant \(R_1=\sqrt{R_1^2}\), on obtient :

$$
m=\frac{\sqrt{R_1^2}}{\sqrt{R_1R_2}}
=\sqrt{\frac{R_1}{R_2}}
$$

Finalement :

$$
m=\sqrt{\frac{904.3}{3617}}
$$

$$
\boxed{m\simeq0.5}
$$

