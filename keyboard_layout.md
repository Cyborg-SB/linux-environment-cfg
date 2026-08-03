## System wide setup for cedilla on linux system using Englsih (US) ( US Intl with dead keys)

### Set the file /etc/default/locale with the content:
    LANG=en_US.UTF-8
    LANGUAGE=
    LC_ADDRESS=pt_BR.UTF-8
    LC_COLLATE=en_US.UTF-8
    LC_CTYPE=pt_BR.UTF-8
    LC_IDENTIFICATION=pt_BR.UTF-8
    LC_MEASUREMENT=pt_BR.UTF-8
    LC_MESSAGES=en_US.UTF-8
    LC_MONETARY=pt_BR.UTF-8
    LC_NAME=pt_BR.UTF-8
    LC_NUMERIC=pt_BR.UTF-8
    LC_PAPER=pt_BR.UTF-8
    LC_TELEPHONE=pt_BR.UTF-8
    LC_TIME=pt_BR.UTF-8

 ### Note: it is important **LANGUAGE= to be empty**.

### Remove the file ~/.pam_environment from the user directory (if there is the file):
    rm ~/.pam_environment

### Restart the system.


## User space alternative 

### Create a ~/.XCompose file with the following content:
     UTF-8 (Unicode) compose sequences
     Overrides C acute with Ccedilla:
     <dead_acute> <C> : "Ç" "Ccedilla"
     <dead_acute> <c> : "ç" "ccedilla"

### Run the following command:
    gsettings set org.gnome.settings-daemon.plugins.xsettings overrides "{'Gtk/IMModule': <'ibus'>}"

### Restart the user session.

### **Extra: the double quote key (use " directly instead of ¨)**
    Run the following command:
    sed -i "s|dead_acute,[ ]*dead_diaeresis,[ ]*apostrophe,[ ]*quotedbl|dead_acute, quotedbl|" /usr/share/X11/xkb/symbols/us
    Restart the system.

## Ubuntu extra


Passos para ajeitar o cedilha errado no Ubuntu

Confirme que o layout (Fonte de entrada) do seu teclado possui “intern.” ou “intl.” no nome
Exemplos: Ingês (EUA, intern. alt.) e English (US, intl., with dead keys). Esta informação está na tela de configuração do teclado do sistema.
  
### Edite o arquivo /etc/environmen. A maneira mais fácil para editar este arquivo é abrir um terminal e digitar:
    sudo gnome-text-editor /etc/environment

OU

    sudo gedit /etc/environment

O comando acima vai pedir a senha do seu usuário e depois de digitá-la (enquanto você digita o terminal não irá mostrar nada) é só apertar a tecla ENTER que o editor gedit vai abrir. Não tem problema se o seu arquivo estiver vazio.
Adicione as seguintes linhas no final do arquivo:

    GTK_IM_MODULE=cedilla
    QT_IM_MODULE=cedilla
    Salve o arquivo

Clique no botão ” Salvar” localizado no canto direito superior da tela, ou use a tecla de atalho CTRL+S.
Encerre a sessão do seu usuário ou reinice o computador
É necessário deslogar e logar novamente para a alteração funcionar. Caso não funcione, reinicie seu computador.


Para aplicativos GTK 4 (como o gnome-text-editor que veio no Ubuntu 24.04) é necessário fazer os passos abaixo.

### Criar um arquivo .~/.XCompose no diretório do seu usuário com o conteúdo abaixo:

    nano ~/.XCompose

Overrides C acute with Ccedilla:

    include "%L"
    <dead_acute> <c> : "ç" ccedilla
    <dead_acute> <C> : "Ç" Ccedilla

### Executar o comando no terminal:
   
        gsettings set org.gnome.settings-daemon.plugins.xsettings overrides "{'Gtk/IMModule': <'ibus'>}"
        Code language: JavaScript (javascript)

###  Encerrar a sessão do seu usuário ou reiniciar o computador.

Essa solução veio do blog do Daniel Garajau.
Solução “manual”

Se por algum motivo a solução acima não funcionar ou você não puder editar o arquivo /etc/environment, é possível utilizar as seguintes teclas de atalho se o seu teclado estiver configurado com qualquer layout de teclado English (Intl):

    ç → AltGR + ,
    Ç → AltGR + Shift + ,

A tecla AltGR fica localizada do lado direito da tecla de Espaço.
dicas  teclado  ubuntu

### Se o KDE ignorar ~/.XCompose

Algumas configurações do Plasma/IBus/Fcitx podem não carregar automaticamente o arquivo Compose.

Verifique:

echo $GTK_IM_MODULE
echo $QT_IM_MODULE
echo $XMODIFIERS

### Se estiver usando IBus (padrão do Fedora), normalmente o Compose funciona sem ajustes adicionais.

 Caso não funcione, force o carregamento criando:

    mkdir -p ~/.config/environment.d
    nano ~/.config/environment.d/compose.conf

Conteúdo:

    XCOMPOSEFILE=%h/.XCompose

### Faça logout/login novamente.

References: https://garajau.com.br/2021/02/enabling-cedilla-acute-c-on-gnome
