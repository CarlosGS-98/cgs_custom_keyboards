# Installationsanleitung (Skorpian Master Keyboard v16.0+)

## Regelerstellung für XKB-Tastaturen
Der Hauptordner des Repos enthält ein Bash-Skript (das als [`xcompose_generator.sh`](../../xcompose_generator.sh) benannt wurde), dessen Hauptfunktion ist, die Sammlung aller `XCompose`-Regeln (die für verschiedenen Schriftsysteme geplant sind) innerhalb `sequences/` zu erledigen. Um solche Regeln automatisch zu generieren, musst du das vorherige Skript **vom Root-Ordner dieses Repos** (**_nachdem du es geklont hast_**) wie folgt aufrufen:

```bash
$ ./xcompose_generator.sh
```

Sobald du das oben gennante Skript ausgeführt hast, wirst du über die `XCompose`-Regeln dieses Repos innerhalb deines `$HOME`-Ordners (genauer gesagt, die in `~/smk_compose/`) und auch ihre entsprechende `.XCompose`-Datei unter deinem `$HOME`-Hauptordner verfügen (wo du jede Regel, die du (de)aktivieren möchtest, (un)kommentieren kannst).

## Installation der XKB-Tastaturen an sich
Wenn du die Tastaturen aus diesem Repo auf deinem Rechner verwenden möchtest, musst du als Nächstes die Tastaturen von `symbols/smk/layouts/` in die folgenden Ordner kopieren (all das nach deinen Präferenzen):
- `~/.config/xkb/symbols/smk/` (falls du sie lokal installieren möchtest).
- Neben den anderen Systemtastaturen (deren genauer Spiecherort sowie vom Betriebssystem als auch von ihren jeweiligen Varianten abhängen kann. Mit auf Arch Linux basierten Distros würde diese an `/usr/share/X11/xkb/symbols/` liegen; das heißt, auf diesem Fall wäre der genaue Spiecherort `/usr/share/X11/xkb/symbols/smk/`).

> **[TIPP]**: Auch wenn benutzerdefinierte Tastaturbelegungen lokal unter `~/.config/xkb/symbols/smk/` platziert werden können, **ist es empfohlen, die Tastaturen aus diesem Repo sowie in den vorherigen Ordner als auch in die Systemstastatursordner zu kopieren**, da es die Möglichkeit existieren wird, diese Tastaturen zu visualisieren (solange die mit den anderen Systemtastaturbelegungen unter demselben Ordner liegen) und auch die Fähigkeit, diese mit verschiedenen Eingabemethoden (unter anderem `fcitx`, `ibus` oder `xim`) enger zu verbinden, **damit sie diese Tastaturbelegungen verwenden können, insbesonders mit Apps, die manchen Kompatibilitätsproblemen mit deiner `.XCompose`-Datei haben könnten**. <br/><br/> Dieser lezte Punkt ist sehr wichtig, denn die Versatilität der SMK-Tastaturbelegungen hängt nicht nur vom Art und Weise Apps diese Regeln verwalten, sondern auch von der An- oder Abwesenheit der SMK-Tastaturbelegungsserie ab.

Nachdem du die XKB-Tastaturen in die richtigen Speicherorte übertragen hast, musst du auch die unter `symbols/smk/rules/` beinhaltenen Regeln in `~/.config/xkb/rules/evdev.xml` (mindestens für XML-Regeln, wenn es sich um eine lokale Installation handelt) und/oder `/usr/share/X11/xkb/rules/evdev.xml` + `/usr/share/X11/xkb/rules/evdev.lst` (für Systeminstallationen) kopieren, damit du die Tastaturbelegungvarianten, die du benutzen möchtest, auswählen kannst.

> **[TIPP]**: Füge die XML-Tastaturdefinitionsregeln und ihre Varianten sowie in `~/.config/xkb/rules/evdev.xml`als auch in `/usr/share/X11/xkb/rules/evdev.xml` (**_am besten in derselben Ordnung für alle Dateien_**) hinzu. Darüber hinaus solltest du auch die LST-Regeln dieses Repos in `/usr/share/X11/xkb/rules/evdev.lst` übertragen. <br/><br> Der Grund für all das oben Gesagte ist ähnlich wie das, was im ersten Tipp festgelegt wurde.

> **[HINWEIS]**: Systemaktualisierungen können in einigen Fällen die Tastaturbelegunsliste (und ihre Varianten) innerhalb `/usr/share/X11/xkb/` überschreiben. Falls dies geschiet, installiere die SMK-Tastaturbelegungsserie in den passenden Systemordnern neu, wie hier oben schon beschrieben wurde.

![Endergebnis nach der Anwendung aller bis jetzt beschriebenen Schritte](../images/SMK_KBD_Selection.png)

## Integration mit Eingabemethoden (IME) 
Letztens, nachdem du all den vorherigen Schritten gefolgt hast, ist es noch notwendig, [ein paar Umgebungsvariablen zu definieren, mit dem Ziel, die Ladung der unter deinem `$HOME`-Hauptordner liegenden `.XCompose`-Datei von kompatiblen Apps zu ermöglichen](https://wiki.archlinux.org/title/Xorg/Keyboard_configuration#Key_combinations). Dafür kannst du diese unten gestellte Vorlage als Beispiel nehmen, um die folgenden Zeilen innerhalb deines Terminalprofils hineinzufügen (`.bash_profile`, `.zprofile`, o. Ä.); oder sogar auf deinen Terminaleinstellungen, falls du das bevorzugst (solange deine Session das Letzte von deinem Terminalprofil importiert) (`.bashrc`, `.zshrc`, o. Ä.):

```bash
export GTK_IM_MODULE=<ime>
export QT_IM_MODULE=<ime>
export XMODIFIERS="@im=<ime>"   # Benötigt nur, wenn xim nicht als Eingabemethode benutzt wird
```

Wo `<ime>` die entsprechende Eingabemethode ist (`fcitx`, `ibus`, `xim`, usw.).

Im Falle, dass du dich für die Verwendung einer anderen Eingabemethode als `xim` entscheidest, wird es noch erforderlich, eine Reihe letzter Schritte durchzuführen, um die Tastaturbelegungen der SMK-Serie von deiner Eingabemethode erkennbar zu machen. So können IMEs auch auf die `.XCompose`-Regeln der SMK-Tastaturbelegungen zugreifen.

### Integration von **Fcitx** mit XKB-Tastaturen der SMK-Serie ***[Bevorzugte Option]***
Gehe zum Einstellungsfenster von Fcitx und füge die Tastaturbelegungen der SMK-Serie in die Liste dieser Eingabemethode ein:

![Wähle eine der SMK-Tastaturen in den Einstellungen von Fcitx](../images/SMK_Fcitx_Selection.png)

![Beispiel einer Liste von Fcitx verwendbaren Tastaturbelegungen](../images/SMK_Fcitx_Result.png)

**🄯 Carlos González Sanz, 2025**
