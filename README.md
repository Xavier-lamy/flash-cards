# Projet FlashCards

## Objectifs généraux

Créer un site/appli de flash cards plus général (pas uniquement pour les langues)

Inspiration principale: les flash card de l'appli [PlecoDictionnary](https://www.pleco.com/)

Autres inspirations utiles:

- [Brainscape](https://www.brainscape.com/) -> notamment pour ses explications sur l'apprentissage espacé, et comment ils ont mis ça en place dans leur appli

## Définition brute du projet et brainstorming d'idées

appli flash card + culture generale
Actions (version mobile):

- tap affiche une card
- swipe haut : affiche le menu de la carte ?
- swipe bas si ne sait pas, tap again affiche la reponse,
- swipe left false,
- swipe right true
- menu sur la gauche en desktop
  Soit:
- utiliser ses propres flashcard et déterminer soi même si on a bon ou pas,
- Pour des raisons d'accessibilité attention avec les swaps, ils doivent pouvoir etre utilisé par un controle à la voix ? si ça marche comme ça ? à voir
- soi utiliser des flashcards prefaites et devoir taper la réponse (validation avec des mots clés), ou qcm,
  - permettrait de faire des classements d'utiliser des flashcards faites par la communauté
  - idée de classement ou de carte avec validation automatique des réponses abandonnée -> cela inciterais à penser un système de validation des cartes, alors qu'il est plus intellignet et rapide de laisser l'utilisateur valider lui meme la carte,, pour l'utilisateur cela lui permet de juste swiper sans avoir a taper de reponses, ce qui est mieux quand il est sur son mobile (cas principal d'utilisation, et qu'il n'a pas beaucoup de temps-> il est dans le bus par exmple, ou entre deux rendez-vous,...), en ce qui concerne d'éventuels compétitions (qui nécessiterais forcément de valider les reponses par l'appli, pour que tout le mond esoit a égalité et que personnne ne puisse tricher,) cela poserait problème dans le sens ou cela casse une parti de l'objectif des flashcards, qui sont normalement des outils pour apprendre , personnelement et chacun à son rythme, créer des concours semble etre typiquement une mauvaise idée créant inutilement un esprit de compétition qui n'a pas lieu d'etre, brainscape utilise un système de compétition intéressant, puisqu'ils mettent en compétition le nombre de cartes jouées et non le taux de réussite, ce qui incite les gens à tenter de faire plsu de cartes, sans se mettre la pressionen se disant qu'ils sont moins bon que les autres -> idée de compétition à éviter: l'objectif est vraiment d'avoir une app utilisable pour n'importe quel type de flashcard , et donc laisser un maximum d'amplitude à l'utilisateur, s'il est en effet moins efficace de faire des applis trop génériques, et qu'il vaut généralemnent mieux se concentrer sur un type en particulier, ici le but est d'avoir justement une app qui fonctionne dans la grande majorité des cas, de façon à ce qu'un utilisateur qui souhaite créer des cartes différentes dans le style (du genre langages, etcartes géographiques), puisse le faire sans avoir besoin de deux applis différentes. L'outil doit donc etre suffisamment maléable pour laissser les utilisateurs créer des cartes de styles très différents (un peu comme pour des mods pour un jeu vidéo où les devs créent un outil de base solide, et les moddeurs peuvent alors créer toute sorte de mods très différents en focntion de ce qu'ils veulent)-> _mdr gé pa lu_

* possibilité d'utiliser les cartes de la communauté sans compte, si on veut créer, ou avoir des stats il faut un compte, sans compte on peut juste tester des cartes de manière random sans que l'appli ne retienne nos scores

* types de flashcards:

  - Mot <-> description/image
  - image <-> description
  - concept <-> schéma (**advanced**:réalisable directment sur l'appli ?)
  - QCM -> réponse (pas vraiment d'intéret à laisser l'utilisateur choisir le sens d'apprentissage)
  - **advanced**: audio (ex: mot de langue étrangère) <-> prononciation phonétique/description/traduction (ex: d'un coté un mot audio, de l'autre sa version écrite, afin de travailler sa prononciation)

* Ajouter une option de dessin ? permettrait à ceux qui apprennent des langues dans un autre alphabet que le leur de répondre en dessinant le caractère puis de comparer leur dessin avec la réponse, leur évitant d'avoir une feuille à coté, (pratique quand on est dns le bus)-> pourrait etre une option avancé, puisque ce système serait légèrement différent, en effet dans tous les autres cas la réponse de l'utilisateur a juste besoin d'etre dans sa tête, là il y aurait un dessin , donc pour la réponse il faut prévoir un espace pour la réponse et un espace pour le dessin/ecriture de l'utilisateur (mais faisable avec des outils de canvas comme celui utilisé sur skribbl par exemple)
- l'espace de dessin peut etre sur la carte en entier (un peu à la façon des flashcards pleco)

* Pour la création des flashcards on pourrait avoir des templates en fonction du type de flashcard ou de la famille de flash cards (exemple les cartes de langues pourraient avoir mot <-> définition/prononciation )

* on peut créer des catégories de cartes (ex: mandarin, formules mathématiques,..)

* En plus des cartes qu'on peut créer pour la communauté on peut créer des decks/collections de cartes, qui pourront aussi etre notés par la communauté ou triés par popularité, ainsi si on ne veut pas créer soit meme une collection de cartes culture générale, on peut prendre une collection, les collections pourraient etre nommés et contenr des sous collections, permettant ainsi d'avoir des séries (par exemple collection: `apprendre l'arabe`, sous collection `1.1 - Les bases`, `1.2 - L'écriture`, ...)

* Pour les collections, indiquer la progression par des graphs (rang de la carte, taux de réussite)

* Quand on crée une carte on peut choisir de mettre plusieurs éléments sur un seul coté, (exemple prononciation + caractère), et il faut choisir quels éléments sont choisis par défaut (tous ceux ajoutés ?, seulement une partie)

* Possibilité de choisir une priorité d'apprentissage: quand c'est la première fois qu'on passe sur une carte le système pourrait ne pas la reproposer avant longtemps ou la reproposer dans peu de temps, mais peut etre que l'utilisateur pourrait estimer que ça il sait mieux que la carte précédente (qu'il connait aussi mais estime moins la connaitre), il faudrait peut etre avoir un système qui permet à l'utilisateur de déterminer la priorité d'apprendtissage de la carte (entre deux cartes réussies au cours d'une session, laquelle il connait le mieux, entre deux échouées laquelle il connait le moins bien), cela pourrait consister à ajouter un niveau de priorité (lié à la difficulté): plusieurs possibilités:

  - Inspiré de brainscape: une jauge, qui permet à l'utilsateur de définir à quel point il pense connaitre ou non la réponse
  - Inspiré de pleco: un niveau de priorité (sur la carte ou dans les paramètres de la carte) qui peut etre changé ou définit automatiquement
  - Optimal, une sorte de mélange des deux, le mieux est d'éviter à l'utilisateur d'avoir à faire ça à chaque fois, il faudrait que la priorité d'apprentissage soit majoritairement automatique en fonction de la difficulté, du taux de réussite, ..., peut etre créer une option de calbrage: l'utilisateur pourrait choisir d'ajouter à ses sessions (notamment lorsqu'il utilises un set de cartes pour la première fois) une jauge ou autre moyen de graduer sa réussite, idées diverses:
    - la direction dans laquelle il swap pour valider pourrait déterminer la difficulté, exemple en haut très bien réussi, à droite comme d'hab réussie, en bas largement echouée (priorité haute), à gauche échouée -> problème , peut etre pas très intuitif, et facile de se rater en swipant, (alors que juste gauche/droite façon appli de rencontre, c'est plus simple et plus intuitif)
    - une simple option prioritaire à cocher/sélectionner, ensuite en fonction du sens dans lequel on swipe cela rend: soit la carte plus prioritaire si on l'a échouée, soit moins importante si on a réussi
    - Une option choix multiples haute priorité/basse priorité, avant de swiper pour valider
    - Une jauge sur 3 ou 5 niveaux d'assurance
    - Utiliser le sytème des rangs, cela permettrait de passer la carte au rang supérieur, cela ne gère qu'en parti la priorité automatique de la carte, mais permet quand même à l'utilisateur de choisir à quel niveau il pense connaitre cette carte, (si elle est à un niveau élevé c'est qu'il la connait bien, et donc dans le cas ou il fait une session générale sans rang particulier cette carte pourrait apparaitre moins ? ou le simple faite qu'elle ai un rang permet à l'utilisateur de choisir lui meme quelle rang de carte il veut lors de l'apprentissage) -> **idée: A coté de l'indication du rang actuel, un plus et un moins pour augmenter le rang ou le réduire si besoin**, à la création des cartes on peut leur attribuer un rang déjà élevé si on estime déjà les connaitre bien

* ¨Possibilité de sauvegarder les cartes hors ligne pour la version appli mobile ? -> qu'est ce que ça implique pour la bdd ? , il faut donc que cela soit stocké sur l'appareil de l'utilisateur
* Possibilité d'importer des cartes en JSON ou autre format, ou des données via une API, à voir ce que cela implique en terme de sécurité pour l'appli ?
* Possibilité d'exporter des cartes ? Intérêt à voir ?, si elles sont uniquement utilisable sur le site/appli, c'est sans doute pas très utiles, à voir peut etre: une option pour convertir en version imprimable ?

* Dans les options il faut pouvoir customiser l'aspect visuel des cartes (couleurs de font, police, couleur du texte, disposition des éléments de réponses)

* Créer un système de réclamation et de signalement, si on s'aperçoit que des cartes ont un problème (infos erronées, insultantes, pas dans la bonne catégorie...), on peut en premier lieu contacter l'auteur de la carte s'il est toujoours présent sur le site, pour signaler l'erreur; si ce n'est plus possible on peut les signaler les cartes signalées pourraient:

  - etre gérées directement par la communauté (lorsqu'une carte est signalée, la communauté peut voter pour déterminer si la carte pose en effet problème ou non, on peut alors choisir d'exclure totalemnt la carte, ou d'y ajouter un avertissement) -> problème, s'il n'y a pas assez d'utilisaeur, soit le système est inutilisable soit il est dangereux (avec des signalements rendus possibles par une minorité capable de nuire au système, exemple virer des cartes juste pour le fun; si beaucoup de personnes, rien n'empêche techniquement un raid organisé (peu probable, mais à prendre en compte tout de même)
  - etre gérée par des modérateurs -> problèmes: nécessite une équipe, fiabilité de l'équipe ?

* Créer un systèm de notes, on peut noter les cartes de la communauté :soit note globale sur 10 points/5 demi étoiles, soit notes divisées: justesse de la carte (l'info est elle vraie ?), efficacité de la carte (est elle bien rédigé, pas d'infos superflu, on peut la lire rapidement), on pourrait aussi utiliser la popularité des cartes (combien d'utilisateurs les utilisent dans leur "deck", ou combien de fois elles ont été utilisés dans des sessions d'apprentissage)

* Pour les infos que l'utilisateur doit avoir, tâcher d'etre le plus efficace possible, phrases courtes et efficaces, avec si besoin un lien vers une aide plus détaillée, plutot qu'un pavé de texte directment

* dans les paramètres on peut choisir la fréquence des cartes:

  - quand une carte est sue (quand on a swipé pour la valider), un timer lui est ajouté pour déterminer dans combien de temps l'appli nous représentera la carte, également en fonction du niveau de succès de la carte:
    - cela est déterminé par les réglages, on peut ajouter un niveau de difficulté au cartes, et déterminer un réglage de temps e fonction de ce niveau:
    - exemple une carte niveau facile si elle est sue une première fois ne réapparaitra que au bout de 20 jours la toute première fois, au bout de 20 jours si on réussi encore, la carte obtient alors un taux de réussite qui est de 100% (il faut minimum deux passages sur une carte pour qu'elle commence a avoir un taux de réussite ), avec ce taux elle sera alors représentée dans 30jours (créer une formule qui prend en compte le temps en fonction du niveau de difficulté et du taux de réussite)

* Possibilité de planifier des sessions d'apprentissage (exemple tous les mercredis à 13h avoir une notif de rappel pour une séance de cartes)

* Créer un système de _rang_ (nom à changer ?), en plus des catégories/sous-catégories et niveaux de difficultés on peut choisir au sein d'une meme catégorie des rangs, les rangs permettent de se laisser de la souplesse sur la valdation des réponses par exemple rang 1 on peut ne connaitre qu'une partie de la réponse alors qu'un rang 5 nécessite la réponse exacte (laissée à l'appréciation de l'utilisateur), , par exmple pour du mandarin on pourrait avoir un rang de base `mot anglais` <-> `mot mandarin écrit/prononciation/Tons`, les cartes lorsqu'elles sont rangées au rang 1, peuvent etre considérées valides juste si on a le bon mot, peu mporte le ton et l'écriture, au rang 2 il faudrait en plus etre capable de connaitre le ton des mots, puis finalement de savoir l'écirre, cela permettrait sur des notions avancées, d'avoir une progression, la personne pourrait choisir de déjà maitriser les traductions, avant de se soucier des prononciations puis de l'écriture/orthographe correcte (puiqu'il faudrait qu'il sache en premier comment dire ce mot, avant de se soucier de la prnonciation exacte ou de l'ortographe), dans les options on peut choisir au bout de combien de fois, un mot réussi dans un rang doit automatiquement passer au rang supérieur (laisser une possibilité de le mettre manuellement ?), exemple quand l'utilisateur a réussi (voir entre nombre de carte réussies d'affilés-> préférable dans ce cas afin de voir plutot en fonction de sa progression récente plutot que de la réussie globale, ou en fonction du taux de réussite ?) 3 fois de suite ou a un taux de réussite de 75% sur une carte alors celle ci peut passer au rang supérieur -> l'idée des rangs pourrait etre abandonnée s'il n'y a pas assez de cas dans lesquels cela pourrait etre utile( en géographie on pourrait avoir le nom d'un pays et au verso, la population, langue parlée, superficie,..., ainsi l'utilisateur pourrait avoir un rang quand il connait la langue parlée, un autre quand il connait la supericie et la langue parlée, un dernier quand il connait tous les éléments)
* Ajouter une option pour rétrogader ou promouvoir automatiquement une carte après un certain nombre (réglable) d'échecs ou de réussite, en plus de laisser l'utilisdateur le faire manuellement
* Les rangs sont nomable et pourraient soit etre pratiqués individuellement exemple: session de cartes rangs 3, soit mélangées quelquesoit le rang et dans ce cas avoir le rang marqué au dessus de la réponse pour indique à l'utilisateur quel sévérité il peut utiliser pour valider ou on la carte), le rang pourrait etre changeable en cours de validation, exempleune fois la réponse affichée, si la carte est en rang 1 (ex:juste définition) et qu'on estime que on sait aussi la prononciation et l'écrit alors on peut la passer au rang supérieur (select ? / Jauge ?)

* Les familles de cartes sont au dessus des catégories et sous catégories, elles sont définies par le site et sont les grands groupes d'apprentissage: langue, géographie, histoire, culture générale,...

* niveaux de difficultés:

  - facile
  - moyen
  - difficile
  - custom (non disponible pour les cartes qu'on crée pour la communauté, ou alors il faudrait ajouter en plus du nom de la difficulté une estimation de la position de cette difficulté par rapport aux autres)
  - Il pourrait etre déterminé: soit par l'auteur, soit automatiquement en fonction de notre taux de réussite par rapport au nombre d'essai (exempple une carte qu'on a faite 20 fois avec seulement 30% de taux de réussite, est clairement une carte difficile en revanche une carte faite uniquement 3 fois, si elle a un taux de réussite de 33%, cela signifie simplement qu'on l'a réussi une fois et échoué deux fois, mais elle n'a pas été faite beaucoup de fois, donc peut etre que seulement deux essais de plus porterait son score à 80% dans ce cas la le taux de réussite seul , n'est pas un bon indicateur de la difficulté, à voir donc comment prendre en compte les deux éléments)

* Paramètres d'une session d'apprentissage:

  - famille de carte
  - catégorie et/ou sous-catégorie
  - difficulté des cartes (toutes, facile, moyen, difficile)
  - rang des cartes (si elles en ont: tous les rangs, rang 1, 2 jusqu'à 5 ou nombre custom ?)
  - nombre de cartes à apprendre/ou chronomètre avec objectif maximum de cartes dans un certain temps (utile ?)
  - Si en mode nombre de cartes , option pour chronométrer le temps passé ?
  - Notes (quand on utilise des cartes de la communauté on peut les filtrer en fonction de leur note/popularité)
  - quelle partie de la carte on montre (recto ou verso, si un des côtés possèdent plusieurs infos, laquelle montrer ? juste la prononciation, prononciation et écriture ?....)

* Recto et verso peuvent avoir plusieurs éléments -> voir au niveau bdd si du coup on stock le contenu recto et verso ou si on stock plutot des types de réponses (définition, description, prononciation, formule, image, qcm, schéma,...) et on choisit ensuite ce que l'on souhaite afficher sur la carte ? à voir car ce ne serait pas la meme chose si on prend des cartes communautaires ou perso -> problème si on a des cartes communautaires avec les types description et image, et d'autres schéma et formule , comment on choisit ça dans les paramètres de session ?, il faudrait que l'option pour changer ce qu'on affiche sur les cartes ne soit dispoque pour les cartes d'un meme type, le mieux serait donc que par défaut on a juste question sur recto/ réponse sur verso, ensuite on peut créer des types de cartes avancées (certains patterns déjà tout fait existeront par exemple pour les langues ou la géographie), sur lesquels on choisit les différents éléments (ex: nom du pays, drapeau, population, langue), toutes les cartes suivant ce modèle ne peuvent que etre mélangés avec des cartes suivant le meme modèle (collection de carte), ou alors des cartes génériques mais à ce moment là on ne peut ps sélectionner les éléments affichables ou non (on pourra ainsi tout de meme utiliser nos cartes dans une collection générique, et afficher toutes les infos)

* Mode flashcard auto ? : si on souhaite apprendre quelquechose ou la création de flash cards serait longue et fastidieuse (exemple vérifier qu'on sait calculer du binaiore rapidement), il pourrait dans ce cas y avoir des listes auto (vu que les cartes ne sont pas sauvegardés les stats ne fonctionneraient pas du coup ?), l'appli envoie à chaque fois un nombre et la réponse en binaire, pour se tester, soit il y aurait des types de listes préfaites, comment construit on ces cartes ?:
  - on pourrait avoir des séries auto-préfaites (exemple pour le binaire, donc codé en dur dans l'appli), 
  - ou alors la possibilité pour l'utilisateur de créer des règles qui régissent ces cartes auto (exemple s'il veut une série de carte pour la table du 11, il pourrait choisir pour règle les nombres entre 0 et 100 * 11)
  - une importation depuis du JSON (mais cela pourrait aussi etre utilisé pour simplement créer des séries de cartes) 

* Faire un systme de succès pour encourager les gens à apprendre des cartes

* statistiques et données des cartes:

  - Générales et personnelles:
    - Contenu du recto (plusieurs éléments ?)
    - Contneu du verso (plusieurs éléments ?)
    - difficulté de la carte
    - Rangs possibles et rang actuel
    - Famille
    - Catégorie
    - Note sur le site globale (si partagée)
    - Popularité globale (si partagée)
  - Propre à une carte de l'utilisateur:
    - rang actuel de la carte
    - Nombre de passage sur la carte
    - taux de réussite
    -
  - Propre à l'utilisateur:
    - Taux de réussite globale
    - Cartes pratiquées par jour
    - difficulté globale des cartes réussi (créer un score en fonction de la difficulté et du taux de réussite ?)

* Pour le design du site
  - on épure au maximum
  - Il faut que les sessions soit le plus accessible possible:
    - Options de base préparamétrées, l'utilisateur n'a plus qu'à choisir une catégorie/famille et il peut lancer,
    - quand il a lancé une fois, cela garde ses paramètres en mémoire donc quand il lance l'app ou le site il peut en un clic relancer sa session en cours ou en lancer une nouvelle (un peu commme un bouton continuer la partie), un autre bouton peut lui permettre de changer les réglages avant d elancer une nouvelle série
  - une page de presentation de ce que sont les falshcard et pourquoi on peut les utiliser (peut servir pour le référencement)
  - un tuto simplifié la première fois qu'on utilise (on peut sauter le tuto), ne pas faire un tuto frustrant avec une fenetre qui pop toutes les deux secondes, mais plutot quelque chose d'épuré et de très simple(ex: swipe à droite pour une carte acceptée, ...)
  - commencer par la version mobile
  - Menu à gauche
  - Fair un schéma des différentes parties et interactions possibles, afin de voir par exmeple en combien de clics on arrive au menu, aux options, on lance une session,...
  - Possibilité de se connecter avec un compte (genre réseau social, google,...) ?
  - Idées logo:
    - Cartes stylisées, logo double sens flash (la forme des cartes peut éoquer à la fois des cartes ou un éclair)

- penser à l'internationalisation: faire site en anglais, mettre une version francaise au moins ?
  - i18n ?

utiliser un linter ?

express.js pour node en mode web
sequelize pour l'ORM

stimulus si on fait avec laravel
vue/react -> pas obligatirmenet de bdd

pour le projet vue en front ? , node en back ? voir Strapi ?

export -> electron (desktop)/capacitor (mobile)

faire une todo en test pour tester vue front

docker:
1. outiller le projet : bdd avec docker par exemple
2. utiliser docker compose meme sur un projet unique
3. mariaDB adminer
En dernier tenter carrément de run le projet sur docker

---

## Définition recadrée du projet
Les parties avec un ``??`` sont en attente d'être complétées

### 1.1 Compétences du référentiel validées par le projet:

REAC:
Front: Développer la partie front-end d’une application web ou web mobile en intégrant les recommandations de sécurité:

1. ✔️Maquetter une application `obligatoire`
2. ✔️Réaliser une interface utilisateur web statique et adaptable `choix dev`
3. ✔️Développer une interface utilisateur web dynamique `choix dev`
4. ❌Réaliser une interface utilisateur avec une solution de gestion de contenu ou e-commerce `choix CMS`

Back: Développer la partie back-end d’une application web ou web mobile en intégrant les recommandations de sécurité:

1. ✔️Créer une base de données
2. ✔️Développer les composants d’accès aux données `obligatoire`
3. ✔️Développer la partie back-end d’une application web ou web mobile `choix dev`
4. ❌Elaborer et mettre en oeuvre des composants dans une application de gestion de contenu ou e-commerce `choix CMS`

### 2. UX Design

#### 2.1 Objectifs généraux
+ L'objectif est de réaliser une application de flashcards maléable.
+ Les utilisateurs doivent pouvoir:
  - Créer leur propres flash cards
  - S'entrainer en utilisant leur flashcards ou celles de la communauté
  - Il doit donc y avoir possibilité d'envoyer ses cartes en visibilité publique
  - Avoir un aperçu de leur progression
#### 2.2 Cas utilisateurs
On crée 3 personnas:
##### 2.2.1 Bob
Bob a 16ans, son professeur d'anglais lui a recommandé les flashcards pour apprendre du nouveau vocabulaire, il a regardé très rapidement le concept des flashcards mais n'est pas sûr de comprendre comment les utiliser.
+ Quelles sont ses attentes ?:
+ Quelles sont ses freins potentielles ?:

##### 2.2.2 Phillipe-Adalbert Germain Du Plessix de l'Escarrère 
PA a 24 ans il est professeur et souhaiterait inciter ses élève à utiliser les flashcards, il voudrait pouvoir les créer lui même sous forme de cours progressifs.

##### 2.2.3 Gertrude
Gertrude a 37ans, elle ne cesse jamais d'apprendre, et est toujours à la recherche de nouveaux éléments à découvrir, néanmoins son emploi de chef dans un palace ne lui laisse que très peu de temps pour apprendre, elle connaît bien le principe des flashcards, récemment elle s'est mis à apprendre l'arabe.

#### 2.3 UI
+ Réaliser un wireframe afin de déterminer la forme général du site en mobile puis en desktop, et définir les cheminements de l'utilisateur
+ Définir la charte graphique et l'identité du site:
  - Les couleurs: ``??``
  - Nom du site: ``??``
  - Slogan : ``??`` 
  - Le logo: Deux cartes se chevauchant, à leur jonction un changement de couleur symbolise un éclair
  - Les formes: ``??``
+ Réaliser la maquette

### 3. Propositions de tests

### Fonctionnement de la BDD

faire des schémas

### Technologies et outils utilisées
- Figma pour le wireframe, et la maquette
- Gimp et Inkscape pour le logo et la retouche d'images
- Front: Vue.js
- Back: 
  - Express.js pour le routing
  - Sequelize pour l'Object Relational Mapper (ORM)
  - ``??`` pour la base de donnée
