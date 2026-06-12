# Interpolatie met formattering

Via stringinterpolatie schrijf je je string min of meer zoals hij er uiteindelijk moet uitzien, maar vervang je de niet-letterlijke delen door geformatteerde waarden. Dit levert een goed leesbaar resultaat.

Door het `$`-teken **VOOR** de string te plaatsen geef je aan dat alle delen in de string die tussen accolades staan als code mogen beschouwd worden. Een voorbeeld maakt dit duidelijk:

```csharp
string name = "Finkelstein";
int age = 17;
string result = $"Ik ben {name} en ik ben {age} jaar oud.";
```

In dit geval zal dus de inhoud van de variabele `name` tussen de string op de plek waar nu `{name}` staat geplaatst worden. Idem voor `age`. Dit mag, zelfs al is `age` geen string: hetgeen tussen de accolades staat, wordt altijd intern omgezet naar een string voor het in het resultaat wordt geplaatst. Dit gebeurt via de methode `ToString`, die voor elk soort data bestaat. Dus eigenlijk wordt het achter de schermen:

```csharp
string result = $"Ik ben {name.ToString()} en ik ben {age.ToString()} jaar oud.";
```

### Berekeningen doen bij string interpolatie

Je mag eender welke *expressie* tussen de accolades zetten bij string interpolation. Een expressie is iets dat je kan uitrekenen en dat je een resultaat oplevert. Bijvoorbeeld:

```csharp
string result = $"Ik ben {name} en ik ben {age+4} jaar oud.";
```

Alle expressies tussen de accolades zullen eerst uitgevoerd worden voor ze tussen de string worden geplaatst. De uitvoer wordt nu dus: `Ik ben Finkelstein en ik ben 21 jaar oud.`

Eender welke expressie is toegelaten, dus je kan ook complexe berekeningen of zelfs andere methoden aanroepen:

```csharp
string result = $"Ik ben {age*age+(3%2)} jaar oud.";
```

### Mooier formatteren

Bij stringinterpolatie kan je ook bepalen hoe de te tonen variabelen en expressies juist weergegeven moeten worden. Je geeft dit aan door na de expressie, binnen de accolades, een dubbelpunt te plaatsen gevolgd door de manier waarop moet geformatteerd worden:

Wil je bijvoorbeeld een kommagetal tonen met maar 2 cijfers na de komma dan schrijf je:

```csharp
double number = 12.345;
Console.WriteLine($"{number:F2}");
```

Hier stelt `2` het aantal cijfers na de komma voor. Je kan zelf kiezen om meer of minder cijfers te tonen door het getal aan te passen. Dit voorbeeld is gelijkaardig aan `Console.WriteLine(Math.Round(number,2))`, maar niet identiek. Dat komt omdat de geformatteerde string **verplicht** twee cijfers na de komma toont, zelfs als die niets veranderen aan de waarde van het getal. Als je een double zonder formattering weergeeft, worden nullen achteraan niet getoond. Dus voor getallen als `12` of `15.1` of `4.999`(met minder dan twee cijfers na de komma **na afronding**) maakt het een verschil.

Nog enkele nuttige vormen:

* D5: geheel getal bestaande uit 5 cijfers (`123` wordt `00123`) (werkt enkel op gehele getallen en je kan het getal 5 vervangen door een positieve waarde naar keuze)
* C: geldbedrag (`12,34` wordt € 12,34: teken van valuta afhankelijk van instellingen pc)

Alle format specifiers staan [hier opgelijst](https://docs.microsoft.com/en-us/dotnet/standard/base-types/standard-numeric-format-strings). Voor deze cursus volstaat het dat je deze specifiers kent voor de verschillende soorten data.

Je kan je data ook een vaste breedte en uitlijning geven. Dit doe je door meteen na de waarde in kwestie een komma te plaatsen, met daarna de gewenste breedte. De tekst wordt dan rechts gealigneerd. Je kan ook een minteken gebruiken en dan wordt de tekst links gealigneerd. Bijvoorbeeld:

```csharp
Console.WriteLine($"{"hallo",20} wereld");
Console.WriteLine($"{"hallo",-20} wereld");
```

Dit levert:

```csharp
               hallo wereld
hallo                wereld
```

Dus de tekst `"hallo"` wordt opgevuld totdat hij in totaal 20 karakters telt. Elke regel telt 27 karakters, want `" wereld"` is niet mee geformatteerd, maar is gewoon achter de geformatteerde tekst gezet.

### Manueel formatteren

Formattering is een handig hulpmiddel, maar het zal niet altijd alle scenario's dekken. In het voorbeeld hierboven is het bijvoorbeeld **verplicht** een constante waarde te gebruiken. Je kan geen variabele invullen waar `20` staat. Het is bijvoorbeeld ook niet mogelijk tekst te centeren (in plaats van links of rechts uit te lijnen). Dat hoeft geen probleem te zijn: je kan altijd een methode schrijven die tekst op de gewenste manier omzet.

#### Ingebouwde methodes voor formattering

Via `PadLeft` en `PadRight` kan je tekst opvullen tot de gewenste lengte met andere karakters dan een spatie. Bijvoorbeeld, voor hetzelfde effect als eerder:

```csharp
Console.WriteLine($"{"hallo".PadLeft(20)} wereld");
Console.WriteLine($"{"hallo".PadRight(20)} wereld");
```

Zoals vaak lever je hiermee wat gemak in voor extra flexibiliteit. Je kan namelijk opvullen met een karakter naar keuze, tot een variabele lengte:

```csharp
Console.WriteLine("Hoe breed wil je de string?");
int breedte = Convert.ToInt32(Console.ReadLine());
Console.WriteLine($"{"hallo".PadLeft(breedte,'!')} wereld");
Console.WriteLine($"{"hallo".PadRight(breedte,'!')} wereld");
```

#### Eigen methodes voor formattering

Als er geen mehode is om een string juist te tonen, kan je er altijd zelf een maken. Je zorgt dat de string en extra opties zoals de gewenste breedte parameters zijn en je geeft de geformatteerde string terug als resultaat. Er is bijvoorbeeld geen methode om tekst in te korten tot een maximale lengte, maar je kan ze zelf schrijven als volgt:

```csharp
static string Trunkeer(string input, int lengte) {
    return input.Substring(0, Math.Min(input.Length, lengte));
}
```

Je zou bijvoorbeeld ook een methode kunnen schrijven om tekst centraal te aligneren.