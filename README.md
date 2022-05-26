# Projet FlashCards

## Objectifs généraux
+ Créer un site/appli de flash cards plus général (pas uniquement pour les langues)

+ Inspiration principale: les flash card de l'appli [PlecoDictionnary](https://www.pleco.com/)

+ Autres inspirations utiles:
  - [Brainscape](https://www.brainscape.com/) -> notamment pour ses explications sur l'apprentissage espacé, et comment ils ont mis ça en place dans leur appli

## Définition brute du projet et brainstorming d'idées
+ Les éléments ensuite renotés dans la définition au propre du projet ou abandonnés seront rayés
+ Les raisons de l'abandon d'éléments seront expliquées en fin de document
+ Voir l'annexe: [Archives des idées du Brainstorming](#archives-des-idées-du-brainstorming), pour la totalité des idées au lancement du projet.


+ Pour les éléments sur les cartes peut etre utilisé un système de checksum par exemple si dans la bdd pour une carte on a 2items au recto 3 au verso elle a une checksum qui dépend de ces items, une autre carte meme si elle a le meme nombre d'items (2 et 3) pourrait ne pas avoir la meme checksum car cela dépendra du nom des items (exemple peut etre quelque chose du genre traduction_prononciation) => problème: qu'arrive-t-il si l'utilisateur ne rentre pas a chaque fois els élements dans le meme ordre ? exemple un coup ol met prononciation puis trduction et l'autre coup il inverse, solution => utiliser l'ordre alphabétique, ainsi peut importe l'ordre dans lequel il met il y aura toujours le meme ordre (ici prononciation_traduction) pour la checksum, pour contrecarrer les problème d'utilisateur qui n'écrivent pas les items de la meme façon à chaque fois on pourrait avoir un select qui permettrait de choisir les types d'items déjà utilisé (exemple "traduction", "caractère"), pour les collections il pourrait aussi y avoir la possibilité de créer des cartes au sein d'une collection, ainsi le template de cartes nous afficherait toutes les options présentes  sur ce type de carte, ne marcherait pas pour les collections génériques du coup ? 

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

* Pour les infos que l'utilisateur doit avoir, tâcher d'etre le plus efficace possible, phrases courtes et efficaces, avec si besoin un lien vers une aide plus détaillée, plutot qu'un pavé de texte directment

* dans les paramètres on peut choisir la fréquence des cartes:
  - quand une carte est sue (quand on a swipé pour la valider), un timer lui est ajouté pour déterminer dans combien de temps l'appli nous représentera la carte, ce time pourrait fonctionner de la manière suivante:
    - On notifie quel est la position de la carte (exemple c'est la 536eme carte qu'on apprend), le "timer" définit dans combien de cartes on pourra la reproposer, au lancement d'une session si il y assez de cartes, l'appli ne choisira pas cette carte si on a pas encore atteint le "time" (ex: c'était la 536eme carte, le timer avait définit qu'on ne devait pas la revoir avant 40 cartes, donc si on en est actuellement à la 556eme carte il ne devrait pas la reproposer car il faut qu'il attende la 576eme carte, je pense qu'il est mieux de ne pas se soucier du nombre de cartes qu'il y aura dans la session, par exemple si on avait une session de 100 cartes techiniquement on atteindrait cette 576eme carte au bout de la 20eme denotre session dans cet exemple néanmoins cela complexifierais le calcul inutilement et poserais problème , en effet vu que les cartes sont définis aléatoirement avant la session, celle ci risquerait d'apparaitre avant le temps imparti, ce qui pourrait ne pas etre un problème mais pourrait aussi le devenir dans le cas ou l'utilsiateur a souvent tendance à ne jamais finir ses sessions)
  - ce timer est également imapcté en fonction du niveau de succès de la carte:
    - cela est déterminé par les réglages, on peut ajouter un niveau de difficulté au cartes, et déterminer un réglage de temps e fonction de ce niveau:
    - exemple une carte niveau facile si elle est sue une première fois ne réapparaitra que au bout de 20 jours la toute première fois, au bout de 20 jours si on réussi encore, la carte obtient alors un taux de réussite qui est de 100% (il faut minimum deux passages sur une carte pour qu'elle commence a avoir un taux de réussite ), avec ce taux elle sera alors représentée dans 30jours (créer une formule qui prend en compte le temps en fonction du niveau de difficulté et du taux de réussite)
  - Le timer pourrait aussi fonctionner avec un temps Unix

* Créer un système de _rang_ (nom à changer ?), en plus des catégories/sous-catégories et niveaux de difficultés on peut choisir au sein d'une meme catégorie des rangs, les rangs permettent de se laisser de la souplesse sur la valdation des réponses par exemple rang 1 on peut ne connaitre qu'une partie de la réponse alors qu'un rang 5 nécessite la réponse exacte (laissée à l'appréciation de l'utilisateur), , par exmple pour du mandarin on pourrait avoir un rang de base `mot anglais` <-> `mot mandarin écrit/prononciation/Tons`, les cartes lorsqu'elles sont rangées au rang 1, peuvent etre considérées valides juste si on a le bon mot, peu mporte le ton et l'écriture, au rang 2 il faudrait en plus etre capable de connaitre le ton des mots, puis finalement de savoir l'écirre, cela permettrait sur des notions avancées, d'avoir une progression, la personne pourrait choisir de déjà maitriser les traductions, avant de se soucier des prononciations puis de l'écriture/orthographe correcte (puiqu'il faudrait qu'il sache en premier comment dire ce mot, avant de se soucier de la prnonciation exacte ou de l'ortographe), dans les options on peut choisir au bout de combien de fois, un mot réussi dans un rang doit automatiquement passer au rang supérieur (laisser une possibilité de le mettre manuellement ?), exemple quand l'utilisateur a réussi (voir entre nombre de carte réussies d'affilés-> préférable dans ce cas afin de voir plutot en fonction de sa progression récente plutot que de la réussie globale, ou en fonction du taux de réussite ?) 3 fois de suite ou a un taux de réussite de 75% sur une carte alors celle ci peut passer au rang supérieur -> l'idée des rangs pourrait etre abandonnée s'il n'y a pas assez de cas dans lesquels cela pourrait etre utile( en géographie on pourrait avoir le nom d'un pays et au verso, la population, langue parlée, superficie,..., ainsi l'utilisateur pourrait avoir un rang quand il connait la langue parlée, un autre quand il connait la superficie et la langue parlée, un dernier quand il connait tous les éléments)
* Ajouter une option pour rétrogader ou promouvoir automatiquement une carte après un certain nombre (réglable) d'échecs ou de réussite, en plus de laisser l'utilisdateur le faire manuellement
* Les rangs sont nomable et pourraient soit etre pratiqués individuellement exemple: session de cartes rangs 3, soit mélangées quelquesoit le rang et dans ce cas avoir le rang marqué au dessus de la réponse pour indique à l'utilisateur quel sévérité il peut utiliser pour valider ou on la carte), le rang pourrait etre changeable en cours de validation, exempleune fois la réponse affichée, si la carte est en rang 1 (ex:juste définition) et qu'on estime que on sait aussi la prononciation et l'écrit alors on peut la passer au rang supérieur (select ? / Jauge ?)

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
  - un tuto simplifié la première fois qu'on utilise (on peut sauter le tuto), ne pas faire un tuto frustrant avec une fenetre qui pop toutes les deux secondes, mais plutot quelque chose d'épuré et de très simple(ex: swipe à droite pour une carte acceptée, ...), par exemple cela pourrait être une session de flashcards avec les tutos à la place des cartes ?
  - commencer par la version mobile
  - Menu à gauche
  - Fair un schéma des différentes parties et interactions possibles, afin de voir par exmeple en combien de clics on arrive au menu, aux options, on lance une session,...
  - Possibilité de se connecter avec un compte (genre réseau social, google,...) ?


- penser à l'internationalisation: faire site en anglais, mettre une version francaise au moins ?
  - i18n ?

---------------------------------------------------------------

## Définition recadrée du projet
+ Les parties avec un ``??`` sont en attente d'être complétées
+ Les termes en gras correspondent aux termes officiels qui seront utilisés par l'application et devront donc être traduits également en anglais pour servir de références dans les BDD notamment

### 1. Compétences du référentiel validées par le projet:

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
  - Il doit donc y avoir possibilité de partager ses cartes avec la communauté
  - Avoir un aperçu de leur progression
#### 2.2 Cas utilisateurs
On crée 3 personnas:
##### 2.2.1 Bob
Bob a 16ans, son professeur d'anglais lui a recommandé les flashcards pour apprendre du nouveau vocabulaire, il a regardé très rapidement le concept des flashcards mais n'est pas sûr de comprendre comment les utiliser.
+ Quelles sont ses attentes ?: 
  - Apprendre à utiliser les flashcards
  - Pouvoir les utiliser rapidement et simplement
+ Quelles sont ses freins potentielles ?:
  - L'utilisation des flashcards ne vient pas de son propre chef, il pourrait donc être plus rapidement frustré ou avoir envie d'abandonner
  - ``??``

##### 2.2.2 Phillipe-Adalbert Germain Du Plessix de l'Escarrère 
PA a 24 ans il est professeur et souhaiterait inciter ses élève à utiliser les flashcards, il voudrait pouvoir les créer lui même sous forme de cours progressifs.
+ Quelles sont ses attentes ?:
  - Pouvoir créer rapidement et facilement des flashcards
  - Pouvoir créer des collections de cartes organisées, avec des progressions différentes en fonction du niveau de ses élèves
  - Pouvoir partager les cartes créés avec ses classes 
  - Pouvoir créer les cartes autant depuis son pc de bureau que depuis son portable afin de pouvoir progresser autant depuis chez lui que dans les transports en commun en allant au travail
+ Quelles sont ses freins potentielles ?:
  - Si l'expérience utilisateur est trop différente entre son pc et son portable, il pourrait ne pas vouloir créer des cartes sur l'une des deux plateformes et donc avoir moins de temps pour préparer les flashcards pour ses élèves


##### 2.2.3 Gertrude
Gertrude a 37ans, elle ne cesse jamais d'apprendre, et est toujours à la recherche de nouveaux éléments à découvrir, néanmoins son emploi de chef dans un palace ne lui laisse que très peu de temps pour apprendre, elle connaît bien le principe des flashcards, récemment elle s'est mis à apprendre l'arabe.
+ Quelles sont ses attentes ?:
  - Pouvoir récupérer des collections de cartes préfaites pour les langages
  - Pouvoir créer ses propres cartes qu'elle pourra intégrer aux collections préfaites (par exemple pour des expressions locales ou d'argot qu'elle ne trouve pas dans les collections de la communauté)
+ Quelles sont ses freins potentielles ?:
  - Elle n'a que très peu de temps pour apprendre (quelques minutes pendant les repas)
  - Elle n'a donc pas vraiment de temps pour créer des cartes
  - Malgré son envie d'apprendre; le manque de temps et la difficulté d'apprendre une nouvelle langue pourrait la décourager, elle pourrait en effet assez rapidement croire qu'elle ne progresse pas


#### 2.3 Conclusions de la recherche utilisateurs et réponses aux problèmes de base
En conclusion on cherche à:
  - Pouvoir créer des cartes de genres variés afin de s'adapter aux différents profils utilisateurs
  - Pouvoir comprendre le fonctionnement sans risque de se décourager, limiter au maximum la frustration
  - Pouvoir utiliser les cartes de manière rapide sans avoir des centaines de réglages à paramétrer au début et pouvoir ainsi lancer des sessions d'apprentissage n'importe où, n'importe quand
  - Pouvoir disposer quand même d'une certaine flexibilité quand aux utilisations qu'on pourra faire de ce site (cela doit donc faire partie de réglages additionnels qui ne doivent pas intérférer avec l'utilisation classique) 
  - Rendre le site ludique, pour inciter les utilisateurs qui n'ont de base pas de volonté d'apprendre de cette manière, mais y sont contraints par leur environnement, ou ceux qui manquent de temps et pourraient se décourager, à poursuivre leur apprentissage, pour cela on pourrait mettre en place un système de succès en plus des statistiques de cartes, les succès étant probablement plus amusants et entrainants que des stats brutes (puisqu'il est nécessaire d'aller voir nos stats et de les comprendres, alors qu'un succès montre rapidement et dans la continuité de l'utilisation classique qu'on a progressé dans un domaine) 

#### 2.4 Mise en place des solutions et concepts généraux du site
+ [Fonctionnement des flashcards](#241-fonctionnement-des-flashcards)
+ [Les catégories et sous-catégories](#242-les-catégories-et-sous-catégories)
+ [Les collections](#243-les-collections)
+ [Les notes](#244-les-notes)
+ Les rangs de cartes
+ Les niveaux de difficulté des cartes
+ La difficulté estimée des collections
+ Les éléments de flashcards
+ Fonctionnement de la création de carte
+ Les statistiques
+ Les succès
+ La progression de l'utilisateur
+ Fonctionnement d'une session d'apprentissage
+ Les paramètres de session
+ Les paramètres généraux
+ Signalement et réclamation
##### 2.4.1 Fonctionnement des flashcards
+ Les flashcards possèdent un recto et un verso
+ Sur chaque côté plusieurs éléments peuvent être affichés (ex: ``traduction + prononciation <=> mot étranger``)
+ Chaque carte doit avoir un affichage par défaut (c'est à dire spécifier ce qui s'affiche par défaut au recto et au verso)

##### 2.4.2 Les catégories et sous-catégories
Les **catégories**  correspondent à la taxonomie la plus élevée du site
+ Certaines sont crées dès le lancement du site
+ Les catégories et sous-catégories peuvent être ajoutées par les utilisateurs pour leurs propres collections
+ Il peut y avoir techniquement une infinité de sous-catégories néanmoins il faudra tenter de limiter à 2 générations de sous-catégories, l'objectif n'est pas de faire une classification réelle du savoir, mais d'avoir une classification générale afin de faciliter la navigation sur le site.
+ Par exemple, tenter de classer toutes les cartes liées aux langues en fonction des familles linguistiques, serait suicidaire; voir les [langues par famille sur Wikipédia](https://fr.wikipedia.org/wiki/Langues_par_famille)
+ De plus classer de manière trop scientifique, bien que plus exacte, risquerait d'être juste incompréhensible pour la majorité des gens, si on souhaite savoir ce qu'est la famille des langues Finno-Ougriennes alors il est plus pertinent d'apprendre une série de cartes sur les familles de langues, plutôt que d'observer les catégories
+ L'ajout de catégories et sous-catégories en version publique, devra faire l'objet d'une demande validée
+ Une carte ou une collection peut techniquement appartenir à plusieurs catégories, mais il est recommandé d'en utiliser qu'une seule
+ Les catégories (liste non exhaustive) avec des exemples de sous catégories:
  - Culture générale
  - Histoire
    - Moyen-Age Européen
    - Renaissance Italienne
    - Histoire des peuples Méso-américains
    - ...
  - Géographie
  - Langues
    - Linguistique
    - Français
    - Anglais
    - Japonais
    - Arabe
    - ...
  - Sciences
    - Mathématiques
    - Biologie
    - Chimie
    - ...
  - Politique
  - Justice & Droit
  - Economie
  - Santé
  - Sport
    - Sports collectifs
    - Sports individuels
  - Arts & Cultures
    - Musique
    - Littérature
    - Cinéma
    - Jeux-vidéos
    - Peinture
    - Sculpture

##### 2.4.3 Les collections
Les collections sont des groupes de cartes généralement liées à une même thématique, et pouvant appartenir à une ou plusieurs catégories
+ Il peut s'agir:
  - d'un groupement de cartes rassemblées par un utilisateur sur son profil privé
  - d'un groupement de cartes rassemblées par un utilisateur sur un profil public et donc accessible à la communauté
+ Seule les collections peuvent être partagées en profil public, les cartes isolées peuvent uniquement être créée de manière privée (il est de toute façon généralement conseillé de créer des collections plutôt que de laisser des cartes seules)
+ Une collection publique possède:
  - Un auteur principal:
    - qui a créé et nommé la collection
    - qui peut accepter ou non les demandes d'édition
    - qui peut accepter les ajouts d'auteurs secondaires
  - Des auteurs secondaires
+ Elle est définie par:
    - Un **nom**
    - une **description**
    - des éventuelles **sous-collections** (exemple pour une collection *Apprendre l'Arabe*, on pourrait avoir *1.1 Les bases*, *1.2 L'écriture*, ... )
    - Une **popularité** définie par le nombre de personnes qui ont choisi de l'utiliser
    - Une **note globale** définie par la moyenne des **notes** utilisateurs
    - Une **difficulté estimée** fixée par l'auteur principal
+ Lorsqu'on utilise une collection on peut choisir:
  - De l'utiliser telle quelle: on ne peut pas la modifier, mais si des cartes sont modifiées ou ajoutées par le créateur elles s'ajouteront à notre instance de la collection
  - De la privatiser: dans ce cas les cartes deviennent comme une de nos collections privée, on peut les modifier, les supprimer en ajouter, mais cela n'impacte pas la collection publique et on ne bénéficie pas des modifications de cette dernière
+ Une collection publique ne peut pas être complètement supprimée, si un auteur principal supprime son compte, alors le premier auteur secondaire devient le responsable pour la maintenance de la collection
+ Si un auteur estime que sa collection n'est plus pertinente, il peut alors la marquer comme étant **inactive**, dans ce cas un message d'avertissement sera affiché aux utilisateurs qui s'en servent lorsqu'il l'utiliseront. Une collection **inactive** ne peut plus être modifiée
+ Si une collection n'a plus aucun auteur actif, alors elle est aussi marquée **inactive**
+ Lors de la recherche des collections, il doit y avoir des filtres pour:
  - Choisir les catégories et sous-catégories
  - Choisir les auteurs
  - Choisir de classer par popularité et/ou par note
  - Choisir d'activer ou non les **collections** **inactives**  

##### 2.4.4 Les notes
+ Les cartes ne peuvent pas être notées individuellement
+ Seules les **collections publiques** peuvent être notées
+ Il faut avoir utilisé (en tant que collection publique ou privée) la collection de cartes qu'on note, un message supplémentaire s'affichera pour alerter l'utilisateur de ne noter la collection qu'après l'avoir suffisamment testée
+ Lors du processus de notation, il est demandé à l'utilisateur de répondre aux questions suivantes:
  - "Les informations sur les cartes ne contiennent pas d'erreur"
  - "Les cartes sont réalisées de manière lisible et agréable"
  - "Les cartes de cette collection sont efficaces et m'ont permis de progresser dans le domaine souhaité"
+ Les 3 questions précédentes peuvent chacune être répondu par 
  - ☆☆☆☆☆ Absolument pas d'accord
  - ★☆☆☆☆ Pas d'accord
  - ★★☆☆☆ Plutôt pas d'accord
  - ★★★☆☆ Plutôt d'accord
  - ★★★★☆ D'accord
  - ★★★★★ Complètement d'accord
+ Ensuite une moyenne des 3 notes est réalisée pour déterminer la note sur 5 des cet utilisateur, les notes de tous les utilisateurs sont réunies pour déterminer la note globale de la collection

##### 2.4.5 Les rangs

##### Les niveaux de difficultés
+ Le **niveau de difficulté** est un indicateur explicite du **taux de réussite** d'une carte, il sert à classer les cartes selon 3 niveaux de difficulté (sujet à rééquilibrage):
  - **facile**: de 100% à 75% de taux de réussite (100% >= x >= 75%)
  - **moyen**: en dessous de 75% jusqu'à 25% non inclus de taux de réussite (75% > x > 25%)
  - **difficile**: de 0% à 25% de taux de réussite (25% >= x >= 0%) 
+ Toutes les cartes commencent avec un niveau de difficulté **moyen** par défaut
+ Dès qu'on s'auto-évalue pour la deuxième fois sur une carte, le niveau de difficulté est alors ré-établi en fonction du taux de réussite, puis le niveau de difficulté est ensuite recalculé à chaque auto-évaluation:
  - en effet si on a qu'un seul passage sur une carte, il n'y aurait donc que deux possibilités de taux de réussite (0% ou 100%), tandis qu'au bout de deux passage on aurrait alors 3 possibilités (0%, 50%, 100%), permettant alors d'établir un niveau de difficulté
+ Le niveau de difficulté d'une carte est bien entendu de plus en plus pertinent à mesure que l'utilisateur pratique (une carte faite 20 fois avec seulement 30% de taux de réussite, est clairement une carte difficile en revanche une carte faite uniquement 3 fois avec un taux de réussite de 33%, cela signifie simplement qu'on l'a réussi une fois et échoué deux fois, mais elle n'a pas été faite beaucoup de fois, donc peut etre que seulement deux essais de plus porterait son score à 80%) 
+ Si on fait une session de cartes de difficultés variées, c'est à dire quand on ne fait pas une session de carte basée sur une difficulté particulière, alors le niveau de diffculté doit s'afficher sur la carte

#####  La difficulté estimée des collections
La difficulté estimée d'une collection est fixée par son **créateur**/**auteur principal**, il s'agit d'une valeur arbitraire, il doit être précisé sur le site, que ce niveau de difficulté peut ne pas être représentatif de la difficulté réelle pour chaque personne
##### Les éléments de flashcards
+ Une flashcard peut avoir différents **éléments** sur son recto et son verso (elle n'est pas limitée à un élément de chaque côté), ces éléments peuvent être de différents **types**:
  - Mot
  - Chaîne de caractères
  - Caractère (exemple caractère arabe, chinois, russe)
  - Image (Dessin/Photo/...)
  - QCM
+ Ces différents types doivent pouvoir permettre de créer de nombreuses combinaisons d'éléments sur les flashcards, exemple:
  - ``Mot <=> Description/image``
  - ``Image <=> Description``
  - ``Concept <=> Schéma`` (**advanced**:réalisable directment sur l'appli ?)
  - ``QCM <=> Réponse`` (pas vraiment d'intéret à laisser l'utilisateur choisir le sens d'apprentissage)
  - ``Caractère/Mot <=> Traduction + Prononciation``
+ A la création de cartes on peut donc choisir plusieurs éléments de chaque côté 
+ Quand on crée une collection on choisit au début le **format** des cartes, soit:
  - Avec des **formats** préfaits proposés par l'application: (ex: ``Caractère/Mot <=> Traduction + Prononciation``)
  - En créant soi même son **format** pour cette **collection**
  - On peut aussi créer des collections avec des **formats** différents mélangées au sein d'une même collection (ex: une partie ``formule <=> explication`` et une partie ``schéma <=> procédé``), dans ce cas on ne pourra pas choisir les éléments affichables lors d'une session , on aura simplement le choix d'affciher le **recto** ou le **verso**
+ Quand on enregistre la collection elle retient:
  - Une version par défaut (``Recto:Caractère/Mot <=> Verso:Traduction + Prononciation``): ce sera utilisé:
    - Quand on lance une session avec cette collection sans changer les paramètres
    - Quand on lance une partie (ou l'ensemble) de ces cartes mélangées à des cartes non compatibles (ex:``Recto:Grammaire <=> Verso:Explication``), dans ce cas on ne pourra pas choisir quelles éléments on affiche sur quel côté, mais on aura tous les **recto** en question et les **verso** en réponse, ce qui permet de mélanger des cartes variées
  - L'ensemble des éléments sans emplacement particulier (``Caractère/Mot; Traduction; Prononciation``), ce qui permettra de sélectionner quels éléments on veut au **recto** et lesquels au **verso** tant qu'on utilise que des cartes du même **format**

##### Fonctionnement de la création de cartes

##### Les statistiques
- Taux de réussite de la carte

##### Les succès
+ Peuvent être affichés sur notre profil ``??``
Idées de succès:
- Créer 1, 5, 10, 25, 50, 100, 1000 cartes
- Lire 1, 5, 10, 25, 50, 100, 1000, 5000, 100 000 cartes
- Maitriser 1, 5, 10, 25, 50, 100, 1000, 5000, 100 000 cartes (les cartes ont atteint le rang max)
- Partager 1, 5, 10, 25, 50, 100, 1000 cartes

##### La progression de l'utilisateur
La progression de l'utilisateur sera indiqué par des graphiques basées sur les statistiques des cartes (rang de la carte, taux de réussite)

##### Fonctionnement général d'une session d'apprentissage
+ L'utilisateur lance une session, des paramètres de base lui sont proposés:
  - basés sur les paramètres de base de l'application si c'est la première fois
  - ou basés sur ses précédents paramètres s'il en a
+ Il peux choisir de changer le type de cartes qui est proposé:
  - **générique** (DEFAUT): toutes les cartes qu'il a en stock, ne permet pas de choisir l'affichage 
  - une **collection**
  - une **catégorie** ou **sous-catégorie**
  - toutes les cartes d'un **rang**
+ L'utilisateur valide lui même sa réponse, c'est à lui d'estimer si sa réponse est correct ou non, ce choix est fait par rapport à une validation par l'application, pour:
  - Eviter à l'utilisateur d'avoir à taper chacune de ses réponses, ce qui lui ferait perdre du temps et créerait de la frustration, ainsi il a juste à choisir la validité de ses réponses
  - Eviter les frustrations liées à une réponse que l'appli juge invalide, mais que l'utilisateur considère comme assez maitrisée pour être considérée correcte
  - Suite à l'abandon de l'idée de compétition entre les utilisateurs (avec un tableau de score), cette validation par l'application n'est en réalité plus nécessaire
+ Il est possible de planifier des sessions d'apprentissage (exemple tous les mercredis à 13h avoir une notif de rappel pour une séance de cartes)

##### Paramètres de session

##### Paramètre généraux
+ Dans les options il faut pouvoir:
  - customiser l'aspect visuel des cartes:
    - couleurs d'arrière plan,
    - Taille de police,
    - couleur du texte,
    - disposition des éléments de réponses

##### Signalement et réclamation
Créer un système de réclamation et de signalement:
+ si on s'aperçoit que des cartes ont un problème:
  - infos erronées, 
  - insultantes, 
  - pas dans la bonne catégorie
+ on peut alors:
  - en premier lieu contacter l'auteur de la carte s'il est toujours présent sur le site, pour signaler l'erreur
  - si ce n'est plus possible on peut alors les signaler, les cartes signalées seront traités par les modérateurs
  - Si les modérateurs estiment que le signalement est en partie valide, mais qu'il n'est pas du ressort du site de juger, alors la carte sera conservée, mais un avertissement sera ajouté (par exemple une affirmation scientifique controversée si elle est signalée, devra avoir un avertissement prévenant de la controverse)

#### Le cheminement de l'utilisateur

##### Les comptes, rôles et autorisations
+ Si un utilisateur n'est pas connecté (**anonyme**) il peut:
  - Créer un compte
  - Observer les collections publiques
  - Tester les collections publiques, mais sa progression ne sera pas sauvegardée, donc il n'aura pas accès au rangs, difficultés,... Il pourra simplement tester ses connaissances sans évaluation
+ Les **utilisateurs** peuvent:
+ Les **modérateurs** peuvent:
  - Avoir les mêmes droits que les utilisateurs
  - S'occuper des cartes signalées par la communauté et juger de la probllématique qu'elles causent (la carte mérite-t-elle son signalement ?)
  - Il faudra mettre en place une charte de ce qui est accepté ou non sur le site, de façon à ce que les modérateurs puissent juger en ayant connaissance du règlement
  - Chaque décision de modérateur sera vérifiée par deux autres modérateurs afin de limiter les décisions injustes
+ L'**administrateur** peut:


#### Options avancées de l'application
Certaines options ne verront le jour qu'après qu'une version déjà pleinement fonctionnelle de l'application soit en état, c'est le cas de:
+ La possibilité de dessiner directement dans l'application pour la création des cartes, ce qui permettrait de réaliser soi même ses propres schémas, dessins, lettres,...; au lieu de les importer directement en format d'images
+ La possibilité de faire des dessins libres pendant les sessions d'apprentissage, ce afin de pouvoir par exemple, écrire des mots dans n'importe quel alphabet et testé notre connaissance de cette écriture, vérifier qu'on est capable de reproduire un schéma un peu complexe (car simplement essayer de le visualiser peut être trop compliqué pour des schémas trop complexes ou des alphabets difficiles):
  - Ces dessins pourraient être réalisées directement sur la carte, une zone de dessin s'afficherait en transparence par dessus, et on pourrait alors dessiner tout ce qu'on souhaite, à l'aide d'un outil type *canvas* comme sur *Skrible*
+ l'ajout de fichiers audio (ex: mot de langue étrangère), afin de créer des cartes de type ``audio <=> prononciation phonétique/description/traduction`` (ex: d'un coté un mot audio, de l'autre sa version écrite, afin de travailler sa prononciation)


#### 2.5 UI et charte graphique
+ Réaliser un wireframe afin de déterminer la forme général du site en mobile puis en desktop, et définir les cheminements de l'utilisateur
+ Définir la charte graphique et l'identité du site:
  - Les couleurs: ``??``
  - Nom du site: ``??``
  - Slogan : ``??`` 
  - Le logo: Deux cartes se chevauchant, à leur jonction un changement de couleur symbolise en double sens la séparation entre les cartes ou un éclair
  - Les formes: ``??``
+ Réaliser la maquette
+ Pour les niveaux de difficultés: Quel logo ? Les étoiles étant déjà prises par les notes, des crânes ? Symbolique peut être trop jeu vidéo``??``

### 3. Propositions de tests

### Fonctionnement de la BDD

faire des schémas

### Technologies et outils utilisées
- ***Figma*** pour le wireframe, et la maquette
- ***Gimp*** et ***Inkscape*** pour le logo et la retouche d'images
- ***Docker*** pour la conteneurisation
- ***i18n*** pour l'internationalisation
- Front: ***Vue.js***
- Back: 
  - ***Express.js*** pour le routing
  - ***Sequelize*** pour l'Object Relational Mapper (ORM)
  - ``??`` pour la base de donnée

### Les idées abandonnées et explications de leur abandon
#### Les familles
```markdown
Les familles d'apprentissage correspondent à la taxonomie la plus élevée du site
+ Il s'agit des grandes familles de connaissances qu'il peut y avoir
+ Elle sont créées au lancement du site
+ Elle ne peuvent pas être crées par la communauté
+ Des familles pourronts être rajoutées en fonction des retours
+ Une carte ne peut appartenir qu'à une seule famille
+ Les familles sont:
  - Culture générale
  - Histoire & Géographie
  - Langues
  - Sciences
  - Politique, Justice & Economie
  - Santé & Sport
  - Arts & Cultures
```
Les familles de cartes sont abandonnées, car:
- leur rôle est trop proche de celui des catégories
- Cela faisait donc un élément en plus en BDD qui n'était pas spécialement pertinent
- Elles étaient supposées être limitées et assez génériques pour être mutuellement exclusives (une carte n'aurait pu faire partie que d'une seule famille), ce qui oblige à faire des choix pour les noms des familles, ce qui aurait pu causer:
  - Des oublis de familles qui auraient pu être importantes
  - Des groupements arbitraires d'éléments au sein de familles (voir des opinions controversées)


#### La compétition entre utilisateurs
L'idée de compétition entre utilisateurs est abandonnée pour:
- Eviter à l'utilisateur d'avoir rentrer une réponse manuellement (ce qui augmenterait inutilement le temps passé sur l'application, et les manipulations), il vaut mieux que l'utilisateur puisse penser mentallement ses réponses, donc l'application ne peut pas les controller, or une compétition basée sur l'honnêteté des réponses des utilisateurs, ne semblent pas pertinente (#euphémisme)
- L'objectif des flash cards est d'apprendre, pour son propre intérêt donc, et ajouter une compétition artificielle ne ferait que créer de la jalousie, de la frustration ou un sentiment d'infériorité vis à vis des personnes à haut score, enlevant ainsi une partie du côté ludique des flashcards
- Les succès personnels sont une meilleure façon d'inciter l'utilisateur à se dépasser lui même sans se comparer aux autres
- Certes *Brainscape* utilise un système de compétition intéressant et plutôt bien trouvé, puisqu'ils comparent le nombre de cartes étudiées et non pas le taux de réussite, mais une véritable absence de compétition me semble plus adaptée à mon projet, puisque l'objectif est d'avoir une grande diversité dans les types de flashcards, et donc une compétition n'aurait pas de sens, puisque tout le monde pourrait potentiellement avoir des cartes très différentes.

#### Les possibilités de swiper pour valider ou non
```markdown
- tap affiche une card
- swipe haut : affiche le menu de la carte ?
- swipe bas si ne sait pas, tap again affiche la reponse,
- swipe left false,
- swipe right true
- menu sur la gauche en desktop
- Pour des raisons d'accessibilité attention avec les swaps, ils doivent pouvoir etre utilisé par un controle à la voix ? si ça marche comme ça ? à voir
``` 
Les options de swipe qui étaient prévues au début du projet, bien qu'intéressantes visuellement sont abandonnées car:
+ C'est visuel justement, et donc pose des problème d'accessibilité, les lecteurs d'écran sont apparemment capables de prendre en compte les actions correspondant à des *swipes* sur la droite ou la gauche, mais le projet nécessitait de modifier ces actions (donc risque d'interférence avec un comportement natif)
+ Il s'agit d'éléments compliqués à implémenter, or ils devront du coup être désactivés ou doublés d'une option plus classique de type clic sur un bouton, il est donc peu intéressant d'investir autant de temps dans des actions qui ne seront valide que dans certains cas, en effet il faudrait les désactiver pour: 
  - Le mode desktop (ou le remplacer par l'utilisation des flches du clavier)
  - Pour l'accessibilité (ou en tout cas doubler d'une autre option)
  - De plus certaines personnes même si elles n'utilisent pas les lecteurs d'écran pourrait avoir des difficultés à comprendre si le fonctionnment n'est pas *classique* (comme un bouton)
  - Il faudrait que j'ajoute exprès des éléments tutoriels pour expliquer ou il faut swiper pour telle ou telle action, alors qu'il serait plus simple d'avoir des boutons, clairs et explicites qui ne nécessite pas de double explications
+ Ainsi on gagne en uniformité sur le projet

## Archives des idées du brainstorming
~~appli flash card + culture generale~~
~~Actions (version mobile):~~

- ~~tap affiche une card~~
- ~~swipe haut : affiche le menu de la carte ?~~
- ~~swipe bas si ne sait pas, tap again affiche la reponse,~~
- ~~swipe left false,~~
- ~~swipe right true~~
- ~~menu sur la gauche en desktop~~
- ~~Pour des raisons d'accessibilité attention avec les swaps, ils doivent pouvoir etre utilisé par un controle à la voix ? si ça marche comme ça ? à voir~~

- ~~utiliser ses propres flashcard et déterminer soi même si on a bon ou pas,~~
- ~~ou utiliser des flashcards prefaites et devoir taper la réponse (validation avec des mots clés), ou qcm,~~
  - ~~permettrait de faire des classements d'utiliser des flashcards faites par la communauté~~
  - ~~idée de classement ou de carte avec validation automatique des réponses abandonnée -> cela inciterais à penser un système de validation des cartes, alors qu'il est plus intellignet et rapide de laisser l'utilisateur valider lui meme la carte,, pour l'utilisateur cela lui permet de juste swiper sans avoir a taper de reponses, ce qui est mieux quand il est sur son mobile (cas principal d'utilisation, et qu'il n'a pas beaucoup de temps-> il est dans le bus par exmple, ou entre deux rendez-vous,...), en ce qui concerne d'éventuels compétitions (qui nécessiterais forcément de valider les reponses par l'appli, pour que tout le mond esoit a égalité et que personnne ne puisse tricher,) cela poserait problème dans le sens ou cela casse une parti de l'objectif des flashcards, qui sont normalement des outils pour apprendre , personnelement et chacun à son rythme, créer des concours semble etre typiquement une mauvaise idée créant inutilement un esprit de compétition qui n'a pas lieu d'etre, brainscape utilise un système de compétition intéressant, puisqu'ils mettent en compétition le nombre de cartes jouées et non le taux de réussite, ce qui incite les gens à tenter de faire plsu de cartes, sans se mettre la pressionen se disant qu'ils sont moins bon que les autres -> idée de compétition à éviter qaund même: l'objectif est vraiment d'avoir une app utilisable pour n'importe quel type de flashcard , et donc laisser un maximum d'amplitude à l'utilisateur, s'il est en effet moins efficace de faire des applis trop génériques, et qu'il vaut généralemnent mieux se concentrer sur un type en particulier, ici le but est d'avoir justement une app qui fonctionne dans la grande majorité des cas, de façon à ce qu'un utilisateur qui souhaite créer des cartes différentes dans le style (du genre langages, etcartes géographiques), puisse le faire sans avoir besoin de deux applis différentes. L'outil doit donc etre suffisamment maléable pour laissser les utilisateurs créer des cartes de styles très différents (un peu comme pour des mods pour un jeu vidéo où les devs créent un outil de base solide, et les moddeurs peuvent alors créer toute sorte de mods très différents en focntion de ce qu'ils veulent)-> _mdr gé pa lu_~~

* ~~possibilité d'utiliser les cartes de la communauté sans compte, si on veut créer, ou avoir des stats il faut un compte, sans compte on peut juste tester des cartes de manière random sans que l'appli ne retienne nos scores~~

* ~~types de flashcards:~~

  - ~~Mot <-> description/image~~
  - ~~image <-> description~~
  - ~~concept <-> schéma (**advanced**:réalisable directment sur l'appli ?)~~
  - ~~QCM -> réponse (pas vraiment d'intéret à laisser l'utilisateur choisir le sens d'apprentissage)~~
  - ~~**advanced**: audio (ex: mot de langue étrangère) <-> prononciation phonétique/description/traduction (ex: d'un coté un mot audio, de l'autre sa version écrite, afin de travailler sa prononciation)~~

* ~~Ajouter une option de dessin ?  permettrait à ceux qui apprennent des langues dans un autre alphabet que le leur de répondre en dessinant le caractère puis de comparer leur dessin avec la réponse, leur évitant d'avoir une feuille à coté, (pratique quand on est dns le bus)-> pourrait etre une option avancé, puisque ce système serait légèrement différent, en effet dans tous les autres cas la réponse de l'utilisateur a juste besoin d'etre dans sa tête, là il y aurait un dessin , donc pour la réponse il faut prévoir un espace pour la réponse et un espace pour le dessin/ecriture de l'utilisateur (mais faisable avec des outils de canvas comme celui utilisé sur skribbl par exemple), s'il y a option de dessin il faudrait que ça désactive le swipe des cartes ?~~
- ~~l'espace de dessin peut etre sur la carte en entier (un peu à la façon des flashcards pleco)~~

* ~~Pour la création des flashcards on pourrait avoir des templates en fonction du type de flashcard ou de la famille de flash cards (exemple les cartes de langues pourraient avoir mot <-> définition/prononciation )~~

* ~~on peut créer des catégories de cartes (ex: mandarin, formules mathématiques,..)~~

* ~~En plus des cartes qu'on peut créer pour la communauté on peut créer des decks/collections de cartes, qui pourront aussi etre notés par la communauté ou triés par popularité, ainsi si on ne veut pas créer soit meme une collection de cartes culture générale, on peut prendre une collection, les collections pourraient etre nommés et contenr des sous collections, permettant ainsi d'avoir des séries (par exemple collection: `apprendre l'arabe`, sous collection `1.1 - Les bases`, `1.2 - L'écriture`, ...), les collections doivent de base avoir le meme genre de cartes (puisqu'il s'agit des groupes utilisables pour une session d'apprentissage) autrement on ne pourrait pas choisir quoi montrer si par exemple on a une carte qui a ``prononciation+signification <=> caractère`` et une autre ``signification <=> règle de grammaire``, on ne pourrait alors pas choisir dans les paramètres ce qui est affiché sur les cartes, si on souhaite faire des collections génériques (qui peuvent donc cumuler toutes les cartes qu'on veut, c'est possible mais il faut alors garder l'affichage par défaut de la carte, on ne peut alors choiir que d'affciher le recto ou le verso lors de la session et pas les options qu'on met dessus)~~

* ~~Pour les collections, indiquer la progression par des graphs (rang de la carte, taux de réussite)~~

* ~~Quand on crée une carte on peut choisir de mettre plusieurs éléments sur un seul coté, (exemple prononciation + caractère), et il faut choisir quels éléments sont choisis par défaut (tous ceux ajoutés ?, seulement une partie)~~

* ~~Dans les options il faut pouvoir customiser l'aspect visuel des cartes (couleurs de font, police, couleur du texte, disposition des éléments de réponses)~~

* ~~Créer un système de réclamation et de signalement, si on s'aperçoit que des cartes ont un problème (infos erronées, insultantes, pas dans la bonne catégorie, du genre astrologie dans la famille science lol, (ou géologie), on peut en premier lieu contacter l'auteur de la carte s'il est toujoours présent sur le site, pour signaler l'erreur; si ce n'est plus possible on peut les signaler, les cartes signalées pourraient:~~
  - ~~etre gérées directement par la communauté (lorsqu'une carte est signalée, la communauté peut voter pour déterminer si la carte pose en effet problème ou non, on peut alors choisir d'exclure totalemnt la carte, ou d'y ajouter un avertissement) -> problème, s'il n'y a pas assez d'utilisaeur, soit le système est inutilisable soit il est dangereux (avec des signalements rendus possibles par une minorité capable de nuire au système, exemple virer des cartes juste pour le fun; si beaucoup de personnes, rien n'empêche techniquement un raid organisé (peu probable, mais à prendre en compte tout de même)~~
  - ~~etre gérée par des modérateurs -> problèmes: nécessite une équipe, fiabilité de l'équipe ?~~

* ~~Créer un systèm de notes, on peut noter les cartes de la communauté :soit note globale sur 10 points/5 demi étoiles, soit notes divisées: justesse de la carte (l'info est elle vraie ?), efficacité de la carte (est elle bien rédigé, pas d'infos superflu, on peut la lire rapidement), on pourrait aussi utiliser la popularité des cartes (combien d'utilisateurs les utilisent dans leur "deck", ou combien de fois elles ont été utilisés dans des sessions d'apprentissage)~~

* ~~Les familles de cartes sont au dessus des catégories et sous catégories, elles sont définies par le site et sont les grands groupes d'apprentissage: langue, géographie, histoire, culture générale,...~~

* ~~Faire un systme de succès pour encourager les gens à apprendre des cartes~~

- ~~Idées logo:~~
  - ~~Cartes stylisées, logo double sens flash (la forme des cartes peut éoquer à la fois des cartes ou un éclair)~~

~~utiliser un linter ?~~

~~express.js pour node en mode web~~
~~sequelize pour l'ORM~~

~~stimulus si on fait avec laravel~~
~~vue/react -> pas obligatirmenet de bdd~~

~~pour le projet vue en front ? , node en back ? voir Strapi ?~~

~~export -> electron (desktop)/capacitor (mobile)~~

~~faire une todo en test pour tester vue front~~

~~docker:~~
1. ~~outiller le projet : bdd avec docker par exemple~~
2. ~~utiliser docker compose meme sur un projet unique~~
3. ~~mariaDB adminer~~
~~En dernier tenter carrément de run le projet sur docker~~

* ~~Possibilité de planifier des sessions d'apprentissage (exemple tous les mercredis à 13h avoir une notif de rappel pour une séance de cartes)~~

* ~~niveaux de difficultés:~~
  - ~~facile~~
  - ~~moyen~~
  - ~~difficile~~
  - ~~custom (non disponible pour les cartes qu'on crée pour la communauté, ou alors il faudrait ajouter en plus du nom de la difficulté une estimation de la position de cette difficulté par rapport aux autres)~~
  - ~~Il pourrait etre déterminé: soit par l'auteur, soit automatiquement en fonction de notre taux de réussite par rapport au nombre d'essai (exempple une carte qu'on a faite 20 fois avec seulement 30% de taux de réussite, est clairement une carte difficile en revanche une carte faite uniquement 3 fois, si elle a un taux de réussite de 33%, cela signifie simplement qu'on l'a réussi une fois et échoué deux fois, mais elle n'a pas été faite beaucoup de fois, donc peut etre que seulement deux essais de plus porterait son score à 80% dans ce cas la le taux de réussite seul , n'est pas un bon indicateur de la difficulté, à voir donc comment prendre en compte les deux éléments)~~