# Guide d'installation (Skorpian Master Keyboard v16.0+)

## Génération de règles pour les distributions de clavier en format XKB
Le dossier racine de ce dépôt contient un script Bash (nommé [`xcompose_generator.sh`](../../xcompose_generator.sh)) dont la fonction principale est celle de rassembler toutes les règles `XCompose` (planifiées pour des différents systèmes d'écriture) chez `sequences/`. Pour autogénérer ces règles, tu dois lancer le script précédant **dans la racine de ce dépôt** (**_après l'avoir cloné_**) de la façon suivante:

```bash
$ ./xcompose_generator.sh
```

Une fois le script mentionné ci-dessus ait été éxécuté, tu disposeras des règles `XCompose` de ce dépôt dans ton dossier `$HOME` (plus pŕecisément, chez `~/smk_compose/`) et son respectif fichier `.XCompose` dans la racine de ton répertoire `$HOME` (où tu pourras (dé)commenter les règles que tu veuilles (dés)activer).

## Installation des claviers XKB eux-mêmes
Si tu veux utiliser les distributions de clavier de ce dépôt dans ton propre dispositif, l'étape suivante que tu devras effectuer consistera en copier les claviers du dossier `symbols/smk/layouts/` vers les répertoires suivants selon tes préférences:
- `~/.config/xkb/symbols/smk/` (si tu décides de faire une installation locale).
- Avec les autres distributions de clavier du système (dont l'emplacement peut varier selon le SO et la distribution concrète. Dans les distros basées sur Arch Linux, ceci se situerait sur `/usr/share/X11/xkb/symbols/`, ce qui donnerait comme résultat `/usr/share/X11/xkb/symbols/smk/`).

> **[CONSEIL]**: Bien que les distributions de clavier customisées puissent être mises localement dans `~/.config/xkb/symbols/smk/`, **il serait plutôt recommandable de copier les claviers de ce dépôt dans le dossier précédant ainsi que chez le répertoire des autres distributions de clavier du système**, car, à part de pouvoir prévisualiser ces distributions de clavier si ceux se trouvent avec le reste de claviers du système, il existira aussi la possibilité que des différentes méthodes d'entrée (tels que `fcitx`, `ibus` ou `xim`, parmi plusieur d'autres) **peuvent avoir à sa disposition ces claviers-là pour son emploi dans des logiciels ayant quelques problèmes de compatibilité avec les règles définies dans ton fichier `.XCompose`**. <br/><br/> Ce dernier point est extrêmement important, parce que la versatilité des distributions de clavier de la ligne SMK dépend en grande partie de comment les logiciels pertinents gèrent-ils ces règles, tout comme la présence (ou absence) des claviers de la ligne SMK eux-mêmes.

Après avoir transféré les distributions de clavier (en format XKB) aux lieux appropriés, tu devras aussi-même copier les règles contenues dans le dossier `symbols/smk/rules/` vers `~/.config/xkb/rules/evdev.xml` (au moins pour celles écrites en XML, s'il s'agit d'une installation locale) et/ou `/usr/share/X11/xkb/rules/evdev.xml` + `/usr/share/X11/xkb/rules/evdev.lst` (pour faire une installation au niveau du système) afin de pouvoir sélectionner les variantes de clavier dont tu aies besoin d'employer.

> **[CONSEIL]**: Ajoute les règles XML de définition de distributions de clavier et ses variantes sur `~/.config/xkb/rules/evdev.xml` ainsi comme dans `/usr/share/X11/xkb/rules/evdev.xml` (**_idéalement dans le même ordre pour tous les fichiers_**); en plus des règles en format LST dont le contenu, dans ce cas-ci, devra être mis chez le répertoire `/usr/share/X11/xkb/rules/evdev.lst`. <br/><br> La raison pour tout ça est pareille à ce déjà prévu dans le dernier conseil de cette même section.

> **[NOTE]**: Les actualisations du système peuvent parfois écraser la liste de distributions de clavier de SMK et ses variantes dans `/usr/share/X11/xkb/`. Si ça arrive, installe de nouveau les claviers de la ligne SMK dans les dossiers correspondants du système exactement comme il a été décrit ci-dessus.

![Résultat d'appliquer toutes les étapes décrites jusqu'au moment](../images/SMK_KBD_Selection.png)

## Integration avec des méthodes d'entrée (IME)
Dernièrement, une fois que les étapes précedantes aient été appliquées correctement, [il restera encore définir quelques variables d'environnement afin que les outils et logiciels compatibles puissent lire le fichier `.XCompose` emplacé à la racine de ton dossier `$HOME`](https://wiki.archlinux.org/title/Xorg_(Français)/Keyboard_configuration_(Français)#Combinaisons_de_touches). Pour y parvenir, tu peux prendre le modèle ci-dessous comme exemple et inclure les lignes suivantes à l'intérieur du profil de ton terminal (`.bash_profile`, `.zprofile`, etc.) ou, si tu le préfères, dans la configuration de ton terminal (si ta session charge cette dernière dès le profil de ton terminal) (`.bashrc`, `.zshrc`, etc.):

```bash
export GTK_IM_MODULE=<ime>
export QT_IM_MODULE=<ime>
export XMODIFIERS="@im=<ime>"   # Nécessaire uniquement dans le cas où xim n'est pas utilisé comme IME
```

Où `<ime>` est la méthode d'entrée choisie (`fcitx`, `ibus`, `xim`, etc.).

Si tu t'inclines à utiliser un IME distinct de `xim`, il deviendra nécessaire de mener quelques dernières étapes pour que la méthode d'entrée que tu aies choisie puisse identifier tes distributions de clavier et, avec ça, accéder à les règles `XCompose` accompagnant les claviers de la ligne SMK.

### Integration de **Fcitx** avec les claviers en format XKB de la ligne SMK ***[Option recommandée]***
Dirige-toi vers la fenêtre de configuration de Fcitx et ajoute les claviers de la ligne SMK à la liste de cette méthode d'entrée:

![Sélectionne un ou plusieurs claviers de SMK dans la fenêtre de configuration de Fcitx](../images/SMK_Fcitx_Selection.png)

![Exemple d'une liste de distributions de clavier reconnues et utilisables par Fcitx](../images/SMK_Fcitx_Result.png)

**🄯 Carlos González Sanz, 2025**
