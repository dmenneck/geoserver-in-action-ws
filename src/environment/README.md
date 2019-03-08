# Vorarbeiten und generelle Informationen

Bevor wir mit dem Workshop starten können, führen Sie bitte die folgenden Schritte
aus:

* Rechner mit OSGeoLive-Medium hochfahren
* Sprache auswählen (Deutsch für korrekte Tastaturbelegung)
* *Lubuntu ohne Installation ausprobieren* auswählen
* Benutzer: user; Passwort: user (wird vermutlich nicht benötigt)

![Die Startansicht der OSGeo Live {{ book.osGeoLiveVersion }} auf Ihrem Rechner.](../assets/startview.png)

# Setup-Script ausführen

Es gibt ein Skript, welches ihr OSGeoLive-System für diesen Workshop einrichtet.
Das Skript führt die folgenden Aktionen aus:

* Installation des *Build-Management-Tools* Maven (~20MB)
* Deinstallation der INSPIRE-Erweiterung vom GeoServer (wir werden diese Erweiterung
  später mit Maven selbst kompilieren und auf dem GeoServer installieren)
* Download des Quellcodes der INSPIRE-Erweiterung für den GeoServer (~0.03MB)
* Initialisierung eines lokalen Maven-Repositories (dieser Schritt ist nicht
  zwingend nötig, beschleunigt aber die späteren Aufrufe von Maven-Befehlen von
  vielen Minuten auf wenige Sekunden) (~100MB)

**Sollten Sie die OSGeoLive zwischenzeitlich neu starten, müssen Sie das Skript erneut ausführen!**

> **note**
>
> Sie können die Ausführung des Skriptes überspringen, wenn Sie den Abschnitt [Kompilieren auf Basis des Quellcodes](../basics/compilesource.md) **nicht** bearbeiten möchten!

----

> **hint**
>
> Sie können Inhalte aus der Zwischenablage, die sie etwa zuvor mit der
> Tastenkombination STRG + C kopiert haben im Terminal mit der Tastenkombination
> STRG + UMSCHALT + V einfügen! Alternativ können Sie auch einen Rechtsklick in
> das Terminal machen und dort *Einfügen* wählen.

Um das Skript zu starten, führen Sie bitte den folgenden Befehl auf dem Terminal
(![](../assets/terminal_icon.png) im unteren Systempanel) aus und geben bei Aufforderung
das Passwort `user` ein:

<pre><code class="bash">wget -q -O - \
  {{ book.workshopRawSourceBaseUrl }}materials/setup_geoserver_workshop.sh | \
  sudo bash
</code></pre>

**Es kann einen Moment dauern bis das Skript durchgelaufen ist!**

Machen Sie sich währenddessen schonmal mit den Pfaden und Zugangsdaten des GeoServers
vertraut:

## Pfade, URLs und Zugangsdaten

* GeoServer: {{ book.geoServerBaseUrl }} (muss zunächst gestartet werden, siehe unten)
* Zugangsdaten GeoServer:
  * Benutzer: <code>{{ book.geoServerUser }}</code>
  * Passwort: <code>{{ book.geoServerPassword }}</code>
* GeoServer (Dateisystem): <code>{{ book.geoServerPhysicalPath }}</code>

## Überprüfung der Maven-Installation

Sobald das Skript durchgelaufen ist, sollten Sie überprüfen, ob die Maven-Installation
erfolgreich war, indem Sie folgenden Befehl auf dem Terminal ausführen:

```bash
mvn -v
```

Sie sollten folgende Ausgabe erhalten:

![Erfolgreiche Installation von maven.](../assets/mvn_check_version.png)

# Starten des GeoServers

Der GeoServer kann durch einen Doppelklick auf **Start GeoServer** im Ordner
**Web Services** auf dem Desktop der OSGeoLive gestartet werden:

> **note**
>
> Kann der GeoServer **nicht** über den o.g. Weg gestart werden, kann er auch
> über den folgenden Befehl im Terminal gestartet werden:
> ```
> sudo /usr/local/lib/geoserver/bin/startup.sh
> ```
> Das Terminal bzw. der Prozess muss dabei während des Workshops geöffnet bleiben!

![GeoServer starten.](../assets/start_geoserver.png)

![GeoServer-Weboberfläche nach erfolgreichem Start](../assets/geoserver_gui.png)

Im [folgenden Abschnitt](../basics/README.md) werden wir mit GeoServer-Basiswissen fortfahren.
