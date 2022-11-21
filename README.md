# it-novum Webinar 24. November 2022.  (Work in progress ...)

Demo Daten und Skripte vom IT Novum Seminar - Graph-Datenbanken: So decken Sie neue Zusammenhänge auf
---
## Verzeichnisse:

#### Daten: Enthält die aufbereiteten Daten von Govdata.de

- **Quelle der Daten**
	- [Govdata.de](https://www.govdata.de/) 
		- [Windkraftanlagen Schleswig-Holstein Stand 18.08.2022]([https://opendata.schleswig-holstein.de/dataset/12fb2027-d2d3-42c9-8774-34a70f584c0f/resource/e47cf6aa-d4eb-4c61-9605-bba859684c13/download/opendata_wka_ib_gv_vb_sh_20220701.csv](https://opendata.schleswig-holstein.de/dataset/12fb2027-d2d3-42c9-8774-34a70f584c0f/resource/e47cf6aa-d4eb-4c61-9605-bba859684c13/download/opendata_wka_ib_gv_vb_sh_20220701.csv))
		- [Ladesäulen Schleswig-Holstein Stand 1.10.2022]([https://opendata.schleswig-holstein.de/dataset/ac7347a6-8011-46b2-97ed-b4816807ef47/resource/a90e6d90-ae46-4b91-997c-c29c9a7b1e71/download/ladesaeulenregister.csv](https://opendata.schleswig-holstein.de/dataset/ac7347a6-8011-46b2-97ed-b4816807ef47/resource/a90e6d90-ae46-4b91-997c-c29c9a7b1e71/download/ladesaeulenregister.csv))
			- [Liste der Ladesäulen](https://www.govdata.de/web/guest/daten/-/details/liste-der-ladesaulenddc56)


#### Datenmodelle: Enthält die zwei Datenmodelle die mit (Neo4j Workspace)[https://workspace-preview.neo4j.io/workspace/query] erstellt wurden

1. Datenmodell für die Ladesäulen: **neo4j_importer_model_ladesaeulen.json**
2. Datenmodell für die Windräder: **neo4j_importer_model_WindRaeder2.json**

Zum Nachstellen der im Workshop gezeigte Demo, soll noch folgendes bzgl. der Daten erwähnt werden. 
Die Daten (im Vergleich zu den original Daten govdata.de) mussten noch ein wenig aufbereitet werden, damit sie verwendet werden konnten. Folgende Aufbereitungen wurden durchgeführt:

**1. Ladesäulen Daten:**
  * lsNr hinzugegügt, als eindeutige Id für die Ladesäulen. Damit jede Ladesäule eindeutig identifizierbar ist.

**2. Windkraftanlagen Daten:**
  * Gemeinde in Ort umbenannt, für einfacheres Laden und  zuordnen der Daten 
  * Spaltennamen wurde von Großbuchstaben auf normale Rechtschreibung umbenannt. 
  * Data Cleansing von zusätzlichen Tabs & Zeilenumbrüche in den Daten --> Qualtät der Daten ist schlecht!

---

Zum Aubau der Demo wird nun folgendermaßen vorgegangen:

1. Falls noch nicht vorhanden, erstellt man sich eine (Neo4j Aura Free)[https://neo4j.com/cloud/platform/aura-graph-database/?ref=get-started-dropdown-cta] Datenbank. Klickt den obigen Link und anschliessend den Button "**Start free**" und meldet Euch für die kostenlose Nutzung an.

2. Nach der Anmeldung, folgt dem Dialog für das Anlegen einer kostenlosen Neo4j Datenbank. Nehmt eine **leeres Datenbank-Template** (Empty Instance) und keines der schon mit Daten geladenen Templates!
<img width="609" alt="Bildschirmfoto 2022-11-21 um 11 28 01" src="https://user-images.githubusercontent.com/8035021/203027751-de1dcc9a-c7e6-4807-9633-da0dd6475bc6.png">

Vergesst anschliessend nicht, Euch das Passwort zu sichern!!! Das benötigt ihr, um Euch in Workspace mit der Datenbank verbinden zu können. Der User Name ist immer **neo4j**!

3. Wenn die leere Neo4j Instance aufgebaut ist, dass sollte in wenigen Sekunden passieren, dann könnt Ihr euch in Workspace an die Datenbank anmelden. Dazu ruft (Workspace)[https://workspace-preview.neo4j.io/workspace/import] auf und falls Ihr nicht direkt auf dem Reiter "**Import**" landet, klickt noch auf Import. Workspace hat drei Reiter, "**Explore**", "**Query**" und "**Import**". Damit können wir nun das Datenmodell bauen, dann die Daten laden und auch die Daten analysieren.

<img width="950" alt="Bildschirmfoto 2022-11-21 um 11 43 02" src="https://user-images.githubusercontent.com/8035021/203030936-217ee614-985f-4c89-84ac-a344bdb9f393.png">

4. Bevor wir anfangen können, müsst ihr Euch noch an Eurer Aura Free Datenbank Instanz anmelden. Dazu klickt ihr mittig oben auf "**No Connection**" und dann auf "**Connect**" (im Bild oben).

Im folgenden Dialog benötigt ihr nun den "**Connect String**" und Benutzername plus Password. Das letztere habt ihr ja schon, aber den Connect String müsst Ihr Euch aus der Aura Free Console kopieren wie im nächsten Bild gezeigt.

<img width="306" alt="Bildschirmfoto 2022-11-21 um 11 48 42" src="https://user-images.githubusercontent.com/8035021/203033126-49266cd1-3fbb-4757-be2c-452e1d450f1f.png">

Damit habt ihr alle Infos, um auch mit Workspace an Eurer Aura Free Instanz anmelden zu können. Der Dialog dazu sieht folgendermaßen aus:

<img width="323" alt="Bildschirmfoto 2022-11-21 um 11 49 45" src="https://user-images.githubusercontent.com/8035021/203033340-6ee79317-5584-42db-a125-269ae49ee744.png">


4. Um nun starten zu können, klickt bitte den Reiter "**Import**", falls noch nicht geschehen und ladet die Datei "**ladesaeulenregister_SH_Ids.csv**" per Drag & Drop oder über den "**browse**" Link in den Daten-Importer. Das sieht dann wie folgt aus:

<img width="482" alt="Bildschirmfoto 2022-11-21 um 12 02 26" src="https://user-images.githubusercontent.com/8035021/203034604-14ce31b7-d909-49f6-9069-71d150f47419.png">

5. Nun haben wir das Datenfile geladen. Anschliessend klickt Ihr rechts oben auf die 3 Punkte neben dem Button "Run Import" und wählt "**Open Model**". Im anschliessenden Dialogfenster wählt ihr dann das Datenmodel mit dem Dateiname "**neo4j_importer_model_ladesaeulen.json**" und klickt "**Öffnen**".

<img width="306" alt="Bildschirmfoto 2022-11-21 um 12 04 30" src="https://user-images.githubusercontent.com/8035021/203035025-9f8c708c-4d3d-40b9-bbf0-32d81310d6e4.png">

Nun sehen wir in der Mitte des Fensters unser Datenmodell, was wir aus den Daten im linken Teil des Fensters "gebaut" haben. Wenn wir nun auf z. B. auf den Knoten "**Ort**" klicken, dann sehen wir im rechten Teil des Fensters, die Zuordnung von Daten zum Knoten "Ort" und welche Properties mit Daten gefüllt werden sollen.
Mit dem hier geladen Datenmodell könnt ihr alle Knoten und Kanten (Relationships) auswählen und mal nachvollziehen, wie Diese miteinander verknüpft wurden. **WICHTIG* hierbei ist zu erwähnen, dass man möglichst jeden einzelnen Knoten durch eine Unique-ID oder einen Namen erkennbar machen sollte. Für den Ort haben wir den Namen gewält, für die Ladesäulen die oben erwähnte ID den Rohdaten hinzugefügt!



Die Datenmodelle bauen aufeinander auf. Zuerst wird das Datenmodell "neo4j_importer_model_ladesaeulen.json" benutzt
