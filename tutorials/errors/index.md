# [Tutorial] Fehler finden

In diesem Tutorial möchte ich euch erklären wie ihr einen Fehler in eurer Arma Mission selber finden könnt, ohne das ihr darauf angewiesen Seit euch hilfe von anderen zu holen.

## Arten von Fehlern

Grundsätzlich unterscheidet man in verschiedene Arten von Fehlern

1. Syntaktische Fehler
   1. Bei einem *Syntaktischen Fehler* habt ihr einen Fehler in der Syntax, alo der vorgegeben Schreibweise (ein Rechtschreibfehler ist Beispielsweise ein Syntaktischer Fehler im weitesten Sinne). Ein Syntaktischer Fehler führt dazu das euer Programm (Script) nicht ausgeführt werden kann bzw. einen Fehler wirft.
2. Semantische Fehler
   1. Ein *Semantischer Fehler* ist ein Fehler in der Semantik, also der Bedeutung bzw. Logik eures Scripts. Diese Art Fehler ist deutlich schwieriger zu finden als ein Syntaktischer Fehler, da euch kein compiler oder Log darauf hinweist das ein Fehler existiert. Für den Computer ist ein Semantisch Fehlerhaftes Programm einwandfrei, es produziert halt das Falsche Ergebnis. Ein sehr einfaches Beispiel wäre das ihr in einer addition versehentlich ein `-` benutzt habt und dadurch am ende ein falsches Ergebniss bekommt.
3. Allgemeine technische Fehler
   1. Hierrunter fasse ich einfach mal jede Art von konfigurations und setup Fehler, ist zwar keine der Typischen sorten Fehler die man in der Informatik behandelt aber man sollte auch wissen wie man sie findet.

# Fehler finden

Es folgen Anleitungen wie ihr die verschiedenen Arten Fehler am besten finden und beheben könnt.

## Syntaktische Fehler

Auch wenn Arma 3 keinen Compiler/Linter von Haus aus hat, ist es doch relativ einfach möglich einen Syntaktischen Fehler in Arma zu finden (Beispiele am Ende).

### RPT-Log

Immer wenn ein Syntaktischer Fehler auftaucht, der dazu führt das ein Script nicht ausgeführt werden kann, loggt arma das in den RPT-Log (so wird das Ding normalerweise genannt).

Ihr findet ihn Standardmäßig unter `C:\Users\<username>\AppData\Local\Arma 3`, die Datei heißt z.B. `Arma3_x64_2017-04-13_17-35-11.rpt`.

### -showScriptErrors

Mit dem Startparameter `-showScriptErrors` ist es möglich sich die Fehler in Arma direkt im Spiel anzeigen zu lassen.

Dies ist besonders praktisch um Fehler zu finden die man zunächst nicht bemerkt, da es sehr leicht ist einen Fehler im RPT-Log zu übersehen.

Ich empfehle beim Testen und auch beim Spielen immer `-showScriptErrors` zu aktivieren, da ihr so immer sofort merkt wenn etwas nicht funktioniert.

### Mikeros/Armake/...

Sollte der RPT und `-showScriptErrors` nicht genug sein, könnt ihr einen Sogenannten [Linter](https://de.wikipedia.org/wiki/Lint_(Programmierwerkzeug)) benutzen.

Hiervon gibt es mehrere für Arma 3, am häufigsten wird [Mikeros](https://community.bistudio.com/wiki/Mikero_Tools) genutzt.

Mit Mikeros (und anderen Lintern/Tools dieser art) könnt ihr nicht nur eure Mission in eine PBO packen und sie gegebenenfalls auch Binalisieren und/oder obfuscaten, ihr könnt auch eine Statische Codeanalyse durchführen.

Diese zeigt euch dann an, wenn ihr in Dateien z.B. ein Komma vergessen oder einen include falsch gesetzt habt.

---

Egal ob ein Linter, der RPT-Log oder `-showScriptErrors`, jede Möglichkeit gibt euch Informationen zu den Fehlern die ihr gemacht habt die ihr sorgsam lesen und verstehen müsst, im Folgenden habe ich ein paar Beispiele zu Fehlermeldungen und was sie bedeuten.

### Beispiel 1

> TODO Screenshot + Beispiel RPT-Log

### Beispiel 2

> TODO Screenshot + Beispiel RPT-Log

### Beispiel 3

> TODO Screenshot + Beispiel RPT-Log

## Semantische Fehler

Ein semantischer Fehler ist schwer, da er keinen Error im Sinne der Syntaktischen Fehler verursacht der euch von irgendeinem Linter oder Programm angezeigt werden kann. Da Arma aktuell noch nicht über einen wirklich guten Debugger verfügt*, müsst ihr euch `hint`, `diag_log` und `systemChat` abfinden um euch Werte ausgeben zu lassen und so den ablauf eures Scripts von Anfang bis ende verfolgen (ggf. müsst ihr das auch über mehrere Scripte hinweg tun).

### Beispiel 1

Ihr wollt in einem hint etwas anzeigen was ihr als Parameter an die Funktion übergebt

```javascript
params [
  ["_sender","",[""]],
  ["_msg","",[""]]
];

if !(_msg isEqualTo "") exitWith {}; //check if msg is empty
hint format["New msg from %1 : %2",_sender,_msg]; //print sender and msg
```

Ihr bekommt keine Ausgabe! Wieso ? Zum testen fügt ihr folgende Ausgaben hinzu:

```javascript
params [
  ["_sender","",[""]],
  ["_msg","",[""]]
];
systemChat "Script Start";
if !(_msg isEqualTo "") exitWith {}; //check if msg is empty
systemChat "Condition passed";
hint format["New msg from %1 : %2",_sender,_msg]; //print sender and msg
systemChat "Script End";
```

Ihr werdet sehen das euer System Chat folgends ausgibt:

> Script Start

Jetzt wisst ihr das das Script nur bis zur Bedingung läuft und stellt fest: Die Bedinung ist fälschlicherweise mit einem `!` negiert.

Gut das war jetzt sehr einfach, aber mit diesem generellen vorgehen könnt ihr belibig komplizierte Scripte "debuggen" und Semantische Fehler finden.

Weil es so schön war gleich noch ein Beispiel

### Beispiel 2

Wir wollen im Array `_test` jeden Wert um 1 erhöhen, vorher aber eine Kopie von `_test` in `_test_old` machen.

```javascript
_test_old = []; // initialize _test_old
_test = [1,2,3,4]; // initialize _test
_test_old = _test; // save _test in _test_old
{
    _test set[_forEachIndex, (_x + 1)]; // increment each value in _test by 1
} forEach(_test)
hint format["%1",_test_old]; // print _test_old
```

Was meint ihr ist der Wert von `_test_old` hier in der letzen Zeile ?
```javascript
_test_old = []; // initialize _test_old
systemChat format["%1", _test_old];
_test = [1,2,3,4]; // initialize _test
_test_old = _test; // save _test in _test_old
systemChat format["%1", _test_old];
{
    _test set[_forEachIndex, (_x + 1)]; // increment each value in _test by 1
  	systemChat format["%1", _test_old];
}forEach(_test)
hint format["%1",_test_old]; // print _test_old
```

Führt die Scripte einfach mal aus und schaut ob ihr selber auf die Lösung kommt.

`_test_old` ist `[5,6,6,8]`

Das liegt daran das ein Array in Arma per Call-by-referenz (einfach gesagt Pointer) übergeben/gespeichert wird (mehr dazu im [Wiki](https://community.bistudio.com/wiki/Array)).

Um tatsächlich den alten Wert von `_test` in `_test_old` zu speichern müssten wir `_test_old = +_test` machen.

Dieses Beispiel ist wieder vergleichsweise einfach, aber stellt euch z.B. vor ihr macht ein Marktsystem und habt da verschiedene Arrays die plötzlich einfach Falsche Werte haben. Hier hilft euch nichts anderes als das (oder die) Script(e) stück für Stück mit der Beschriebene Methode durch zu gehen und zu prüfen was tatsächlich passiert.

Natürlich müsst ihr nicht zwangsläufig in jeder Zeile eine Ausgabe sezten, häufig ist es gut den Fehler erst auf einen Groben Bereich zu begrenzen und dann genauer zu gucken.

## Allgemeine technische Fehler

Hier sind vor allem Fehler mit `extDB` relevant. Um einen Fehler mit extDB zu finden hilft meist einen blick in die Logs, diese findet ihr im Normalfall unter `<arma path>\@extDB3\logs\<monat\<tag>\<zeit>.log`.

Es gitb ein paar übliche Fehler:

- `Could not connect` : Wie der Fehler sagt, extDB kann keine Verbindung zur Datenbank herstellen. Das liegt üblicherweise an den Logindaten in der Config oder auch an einer Firewall bzw. einer Host-Beschränkung des MySQL Users.
- `Statement Error`: Ein Fehler im Query selber, hier müsst ihr entsprechend der Fehlermeldung euer Query fixen. Dafür bietet es sich das Query mit 'dummy' Werten direkt in einem DB Client (DataGrip, Navicat, PHPMyAdmin) testen.
- `Invalid number of Inputs`: Wenn ihr SQL_Custom nutzt (was ich empfehle), müsst ihr angeben wie viele Inputs und Outputs euer query hat, verzählt ihr euch dabei bekommt ihr den genannten Fehler

Ein paar übliche Fehler bei Servern sind:

- Falsche Arma Version
- Addons nicht richtig installiert/gestartet (life_server, extDB, o.ä.)
- Firewall nicht richtig konfiguriert
- Bei `extDB` vergessen die <u>richitigen</u> C++ Redistributables zu installieren

---

\* Es ist ein Tool in Entwicklung welches Debugging in Arma verbessern soll [ArmA.Studio](https://github.com/ArmA-Studio/ArmA.Studio)