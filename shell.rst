Shell in Schnell
----------------

.

-----

Diese Folien: https://spline-fu.github.io/shellkurs/

Erstellt von bngs, cent, jrt
Adaption der Arbeit von: Lusy, Yves, Philipp, Alex, Marian, Marco

----

Warum?
------
Beispiele:

Welches Unterverzeichnis braucht den meisten Platz?

::

    $ du -s -h * | sort -h | tail -n 100

Gib alle Wörter einer Datei und ihre Häufigkeiten aus

::

    $ wget -q -O- http://discoproject.org/media/text/chekhov.txt 
        | tr -sc "A-Za-z" "\n" | sort | uniq -ic | sort -n

----

Warum CLI statt GUI?
--------------------

- Die graphische Oberfläche (GUI) ist explorativ, aber nicht effizient
- Das Terminal (CLI) ist effizienter, wenn man weiß was man will
- Terminaleingaben sind leicht automatisierbar und wiederholbar

----

Was kann ich damit alles machen?
--------------------------------

* Im Dateisystem navigieren
* Verzeichnisse/Dateien erstellen/löschen/kopieren
* Programme starten
* Einfache (oder auch kompliziertere) Operationen auf Texten ausführen
* Quelltext Versions Verwaltung (git,...)
* und vieles mehr. (eigentlich alles.)

----


Wie öffne ich ein Terminal?
---------------------------

Mehrere Alternativen:

* LINUX: Terminalemulator starten (terminal, gnome terminal oder konsole)
* LINUX: Super bzw. Meta (Windows-Taste), anfangen "Terminal" zu schreiben und enter drücken
* WINDOWS: PowerShell (ssh zedatnutzer@andorra.imp.fu-berlin.de)
* Mobilgeräte: Nur wenn es nicht anders geht!
* ANDROID: Termux (via F-Droid) (pkg install openssh && ssh zedatnutzer@andorra.imp.fu-berlin.de)
* iPhone/iPad: Termius

-----

Windows
-------

In modernen Versionen von Windows ist SSH enthalten, jedoch kein sinnvolles Terminal. Um ein sinnvolles Terminal zu erhalten, öffnet eine Eingabeaufforderung (cmd.exe) und gebt den folgenden Befehl ein:

::

    winget install --id Microsoft.WindowsTerminal

Alternativ könnt ihr auch die `Anleitung der Zedat <http://www.zedat.fu-berlin.de/tip4u_03.pdf>`_ folgen, jedoch müsst ihr bei Rechnername ``andorra.imp.fu-berlin.de`` angeben.

----

Wie beende ich die Shell?
-------------------------

Mehrere Alternativen:

* Fenster (Terminalemulator) schließen
* [Strg]-[d] beendet Shell
* Eingabe von exit

----

Der erste Befehl
----------------

::

    $ echo "Hallo Welt"
    
----

Aufbau eines Befehls
--------------------

::

    $ programm -f --flag argument1 argument2

----

Befehle mit Parametern
----------------------
Parameter werden benutzt, um Kommandozeilen-Programme zusätzliche Informationen mitzugeben (z.B. Namen von Dateien/Ordnern, mit denen ein Programm arbeiten soll).

::

    $ ls
    $ ls /usr

----

Befehle mit Optionen/Flags
--------------------------

Optionen/Flags verändern die Arbeitsweise von Programmen. Zum Beispiel welche oder wie viele Informationen sie ausgeben.

::

    $ ls -l -h -a
    $ python -i datei.py

Die meisten Optionen gibt es in einer langen und einer kurzen Version. Kurze haben ein ``-`` und einen Buchstaben, lange fangen mit zwei ``--`` an:

::

    $ ls --all
    $ ls -a

Kurze Optionen können kombiniert werden:

::

    $ ls -lha

----

Optionen mit Parametern
-----------------------

Es gibt Optionen, die stehen nicht für sich, sondern erwarten noch einen Parameter:

::

    $ ls -lh --ignore 'foo.pdf'
    $ ls -lh foo.pdf

Achtet darauf, was zur Option gehört und was ein allgemeiner Parameter ist:

::

    $ ls -lh --ignore 'foo.pdf' /


----

Eingabehilfen: Wildcards
------------------------

Wir können die Eingabe verkürzen:

* ``*`` ersetzt beliebig viele Zeichen (auch null!)
* ``?`` ersetzt genau ein Zeichen

::

    $ touch foo bar brr foobar
    $ ls fo*
    $ ls b?r
    $ ls *

Diese Wildcards werden direkt von der Shell interpretiert, das heißt, sie funktionieren mit jedem Programm. Das Programm kriegt davon gar nichts mit. Wollen wir das nicht, müssen wir Anführungszeichen benutzen.

::

    $ echo fo*
    $ echo 'fo*'

----

Eingabehilfen: History
----------------------

Die Shell speichert eure Eingaben. Mit "Pfeil nach oben" könnt ihr zuvor eingegebene Befehle wieder zurückholen, ggf verändern und nochmal ausführen.

Mit [Strg]-[r] könnt ihr in der History suchen. Dann:

* Weiteres drücken von [Strg]-[r] sucht weiter. (Neuere Eingaben zuerst, dann ältere.)
* Durch Enter könnt ihr den gefundenen Befehl direkt ausführen
* Durch links/rechts könnt ihr den gefundenen Befehl bearbeiten

----

Navigation im Dateisystem
-------------------------

Augen auf:

::

    $ ls
    $ ls -lh
    $ ls -la
    
----

Linux-Verzeichnisstruktur
-------------------------

::

    /    # Wurzel, alle anderen Verzeichnisse hängen dadrunter
        /bin    # grundlegende ausführbare Dateien
        /lib    # grundlegende Bibliotheken
        /usr    # statische Resourcen
            /usr/bin    # alle anderen Programme
            /usr/lib    # alle anderen Bibliotheken
        /boot    # alles, was zum Starten des Kernels benötigt wird
        /var     # veränderliche Daten
            /var/lib    # Daten von Programmen, die zur Laufzeit gebraucht werden
            /var/log    # Log-Dateien
        /media    # Alle eingebundenen Datenträger
        /tmp      # Temporäre Dateien
        /run      # Temporäre Dateien für die Kommunikation zwischen Programmen
        /home     # Home-Verzeichnisse der Benutzer
        /proc     # Pseudo-Dateisystem zum Auslesen von Systemdaten
        /sys      # Pseudo-Dateisystem zur Kommunikation mit dem Kernel
        /dev      # Pseudo-Dateisystem zum Zugriff auf Geräte
        /root     # Home-Verzeichnis vom root-Benutzer
        /etc      # systemweite Konfigurationsdateien



----

Verzeichnisse wechseln
----------------------

::

    $ cd /tmp   
    $ cd ~      # ins home directory wechseln
    $ cd        # auch 
    $ cd ..     # ins darüberliegende Verzechnis wechseln
    $ cd -      # ins letzte Verzeichnis wechseln
    $ pwd       # zeigt wo wir sind
    /home/...

~ = $HOME = /home/nutzername

Den Weg zu einem Ordner oder Datei bezeichnen wir als Pfad.
Pfade können immer absolut oder relativ (heißt: in Abhängigkeit vom aktuellen Ordner) angegeben werden.

Folgende Beispiele zeigen immer auf den selben Ordner (wenn wir uns in /dev befinden):
::

    $ pwd
    $ ls /dev/fd # absoluter Pfad
    $ ls fd # relativer Pfad
    $ ls ../dev/fd # auch relativ (.. ist der Eltern-Ordner)


----

Hilfe zur Selbsthilfe
---------------------

Beschreibt was ein Befehl tut, die möglichen Optionen und Parameter, und gibt Hinweise zu verwandten Befehlen:

::

    $ man <Befehlname> 
    $ man man

Mit ``q`` kommt man zurück zur Shell.

Meistens geht auch:

::

    $ <befehl> --help
    $ <befehl> -h

Manchmal Befehl ohne Argumente

----

Operationen auf Dateien
-----------------------

::

    $ cat >> somefile.txt                # beenden mit strg-d
    $ cp somefile.txt otherfile.txt     # copy
    $ mv otherfile.txt anotherfile.txt  # move
    $ rm somefile.txt anotherfile.txt   # remove


----

Operationen auf Ordner
----------------------

Geht auch alles (so ähnlich) auf Ordner:

::

    $ mkdir aFolder           # make directory
    $ cp -r aFolder bFolder   # copy
    $ mv aFolder cFolder      # move
    $ rm -r cFolder           # löscht alles was drin ist

----

Eingabehilfen: Tabcompletion
----------------------------

Schreib die Hälfte eines Befehls oder Dateinamens und drück [TAB] aka Tabulatortaste.

.. image:: https://spline-fu.github.io/shellkurs/tab.jpg

----

Programme starten
-----------------
Aus der Shell kann man Programme, die in der Shell laufen, starten:

::

    $ python3
    >>> 3+5
    8

(man kann die Pythonshell durch drücken von [Strg]-[d] wieder beenden)

Oder auch Programme, die eine graphische Oberfläche haben:

::

    $ gedit

Wenn man ein Programm in seinem Terminal am Laufen hat, kann man in diesem Terminal erstmal nichts weiteres machen. Er ist wieder frei, erst nachdem das Programm beendet wird.

Die Eingabe:

::

     $ gedit &

startet gedit im Hintergrund, das heißt die Shell steht weiter bereit, um weitere Befehle auszuführen.

----

Werkzeuge für Umgang mit Texten
-------------------------------

In eine Datei schreiben (Umleitungen: später)

::

    $ echo bla bla bla >> bullshit.txt
    $ cat >> bullshit.txt
    eins
    zwei
    zwei
    ...
    zwölf
    <strg-d>
    $

Inhalt von Datei bullshit.txt zeigen (falls bullshit.txt existiert)

::

    $ cat bullshit.txt
    $ less bullshit.txt # für lange dateien

Anfang von Datei zeigen:

::

    $ head bullshit.txt

Ende von Datei zeigen:

::

    $ tail bullshit.txt

----

Word count
----------

Anzahl von Bytes, Zeichen, Wörtern, Zeilen einer Datei zeigen:

::

    $ wc -c bullshit.txt # bytes
    $ wc -m bullshit.txt # characters
    $ wc -w bullshit.txt # words
    $ wc -l bullshit.txt # lines
    $ wc bullshit.txt # lines words bytes

----

Datei durchsuchen
-----------------

::

    $ grep 'e' bullshit.txt
    $ grep --color 'e' bullshit.txt

Grep ist viel mächtiger, man kann auch die sogenannten regulären Ausdrücke damit verwenden.

::

    $ grep '^e' bullshit.txt
    $ grep 'e.n' bullshit.txt

Mehr zu regulären Ausdrücke gibt es z.b. hier:

* `wikipedia <https://de.wikipedia.org/wiki/Regul%C3%A4rer_Ausdruck>`_
* `regular-expressions.info <http://www.regular-expressions.info/>`_

… oder einfach nächstes Semester :)

**Achtung:** Reguläre Ausdrücke sind *nicht* das selbe wie die Shell-Wildcards (``*.pdf`` etc). Wildcards können nur recht wenig, sind dafür einfach zu benutzen; reguläre Ausdrücke sind wesentlich mächtiger, aber auch komplexer.

----

Nach Dateien suchen
-------------------

::

    $ find -name bullshit.txt
    $ find /bin -name '*dir'
    $ find -name desktop
    $ find -name Desktop
    $ find -iname desktop # case insensitive


----

Pipes
-----

Statt Dateien oder Zeichenketten als Argumente anzugeben, können wir auch die Ausgabe eines anderen Befehls als Eingabe verwenden. Dazu brauchen wir die Pipe ``|``.

.. image:: https://spline-fu.github.io/shellkurs/pipe.jpg


::

    $ ps -A | grep -i terminal
    $ ls /usr/bin | grep haskell
    $ sort bullshit.txt | tr ' ' '\n' | uniq -c

----

Umleitungen
-----------

Ähnlich wie Pipes funktionieren die Umleitungen ``<``, ``>`` und ``>>``. Nur das sie nicht zwischen Befehlen sondern zwischen Befehlen und Dateien umleiten.

::

    $ echo -e 'Schreibe diesen\nText in eine Datei' > datei.txt
    $ cowsay < datei.txt
    $ echo -e 'Überschreibe den alten Inhalt' > datei.txt
    $ echo -e 'Hänge was an die Datei an' >> datei.txt
    $ cat datei.txt
    $ sort < datei.txt > sortiert.txt

Achtung: Dinge wie ``sort < datei.txt > datei.txt`` funktionieren nicht! Die Datei wird geleert (aufgrund des ``>``), bevor ``sort`` anfängt zu lesen, d.h. es gibt nichts aus und der Inhalt ist weg. Abhilfe schafft z.B. ``sponge`` (siehe ``man sponge``).

----

Auf anderen Rechnern arbeiten
-----------------------------

Shell auf einem entfernten Rechner öffnen:

::

    $ ssh <username>@andorra.imp.fu-berlin.de

Dateien auf einen bzw. von einem anderen Rechner kopieren:

::

    $ date > DATEINAME
    $ scp DATEINAME <username>@andorra.imp.fu-berlin.de:/tmp
    $ scp <username>@andorra.imp.fu-berlin.de:/tmp/DATEINAME DATEINAME_2

Befehl auf einem anderen Rechner ausführen, z.B. rm:

::

    $ ssh andorra rm /tmp/DATEINAME

ssh fungiert auch als pipe zwischen den Rechnern

::

    cat file.pdf | ssh <username>@andorra.imp.fu-berlin.de lp -

----


Nützliche Befehle: less
-----------------------

Damit kann man eine längere Datei oder Ausgabe eines Befehls besser handhaben.

::

    $ less grossedatei.txt
    $ wget -qO- http://discoproject.org/media/text/chekhov.txt | less
    $ ls -lh /usr/bin | less

* mit ``/`` kann man suchen, mit ``n`` weitersuchen
* mit ``q`` kommt man wieder raus
* es kann noch mehr: ``h`` zeigt die Hilfe an

----

Nützliche Befehle: file
-----------------------

Rät, um was für eine Art von Datei es sich handelt.

::

    $ file ~
    $ file ~/.bashrc
    $ file /bin/bash
    $ file /usr/share/zim/zim.png

----

Nützliche Befehle: diff
-----------------------

Zeigt Unterschiede zwischen Dateien an. Sehr nützlich auch für Code.

Man kann sich die Unterschiede auch in einem maschinenlesbaren Format ausgeben lassen. Dann kann man mit dem Programm ``patch`` automatisiert die selben Änderungen an einer anderen Datei durchführen lassen. Ganz besonders nützlich für Code.

----


Rechte
------

Für jede Datei kann man einstellen, welche Zugriffsrechte für sie gelten.

::

    $ ls -lh shellkurs/bullshit.txt 
    -rwxr-xr-x 1 root   root     953K Sep 25 21:49 /bin/bash
    -rw-r--r-- 1 sigler students   77 Oct  6 20:29 shellkurs/bullshit.txt
     ^^^         ^^^^^^                - user (Besitzer*in der Datei)
        ^^^             ^^^^^^^^       - group (Gruppe der Datei)
           ^^^                         - others (alle anderen)

Dabei steht das ``r`` für Leserechte, das ``w`` für Schreibrechte für die jeweilige Personengruppe.

Das ``x`` (execute) steht für Ausführungsrechte (bei Dateien), bei Verzeichnissen ist dieses Recht nötig, um *irgendwas* innerhalb des betroffenen Verzeichnisses tun zu dürfen (unabhängig von den individuellen Rechten der dort liegenden Dateien/Unterverzeichnisse)

Man kann diese Rechte ändern:

::

    $ chmod o-rwx   # others gar nichts mehr erlauben
    $ chmod o=      # ebenso
    $ chmod g+r     # group das Lesen erlauben       ⎱ schon bestehende Rechte
    $ chmod ugo+x   # allen das Ausführen erlauben   ⎰ bleiben erhalten
    $ chmod a+x     # ebenso

----

Eingabehilfen: Tastenkombinationen
----------------------------------

* ``Strg-U`` löscht bis zum Anfang der Zeile
* ``Strg-K`` löscht bis zum Ende der Zeile
* ``Strg-W`` löscht das letzte Wort
* ``Strg-Y`` fügt das zuletzt gelöschte ein
* ``Strg-T`` tauscht die letzten beiden Zeichen

----

Ausblick: Anpassung der Shell
-----------------------------

Man kann sich einen Alias für viel genutzte Befehle erstellen:

::

    $ alias ll='ls -lh'
    $ alias grep='grep --color'

(Am besten in die ``~/.bashrc`` eintragen)

Man kann den Prompt (das ``name@computer:~$``) anpassen und alle möglichen Informationen reintun, die man für sinnvoll hält.

Man kann eine andere Shell als die bash benutzen (viele schwören zum Beispiel auf die zsh).

Man kann bestimmten Tastenkombinationen alles mögliche zuweisen.

Und vieles mehr...

----

Noch Fragen?
------------

Ihr könnt gerne jederzeit im Spline-Raum (Raum K60) vorbeikommen, die meisten Menschen dort kennen sich recht gut mit der Shell aus. Während des Semesters ist den Nachmittag über meistens jemand da.

----

Links
-----

* Learning the shell: https://web.archive.org/web/20161001014753/http://linuxcommand.org/learning_the_shell.php
* Teaching Unix: http://www.ee.surrey.ac.uk/Teaching/Unix/
* Learning Unix in 10 Minutes: https://web.archive.org/web/20160727225944/http://freeengineer.org/learnUNIXin10minutes.html


----

Diese Präsentation wurde erstellt mit darkslide

::
    
    git clone https://gitlab.spline.inf.fu-berlin.de/spline/talks/shellkurs.git && cd shellkurs
    darkslide -i shell.rst -d shell.html
    scp shell.html fob:public_html/webroot/shell.html

Diese Präsentations steht unter `cc-by-sa <http://creativecommons.org/licenses/by-sa/3.0/de/>`_ Lizenz. Autor_innen siehe erste Folie.
