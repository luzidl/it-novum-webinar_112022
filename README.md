# it-novum Webinar 24. November 2022.  (Work in progress ...)

## Demo Daten und Skripte vom IT Novum Seminar - Graph-Datenbanken: So decken Sie neue Zusammenhänge auf

## Verzeichnisse:

#### Daten: Enthält die aufbereiteten Daten von Govdata.de

#### Quelle der Daten:
- Webseite: [Govdata.de](https://www.govdata.de/) 
- [Windkraftanlagen Schleswig-Holstein Stand 18.08.2022](https://opendata.schleswig-holstein.de/dataset/12fb2027-d2d3-42c9-8774-34a70f584c0f/resource/e47cf6aa-d4eb-4c61-9605-bba859684c13/download/opendata_wka_ib_gv_vb_sh_20220701.csv)
- [Ladesäulen Schleswig-Holstein Stand 1.10.2022](https://opendata.schleswig-holstein.de/dataset/ac7347a6-8011-46b2-97ed-b4816807ef47/resource/a90e6d90-ae46-4b91-997c-c29c9a7b1e71/download/ladesaeulenregister.csv)


#### Datenmodelle: 

Enthält die zwei Datenmodelle die mit [Neo4j Workspace](https://workspace-preview.neo4j.io/workspace/query) erstellt wurden

1. Datenmodell für die Ladesäulen: **neo4j_importer_model_ladesaeulen.json**
2. Datenmodell für die Windräder: **neo4j_importer_model_WindRaeder2.json**

#### Folien des Webinars:
- Hier liegt die PDF Datei mit den gezeigten Folien

---

Zum Nachstellen der im Workshop gezeigte Demo, soll noch folgendes bzgl. der Daten erwähnt werden. 
Die Daten (im Vergleich zu den original Daten govdata.de) mussten noch ein wenig aufbereitet werden, damit sie verwendet werden konnten. Folgende Aufbereitungen wurden durchgeführt:

**1. Ladesäulen Daten:**
  * lsNr hinzugegügt, als eindeutige Id für die Ladesäulen. Damit jede Ladesäule eindeutig identifizierbar ist.

**2. Windkraftanlagen Daten:**
  * Gemeinde in Ort umbenannt, für einfacheres Laden und  zuordnen der Daten 
  * Spaltennamen wurde von Großbuchstaben auf normale Rechtschreibung umbenannt. 
  * Data Cleansing von zusätzlichen Tabs & Zeilenumbrüche in den Daten --> Qualtät der Daten ist schlecht!

Ladet bitte die Dateien mit den Daten und den Datenmodellen auf Euren Rechner herunter, um die Demo nachstellen zu können. Die benötigt ihr dann später, nachdem Ihr Euch eine kostenlose Datenbank angelegt habt.

---

## Aufbau der Graphdatenbank mittels Neo4j Aura free und Neo4j Workspace

Zum Aubau der Demo-Datenbank wird folgendermaßen vorgegangen:

1. Falls noch nicht vorhanden, erstellt man sich eine [Neo4j Aura Free](https://neo4j.com/cloud/platform/aura-graph-database/?ref=get-started-dropdown-cta) Datenbank. Klickt den obigen Link und anschliessend den Button "**Start free**" und meldet Euch für die kostenlose Nutzung an.

2. Nach der Anmeldung, folgt dem Dialog für das Anlegen einer kostenlosen Neo4j Datenbank. Nehmt eine **leeres Datenbank-Template** (Empty Instance) und keines der schon mit Daten geladenen Templates!
<img width="609" alt="Bildschirmfoto 2022-11-21 um 11 28 01" src="https://user-images.githubusercontent.com/8035021/203027751-de1dcc9a-c7e6-4807-9633-da0dd6475bc6.png">

Vergesst anschliessend nicht, Euch das Passwort zu sichern!!! Das benötigt ihr, um Euch in Workspace mit der Datenbank verbinden zu können. Der User Name ist immer **neo4j**!

3. Wenn die leere Neo4j Instance aufgebaut ist, dass sollte in wenigen Sekunden passieren, dann könnt Ihr euch in Workspace an die Datenbank anmelden. Dazu ruft [Workspace](https://workspace-preview.neo4j.io/workspace/import) auf und falls Ihr nicht direkt auf dem Reiter "**Import**" landet, klickt noch auf Import. Workspace hat drei Reiter, "**Explore**", "**Query**" und "**Import**". Damit können wir nun das Datenmodell bauen, dann die Daten laden und auch die Daten analysieren.

<img width="950" alt="Bildschirmfoto 2022-11-21 um 11 43 02" src="https://user-images.githubusercontent.com/8035021/203030936-217ee614-985f-4c89-84ac-a344bdb9f393.png">

4. Bevor wir anfangen können, müsst ihr Euch noch an Eurer Aura Free Datenbank Instanz anmelden. Dazu klickt ihr mittig oben auf "**No Connection**" und dann auf "**Connect**" (im Bild oben).

Im folgenden Dialog benötigt ihr nun den "**Connect String**" und Benutzername plus Password. Das letztere habt ihr ja schon, aber den Connect String müsst Ihr Euch aus der Aura Free Console kopieren wie im nächsten Bild gezeigt.

<img width="306" alt="Bildschirmfoto 2022-11-21 um 11 48 42" src="https://user-images.githubusercontent.com/8035021/203033126-49266cd1-3fbb-4757-be2c-452e1d450f1f.png">

Damit habt ihr alle Infos, um auch mit Workspace an Eurer Aura Free Instanz anmelden zu können. Der Dialog dazu sieht folgendermaßen aus:

<img width="323" alt="Bildschirmfoto 2022-11-21 um 11 49 45" src="https://user-images.githubusercontent.com/8035021/203033340-6ee79317-5584-42db-a125-269ae49ee744.png">


5. Um nun starten zu können, klickt bitte den Reiter "**Import**", falls noch nicht geschehen und ladet die Datei "**ladesaeulenregister_SH_Ids.csv**" per Drag & Drop oder über den "**browse**" Link in den Daten-Importer. Das sieht dann wie folgt aus:

<img width="482" alt="Bildschirmfoto 2022-11-21 um 12 02 26" src="https://user-images.githubusercontent.com/8035021/203034604-14ce31b7-d909-49f6-9069-71d150f47419.png">

6. Nun haben wir das Datenfile geladen. Anschliessend klickt Ihr rechts oben auf die 3 Punkte neben dem Button "Run Import" und wählt "**Open Model**". Im anschliessenden Dialogfenster wählt ihr dann das Datenmodel mit dem Dateiname "**neo4j_importer_model_ladesaeulen.json**" und klickt "**Öffnen**".

<img width="306" alt="Bildschirmfoto 2022-11-21 um 12 04 30" src="https://user-images.githubusercontent.com/8035021/203035025-9f8c708c-4d3d-40b9-bbf0-32d81310d6e4.png">

Nun sehen wir in der Mitte des Fensters unser Datenmodell, was wir aus den Daten im linken Teil des Fensters "gebaut" haben. Wenn wir nun auf z. B. auf den Knoten "**Ort**" klicken, dann sehen wir im rechten Teil des Fensters, die Zuordnung von Daten zum Knoten "Ort" und welche Properties mit Daten gefüllt werden sollen.
Mit dem hier geladen Datenmodell könnt ihr alle Knoten und Kanten (Relationships) auswählen und mal nachvollziehen, wie Diese miteinander verknüpft wurden. **WICHTIG** hierbei ist zu erwähnen, dass man möglichst jeden einzelnen Knoten durch eine Unique-ID oder einen Namen erkennbar machen sollte. Für den Ort haben wir den Namen gewält, für die Ladesäulen die oben erwähnte ID den Rohdaten hinzugefügt!

<img width="1024" alt="Bildschirmfoto 2022-11-21 um 12 08 30" src="https://user-images.githubusercontent.com/8035021/203038286-7067f3ee-4de0-49e7-833f-7472e886ece4.png">

7. Mit einem Klick auf den Button "**Run Import**" können wir nun die Daten importieren. Nach ein paar Sekunden sollte das fertig sein und ein Fenster mit der Information aufgehen, dass alle Daten importiert wurden:

<img width="524" alt="Bildschirmfoto 2022-11-21 um 12 23 56" src="https://user-images.githubusercontent.com/8035021/203038974-4bbd9d84-a811-4cc4-8897-c4d785fa7d86.png">

Wir könnten nun schon in den Reiter "**Query**" oder "**Explorer**" springen und anfangen, die Daten zu analysieren. Bevor wir das tun, laden wir aber erst noch eine weitere Datei und das zugehörige Daten model.

8. Wiederholt nun die Schritte 6 + 7 für das Datenmodell mit dem Namen "**neo4j_importer_model_WindRaeder.json**" und die Datendatei "**Windraeder_SH_lc.csv**". **WICHTIG**, bevor ihr die CSV Datei ladet, müsst ihr noch die Datei mit den Ladesäulen Daten entfernen. Das könnt Ihr über die drei Punkte rechts neben dem Dateinamen machen, wie im Bild gezeigt. Danach ist das Feld mit den Dateien leer und ihr könnt die Windrad-Datei laden.

<img width="244" alt="Bildschirmfoto 2022-11-21 um 12 31 46" src="https://user-images.githubusercontent.com/8035021/203041010-4e6e951c-652c-4264-baf3-07edf1180342.png">

Wenn beide Dateien geladen sind, sollte das wie folgt aussehen:

<img width="1024" alt="Bildschirmfoto 2022-11-21 um 12 35 27" src="https://user-images.githubusercontent.com/8035021/203041447-19455418-9d95-4e40-aa2b-e2806d2d26f9.png">

Nun wieder "**Run Import**" anklicken und alle Daten sind geladen! Das "Import results" Fenster könnt ihr dann schliessen. 

Nun sind wir bereit, die Daten zu analysieren. Wie im Webinar gezeigt, kann man dazu den Neo4j Browser (Query Reiter in Workspace) oder Neo4j Bloom (Explore Reiter in Workspace) nutzen. Wir werden erst mal ein paar Queries ausprobieren.

Noch eines vorweg, die Datenmodelle bauen aufeinander auf. Als gemeinsamer Knoten für beide Datensets wird der Knoten "**Ort**" genutzt und mit dessen Name als eindeutige Verbindung der Daten genutzt. Da benötigen wir, um nun Abfragen stellen zu können, wie sehr ein Ort "unabhängig" vom Stromnetzt arbeiten kann oder ob mehr Verbraucher da sind, als Energie produziert wird.

---

## Abfragen und Analysen der Daten

Wir wechseln nun in den Reiter "**Query**" und testen dort ein paar Abragen in der Query Sprache "Cypher", welche Neo4j entwickelt hat. Die Sprache Cypher wird aktuell in einem ISO Gremium standartisiert und wird dann zukünftig als Graph Query Language ([GQL](https://www.gqlstandards.org/)) verfügbar sein. In der [Neo4j Graph Academy](https://graphacademy.neo4j.com/) gibt es diverse frei verfügbare Online-Kurse, wo man Cypher lernen kann.

Als Erstes schauen wir uns mal an, welcher Ort wieviel Gesamt-Verbrauch hat und wieviele Ladesäulen das sind. Hier ist die Cypher Query dazu:

```cypher
MATCH (o:Ort)-[:HAT_VERBRAUCHER]->(v:Verbraucher)
RETURN DISTINCT o.Ort AS Ortsname, sum(v.Anschlussleistung) AS `Verbrauch-Gesamt`, sum(v.AnzahlLadepunkte) AS `Anzahl Ladepunkte`;
```

Diese kopieren wir in die obere Kommandozeile des Neo4j Browsers (Reiter Query in Workspace), was dann wie folgt aussieht:

<img width="1024" alt="Bildschirmfoto 2022-11-21 um 12 53 35" src="https://user-images.githubusercontent.com/8035021/203046732-52a04a9b-f07e-455a-85e3-912e6cfe7638.png">

Wenn man die Query dann laufen lässt (Klick auf den kleinen blauen Button rechts in der Query Zeile), dann bekommt man sofort das Ergebnis angezeigt:

<img width="2047" alt="Bildschirmfoto 2022-11-21 um 12 53 51" src="https://user-images.githubusercontent.com/8035021/203047100-6b385b52-3b9a-44db-a14a-04e5886396b3.png">

Analog kann man dann mit den folgenden Queries verfahren.


Diese Query zeigt nun statt der Verbraucher alle Erzeuger und deren gesamt Produktion an Energie an:
```cypher
MATCH (o:Ort)-[:HAT_ERZEUGER]->(e:Erzeuger)
RETURN DISTINCT o.Ort AS Ortsname, sum(e.Leistung) AS `Erzeugung-Gesamt`ORDER BY `Erzeugung-Gesamt` DESC;
```

Diese Query vergleicht, wieviel Energie in einem Ort (hier Kiel) verbraucht wird und stellt das der gesamten Erzeugung von Energie gegenüber:
```cypher
MATCH (v:Verbraucher)<-[:HAT_VERBRAUCHER]-(o1:Ort {Ort: 'Kiel'})
WITH sum(v.Anschlussleistung) AS usedKW
MATCH (o2:Ort {Ort: 'Kiel'})-[:HAT_ERZEUGER]->(e:Erzeuger)
RETURN o2.Ort AS Ort, usedKW AS `Verbraucher-Gesamt`, sum(e.Leistung) AS `Erzeuger-Gesamt`;
```

Diese Query macht das gleiche, nur für alle Ortschaften in unserer Graph-Datenbank:
  ```cypher
MATCH (v:Verbraucher)<-[:HAT_VERBRAUCHER]-(o:Ort)
WITH toInteger(sum(v.Anschlussleistung)) AS kwVerbrauch, o.Ort AS orte
UNWIND orte AS ort
MATCH (o:Ort)-[:HAT_ERZEUGER]->(e:Erzeuger)
WHERE o.Ort = ort
WITH sum(e.Leistung) AS kwErzeug, ort, kwVerbrauch
RETURN ort AS Ort, kwErzeug AS `Erzeuger-Gesamt`, kwVerbrauch AS `Verbraucher-Gesamt`;
```

  











