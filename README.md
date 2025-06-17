# TP-B---Bienvenue-internet


## 1.5 Questions intermédiaires

*RFC = Request for Comments désigne un document numéroté où sont traités, décrits et définis des protocoles, concepts, méthodes et programmes Internet.*

1. La ligne `GET / HTTP/1.1` contient trois éléments : la méthode HTTP (GET) qui indique ce qu’on veut faire, le chemin (/) qui est la ressource qu’on demande, et la version du protocole (HTTP/1.1) qui précise comment la communication doit se faire

2. Il faut appuyer deux fois sur Entrée parce que la première ligne vide marque la fin des entêtes dans une requête HTTP, sans cette ligne le serveur ne sait pas que la requête est terminée

3. Si on oublie la ligne vide le serveur ne répond pas ou alors il reste bloqué en attente, car il ne sait pas que la requête est finie

4. Le code 200 OK signifie que la requête a réussi et que le serveur renvoie bien une ressource, un code 404 veut dire que la ressource n’existe pas, un 301 c’est une redirection permanente vers une autre URL

5. La toute première ligne envoyée par le serveur est la ligne de statut, elle contient la version du protocole (par ex HTTP/1.1), le code de réponse (comme 200) et un message (comme OK)

6. Les entêtes présents dans la réponse comme Content-Type ou Content-Length servent à décrire le type de contenu renvoyé (texte, HTML, etc.) et la taille en octets du corps de la réponse, d’autres entêtes comme Connection ou Server donnent aussi des infos utiles au client

7. La première ligne non entête du corps est juste après la ligne vide qui sépare les entêtes du contenu, on la reconnaît parce qu’elle vient juste après cette ligne blanche

8. Si je tape une URL invalide comme `GET /truc HTTP/1.1` le serveur renvoie souvent un code 404 pour dire que la page n’existe pas

9. Oui même dans ce cas le contenu retourné est souvent du HTML, c’est une page d’erreur générée par le serveur qui explique que la ressource est introuvable
