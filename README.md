# TP-B---Bienvenue-internet PEDRERO/LOURS


## 1.5 Questions intermédiaires

*RFC = Request for Comments désigne un document numéroté où sont traités, décrits et définis des protocoles, concepts, méthodes et programmes Internet.*
--------------------------------------------------------------------------------------------------------------------------------------------------------

1. La ligne `GET / HTTP/1.1` contient trois éléments : la méthode HTTP (GET) qui indique ce qu’on veut faire, le chemin (/) qui est la ressource qu’on demande, et la version du protocole (HTTP/1.1) qui précise comment la communication doit se faire

2. Il faut appuyer deux fois sur Entrée parce que la première ligne vide marque la fin des entêtes dans une requête HTTP, sans cette ligne le serveur ne sait pas que la requête est terminée

3. Si on oublie la ligne vide le serveur ne répond pas ou alors il reste bloqué en attente, car il ne sait pas que la requête est finie

4. Le code 200 OK signifie que la requête a réussi et que le serveur renvoie bien une ressource, un code 404 veut dire que la ressource n’existe pas, un 301 c’est une redirection permanente vers une autre URL

5. La toute première ligne envoyée par le serveur est la ligne de statut, elle contient la version du protocole (par ex HTTP/1.1), le code de réponse (comme 200) et un message (comme OK)

6. Les entêtes présents dans la réponse comme Content-Type ou Content-Length servent à décrire le type de contenu renvoyé (texte, HTML, etc.) et la taille en octets du corps de la réponse, d’autres entêtes comme Connection ou Server donnent aussi des infos utiles au client

7. La première ligne non entête du corps est juste après la ligne vide qui sépare les entêtes du contenu, on la reconnaît parce qu’elle vient juste après cette ligne blanche

8. Si je tape une URL invalide comme `GET /truc HTTP/1.1` le serveur renvoie souvent un code 404 pour dire que la page n’existe pas

9. Oui même dans ce cas le contenu retourné est souvent du HTML, c’est une page d’erreur générée par le serveur qui explique que la ressource est introuvable

-------------------------------------------------------------
-------------------------------------------------------------

## 2.1 Questions – Serveur minimal "Hello World"

1. Oui le client reçoit bien une réponse, dans le navigateur on voit "Hello World!" et dans telnet ou curl aussi

2. Le message est composé d’une ligne de statut (`HTTP/1.1 200 OK`), d’entêtes (`Content-Type`, `Content-Length`, `Connection`), d’une ligne vide et enfin du corps de la réponse avec le texte "Hello World!"

3. Si je change la valeur de `Content-Length`, soit le message est tronqué si la valeur est trop petite, soit il y a des caractères en trop ou des bugs d’affichage si la valeur est trop grande

4. Si j’enlève complètement `Content-Length`, certains clients comme curl ou telnet peuvent quand même afficher le contenu mais d’autres comme le navigateur peuvent bloquer ou ne rien afficher du tout

5. Si je supprime la ligne vide entre les entêtes et le corps, le client ne comprend pas où commence le corps, donc souvent il n’affiche rien ou affiche une erreur

6. Le message s’affiche bien dans telnet et curl mais le navigateur est plus strict donc il peut refuser d’afficher si le format n’est pas respecté à la lettre, ça dépend des clients

---

## 2.2 Questions – Serveur avec analyse du chemin

1. La ligne de requête reçue est du type `GET /motd HTTP/1.1`, il faut extraire trois éléments : méthode, chemin, version

2. Si la ligne est vide ou mal formée ça peut générer une erreur, il faut tester qu’elle contient bien trois morceaux pour éviter un `ValueError`

3. La variable `chemin` contient ce que le client tape dans l’URL, comme `/motd` ou `/date`, elle commence toujours par un slash

4. Si la méthode n’est pas `GET`, le serveur n’est pas préparé à gérer donc il peut planter ou ne rien faire, faut soit l’ignorer soit renvoyer une erreur

5. Si le chemin n’est pas reconnu comme `/truc`, le serveur renvoie "404 Not Found", c’est lisible mais pas très joli donc on peut améliorer

6. Le message 404 est correct mais je peux ajouter un texte plus sympa genre "Désolé cette page n'existe pas" pour que ce soit plus clair

7. Les chemins `/motd`, `/motd/` et `/motd?x=42` sont différents, il faut les normaliser si je veux les traiter comme équivalents

8. Pour ajouter un nouveau chemin comme `/bonjour`, je dois ajouter une condition dans le `if` ou `elif`, c’est simple mais si j’en ajoute beaucoup ça devient vite brouillon

9. Si quelqu’un tape une URL comme `/../../etc/passwd`, ça peut poser un problème si je lis les fichiers du système, faut bien vérifier les chemins pour pas sortir de mon dossier serveur

10. Pour l’instant je traite le chemin comme une simple chaîne, mais pour éviter les attaques faut filtrer ce que l’utilisateur peut demander et bloquer les caractères suspects comme `..` ou `%2e`



