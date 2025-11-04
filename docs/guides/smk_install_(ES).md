# Guía de instalación (Skorpian Master Keyboard v16.0+)

## Generación de reglas para teclados XKB
La carpeta raíz del repo contiene un script de Bash (llamado [`xcompose_generator.sh`](../../xcompose_generator.sh)) cuya función principal es la de recopilar todas las reglas de `XCompose` (pensadas para su uso con diversos sistemas de escritura) contenidas en el directorio `sequences/`. Para autogenerar dichas reglas, debes invocar el script anterior **desde la carpeta raíz del repositorio** (**_y tras haberlo clonado_**) del siguiente modo:

```bash
$ ./xcompose_generator.sh
```

Una vez que hayas ejecutado el script anteriormente mencionado, dispondrás de las reglas de `XCompose` de este repositorio dentro de tu directorio `$HOME` (más concretamente, en `~/smk_compose/`) y su correspondiente archivo `.XCompose` en la raíz de tu directorio `$HOME` (donde podrás (des)comentar las reglas que quieras (des)activar).

## Instalación de los propios teclados XKB
Si quieres utilizar los teclados de este repositorio en tu propio equipo, el siguiente paso que tendrás que realizar consistirá en copiar los teclados de la carpeta `symbols/smk/layouts/` en los siguientes directorios según tus preferencias:
- `~/.config/xkb/symbols/smk/` (si decides instalarlos localmente).
- Junto con los demás teclados del sistema (cuya localización puede variar según el SO y la distribución concreta. En distribuciones basadas en Arch Linux, la misma se hallaría en `/usr/share/X11/xkb/symbols/` (por lo que, en este caso, resultaría en `/usr/share/X11/xkb/symbols/smk/`)).

> **[CONSEJO]**: Si bien los teclados customizados se pueden colocar localmente en `~/.config/xkb/symbols/smk/`, **es recomendable copiar los teclados de este repositorio tanto en el directorio anterior como dentro de la carpeta de los teclados del sistema**, puesto que, aparte de poder previsualizar las distribuciones de teclado siempre y cuando estén junto a los demás teclados del sistema, existirá la posibilidad de que distintos métodos de entrada (IMEs) como `fcitx`, `ibus` o `xim` (entre muchos otros) **dispongan de los mismos para su uso en aplicaciones que presenten ciertos problemas de compatibilidad con las reglas definidas en tu archivo `.XCompose`**. <br/><br/> Este último punto es extremadamente importante, dado que la versatilidad de los teclados de la serie SMK depende en gran medida de cómo manejen las aplicaciones correspondientes dichas reglas, así como de la presencia (o ausencia) de los propios teclados de la serie SMK.

Después de que hayas traspasado los teclados XKB a los lugares pertinentes, también deberás copiar las reglas contenidas en el directorio `symbols/smk/rules/` dentro de `~/.config/xkb/rules/evdev.xml` (al menos para las reglas en XML, si se trata de una instalación local) y/o `/usr/share/X11/xkb/rules/evdev.xml` + `/usr/share/X11/xkb/rules/evdev.lst` (para una instalación a nivel de sistema) con tal de poder seleccionar la(s) variante(s) de teclado(s) SMK que necesites utilizar.

> **[CONSEJO]**: Añade las reglas en XML de definición de teclados y sus variantes tanto en `~/.config/xkb/rules/evdev.xml` como en `/usr/share/X11/xkb/rules/evdev.xml` (**_preferiblemente en el mismo orden para todos los archivos_**); además de las reglas en formato LST, en cuyo caso su contenido se tendrá que poner en `/usr/share/X11/xkb/rules/evdev.lst`. <br/><br> El motivo de todo lo anterior es similar a lo dispuesto en el primer consejo.

> **[NOTA]**: Las actualizaciones del sistema pueden, en ocasiones, sobrescribir la lista de teclados y variantes de `/usr/share/X11/xkb/`. Si esto ocurre, reinstala los teclados de SMK en las carpetas correspondientes del sistema tal y como se ha descrito más arriba.

![Resultado de aplicar todos los pasos descritos hasta el momento en este documento](../images/SMK_KBD_Selection.png)

## Integración con métodos de entrada (IME)
Tras haber aplicado correctamente los pasos anteriores, [quedará por definir algunas variables de entorno para que las aplicaciones compatibles puedan cargar el archivo `.XCompose` situado en la raíz de tu directorio `$HOME`](https://wiki.archlinux.org/title/Xorg/Keyboard_configuration#Key_combinations). Para ello, puedes tomar la siguiente plantilla como ejemplo e incluir las siguientes líneas dentro del perfil de tu terminal (`.bash_profile`, `.zprofile`, etc.) o, si lo prefieres, en la configuración de tu terminal (si tu sesión carga esta última desde tu perfil de terminal) (`.bashrc`, `.zshrc`, etc.):

```bash
export GTK_IM_MODULE=<ime>
export QT_IM_MODULE=<ime>
export XMODIFIERS="@im=<ime>"   # Necesario únicamente si no se usa xim como IME
```

En donde `<ime>` es el método de entrada correspondiente (`fcitx`, `ibus`, `xim`, etc.).

Si te decantas por utilizar un IME distinto de `xim`, será necesario llevar a cabo unos últimos pasos para que el método de entrada que hayas escogido pueda reconocer tus teclados y, con ello, poder acceder a las reglas de `XCompose` que acompañan a los teclados de SMK.

### Integración de **Fcitx** con teclados XKB de SMK ***[Opción recomendada]***
Accede a la ventana de configuración de Fcitx y añade los teclados de la serie SMK a la lista de este IME:

![Escoge uno de los teclados de SMK desde la configuración de Fcitx](../images/SMK_Fcitx_Selection.png)

![Ejemplo de una lista de teclados empleables por Fcitx](../images/SMK_Fcitx_Result.png)

**🄯 Carlos González Sanz, 2025**
