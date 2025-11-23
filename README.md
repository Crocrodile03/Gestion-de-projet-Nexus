# Demo Nexus Gestion de projet
## Installer Nexus et le comprendre facilement :
---

### Installer l'image docker :

Vérifie que tu as bien docker et installe l'image nexus avec cette commande :

```docker run -d \ -p 8081:8081 \ -v nexus-data:/nexus-data \ --name nexus \ sonatype/nexus3```

### Se connecter à nexus :

Lance en paralèlle une page web et connecte là au le localhost sur le port 8081 :

```https://localhost:8081```

### Vérifier la connexion :

Pour vérifier que Nexus s'est bien lancé utilise la commande :

```docker logs -f nexus```

une fois que tu vois la ligne :

- _Started Sonatype Nexus_

c'est que nexus s'est bien lancé

### Récupération du mot de passe admin :

Récupère le mot de passe admin avec cette commande :

```docker exec nexus cat /nexus-data/admin.password```

Tu peux ensuite te connecter avec ce mot de passe sur la page nexus que tu as ouverte précédement. Utilise _admin_ comme user et le mot de passe récupéré comme mot de passe.

### Créer un repo :

Pour pouvoir créer un repo tu dois :

- Aller dans settings
- puis dans Repository
- cliquer sur repositrories 
- cliquer sur _+create repository_
- choisis le type _raw(hosted)_
- donne lui un nom (par exemple _demo_raw_)
- _Create_

### Création de fichier :

Crée un simple fichier par exemple

```echo "Hello world" > hello.txt```

### Envoit du fichier :

Envoit le fichier crée sur nexus dans ton repo avec la commande :
(Oublie pas de changer _MON_MDP_ par ton mot de passe)

```curl -u admin:MON_MDP \ --upload-file hello.txt \ http://localhost:8081/repository/demo-raw/hello.txt```

### Téléchargement et lecture du fichier :

Tu peux ensuite consulter le fichier grace à la commande :

```curl http://localhost:8081/repository/demo-raw/hello.txt```

Si tout fonctionne correctement tu devrais obtenir le contenu de ton fichier
