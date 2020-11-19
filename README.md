# **M141 Doku**

## **5. Anbindung**

### **5.1 Webserver Installation**

Als aller erstes muss der Webserver auf der vm-LS2 installiert werden. Diesen kann man unter /sh-modules/iet-141/98_Software/web-server herunterladen.

    sftp benutzername@sftp.iet-gibb.ch

    get /sh-modules/iet-141/98_Software/web-server/gna_0.6_all.deb

Nun muss gdebi installiert werden um das heruntergeladene Paket zu isntallieren

    sudo apt-get install gdebi

    sudo gdebi gna_0.6_all.deb

Als nächstes muss man noch den Treiber für die Datenbank installieren

    sudo apt-get install libdbd-pg-perl

Ausserdem kann man nun das gna.conf.yml vom Share herunterladen und im home Verzeichnis von vmadmin ablegen.

    sftp benutzername@sftp.iet-gibb.ch

    get /sh-modules/iet-141/98_Software/web-server/gna.conf.yml

Danach muss man die db Konfiguration und die author Query anpassen

DB Konfiguration

    db:
        dsn: 'DBI:Pg:database=modul141;host=192.168.210.30;port=5432'
        user: friggapp
        pass: sml12345

Author Query

    author: "select content from Data join Meta on Data.digest = Meta.fk_digest where Meta.path = '/opt/frigg/admin/projekt.txt';"
Um nun auch eine funktionierende Aplikation zu erhalten, müssen noch die Queries im Rest des Config files anpassen. Diese werde ich hier jedoch nicht auflisten und können hier nachgeschaut werden:  [gna.conf.yml](https://github.com/simkel/test/blob/main/src/gna.conf.yml)

### **5.2 Firewall Rules**
