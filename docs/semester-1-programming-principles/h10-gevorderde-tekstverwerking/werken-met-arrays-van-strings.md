# Werken met arrays van strings

### Split

De `Split` methode laat toe een string te splitsen op een bepaald teken. Het resultaat is steeds een **array van strings**.

```csharp
string data= "12,13,20";
string[] gesplitst= data.Split(',');

for(int i=0; i<gesplitst.Length; i++)
{
    Console.WriteLine(gesplitst[i]);
}
```

Uiteraard kan je dit dus gebruiken om op eender welk `char` te splitsen en dus niet enkel op een `','` (komma).

Dit is bijzonder nuttig voor het verwerken van bestanden met gestructureerde data, bijvoorbeeld CSV-bestanden. Dit zijn bestanden waarin elke regel een groepje verwante gegevens voorstelt, gescheiden via een afgesproken symbool zoals `,`. Deze files worden vaak gebruikt als exportformaat voor spreadsheets en databasetabellen.

### Join

Via `Join` kunnen we array van `string` terug samenvoegen. Het resultaat is een nieuwe `string`.

Volgende voorbeeld zal de eerder array van het vorige voorbeeld opnieuw samenvoegen maar nu met telkens een `;` tussen iedere string:

```csharp
string joined = String.Join(";", gesplitst);
```