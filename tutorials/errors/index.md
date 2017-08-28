# [Tutorial] Fehler finden

In diesem Tutorial möchte ich euch erklären wie ihr einen Fehler in eurer Arma Mission selber finden könnt, ohne das ihr darauf angewiesen Seit euch hilfe von anderen zu holen.

### Arten von Fehlern

Grundsätzlich unterscheidet man in verschiedene Arten von Fehlern

1. Syntaktische Fehler
   1. Bei einem `Syntaktischen Fehler` habt ihr einen Fehler in der Syntax, alo der vorgegeben Schreibweise (ein Rechtschreibfehler ist Beispielsweise ein Syntaktischer Fehler im weitesten sinne). Ein Syntaktischer Fehler führt dazu das euer Programm (Script) nicht ausgeführt werden kann.
2. Semantische Fehler
   1. Ein `Semantischer Fehler` ist ein Fehler in der Semantik, also der bedeutung bzw. Logik eures Scripts. Diese Art Fehler ist deutlich schwieriger zu finden als ein Syntaktischer Fehler, da euch kein compiler oder Log darauf hinweist das ein Fehler existiert. Für den Computer ist ein Semantisch Fehlerhaftes Programm einwandfrei, es produziert halt das Falsche Ergebnis. Ein einfaches Beispiel wäre das ihr in einer addition versehentlich ein `-` benutzt habt und dadurch am ende ein Falsches Ergebniss bekommt.
3. Allgemeine technische Fehler
   1. Hierrunter fasse ich einfach mal jede Art von configurations und setup Fehler, ist zwar keine der Typischen Sorten Fehler die man in der Informatik behandelt aber man sollte auch wissen wie man sie findet.

## Fehler finden

Es folgen Anleitungen wie ihr die verschiedenen Arten Fehler am besten finden und beheben könnt

### Syntaktische Fehler

Auch wenn Arma 3 keinen Compiler/Linter von Haus aus hat, ist es doch relativ einfach möglich einen Syntaktischen Fehler in Arma zu finden.

#### RPT-Log

Immer wenn ein Syntaktischer Fehler auftaucht, der dazu führt das ein Script nicht ausgeführt werden kann, loggt arma das in den RPT-Log (so wird das Ding normalerweise genannt).

Ihr findet ihn normalerweise unter `C:\Users\bene\AppData\Local\Arma 3`, die Datei heißt z.B. `Arma3_x64_2017-04-13_17-35-11.rpt`.

#### -showScriptErrors

#### Mikeros/Armake/...

### Semantische Fehler

Ein semantischer Fehler ist schwer zu finden, da Arma aktuell noch nicht über einen wirklich guten Debugger verfügt müsst ihr euch `hint`, `diag_log` und `systemChat` bedienen um euch Werte ausgeben zu lassen.

Dann müsst ihr Stück für stück durch euer Script (bzw. auch eine Reihe von Scripten) Ausgaben einfügen und schaun an welcher Stelle der Fehler auftritt bzw. andere Werte entstehen als ihr erwartet.

Beispiel:

```javascript
_test_old = [];
_test = [1,2,3,4];
_test_old = _test;
{
    _test set[_forEachIndex, (_x + 1)];
}forEach(_test)
hint format["%1",_test_old];
```

Was meint ihr ist der Wert von `_test_old` ist hier in der letzen Zeile ?
```javascript
_test_old = [];
systemChat format["%1", _test_old];
_test = [1,2,3,4];
_test_old = _test;
systemChat format["%1", _test_old];
{
    _test set[_forEachIndex, (_x + 1)];
  	systemChat format["%1", _test_old];
}forEach(_test)
hint format["%1",_test_old];	
```

Führt die Scripte einfach mal aus und schaut ob ihr selber auf die Lösung kommt.

Es ist `[5,6,6,8]` ! Das liegt daran das ein Array in Arma per Call-by-referenz (einfach gesagt Pointer) gespeichert wird.

Stellt euch jetzt vor das ganze ist in einem komplizierten Script in dem mit mehreren Arrays gearbeitet und Werte geändert werden.

### Allgemeine technische Fehler

Hier sind vor allem Fehler mit `extDB` relevant. Um einen Fehler mit extDB zu finden hilft es meist einen blick in die Logs von extDB zu werfen, diese findet ihr unter `@extDB3\logs\<monat\<tag>\<zeit>.log`.

Es gitb ein paar übliche Fehler:

- `Could not connect` : Wie der Fehler sagt, extDB kann keine Verbindung zur Datenbank herstellen. Das liegt üblicherweise an den Logindaten in der Config oder auch an einer Firewall bzw. einer Host-Beschränkung des MySQL Users.
- `Statement Error`: Ein Fehler im Query selber, hier müsst ihr entsprechend der Fehlermeldung euer Query fixen. Dafür bietet es sich das Query mit 'dummy' Werten direkt in einem DB Client (DataGrip, Navicat, PHPMyAdmin) testen.