### Erreurs de `dpkg` lors de l'utilisation de `sudo`

Lorsque vous utilisez `sudo` pour exécuter des commandes, vous pourriez rencontrer des erreurs spécifiques de `dpkg`. Les lignes pertinentes sont les suivantes :

```
dpkg: warning: 'ldconfig' not found in PATH or not executable.
dpkg: warning: 'start-stop-daemon' not found in PATH or not executable.
```

Ces avertissements sont communs pour les utilisateurs de Debian et Ubuntu et peuvent être facilement résolus en ajustant la variable `PATH`.

### Solution 1 : Définir le chemin sécurisé par défaut pour `sudo`

Pour ce faire, ouvrez le fichier `/etc/sudoers` en utilisant la commande `visudo` dans votre terminal. Assurez-vous que le fichier contient la ligne suivante :

```shell
Defaults env_reset
Defaults secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
```

Pour plus de détails sur ce problème, vous pouvez consulter [ce lien](Problèmes et astuces > PATH non défini).

### Solution 2 : Utiliser le compte `root` directement

Si vous préférez, vous pouvez exécuter vos commandes en tant que `root` sans utiliser `sudo`. Voici comment passer au compte `root` :

```shell
$ sudo -i
$ su
```

Une fois connecté en tant que `root`, vous pouvez utiliser `apt-get` comme d'habitude pour vos opérations :

```shell
# apt-get ...
```

Cependant, assurez-vous que le chemin (`PATH`) pour `root` est correctement défini. Vous pouvez éditer le fichier `/root/.bashrc` (en tant que `root`, bien sûr) et ajouter la ligne suivante :

```shell
export PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
```

Cette modification garantit que les commandes s'exécutent correctement lorsque vous utilisez le compte `root`.
