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

    References: https://garajau.com.br/2021/02/enabling-cedilla-acute-c-on-gnome
