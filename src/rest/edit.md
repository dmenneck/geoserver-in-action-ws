Katalogeinträge editieren
=========================

Neben dem Hinzufügen von Katalogressourcen ist das Editieren bestehender Ressourcen
der häufigste Anwendungsfall in der Administration des GeoServers. Selbstverständlich
kann uns auch hier die REST-API bei wiederkehrenden Prozeduren zur Seite stehen.
Als Beispiel werden wir mit dem folgenden cURL das standardmäßige Ausgabeprojektionssystem
des Layers `states_provinces` zu EPSG:54029 ändern:

```bash
curl \
  -v \
  -u admin:geoserver \
  -XPUT \
  -H "Content-type: application/xml" \
  -d "<featureType>
        <enabled>true</enabled>
        <srs>EPSG:54029</srs>
        <projectionPolicy>REPROJECT_TO_DECLARED</projectionPolicy>
      </featureType>" \
  http://localhost:8082/geoserver/rest/workspaces/fossgis/datastores/natural_earth/featuretypes/states_provinces
```

Nachdem dieser Schritt mit `HTTP/1.1 200 OK` bestätigt wurde, können wir anschließend
automatisch über REST die neue native Bounding Box des Layers mit dem Parameter
`recalculate=nativebbox,latlonbbox` berechnen lassen:

```bash
curl \
  -v \
  -u admin:geoserver \
  -XPUT \
  -H "Content-type: application/xml" \
  -d "<featureType>
        <enabled>true</enabled>
      </featureType>" \
  http://localhost:8082/geoserver/rest/workspaces/fossgis/datastores/natural_earth/featuretypes/states_provinces?recalculate=nativebbox,latlonbbox
```

Betrachten wir nun den Layer in der Layerübersicht des GeoServers (![layer\_icon](../assets/gui3.png))
sehen wir, dass der Layer - wie zu erwarten - mit dem angegebenen Koordinatensystem
EPSG:54029 und einer Bounding Box im entsprechenden Koordinatensystem konfiguriert
ist:

![Ausschnitt der Layerkonfiguration states_provinces im nativen Koordinatensystem EPSG:54029](../assets/edit1.png)

Das Ergebnis unserer Änderung können wir uns abschließend über die GeoServer Layervorschau (![layer\_preview\_icon](../assets/gui1.png)) anschaulich illustrieren lassen:

![Layer states_provinces mit zugehörigem Stil in EPSG:54029](../assets/edit2.png)

**Wichtiger Hinweis**: Das REST-Paradigma beschreibt, dass Repräsentationen (hier
    in den Formaten `XML` und `JSON`) sowohl gelesen als auch geschrieben werden
    können. Dies bedeutet, dass jede XML-Antwort (siehe z.B. [Layer anlegen](create.md))
    in der obigen Form abgeändert (z.B. mit neuem Layernamen oder als deaktiviert
        markiert) und direkt über die REST-API an den Server gesendet werden kann.

Nachdem wir bestehende Ressourcen editiert haben, wird das [letzte Kapitel](delete.md)
dieses Moduls erläutern, wie Sie Ressourcen entfernen können.
