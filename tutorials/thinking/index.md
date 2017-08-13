# Selber Denken

In diesem Tutorial möchte ich euch erklären wie ihr lernt, selber zu denken.

Klingt jetzt erstmal abstrakt und etwas ungreifbar, aber ich hoffe das ihr mit diesem Tutorial lernt wie ihr an einen Fehler oder ein Problem herran geht um es zu lösen.



Keine Sorge, ich probiere das ganze so unlangeweilig wie möglich zu halten. Wer keine Lust auf die Einleitung hat kann gerne bis zum Beispiel runter scrollen, aber gerade für die Art Leute die keine Lust haben zu lesen (gehöre ich auch zu) könnte dieses Tutorial sehr hilfreich sein, also nehmt euch die 10-20 min). 

### Wofür Selber Denken

Ohne selber zu Denken werdet ihr (höchstwahrscheinlich) keinen Erfolgreichen Arma Server aufziehen können. 

Ich persöhnlich bin nicht so aktiv in gängigen Hilfeforen, aber was man so beim Überfliegen der verschiedenen Fragen sieht ist doch immer das gleiche: Simple Fragen die mit etwas analytischem denken und überlegen einfach zu lösen sind. 

Wir haben auch immer mal wieder Menschen die zu uns auf den TS kommen und uns Fragen stellen, z.B.: *"Wie kann man ACE Items in den Shops kaufen"* oder *"Woher kann ich mir am besten Mods nehmen/klauen ?"* (sie sagen vielleicht nicht direkt klauen aber sie meinen es).

Grundsätzlich helfe ich diesen Leuten sehr gerne und ich freue mich auch immer wenn ich sehe wie viele Leute in Foren die "Simplen Fragen" beantworten um der Community zu helfen, ABER was viele Leute bei all diesen Tutorials und Hilfestellungen vergessen ist selber zu denken. 

Wenn mich jemand fragt "Wie kann man ACE Items im Shop kaufen", dann sage ich ihnen nicht welche Zeile an der `fn_handleInv.sqf` sie ändern müssen, sondern ich probiere ihnen zu erklären wie sie selber heraus finden können welche Zeile sie ändern müssen und damit auch wie sie an zukünftige Probleme heran gehen können.

Hier Spaltet sich die Community: 

1. gibt es die Menschen die Probieren wollen ihr Problem zu verstehen und es sinnvoll zu lösen
2. Die Leute die so tun als wollten sie es verstehen am ende aber doch nur die Lösung haben wollen
3. und zu guter letzt die die keine Lust haben sich irgendeine Erklärung an zu hören und nur wissen wollen welche Zeile sie ändern müssen. 

Die Menschen der Kategorien 2 und 3 können und wollen nicht selber Denken, sie wollen eine Frage stellen und eine Antwort bekommen und wenn die Antwort nicht funktioniert dann wollen sie erklärt haben warum sie nicht funktioniert (bzw. einen neuen Lösungsvorschlang bekommen) anstatt selber zu verstehen was das Problem ist und darin sehe ich einen der größten Gründe für das scheitern vieler Arma Server.

Jetzt zum Tutorial: Ich möchte euch jetzt an einem Beispiel erklären wie ihr lernen könnt selber zu denken, wie ihr Scripte verstehen und selber auf die Lösung eines Problems kommen könnt oder zumindest eure Fragen so stellen könnt das ihr etwas daraus lernt. Auch ist das hier ein Appell an all die, die Fragen beantworten dies so zu tun das die Fragesteller dazu angeregt werden etwas dabei zu lernen. 

Das Beispiel ist so geschrieben wie ein möglicher Denkprozess beim Lösen eines Problems ablaufen **kann**, los gehts:

## Beispiel

Ein ganz einfaches Beispiel

> "Wie mache ich ein Schild (Objekt) um Spieler mit ACE zu heilen ?"

Ich werde das ganze jetzt so beschreiben, das ich möglichst die Gedankengänge niederschreibe die ihr euch so machen könntet.

---

Ich denke mir ok, es geht um schaden, auf englisch ist das damage (zur not hilft [translate.google.com](https://translate.google.com))

Ich tippe also in google ein "Arma 3 set damage" weil ich möchte ja den schaden setzen und ich finde den [Wiki Eintrag für setDamage]( https://community.bistudio.com/wiki/setDamage) 

Ich gehe also in mein Spiel, fahre gegen eine Wand und nutze den Befehl um mich zu Heilen und stelle fest: geht nicht !

Gut diesen ersten Schritt hätte man sich natürlich sparen können wenn man in das ursprüngliche Heil Script geschaut hätte und gesehen hätte das das da ja schon so ist und nicht geht. 

> Was mache ich jetzt ? 

Das Problem besteht seit wir ACE installiert haben, also hängt es vermutlich damit zusammen, also schauen wir uns mal ACE an.

> Wie macht man das ? 

Auch hier ist wieder google unser freund und wir googeln: `Arma 3 ACE 3` und finden die Website von ACE Hier finden wir den Link zu einem GitHub repository und das ist auch schon eine erste wichtige Erkenntnis:

**Auf GitHub und ähnlichen Seiten wird Code (Scripte) gehostet die man sich dort anschauen kann.**

Man kann natürlich das ganze auch mit den herruntergeladenen PBO's machen aber so ist es einfacher. 

Wer nicht folgen konnte, wir sind jetzt [hier](https://github.com/acemod/ACE3).

Jetzt kommt ein wenig herrum geschaue aber irgendwann stellen wir fest, der eigentliche Teill von ACE befindet sich im Ordner "addons". Dort scrollen wir jetzt einfach mal ein bisschen durch und gucken was da so ist und es springen uns sofort die Folgenden Ordner ins Gesicht: 

![ace_repo](ace_repo.png) 

Wir schauen uns in den Ordner um und finden jeweils einen functions Ordner. Beim Ordner "medical" finden wir davon besonders viele mit namen die so klingen als hätten sie was mit dem Medical system zu tun. Da der Code von ACE sehr gut ist (generell eine Empfehlung: Schaut euch das mal ganz genau an) und in vielen Dateien steht was sie machen, kann man einfach durch gehen und zur not mit Google Übersetzer alles übersetzen was man nicht versteht.

Man findet mehrere Dateien die `FullHeal` im Namen haben, klingt doch schon mal vielversprechend oder ? 

Ihr schaut also durch die Dateien und findet in der 'fnc_treatmentAdvanced_fullHealLocal.sqf' .. wir kommen unserem Ziel also näher.

Jetzt machen wir wieder das womit wir schon angefangen haben: 

> Wir probieren aus ! 

Dafür muss man wissen wie ACE seine Funktionen aufruft weil `[] call life_fnc_treatmentAdvanced_fullHealLocal` wird nicht funktionieren. 

Heraus zu finden wie ACE seine funktionen hat ist tatsächlich gar nicht so einfach (man könnte einfach das CBA macro nutzen aber das geht hier zu weit) aber irgendwann findet ihr ein Beispiel was so aus sieht: `ace_<name des komponenten (siehe bild oben)_fnc_<name der funktion>` Also nehmt ihr den namen des Kompontenen "medical" und die funktion "treatmentAdvanced_fullHealLocal" und kommt auf `ace_medical_fnc_treatmentAdvanced_fullHealLocal` also habt ihr jetzt: `[] call ace_medical_fnc_treatmentAdvanced_fullHealLocal;`

Ihr probiert es aus und: Nichts :/

Ihr schaut euch also das script noch mal an und euch fällt die Zeile auf: `params ["_caller", "_target"];` Offensichtlich müssen an die Funktion Parameter übergeben werden, wir werfen also (falls wir es nicht wissen) caller und target in google translate und denken uns, das target ist das was wir heilen wollen, der caller ist der Medic, in unserem fall also das Schild (eigentlich ist der caller egal aber ...) also sagen wir `[schild,player] call ace_medical_fnc_treatmentAdvanced_fullHealLocal;` oder `[player,player] call ace_medical_fnc_treatmentAdvanced_fullHealLocal;` und siehe da, schon sind wir wieder heile. 

Das ganze jetzt noch schnell in die Krankenhaus Funktion gepackt und Tada es funktioniert. 

 So genug langweiliger Text: nehmt euch euer nächste Problem/Projekt und probiert es zu Lösen, hier noch mal die wichtigsten Tipps

## TIPPS

- Viele Sachen sind so benannt, wie das was sie machen: Lernt daraus, zur not übersetzt es
- Lest guten Code, den findet ihr in den PBO's oder auf seiten wie GitHub, etc. (Stichworte: ACE, CBA)
- Nutzt google und unterteilt euer Problem in viele kleine Probleme die sich lösen lassen
- Nutzt die Ingame Console oder probiert verschiedene Commands und Funktionen aus und guckt was passiert
- Nutzt das Wiki von Bohemia, am besten in kombination mit Google oder einer anderen Suchmaschiene
  - Mit "Arma 3 FunktionXYZ" kommt ihr eigentlich immer zuerst auf den Wiki Artikel
- Wenn ihr Fragt: Lasst euch nicht die Lösung geben sondern erklären wie man auf die Lösung kommt

### Quellen/Links

- Bohemia Wiki: https://community.bistudio.com/wiki/
- ACE 3 Website: https://ace3mod.com/
- ACE 3 GitHub: https://github.com/acemod/ACE3