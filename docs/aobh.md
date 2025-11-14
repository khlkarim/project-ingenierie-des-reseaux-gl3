# IPv6

## Introduction

**IPv6** (Internet Protocol version 6) est la version la plus récente de IP (Internet Protocol) conçue pour être le successeur de IPv4.

Certaines demandes ont possé la création de IPv6 pour traiter les lacunes de IPv4. Ces améliorations tombent dans les catégories suivantes :

- **Capacités d’adressage étendues :** IPv6 passe de 32 à 128 bits, permettant plus de niveaux hiérarchiques, un nombre plus élevé d’adresses (2^128 contre 2^32) et une autoconfiguration simplifiée. Le routage multicast est amélioré grâce au champ « scope », et les adresses anycast permettent d’envoyer un paquet vers n’importe quel nœud d’un groupe.
- **Simplification de l’entête :** Certains champs IPv4 ont été supprimés ou rendus optionnels, réduisant le coût de traitement et la taille de l’entête IPv6.
- **Meilleur support des extensions et options :** L’encodage des options permet un routage plus efficace, des options plus longues et une flexibilité pour de futures extensions.
- **Étiquetage de flux :** IPv6 peut identifier des séquences de paquets comme un flux unique pour un traitement cohérent dans le réseau.
- **Sécurité et confidentialité :** IPv6 inclut des extensions pour l’authentification, l’intégrité des données et, optionnellement, la confidentialité.

    Ces améliorations sont rendues possibles par la nouvelle structure de l’entête IPv6, qui sera détaillée dans la section suivante.

## Entête IPv6

![Figure 1 : L’entête d’un datagramme IPv6](/assets/images/ipv6-header.png)

Figure 1 : L’entête d’un datagramme IPv6

- **Version :** Champ de 4 bits. Il contient la version de IP utilisée (sa valeur est 0110 pour IPv6)
- **Priorité :** Champ de 8 bits. Il sert à indiquer la priorité et le type de traitement d’un paquet dans le réseau.
- **Etiquette de Flux :** Champ de 20 bits. Il est utilisé par la source pour grouper une séquence de paquets qui doivent être traitées comme un seul flux dans le réseau.
- **Longueur de la Charge Utile :** Champ de 16 bits. Il contient la longueur de la charge utile du datagramme, qui est la partie qui se trouve au dessous de ce champ (extensions + données).
- **Prochaine Entête :** Champ de 8 bits. Il sert a identifier le type de l’entête qui se trouve directement après l’entête IPv6. (Voir …)
- **Hop Limit :** Champ de 8 bits. Il est décrémenté de 1 par chaque nœud qui l’envoie. Si ce champ est déjà à 0 à la reception ou est décrémenté à 0, le paquet est rejeté par le nœud. Le nœud de destination ne rejette pas le paquet si ce champ est égal à 0.
- **Adresse Source :** Champ de 128 bits. Il contient l’adresse de la source.
- **Adresse Destination :** Champ de 128 bits. Il contient l’adresse de la destination.

Après avoir détaillé le format du datagramme IPv6, il est important d’examiner les extensions, qui permettent d’ajouter des fonctionnalités supplémentaires au protocole.

## Extensions en IPv6

En IPv6, les informations optionnelles de la couche Internet sont codées dans des entêtes d’extension, insérées entre l’entête IPv6 et l’entête de la couche supérieure. Il en existe un nombre limité, chacun identifié par une valeur **Prochaine Entête** spécifique.

Lors du traitement d’une séquence de **Prochaine Entête**, le premier qui n’est pas une entête d’extension indique que l’élément suivant est l’entête de la couche supérieure. Une valeur spéciale **No Next Header** est utilisée lorsqu’il n’y a pas d’entête de couche supérieure.

Comme illustré dans cette figure, un paquet IPv6 peut contenir zéro, un ou plusieurs entêtes d’extension identifiés par le champ **Prochaine Entête** de l’entête précédente :

![Figure 2 : Enchainement des entêtes dans IPv6](/assets/images/ipv6-extensions.png)

Figure 2 : Enchainement des entêtes dans IPv6

Au nœud destinataire, le champ **Prochaine Entête** de l’entête IPv6 permet d’invoquer le module traitant la première entête d’extension, ou l’entête de la couche supérieure s’il n’y a pas d’extension. Chaque entête d’extension doit être traitée dans l’ordre, car son contenu détermine si le traitement doit passer à la suivante. Il est interdit de sauter une entête pour en traiter une autre plus loin dans le paquet.

Si un nœud doit passer à l’entête suivante mais rencontre une valeur **Prochaine Entête** inconnue, le paquet doit être supprimé et un message ICMP « Parameter Problem » envoyé à la source, avec le code 1 et le pointeur indiquant l’emplacement de la valeur non reconnue. La même procédure s’applique si une valeur 0 est trouvée dans une entête autre que l’entête IPv6.

Chaque entête d’extension est un multiple de 8 octets pour garantir l’alignement des entêtes suivantes. Les champs multi-octets sont alignés sur leurs bornes naturelles (1, 2, 4 ou 8 octets).

Une implémentation complète d’IPv6 contient les entêtes d’extension suivantes :

![Figure 3 : Ordre des extensions en IPv6](/assets/images/ipv6-ext-order.png)

Figure 3 : Ordre des extensions en IPv6

Dans ce rapport, on s’intéressera à l’extension **Fragmentation**.

## Fragmentation en IPv6