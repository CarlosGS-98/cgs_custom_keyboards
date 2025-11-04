# Guia de instalação (Skorpian Master Keyboard v16.0+)

## Geração de regras para teclados no formato XKB
O diretório raiz do repositório contém um script Bash (chamado [`xcompose_generator.sh`](../../xcompose_generator.sh)) cuja função principal é coletar todas as regras `XCompose` (pensadas pelo seu emprego com diferentes sistemas de escrita) contidas no diretório `sequences/`. Para auto-gerar tais regras, deves invocar o script anterior **desde o diretório raiz do repo** (**_e depois de cloná-lo_**) da seguinte forma:

```bash
$ ./xcompose_generator.sh
```

Uma vez que tenhas executado o script mencionado acima, terás as regras `XCompose` deste repositório dentro do teu diretório `$HOME` (mais concretamente, em `~/smk_compose/`) e o seu correspondente ficheiro `.XCompose` na raiz do teu diretório `$HOME` (onde poderás (des)comentar as regras que desejes (des)ativar).

## Instalação dos próprios teclados XKB
Se quiseres utilizar as disposições de teclado no teu próprio computador, o seguinte passo que deverás realizar consistirá em copiar os teclados da pasta `symbols/smk/layouts/` nos seguintes diretórios conforme às tuas preferências:
- `~/.config/xkb/symbols/smk/` (se decidires instalá-los localmente).
- Junto com o resto de disposições de teclado do sistema (cujo caminho pode variar segundo o SO e a sua distribuição concreta. No âmbito das distribuições baseadas no Arch Linux, este encontrar-se-ia em `/usr/share/X11/xkb/symbols/` (o que, neste caso, resultaria em `/usr/share/X11/xkb/symbols/smk/`)).

> **[CONSELHO]**: Apesar dos teclados customizados poderem estar situados em `~/.config/xkb/symbols/smk/`, **é recomendável copiar as disposições de teclado deste repositório tanto na pasta anterior como dentro do diretório dos teclados do sistema**, já que, além de poder pré-visualizar as disposições de teclado sempre que estejam localizadas junto ao resto dos teclados do sistema, existirá também a possibilidade de que diferentes métodos de entrada (IMEs) como `fcitx`, `ibus` ou `xim` (entre muitos outros) **disponham das mesmas pelo seu uso em aplicações que apresentem certos problemas de compatibilidade com as regras definidas no teu arquivo `.XCompose`**. <br/><br/> Este último ponto é extremamente importante, dado que a versatilidade dos teclados da série SMK depende, em grande parte, de como as aplicações correspondentes gerenciem tais regras, assim como também a presença (ou ausência) das próprias disposições de teclado da série SMK.

Depois ter transferido os teclados no formato XKB aos logos pertinentes, também deverás copiar as regras contindas no diretório `symbols/smk/rules/` dentro de `~/.config/xkb/rules/evdev.xml` (almenos para as regras XML, se for uma instalação local) e/ou `/usr/share/X11/xkb/rules/evdev.xml` + `/usr/share/X11/xkb/rules/evdev.lst` (para uma instalação ao nível do sistema) a fim de poder selecionar a(s) variante(s) de teclado(s) da série SMK que precises de empregar.

> **[CONSELHO]**: Adiciona as regras XML de definição de teclados (com as suas variantes) tanto em `~/.config/xkb/rules/evdev.xml` como em `/usr/share/X11/xkb/rules/evdev.xml` (**_preferivelmente na mesma ordem para todos os ficheiros_**); além das regras no formato LST, que, nesse caso, o seu conteúdo terá de ser posto em `/usr/share/X11/xkb/rules/evdev.lst`. <br/><br> O motivo de tudo o dito anteriormente é semelhante ao disposto no primeiro conselho.

> **[NOTA]**: As atualizações do sistema podem, às vezes, sobrescrever a lista de teclados e variantes de `/usr/share/X11/xkb/`. Se isto acontecer, reinstala as disposições de teclado da série SMK nas pastas correspondentes do sistema tal como foi descrito acima.

![Resultado de aplicar todos os passos descritos até o momento neste documento](../images/SMK_KBD_Selection.png)

## Integração com métodos de entrada (IME)
Após ter aplicado corretamente os passos anteriores, [restará definir algumas variáveis de ambiente para que as aplicações compatíveis possam carregar o ficheiro `.XCompose` situado na raiz do teu diretório `$HOME`](https://wiki.archlinux.org/title/Xorg/Keyboard_configuration#Key_combinations). Para lograr isso, podes tomar o seguinte modelo como exemplo e incluir as seguintes líneas dentro do teu perfil do teu terminal (`.bash_profile`, `.zprofile`, etc.) ou, se o preferes, na configuração do teu terminal (assumindo que a tua sessão carregue esta última desde o teu perfil de terminal) (`.bashrc`, `.zshrc`, etc.):

```bash
export GTK_IM_MODULE=<ime>
export QT_IM_MODULE=<ime>
export XMODIFIERS="@im=<ime>"   # Necessário unicamente quando xim não é utilizado como IME
```

Onde `<ime>` é o método de entrada correspondente (`fcitx`, `ibus`, `xim`, etc.).

Se optares por empregar um IME distinto do `xim`, será ainda necessário realizar uns últimos passos para que o método de entrada que tenhas escolhido possa reconhecer os teus teclados e, com isso, poder aceder às regras `XCompose` que acompanham as disposições de teclado da série SMK.

### Integração de **Fcitx** com teclados XKB da série SMK ***[Opção recomendada]***
Acede à janela de configuração do Fcitx e adiciona os teclados da série SMK à lista deste método de entrada:

![Escolhe um dos teclados da série SMK desde a configuração do Fcitx](../images/SMK_Fcitx_Selection.png)

![Exemplo duma lista de teclados empregáveis pelo Fcitx](../images/SMK_Fcitx_Result.png)

**🄯 Carlos González Sanz, 2025**
