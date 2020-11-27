# Natas 0
Zugriff:	[http://natas0.natas.labs.overthewire.org](http://natas0.natas.labs.overthewire.org)
Username: `natas0`
Passwort: `natas0`

Das Passwort für Natas1 ist im Seitenquelltext als Kommentar hinterlegt.

# Natas 1
Zugriff:	[http://natas1.natas.labs.overthewire.org](http://natas1.natas.labs.overthewire.org)
Username: `natas1`
Passwort: `gtVrDuiDfck831PqWsLEZy5gyDz1clto`

Das Passwort für Natas2 lässt sich wie folgt auslesen: Mit `F12` den Debugger öffnen und im Haupt-Thread auf `index` navigieren. Dort ist das Passwort als Kommentar hinterlegt.

# Natas 2
Zugriff:	[http://natas2.natas.labs.overthewire.org](http://natas2.natas.labs.overthewire.org)
Username: `natas2`
Passwort: `

Im Quelltext der Seite befindet sich ein il een oe it `iesien neeben tSmi ist klrdas sich ter er dresse natas.natas.labs.overthewire.org/fies in aerzeichnis t.
Beim Aufrufen des Verzeichnisses finde i neen erxel.pnateiaheine tate mit de Naen user.tt. n dieer indet sich das asswUser.zxzort r eel 

# Natas 3
Zugriff:	[http://natas3.natas.labs.overthewire.org](http://natas.natas.labs.overthewire.org)
Username: `natas3`
Passwort: `sJIJNW6ucpu6HPZ1ZAchaDtwd7oGrD14`

Im Quelltext der Seite befindet sich folgender inwis:o mre information les ot even oole wi fnd i this t.
Dies ist ein Hinweis auf die Robots.txt, welche das Verhalten der Roboter der Suchmaschinen beeinflusst. 
> https://wiki.selfhtml.org/wiki/Grundlagen/Robots.txt

Da sich die robots.txt immer im Root-Verzeichnis der Website befindet, können wir diese über http://natas3.natas.labs.overthewire.org/robots.txt aufrufen.
In dieser finden wir das Verzeichnis `/s3cr3t/`.
Beim Aufrufen des Verzeichnisses finden wir wie in Level 2 eine users.txt, welche das Passwort für das folgende Level enthällt.


# Natas 4
Zugriff:	[http://natas4.natas.labs.overthewire.org](http://natas4.natas.labs.overthewire.org)
Username: `natas4`
Passwort: `Z9tkRkWmpt9Qr7XrR5jWRkgOU901swEZ`

Natas 4 begrüßt uns mit der Nachricht:
> Access disallowed. You are visiting from "" while authorized users should come only from "http://natas5.natas.labs.overthewire.org/"

Als Lösung kommen hier die HTTP-Header ins Spiel:
> https://de.wikipedia.org/wiki/Liste_der_HTTP-Headerfelder

Diese lassen sich zum Beispiel durch dass Add-on "Tamper" bearbeiten.
Nun kann der Http-Referer von "http://natas4.natas.labs.overthewire.org/" zu "http://natas5.natas.labs.overthewire.org/" geändert werden.

Beim Neuladen der Seite geben wir so nun vor, von der Natas5 Seite zu kommen, was die Lösung dieses Levels ist. 

# Natas 5
Zugriff:	[http://natas5.natas.labs.overthewire.org](http://natas5.natas.labs.overthewire.org)
Username: `natas5`
Passwort: `iX6IOfmpN7AYOQGPwtn3fXpbaJVJcHfq`

Der Starttext von Natas5 lautet: 
> Access disallowed. You are not logged in

Im Cookieverzeichnis der Website findet sich ein Cookie mit dem Namen "loggedin". Wenn wir diesen auf "1" setzen und die Seite neuladen, erhalten wir das Passwort für Natas6.

# Natas 6
Zugriff:	[http://natas6.natas.labs.overthewire.org](http://natas6.natas.labs.overthewire.org)
Username: `natas6`
Passwort: `aGoY4q2Dc6MgDq4oL4YtoKtyAg9PeHa1`

Bei diesem Level erhalten wir einen Link zum Sourcecode der Seite:
```php
include "includes/secret.inc";

    if(array_key_exists("submit", $_POST)) {
        if($secret == $_POST['secret']) {
        print "Access granted. The password for natas7 is <censored>";
    } else {
        print "Wrong secret";
    }
    }
```
Die Lösung liegt hier in der Zeile `"includes/secret.inc";`
Beim Aufruf dieser Datei finden wir eine leere Datei vor, jedoch befindet sich das "secret"-Wort als Kommentar im Quelltext.

# Natas 7
Zugriff:	[http://natas7.natas.labs.overthewire.org](http://natas7.natas.labs.overthewire.org)
Username: `natas7`
Passwort: `7z3hEENjQtflzgnT29q7wAvMNfZdh0i9`

Beim Klicken auf die Links "Home" und "About" sieht man, dass an die URL die Parameter "?page=home" oder "?page=about" angehängt werden.
Im Quelltext findet man den Hinweis, dass sich das Passwort in einer Datei unter dem Pfad `/etc/natas_webpass/natas8` befindet.

>https://en.wikipedia.org/wiki/File_inclusion_vulnerability

Mit dem Wissen über die File-inclusion-vulnerability können wir nun versuchen uns das Passwort ausgeben zu lassen, in dem wir den Pfad als Parameter übergeben: `?page=/etc/natas_webpass/natas8`
Daraufhin gibt uns die Seite das Passwort für Natas8 aus.

# Natas 8
Zugriff:	[http://natas8.natas.labs.overthewire.org](http://natas8.natas.labs.overthewire.org)
Username: `natas8`
Passwort: `DBfUBfqQG69KvJvJ1iAbMoIpwSNQ9bWe`