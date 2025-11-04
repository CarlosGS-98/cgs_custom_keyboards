# Guida all'installazione (Skorpian Master Keyboard v16.0+)

## Generazione di regole per tastiere XKB
La cartella radice del repositorio contiene uno script Bash (denominato [`xcompose_generator.sh`](../../xcompose_generator.sh)), la cui funzione principale è quella di raccogliere tutte le regole `XCompose` (pensate per diversi sistemi di scrittura) contenute in `sequences/`. Per autogenerare tale regole, devi invocare lo script precedente **dalla cartella radice del repo** (**_e dopo averlo clonato_**) come segue:

```bash
$ ./xcompose_generator.sh
```

Una volta eseguito lo script precedentemente menzionato, disporrai delle regole `XCompose` di questo repo dietro la tua cartella `$HOME` (più concretamente, in `~/smk_compose/`) e anche del suo correspondente archivio `.XCompose` nella radice della tua cartella `$HOME` (dove potrai (s)commentare le regole che tu voglia (dis)attivare).

## Installazione delle proprie tastiere XKB
Se vuoi utilizzare le tastiere di questo repositorio nel tuo propio computer, il seguente paso che dovrai effettuare consisterà in copiare le mappature di tastiera dalla cartella `symbols/smk/layouts/` a questi luoghi secondo le tue preferenze:
- `~/.config/xkb/symbols/smk/` (se decidessi installarli localmente).
- Con le altri mappature di tastiera del sistema (dove il loro percorso può variare secondo il SO e la distribuzione concreta. All'interno delle distribuzioni basate su Arch Linux, questo si troverebbe in `~/.config/xkb/symbols/smk/` (che, in questo caso, darebbe come risultato `/usr/share/X11/xkb/symbols/smk/`)).

> **[SUGGERIMENTO]**: Sebbene le mappature di tastiera possano essere messe in `~/.config/xkb/symbols/smk/`, **si raccomanda di copiare le tastiere di questo repo sia nella cartella precedente che nella cartella di tastiere del sistema**, poiché oltre a poter visualizzare le mappature di tastiera purché queste siano con le altri tastiere del sistema, esisterà anche la possibilità che diversi metodi di ingresso (IMEs) come `fcitx`, `ibus` o `xim` (tra molti altri) dispongano delle stesse per il suo uso con applicazioni che presentino problemi di compatibilità con le regole definite nel tuo archivio `.XCompose`.<br/><br/> Quest'ultimo ponto è estremamente importante, dato che la versatilità delle mappature di tastiera della serie SMK dipende in gran misura di come i programmi pertinenti gestiscano tale regole, così come la presenza (oppure assenza) delle mappature di tastiera stesse della serie SMK.

Dopo aver spostato le tastiere XKB nei luoghi correspondenti, dovrai anche copiare le regole contenute all'interno di `symbols/smk/rules/` in `~/.config/xkb/rules/evdev.xml` (almeno per le regole XML, se si tratta di un'installazione locale) e/o `/usr/share/X11/xkb/rules/evdev.xml` + `/usr/share/X11/xkb/rules/evdev.lst` (per fare un'installazione a livello del sistema) al fine di poter scegliere la/le variante/i di tastiera/e della serie SMK delle cui tu abbia bisogno di usare.

> **[SUGGERIMENTO]**: Aggiunge le regole XML di definizione di tastiere (con le loro varianti) tanto in `~/.config/xkb/rules/evdev.xml` come in `/usr/share/X11/xkb/rules/evdev.xml` (**_preferibilmente nello stesso ordine per tutti gli archivi_**); inoltre alle regole in formato LST, nel qual caso il loro contenuto dovrà essere messo in `/usr/share/X11/xkb/rules/evdev.lst`. <br/><br> Il motivo di tutto ciò è simile a quello del primo suggerimento.

> **[NOTA]**: Le attualizzazioni del sistema possono, a volte, sovrascrivire la lista di tastiere (e le loro varianti) contenuta in `/usr/share/X11/xkb/`. Se questo succedesse, reinstalla le tastiere della serie SMK nelle cartelle correspondenti del sistema come descritto sopra.

![Risultato di applicare tutti i passaggi descritti finora in questo documento](../images/SMK_KBD_Selection.png)

## Integrazione con metodi di ingresso (IME)
Dopo che tu abbia applicato correttamente i passaggi precedenti, [resterà da definire qualcune variabili d'ambiente con l'obiettivo che le programmi compatibili possano caricare l'archivio `.XCompose` ubicato nella radice della tua cartella `$HOME`](https://wiki.archlinux.org/title/Xorg/Keyboard_configuration#Key_combinations). Per raggiungere quello, puoi prendere il seguente modello come esempio e includere le regole qui sotto dietro il profilo del tuo terminale (`.bash_profile`, `.zprofile`, etc.), oppure, se lo preferisci, nella configurazione del tuo terminale (sempre che la tua sessione carichi quest'ultima dal tuo profilo di terminale) (`.bashrc`, `.zshrc`, etc.):

```bash
export GTK_IM_MODULE=<ime>
export QT_IM_MODULE=<ime>
export XMODIFIERS="@im=<ime>"   # Necessario unicamente se non si impiega xim come IME
```

Dove `<ime>` è il metodo di ingresso scegliato (`fcitx`, `ibus`, `xim`, etc.).

Se optassi per utilizzare un metodo di ingresso diverso da `xim`, sarà ancora necessario da eseguire qualchi ultimi passaggi affinché il metodo di ingresso que tu abbia scegliato possa riconoscere le tue tastiere e, con quello, poter accedere alle regole `XCompose` che accompagnano alle mappature di tastiera della serie SMK.

### Integrazione di **Fcitx** con mappature di tastiera di SMK ***[Opzione consigliata]***
Vai verso la finestra di configurazione di Fcitx e aggiungi le tastiere della serie SMK alla lista di questo IME:

![Seleziona una delle tastiere della serie SMK dalla configurazione di Fcitx](../images/SMK_Fcitx_Selection.png)

![Esempio di una lista di tastiere utilizzabil da Fcitx](../images/SMK_Fcitx_Result.png)

**🄯 Carlos González Sanz, 2025**
