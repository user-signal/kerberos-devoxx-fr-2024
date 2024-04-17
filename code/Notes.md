### Pitch moi

Je m'appelle Frédéric Cabestre, je suis développeur indépendant basé à Toulouse, mais de nos jours cela importe
beaucoup moins. Je suis un « artisan du logiciel » issu il y a très longtemps du monde académique. J'y ai développé
un goût prononcé pour les langages de programmation, leur mise en œuvre et les systèmes distribués.

Mon client principal aujourd'hui c'est **Bravas**...

### Pitch Bravas

**Bravas**, techniquement c'est une combinaison d'un `MDM`, d'un `IDP` et d'une `PKI`.
Fonctionnellement **Bravas** aide les entreprises à gérer et sécuriser leur parc informatique matériel et logiciel.
Cela permet des on/off-boardings automatisés, le maintien en conditions opérationnelles des appareils et
de la connexion sans mots de passe aux services en ligne.

Dans ce contexte, c'est d'avoir beaucoup travaillé sur `SAML` qui ma donné envie de parler de son ancêtre, `Kerberos`,
que j'avais pas mal manipulé autour de 2010.

### Mythologie

**Cerbère** est la créature qui garde l'entrée du royaume d'**Hades** et **Perséphone**. Selon les auteurs, il a pu
être décrit de manières très diverses. Même si la représentation qui demeure aujourd'hui dans notre inconscient
collectif, peut-être à cause d'Harry Potter, c'est celle d'un chien à trois têtes.

Est son rôle de gardien consiste à **authentifier** celles et ceux qui souhaitent entrer ou sortir de ce
royaume. Seuls les défunts peuvent y entrer et en aucun cas en ressortir. On connait au moins deux personnes
de renom qui on réussit à **hacker** Cerbère:

* **Orphée** pour aller chercher sa chère **Eurydice** qui l'a endormi par sa divine musique
* **Hercule** qui dans le cadre de ses 12 travaux la « Brute forcé »

### Contexte

La naissance de **Kerberos**, le protocole, s'articule autour de 1990. C'est une période de transition. On passe
de terminaux assez idiots dédiés à l'affichage (`VT100`) connectés par des lignes séries à des calculateurs centraux
(`PDP11/20`). Une telle connexion aujourd'hui équivaut à ouvrir un quelconque `xterm`, `iterm`, `alacritty`,
`kitty`...

Et on se dirige vers un monde où des stations de travail, munies d'une capacité de calcul autonome et des serveurs
sont connectés par un réseau comme `Ethernet` (ici le célèbre connecteur en T de l'Ethernet fin).

En cryptographie, on connait depuis bien longtemps le chiffrement à clef partagée (**César**?) ou symétrique.
`DES` dérivé de `Lucifer` est un standard `FIPS` (Federal Information Procession Standard) depuis 1977. D'ailleurs
soumis à cette période à des limitations d'exportation pour raison stratégique.

L'idée d'un système de chiffrement asymétrique commence à poindre le nez, et sa faisabilité concrète est mise en
avant dans ce papier de 1978 (`RSA`) et breveté par le `MIT` en 1983.

`HTTP` n'éxiste pas encore, ou sous forme embryonnaire dans un labo au `CERN`. Et `SSL`n'existe pas non plus (ne
parlons même pas de son dérivé actuel `TLS`)

Par acquit de conscience je vous fais rappel ultra bref de ce que sont chiffrements symétrique et asymétrique,
et de leurs propriétés caractéristiques. [...]

### Problème

L'**authentification** c'est... roulement de tambour...
C'est basé sur quelque chose que l'on est le seul à posséder, que ce soit un mot de passe dans sa tête, un
jeton de sécurité dans ça poche ou une empreinte rétinienne au fon de son œil. Enfin, seul à posséder mais
que ce qui doit réaliser l'authentification doit pouvoir vérifier et nécessite parfois un partage.

Dans ce nouveau monde client serveur vers lequel on bascule dans les années 1990, l'astuce immédiate est
d'utiliser un système à mot de passe, finalement comme au bon vieux temps des terminaux série. Mais maintenant
les occasions nécessitant de s'authentifier se multiplient avec le nombre de machines auxquelles on veut se
connecter. Le réseau n'est absolument pas chiffré et les oreilles indiscrètes ont plus de facilité sur éthernet
(medium sur lequel on diffuse les messages à tout le monde, le destinataire reconnait les siens). Chaque serveur
doit donc gérer l'authentification **et** les identités individuellement. Je passe sous silence la partie
annuaire d'identité qui est en soit un vaste problème.

### Needham-Schroeder

L'inspiration initiale va venir du célèbre **PARC** (Palo Alto Research Center), voir la présentation de ???
durant cette édition de **Devoxx**. Needham et Schroeder vont publier un papier en 1978 décrivant un usage
du chiffrement pour l'authentification sur des réseaux.

Dans ce papier, ils utilisent un formalisme pour décrire des protocoles de sécurité qu'ultérieurement on
appellera « narration Alice et Bob ». Je ne vais pas vous plomber aujourd'hui avec cette notation, mais
j'aimerais attirer votre attention sur le fait que de telles notations améliorent la communication et le
raisonnement sur les protocoles (en particulier en sécurité) et ont conduit à des tentatives de preuve
mécanisée de leur correction... C'est quand même mieux qu'un truc fait avec les doigts sur un coin de table !

Mais pour cette présentation, je vais m'appuyer sur des schémas plus amicaux et colorés pour décrire la version
symétrique du protocole de Needham et Shroeder (d'ailleurs je m'excuse auprès des personnes ayant des troubles
de la perception des couleurs, mais il était trop tard pour changer)

`Nonce`: de la nécessité de disposer d'un bon générateur de nombres aléatoires.

Mais avec ça on a résolu qu'une partie du problème : l'authentification est centralisée et uniforme. Mais
pour chaque service, il faut saisir à nouveau son mot de passe.

### Kerberos V5

`Hesiod`: DNS, `Moira`: admin système distribué
`Heimdal`: à cause des restrictions d'exportation de la cryptographie.
`Microsoft`: en remplacement de `NTLM`.

Le système bicéphale (`AS`, `TGS`) est peut-être une des raisons d'avoir choisi le nom de **Kerberos** ?

`Str2key`: source potentielle de problème, comme avec tout système à mot de passe.
`Hrodatage` : contrainte supplémentaire de synchronisation des horloges sur le réseau. Tolérance au décalage. 

### Pré authentification

La description de `Kerberos V5` est entièrement formalisée avec `ASN.1` (qui est par ailleurs aussi utilisé 
dans bon nombre de documents de l'**IETF** surtout autour de la cryptographie). Il s'agit d'une syntaxe 
indépendante de tout langage de programmation pour décrire des structures de données. On peut le comparer
avec des systèmes comme `Protocol buffers`, `Thrift` ou `Avro`.

