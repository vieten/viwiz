Ein einfacher VIM Spickzettel.

Responsive
Einfach

Kannste so machen ist aber kacke.

TODO

1) Den Style bitte besser semantisch aufbauen.

So ist es bisher:
            <div class="row-fluid">
                <div class="span3">zc</div>
                <div class="span3">Aktuelle Faltungen schließen.</div>
            </div>

Besser wäre jedoch:
            <div class="zweispalt">
                <div>zc</div>
                <div>Aktuelle Faltungen schließen.</div>
            </div>

Die Klasse Zweispalt definiert den Vater. Die Styles der Unterelemente ergeben
sich in Abhängigkeit zum Vaterelement.


2) Beim ersten Aufruf der Seite soll alles zusammengeklappt sein.


Some changes to test new github key.
