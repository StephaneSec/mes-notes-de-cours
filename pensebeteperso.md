
### Connexion sftp :

* `sftp 95006464@gw.info.unicaen.fr`
* on télécharge via `get nomDuFichier` (la destination se fait sur le répertoire courant).


### Connexion ssh sur une machine de la fac :

* `ssh 	95006464@gw.info.unicaen.fr`
* `ssh 95006464@n304l-417002` par exemple pour la machine n304l de la 417.

### Lancement de mongo

* Connexion ssh sur une machine
* aller sur le répertoire contenant le projet
* npm start

### Faire une requête

* lancer mongo dans un terminal
* connexion ssh sur la même machine dans un autre terminal.
* curl "http://localhost:3000/places?when=now";


## Mongo en ligne de commande
### Connexion à la base

* Connexion ssh sur une machine
* mongo --host mongodb.info.unicaen.fr --authenticationDatabase admin -u 95006464 -p
* use 95006464_"nomdelabase" (par exemple dev)

### Utilisation de la base
* db.locations.insert({"latitude":20.12,"longitude":0.3}) : pour insérer un truc (ici l'objet qu'on veut pas en fait location)
* db.locations.find([filtre]) : affiche ces objet
* db.places.update({"title":"le Dom"},{$set:{"comments":[{"author":"OjectId("...")","date":Date("2016/08/15D19:30:00.000+0200"),"content":"blabla"}]}});   **ajoute comments (qui est un tableau)**
* db.places.update({"title":"le Dom"},{$get:{"comments":[{"author":"OjectId("...")","date":Date("2016/08/15D19:30:00.000+0200"),"content":"blabla"}]}});   **ajoute un commentaire dans le tableau)**
* db.places.find({"_id";OjectID("...")},{"comments":true}) **affiche les commentaires**
