# De Math klasse

### Berekeningen

Een groot deel van je leven als ontwikkelaar zal bestaan uit het bewerken van variabelen in code. Meestal zullen die bewerkingen de vorm aannemen van berekeningen. De `Math` klasse zal ons hier bij kunnen helpen.

#### De Math klasse

De Math klasse bevat aardig wat handige methoden. Deze klasse bevat methoden voor een groot aantal typische wiskundige methoden (sinus, cosinus, vierkantswortel, macht, afronden, etc.) en kan je dus helpen om leesbaardere expressies te schrijven.

Stel dat je de derde macht van een variabel `getal` wenst te berekenen. Zonder de Math-klasse zou dat er zo uitzien:

```csharp
double result = getal*getal*getal;
```

Met de klasse kunnen we schrijven:

```csharp
double result = Math.Pow(getal, 3);
```

Het voordeel is dat je dit makkelijk kan aanpassen naar een hogere macht.

**De Math klasse ontdekken**

Als je in Visual Studio Code `Math` schrijft, gevolgd door een punt `.` krijg je alles te zien wat de Math-klasse kan doen.

**Methoden gebruiken**

1. Schrijf de Methode zonder argumenten. Bijvoorbeeld `Math.Pow()` (je mag de rode error negeren).
2. Je krijgt nu de help-files te zien van deze methode op MDSDN.
3. Klik desnoods op de pijltjes voor de verschillende versies van deze methode.

**PI (π)**

Ook het getal Pi (`3.141...`) is beschikbaar in de Math klasse. Dit is geen methode, maar een gewone waarde. Het woordje `const` betekent dat je deze waarde niet kan aanpassen.

Je kan deze als volgt gebruiken in berekeningen:

```csharp
double straal = 5.5;
double omtrek = Math.PI * 2 * straal;
```

#### Klassiek afronden

"Klassiek" afronden is afronden tot het dichtstbijzijnde getal. Dit doe je met `Math.Round`. Deze methode heeft twee parameters: het getal dat je wil afronden en het aantal cijfers na de komma dat je wil bewaren. Let hierbij goed op: dit berekent een nieuwe waarde (van type `double`) met de gewenste **precisie**, maar zorgt er niet automatisch voor dat deze waarde ook met dat aantal cijfers **getoond** wordt. Anders gezegd: `Math.Round(12.0, 2)` kan exact voorgesteld worden met hooguit twee cijfers na de komma, maar wordt standaard niet getoond met twee cijfers na de komma. Dat laatste behandelen we verder bij stringformattering.

#### Afronden naar boven of beneden

Naast "klassiek" afronden kan je ook zuiver in één richting afronden. Dan krijg je het dichtstbij gelegen gehele getal waarvoor geldt benadering =< getal (bij naar beneden afronden) of benadering >= getal (bij naar boven afronden). Dit doen we met `Math.Floor` en `Math.Ceiling`. Bijvoorbeeld: `Math.Floor(12.6)` is `12.0`, ook al is 13 een benadering die dichter bij ligt. Dat komt omdat 12 =< 12.6, terwijl 13 > 12.6.