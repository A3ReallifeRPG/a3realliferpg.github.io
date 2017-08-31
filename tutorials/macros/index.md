# [Tutorial] Macros

In diesem Tutorial möchte ich euch erklären was Macros sind, wofür man sie bentuzen kann und ich werde auch auf kurz auf das CBA Addon Framework bzw. die CBA Macros eingehen.

## Was sind Macros

Macros oder auch [PreProcessor Commands](https://community.bistudio.com/wiki/PreProcessor_Commands) sind stücke von text die definiert werden und welche die Arma 3 Engine vor dem ausführen eines Scripts bzw. vor dem Parsen einer Config evaluiert und "austauscht".

Das vermutlich simpleste Macro was ihr alle regelmäßig nutzt ist `//`. Findet die Arma Engine beim Parsen einer Config ein `//` so überspringt bzw. löscht es schlicht den rest der Zeile.

> Es ist im Wiki Beitrag nicht richtig Differenziert, aber normalerweise bezeichnet man all die `#` Anweisungen wie `#define`, `#include` als Präprozessor Anweisung (eng. PreProcessor Command) und die Verknüpfungen von Code mit wörtern mithilfe von `#define test hint "Hello World"` als Macro. Wenn ihr schon mal c programmiert habt wird euch das ganze [bekannt vorkommen](https://gcc.gnu.org/onlinedocs/cpp/Macros.html).

## Wofür brauche ich Macros

Prinzipiell braucht man gar keine Macros, sie können einem das Leben jedoch auf verschiedene Arten vereinfachen:

- Variablen (oder besser Konstanten) in Configs: In einer Config Datei können keine Variablen benutzt werden, möchte man aber dennoch den gleichen Wert an mehreren Stellen nutzen und gleichzeitig in der Lage sein in auf ein mal überall zu ändern kann man ein macro nutzen
- "Verschönerung" des Codes: Hier spalten sich die Meinungen, aber Prinzipiell ist es möglich durch Macros den code übersichtlicher zu gestalten bzw. kürzer zu machen.
- "Verstecken" von Code: Macros sind übersichtlich und ihr inhalt kann von z.B. Mikeros gut binalisiert werden, will man also z.B. den wahren Namen einer Varibale verschleiern oder [Code in Code](http://www.underhanded-c.org/) "verstecken" bieten sich Macros an. Wichtig ist hier, das es natürlich nur Sicherheit auf den ersten Blick bietet.

## Macros Nutzen

Anders als bei den verschiedenen Präprozessor Anweisungen die ihr einfach so nutzen könnt weil sie in der Arma Engine definiert sind müsst ihr ein Macro zunächst mit der Anweisung `#define` definieren.

Beispiel:

```javascript
#define hello systemChat format["Hello %1",(name player)];
hello
hello
```

Dieses simple Script definiert das Macro `hello` und ruft es zwei mal auf.

Für die Arma Engine, die Später das Script ausführt sieht das ganze so aus (in der theorie)
```javascript
systemChat format["Hello %1",(name player)];
systemChat format["Hello %1",(name player)];
```

Das Macro ist weg und wurde durch das ersetzt was wir im define angegeben haben.

Ein etwas Sinnvolleres Beispiel:

```javascript
#define LOG(msg) diag_log format["ERROR_TAG : %1",msg];
LOG("Script Start")
// some code
LOG("Script End")
```

In diesem Macro seht ihr auch, das es möglich ist einem Macro Werte zu übergeben.

In wirklichkeit übergebt ih rjedoch keine Werte, nachdem der Präprozessor das Script verarbeitet hat sieht es so aus:

```javascript
diag_log format["ERROR_TAG : %1","Script Start"];
// some code
diag_log format["ERROR_TAG : %1","Script End"];
```

Wenn ihr ein Macro in mehreren Dateien nutzen wollt könnt ihr all eure Macros in eine Datei schreiben und diese Datei mit dem Präprozessor Befehl `#include` in ein Script einbinden, dieser macht nichts anderes als den Gesamten Inhalt der angegebenen Datei an seine Stelle zu kopieren.

Das sind die zwei wichtigsten Anweisungen um Macros zu nutzen, wenn ihr sehen wollt welche weiteren nützlichen Präprozessor Anweisungen es gibt schaut ins [BI Wiki](https://community.bistudio.com/wiki/PreProcessor_Commands).

## CBA Macros

CBA oder [Community Based Addons](https://github.com/CBATeam/CBA_A3) definiert eine Reihe von Regeln und Macros die dazu dienen Funktionen und Variablen so zu definieren das mehrere Mods gleichzeitig ausgeführt werden können ohne das namespace Konflikte entstehen.

Das kann auf den ersten Blick alles recht kompliziert wirken, ist aber wenn man es erstmal verstanden hat relativ simpel.

