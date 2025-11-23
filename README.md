# Demo Nexus Gestion de projet
## Installer Nexus et le comprendre facilement :
---

### Installer l'image docker :

Vérifie que tu as bien docker et installe l'image nexus avec cette commande :

```docker run -d -p 8081:8081 -v nexus-data:/nexus-data --name nexus sonatype/nexus3```

### Se connecter à nexus :

Lance en paralèlle une page web et connecte là au le localhost sur le port 8081 :

```https://localhost:8081```

Si la page ne s'affiche pas tu peux vérifier que Nexus s'est bien lancé utilise la commande (la page peut prendre plusieurs minutes avant de s'afficherà :

*Dans ton invite de commande*

```docker logs -f nexus```

Une fois que tu vois la ligne :


----
- _Started Sonatype Nexus_
----

c'est que nexus s'est bien lancé

### Récupération du mot de passe admin :

Récupère le mot de passe admin avec cette commande :

```docker exec nexus cat /nexus-data/admin.password```

*Sur la page web de nexus*

Tu peux ensuite te connecter avec ce mot de passe sur la page nexus que tu as ouverte précédement. Utilise _admin_ comme user et le mot de passe récupéré comme mot de passe.

On va ensuite te demander de changer de mot de passe (ce qui est fortement recommandé). Dans le cadre de la demo tu peux *enable anonymous user* ce qui t'évitera de devoir tout le temps taper ton mot de passe quand tu voudra faire un *curl* sur ton repo. Si tu décides de quand même *disable anonymous user* alors rajoute ```-u admin:MON_MDP``` (**MON_MDP corresponds au mot de passe que tu as choisis pour admin**) à chacun de tes ```curl```

### Créer un repo :

Pour pouvoir créer un repo tu dois :

- Aller dans settings
- puis dans Repository
- cliquer sur repositrories 
- cliquer sur _+create repository_
- choisis le type _raw(hosted)_
- donne lui un nom (par exemple _demo-raw_)
- _Create repository_

### Création de fichier :
*Retourne dans ton invite de commande*

Crée un simple fichier par exemple

```echo "Hello world" > hello.txt```

### Envoie du fichier :

Envoie le fichier crée sur nexus dans ton repository avec la commande :
(**Oublie pas de changer _MON_MDP_ par ton mot de passe choisis pour admin**)

```curl -u admin:MON_MDP --upload-file hello.txt http://localhost:8081/repository/demo-raw/hello.txt```

*Retourne sur la page web*

Pour vérifier que le fichier s'est bien ajouté clique sur *Browse* et va dans le repository que tu as crée. Tu devrais voir apparaître le fichier que tu viens de rajouter.

### Téléchargement et lecture du fichier :

Tu peux ensuite consulter le fichier grâce à la commande :

```curl http://localhost:8081/repository/demo-raw/hello.txt```

Si tout fonctionne correctement tu devrais voir le contenu de ton fichier (dans notre cas c'est _Hello world !_) s'afficher dans ton invite de commande.
