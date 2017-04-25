# photorename

Benennt Fotos und Videos anhand der EXIF-Daten konsistent um.

Ich nutze hier die Dropbox, um regelmäßig und kontinuierlich Fotos und Videos vom Smartphone auf den Rechner zu bekommen.
Um das Chaos möglichst gering zu halten, erhalten alle Fotos und Videos eine Benennung nach einer Datums-Uhrzeit-Konvention.

Die Bilder und Videos werden entweder direkt verschoben oder nur kopiert - aber auf jeden Fall umbenannt und Bilder nach ~/Bilder/Eingang und Videos nach ~/Videos/Eingang gestellt.

Sollte im Zielverzeichnis schon eine Datei mit dem gleichen Namen vorhanden sein, wird ein incrementell erhöhter Index vor der Dateiendung angehängt.

Damit das automatisch ausgeführt wird, muss incron am System installiert sein.
Als User muss in der incrontab eine Zeile eingefügt werden:

    incrontab -e
    
    /home/jakob/Dropbox/Kamera-Uploads IN_CREATE,IN_CLOSE_WRITE,IN_MOVED_TO /usr/bin/photorename $@/$#

Dies kopiert benennt jedes neue File im Verzeichnis /home/jakob/Dropbox/Kamera-Uploads in die oben genannten Eingangs-Verzeichnisse.
    
    /home/jakob/Dropbox/Kamera-Uploads IN_CREATE,IN_CLOSE_WRITE,IN_MOVED_TO /usr/bin/photorename --move $@/$#

Dies verschiebt und benennt die neuen Files gleich um. Dieser Befehl ist sinnvoll, wenn die Dropbox nicht voll werden soll.



Sollte das Medienformat nicht vom Skript erkannt werden, wird ein Verzeichnis ~/unsortiert erstellt und das File dahin verschoben/kopiert.

Um beim Kopieren Speicherplatz zu sparen, wird die Option --reflink=auto verwendet (sofern es das Filesystem erlaubt)
