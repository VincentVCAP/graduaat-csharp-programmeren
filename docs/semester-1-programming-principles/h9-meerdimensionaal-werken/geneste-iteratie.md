# Geneste iteratie

### Itereren over een tweedimensionale array

Met meerdimensionale arrays kunnen we de richtingen los van elkaar bekijken. Bijvoorbeeld, om ons OXO-rooster af te printen (eerste rij op één regel, tweede rij op een volgende regel, derde rij op een derde regel), kunnen we dit doen:

```csharp
public static void PrintRij(int rij, string[,] array) {
	for(int i = 0; i < array.getLength(1); i++) {
		Console.Write(array[rij,i]);
	}
	Console.WriteLine();
}

// ergens anders in de code
for(int rij = 0; rij < oxoRooster.GetLength(0); rij++) {
    PrintRij(rij,oxoRooster);
}
```

Als we het rooster in één dimensie zouden voorstellen met een variabele `oxoArray`, moesten we dit doen:

```csharp
// na elementen met index 2, 5 en 8 moeten we een newline printen
for(int i = 0; i < oxoArray.Length; i++) {
    Console.Write(oxoArray[i]);
    // dit omvat meer rekenwerk
    // 3 is hier ook "hardgecodeerd" als lengte van een rij
    // dus als we de spelregels wijzigen (bv. OXOXO), werkt deze code niet meer
    if((i + 1) % 3 == 0) {
        Console.WriteLine();
    }
}
```

We hebben de tweedimensionale versie voor een beter inzicht met een hulpmethode gedaan. Dat hoeft niet, want je kan de inhoud van `PrintRij` ook rechtstreeks invullen. Dan krijg je een **geneste lus**:

```csharp
// per rij doorlopen we de kolommen en printen we een newline
for(int rij = 0; rij < oxoRooster.GetLength(0); rij++) {
    // voor een kolom tonen we gewoon alle waarden
    for(int kolom = 0; kolom < oxoRooster.GetLength(1); kolom++) {
        Console.Write(oxoRooster[rij,kolom]);
    }
    Console.WriteLine();
}
```

In het begin kan deze structuur wat intimiderend zijn, maar er is niets nieuws aan deze luscode. Kijk eerst naar wat één uitvoering doet en zie dat als één geheel. Denk dan na over wat er gebeurt als je dat geheel herhaalt, zonder na te denken over hoe dat geheel werkt.

### Itereren met onderling afhankelijke indexen

In het vorige voorbeeld toonden we per rij even veel symbolen. Dus de werking van `PrintRij` hing niet echt af van de kolom waarop we ons bevonden. Dat is niet altijd zo. Soms is er interactie tussen de tellers van de buitenste en de binnenste for-lus.

Volgend voorbeeld toont hoe je enkel een driehoekig deel van een rooster toont:

```csharp
public static void PrintRij(int rij, string[,] array, int maxI) {
	for(int i = 0; i < array.getLength(1) && i <= maxI; i++) {
		Console.Write(array[rij,i]);
	}
	Console.WriteLine();
}

for(int rij = 0; rij < oxoRooster.GetLength(0); rij++) {
    PrintRij(rij,oxoRooster,rij); // print bv. 3 karakters van rij 3, 4 karakters van rij 4,...
}
```

Opnieuw kan je de lussen in elkaar schuiven:

```csharp
for(int rij = 0; rij < oxoRooster.GetLength(0); rij++) {
    for(int kolom = 0; kolom < oxoRooster.GetLength(1) && kolom <= rij; kolom++) {
        Console.Write(oxoRooster[rij,kolom]);
    }
    Console.WriteLine();
}
```

En opnieuw hanteer je dezelfde denkwijze om hier uit wijs te raken. Kijk eerst naar wat **in** de lus staat. Zie `rij` gewoon als een getal dat bepaalt hoe veel karakters je maximum kan printen, zonder na te denken over hoe dat getal verandert. Pas als je de werking van de inhoud van de lus goed in je hoofd hebt, denk je na over wat er gebeurt als je die inhoud gaat herhalen met verschillende waarden voor `rij`.

### Itereren zonder arrays

Geneste lussen komen vaak voor bij meerdimensionale arrays, maar dat is vooral omdat de twee technieken goed samen gaan. Er is geen verplichting om ze samen te gebruiken.

Je kan geneste lussen gebruiken voor allerlei taken waarbij je herhaling hebt op meerdere niveaus. Bijvoorbeeld voor volgende figuur:

```
1 
2 2 
3 3 3 
4 4 4 4 
5 5 5 5 5 
```

Hier zijn twee vormen van herhaling:

* de herhaling die het snelst terugkeert, namelijk van links naar rechts (we printen een aantal keer hetzelfde getal)
* de herhaling die minder vaak gebeurt, namelijk van boven naar onder (we printen een aantal keer een regel)

We denken eerst na over de herhaling die het snelst terugkeert. We kennen alles om een getal een aantal keer (gelijk aan zichzelf) te printen:

```csharp
for (int i = 1; i <= getal; i++) {
  Console.Write($"{getal} ");
}
```

We kennen ook alles om een newline een aantal keer te printen:

```csharp
for (int i = 1; i <= anderGetal; i++) {
  Console.WriteLine();
}
```

Om de twee lussen te combineren, moeten we vermijden dat we dezelfde naam `i` gebruiken, dus we hernoemen die van de binnenste herhaling naar `j`. En het aantal keer dat we een getal op een regel willen herhalen, is gelijk aan het nummer van die regel. Dan krijgen we dus:

```csharp
for (int i = 1; i <= anderGetal; i++) {
  for (int j = 1; j <= i; j++) {
    Console.Write($"{i} ");
  }
  Console.WriteLine();
}
```