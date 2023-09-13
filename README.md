# Développer un plugin ITSM-NG1.5

ITSM-NG est doté d'un puissant moteur de plugin qui permet de modifier la majorité des pages du logiciel et d'en créer.
Les méthodes de création d'un plugin sont assez libre mais nécessite de suivre quelques standards.
(Cette page est liée a un [repo github](https://github.com/AntoineLemarchand/examplePlugin) contenant un exemple minimal)

## L'arborescence
L'arborescence des plugins ITSM-NG se présente de la sorte:
```
MyPlugin/
┣ front/
┣ inc/
┣ locales/
┣ */
┣ hook.php
┗ setup.php
```

### Les dossiers
* [front/](https://github.com/AntoineLemarchand/examplePlugin/tree/main/front) contient les fichiers contenant les pages et formulaires du plugin.
* [inc/](https://github.com/AntoineLemarchand/examplePlugin/tree/main/inc) contient les fichier contenant les classes et la logique du plugin.
* [locales/](https://github.com/AntoineLemarchand/examplePlugin/tree/main/locales) contient les fichier de traduction (*.po, *.mo).
* Vous avez la liberté d'ajouter d'autres dossiers en veillant a garder l'arborescence compréhensible.

### Les fichiers

#### setup.php
setup.php défini la fiche d'identité et les vérifications d'installation du plugin.
il doit au moins contenir ces cinq fonctions ({MONPLUGIN} étant le nom de votre plugin):

* [`plugin_version_{MONPLUGIN}(): array`](https://github.com/AntoineLemarchand/examplePlugin/blob/main/setup.php#L40): La fiche d'identité du plugin.
* [`plugin_init_{MONPLUGIN}(): void`](https://github.com/AntoineLemarchand/examplePlugin/blob/main/setup.php#L81): pour initialiser les hooks du plugin.
* [`plugin_{MONPLUGIN}_check_prerequisites(): bool`](https://github.com/AntoineLemarchand/examplePlugin/blob/main/setup.php#L63): Vérification des dépendances nécessaire au plugin AVANT l'installation.
* [`plugin_{MONPLUGIN}_check_config($verbose = false): bool`](https://github.com/AntoineLemarchand/examplePlugin/blob/main/setup.php#L72): Vérification de la configuration nécessaire au plugin AVANT l'installation.

Il est aussi encouragé de charger la version du plugin dans une constance [`{MONPLUGIN_VERSION}`](https://github.com/AntoineLemarchand/examplePlugin/blob/main/setup.php#L30)

#### hook.php
hook.php contient la définition des hooks du plugin.
il doit au moins contenir ces deux fonctions ({MONPLUGIN} étant le nom de votre plugin):

* [`plugin_{MONPLUGIN}_install(): bool`](https://github.com/AntoineLemarchand/examplePlugin/blob/main/hook.php#L31): créer les bases de données du plugin et éffectue les étapes nécessaire a son l'installation.
* [`plugin_{MONPLUGIN}_uninstall(): bool`](https://github.com/AntoineLemarchand/examplePlugin/blob/main/hook.php#L40): supprime les bases de données du plugin et éffectue les étapes nécessaire a son l'installation.
