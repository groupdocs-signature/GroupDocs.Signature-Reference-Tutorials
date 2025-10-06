---
"description": "Skydda och förbättra Excel-kalkylblad genom att bädda in metadatasignaturer med GroupDocs.Signature för .NET. Lägg till författarinformation, tidsstämplar och anpassade data för att förbättra dokumentspårbarhet och autenticitet."
"linktitle": "Signera kalkylblad med metadata"
"second_title": "GroupDocs.Signature .NET API"
"title": "Lägg till metadatasignaturer i Excel-kalkylblad i C# .NET"
"url": "/sv/net/document-signing/sign-spreadsheet-with-metadata/"
"weight": 13
type: docs
---
## Introduktion

Excel-kalkylblad innehåller ofta kritisk affärsdata, finansiell information och viktiga beräkningar. Att säkerställa deras äkthet, spåra deras ursprung och skydda deras integritet är avgörande i många professionella miljöer. En effektiv metod för att förbättra kalkylbladssäkerhet och spårbarhet är att bädda in metadatasignaturer.

Den här omfattande handledningen guidar dig genom processen att signera Excel-kalkylblad med metadata med GroupDocs.Signature för .NET. Genom att lägga till metadatasignaturer kan du bädda in värdefull information som författaruppgifter, tidsstämplar för skapande, dokumentidentifierare och andra anpassade egenskaper direkt i kalkylbladets filstruktur.

## Förkunskapskrav

Innan du fortsätter med den här handledningen, se till att du har följande:

1. [GroupDocs.Signature för .NET](https://releases.groupdocs.com/signature/net/) - Ladda ner och installera biblioteket
2. Utvecklingsmiljö - Visual Studio eller annan .NET-kompatibel IDE
3. Excel-kalkylblad - Ett exempel på en kalkylbladsfil (XLSX, XLS, etc.)
4. Grundläggande C#-kunskaper - Bekantskap med programmeringsspråket C#

## Importera namnrymder

Börja med att importera de namnrymder som behövs för att komma åt GroupDocs.Signature-funktionen:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## Steg 1: Konfigurera filsökvägar

Definiera sökvägarna för ditt källkalkylblad och var den signerade utdata ska sparas:

```csharp
// Ange sökvägen till din Excel-fil
string filePath = "sample.xlsx";

// Definiera utdatakatalogen och filnamnet för det signerade kalkylbladet
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignSpreadsheetWithMetadata", "SignedWithMetadata.xlsx");

// Se till att utdatakatalogen finns
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## Steg 2: Initiera signaturobjektet

Skapa en instans av Signature-klassen med din källfil för kalkylblad:

```csharp
using (Signature signature = new Signature(filePath))
{
    // Resten av koden kommer att hamna här
}
```

## Steg 3: Skapa och konfigurera metadatasignaturer

Definiera sedan metadataalternativen och skapa en matris med metadatasignaturer för kalkylblad:

```csharp
// Skapa metadataalternativobjekt
MetadataSignOptions options = new MetadataSignOptions();

// Skapa en matris med kalkylbladsmetadatasignaturer med olika datatyper
SpreadsheetMetadataSignature[] signatures = new SpreadsheetMetadataSignature[]
{
    new SpreadsheetMetadataSignature("Author", "Mr.Sherlock Holmes"), // Strängvärde
    new SpreadsheetMetadataSignature("CreatedOn", DateTime.Now),      // DateTime-värde
    new SpreadsheetMetadataSignature("DocumentId", 123456),           // Heltalsvärde
    new SpreadsheetMetadataSignature("SignatureId", 123.456D),        // Dubbelt värde
    new SpreadsheetMetadataSignature("Amount", 123.456M),             // Decimalvärde
    new SpreadsheetMetadataSignature("Total", 123.456F)               // Flytvärde
};

// Lägg till signaturinsamling i alternativen
options.Signatures.AddRange(signatures);
```

## Steg 4: Signera kalkylarket med metadata

Tillämpa metadatasignaturerna i kalkylbladet och spara resultatet:

```csharp
// Signera dokumentet och spara det i sökvägen för utdatafilen
SignResult result = signature.Sign(outputFilePath, options);

// Visa meddelande om framgång
Console.WriteLine($"\nSource spreadsheet signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed spreadsheet saved at: {outputFilePath}");
```

## Komplett exempel

Här är det kompletta kodexemplet som sammanför alla steg:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignSpreadsheetWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // Ange sökvägar för filer
            string filePath = "sample.xlsx";
            string outputFilePath = Path.Combine("Your Document Directory", "SignSpreadsheetWithMetadata", "SignedWithMetadata.xlsx");
            
            // Se till att utdatakatalogen finns
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // Signera kalkylbladet med metadata
            using (Signature signature = new Signature(filePath))
            {
                // Skapa metadataalternativobjekt
                MetadataSignOptions options = new MetadataSignOptions();
                
                // Skapa en matris med kalkylbladsmetadatasignaturer med olika datatyper
                SpreadsheetMetadataSignature[] signatures = new SpreadsheetMetadataSignature[]
                {
                    new SpreadsheetMetadataSignature("Author", "Mr.Sherlock Holmes"), // Strängvärde
                    new SpreadsheetMetadataSignature("CreatedOn", DateTime.Now),      // DateTime-värde
                    new SpreadsheetMetadataSignature("DocumentId", 123456),           // Heltalsvärde
                    new SpreadsheetMetadataSignature("SignatureId", 123.456D),        // Dubbelt värde
                    new SpreadsheetMetadataSignature("Amount", 123.456M),             // Decimalvärde
                    new SpreadsheetMetadataSignature("Total", 123.456F)               // Flytvärde
                };
                
                // Lägg till signaturinsamling i alternativen
                options.Signatures.AddRange(signatures);
                
                // Signera dokumentet och spara det i filen
                SignResult result = signature.Sign(outputFilePath, options);
                
                // Visa resultat
                Console.WriteLine($"\nSource spreadsheet signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## Avancerade metadatatekniker för kalkylblad

### Arbeta med anpassade och inbyggda kalkylbladsegenskaper

Excel-kalkylblad har både inbyggda och anpassade egenskaper som kan nås via dialogrutan för filegenskaper. GroupDocs.Signature låter dig arbeta med båda:

```csharp
// Lägg till inbyggda egenskaper
signatures = new SpreadsheetMetadataSignature[]
{
    new SpreadsheetMetadataSignature("Company", "Sherlock Holmes Consulting"),
    new SpreadsheetMetadataSignature("Category", "Financial"),
    new SpreadsheetMetadataSignature("Keywords", "budget,forecast,analysis"),
    new SpreadsheetMetadataSignature("Comments", "This spreadsheet contains confidential information"),
    new SpreadsheetMetadataSignature("Manager", "John Watson")
};
options.Signatures.AddRange(signatures);

// Lägg till anpassade egenskaper
options.Signatures.Add(new SpreadsheetMetadataSignature("Department", "Finance"));
options.Signatures.Add(new SpreadsheetMetadataSignature("SecurityLevel", "Confidential"));
```

### Söka efter metadata i signerade kalkylblad

Efter signeringen kan du verifiera eller extrahera metadata:

```csharp
// Skapa sökalternativ för metadata
MetadataSearchOptions searchOptions = new MetadataSearchOptions();

// Sök efter metadatasignaturer
SearchResult searchResult = signature.Search(searchOptions);

// Visa funna signaturer
Console.WriteLine($"Found {searchResult.Signatures.Count} metadata signatures:");
foreach (var foundSignature in searchResult.Signatures)
{
    MetadataSignature metadataSignature = foundSignature as MetadataSignature;
    if (metadataSignature != null)
    {
        Console.WriteLine($"- {metadataSignature.Name}: {metadataSignature.Value} ({metadataSignature.Value.GetType().Name})");
    }
}
```

### Uppdatering av befintliga metadata

Du kan uppdatera befintliga metadata i kalkylblad genom att använda samma egenskapsnamn:

```csharp
// Uppdatera befintliga metadata
options.Signatures.Add(new SpreadsheetMetadataSignature("Author", "Updated Author Name"));
```

## Slutsats

I den här omfattande handledningen har du lärt dig hur du signerar Excel-kalkylblad med metadata med GroupDocs.Signature för .NET. Att bädda in metadata i kalkylbladsfiler förbättrar dokumentens spårbarhet, ger värdefull kontext och hjälper till att fastställa autenticitet.

Metadatasignaturer i kalkylblad är särskilt användbara i affärsmiljöer där dokumentets ursprung, författarskap och versionsspårning är viktiga. De inbäddade metadata kan innehålla information om författaren, skapandetid, dokumentidentifierare och anpassade egenskaper som är relevanta för din organisations behov.

Genom att implementera metadatasignaturer med GroupDocs.Signature kan du säkerställa att dina Excel-kalkylblad bibehåller sin integritet och tillhandahåller verifierbar information under hela sin livscykel.

## Vanliga frågor

### Kan jag lägga till metadata i kalkylblad som redan har vissa definierade egenskaper?

Ja, du kan lägga till nya metadata eller uppdatera befintliga metadata i kalkylblad. GroupDocs.Signature hanterar integrationen, antingen genom att lägga till nya egenskaper eller uppdatera befintliga med samma namn.

### Vilka kalkylbladsformat stöds för metadatasignering?

GroupDocs.Signature för .NET stöder metadatasignering för olika kalkylbladsformat, inklusive XLSX, XLS, XLSM, ODS med flera. För en komplett lista, se [officiell dokumentation](https://docs.groupdocs.com/signature/net/).

### Är metadatasignaturer i kalkylblad synliga för användarna?

Metadatasignaturer syns inte i själva kalkylbladets innehåll. De kan dock visas via dokumentegenskapspanelen i Excel eller andra kompatibla program.

### Kan jag programmatiskt validera om ett kalkylblad har manipulerats efter att jag har lagt till metadata?

Ja, GroupDocs.Signature tillhandahåller verifieringsfunktioner som kan hjälpa till att upptäcka om ett dokument har ändrats efter signering, inklusive ändringar av metadata.

### Påverkar det kalkylbladets funktionalitet att lägga till metadata?

Att lägga till metadata har minimal inverkan på filstorleken och ingen inverkan på kalkylbladets funktionalitet. Det är ett enkelt sätt att förbättra dokumentegenskaper utan att påverka beräkningar, formler eller andra Excel-funktioner.

### Var kan jag hitta fler resurser och stöd?

- [API-referens](https://reference.groupdocs.com/signature/net/)
- [Nedladdningar](https://releases.groupdocs.com/signature/net/)
- [Exempel](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [Dokumentation](https://docs.groupdocs.com/signature/net/)
- [Produktsida](https://products.groupdocs.com/signature/net/)
- [Blogg](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [Supportforum](https://forum.groupdocs.com/c/signature/13)
- [Tillfällig licens](https://purchase.groupdocs.com/temporary-license/)