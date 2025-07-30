---
"description": "Lägg till metadatasignaturer i Word-dokument med GroupDocs.Signature för .NET. Bädda in författaruppgifter, tidsstämplar och anpassade egenskaper för att förbättra dokumentsäkerhet och spårbarhet."
"linktitle": "Teckenbehandling med metadata"
"second_title": "GroupDocs.Signature .NET API"
"title": "Förbättra Word-dokument med metadatasignaturer i C# .NET"
"url": "/sv/net/document-signing/sign-word-processing-with-metadata/"
"weight": 14
---

## Introduktion

Ordbehandlingsdokument är bland de vanligaste filtyperna som används inom affärsverksamhet, utbildning och personlig kommunikation. Att säkerställa äktheten, spåra ursprunget och upprätthålla integriteten hos dessa dokument är avgörande i många professionella miljöer. En effektiv metod för att förbättra dokumentsäkerhet och spårbarhet är att bädda in metadatasignaturer.

Den här omfattande handledningen guidar dig genom processen att signera ordbehandlingsdokument med metadata med GroupDocs.Signature för .NET. Genom att lägga till metadatasignaturer kan du bädda in värdefull information som författaruppgifter, tidsstämplar för skapande, dokumentidentifierare och andra anpassade egenskaper direkt i dokumentets filstruktur.

## Förkunskapskrav

Innan du fortsätter med den här handledningen, se till att du har följande:

1. [GroupDocs.Signature för .NET](https://releases.groupdocs.com/signature/net/) - Ladda ner och installera biblioteket
2. Utvecklingsmiljö - Visual Studio eller annan .NET-kompatibel IDE
3. Word-dokument - En exempeldokumentfil (DOCX, DOC, etc.)
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

Definiera sökvägarna för ditt källdokument i Word och var den signerade utdata ska sparas:

```csharp
// Ange sökvägen till ditt Word-dokument
string filePath = "sample.docx";

// Definiera utdatakatalogen och filnamnet för det signerade dokumentet
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignWordProcessingWithMetadata", "SignedWithMetadata.docx");

// Se till att utdatakatalogen finns
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## Steg 2: Initiera signaturobjektet

Skapa en instans av Signature-klassen med ditt källdokument i Word:

```csharp
using (Signature signature = new Signature(filePath))
{
    // Resten av koden kommer att hamna här
}
```

## Steg 3: Skapa och konfigurera metadatasignaturer

Definiera sedan metadataalternativen och lägg till olika typer av metadatasignaturer:

```csharp
// Skapa metadataalternativobjekt
MetadataSignOptions options = new MetadataSignOptions();

// Lägg till olika typer av metadata med hjälp av det smidiga gränssnittet
options
    .Add(new WordProcessingMetadataSignature("Author", "Mr.Sherlock Holmes")) // Strängvärde
    .Add(new WordProcessingMetadataSignature("CreatedOn", DateTime.Now))      // DateTime-värde
    .Add(new WordProcessingMetadataSignature("DocumentId", 123456))           // Heltalsvärde
    .Add(new WordProcessingMetadataSignature("SignatureId", 123.456D))        // Dubbelt värde
    .Add(new WordProcessingMetadataSignature("Amount", 123.456M))             // Decimalvärde
    .Add(new WordProcessingMetadataSignature("Total", 123.456F));             // Flytvärde
```

## Steg 4: Signera dokumentet med metadata

Använd metadatasignaturerna i Word-dokumentet och spara resultatet:

```csharp
// Signera dokumentet och spara det i sökvägen för utdatafilen
SignResult result = signature.Sign(outputFilePath, options);

// Visa meddelande om framgång
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed document saved at: {outputFilePath}");
```

## Komplett exempel

Här är det kompletta kodexemplet som sammanför alla steg:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignWordProcessingWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // Ange sökvägar för filer
            string filePath = "sample.docx";
            string outputFilePath = Path.Combine("Your Document Directory", "SignWordProcessingWithMetadata", "SignedWithMetadata.docx");
            
            // Se till att utdatakatalogen finns
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // Signera Word-dokumentet med metadata
            using (Signature signature = new Signature(filePath))
            {
                // Skapa metadataalternativobjekt
                MetadataSignOptions options = new MetadataSignOptions();
                
                // Lägg till olika typer av metadatasignaturer
                options
                    .Add(new WordProcessingMetadataSignature("Author", "Mr.Sherlock Holmes")) // Strängvärde
                    .Add(new WordProcessingMetadataSignature("CreatedOn", DateTime.Now))      // DateTime-värde
                    .Add(new WordProcessingMetadataSignature("DocumentId", 123456))           // Heltalsvärde
                    .Add(new WordProcessingMetadataSignature("SignatureId", 123.456D))        // Dubbelt värde
                    .Add(new WordProcessingMetadataSignature("Amount", 123.456M))             // Decimalvärde
                    .Add(new WordProcessingMetadataSignature("Total", 123.456F));             // Flytvärde
                
                // Signera dokumentet och spara det i filen
                SignResult result = signature.Sign(outputFilePath, options);
                
                // Visa resultat
                Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## Avancerade metadatatekniker för Word-dokument

### Arbeta med anpassade och inbyggda dokumentegenskaper

Word-dokument har både inbyggda och anpassade egenskaper som kan nås via dokumentegenskapspanelen. GroupDocs.Signature låter dig arbeta med båda:

```csharp
// Lägg till inbyggda egenskaper
options
    .Add(new WordProcessingMetadataSignature("Company", "Sherlock Holmes Consulting"))
    .Add(new WordProcessingMetadataSignature("Category", "Legal Document"))
    .Add(new WordProcessingMetadataSignature("Keywords", "contract,agreement,legal"))
    .Add(new WordProcessingMetadataSignature("Comments", "This document is confidential"))
    .Add(new WordProcessingMetadataSignature("Manager", "John Watson"));

// Lägg till anpassade egenskaper
options.Add(new WordProcessingMetadataSignature("Department", "Legal"));
options.Add(new WordProcessingMetadataSignature("SecurityLevel", "Confidential"));
```

### Söka efter metadata i signerade Word-dokument

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

### Arbeta med dokumentvariabler

Word-dokument stöder även dokumentvariabler, vilka är en annan form av metadata:

```csharp
// Lägg till dokumentvariabler
options.Add(new WordProcessingMetadataSignature("DocVariable1", "Custom Value 1", true));
options.Add(new WordProcessingMetadataSignature("DocVariable2", DateTime.Now, true));
```

## Slutsats

I den här omfattande handledningen har du lärt dig hur du signerar ordbehandlingsdokument med metadata med GroupDocs.Signature för .NET. Att bädda in metadata i Word-dokument förbättrar dokumentens spårbarhet, ger värdefull kontext och hjälper till att fastställa äkthet.

Metadatasignaturer i Word-dokument är särskilt användbara i affärs- och juridiska miljöer där dokumentets ursprung, författarskap och versionsspårning är viktiga. De inbäddade metadata kan innehålla information om författaren, skapandetid, dokumentidentifierare och anpassade egenskaper som är relevanta för din organisations behov.

Genom att implementera metadatasignaturer med GroupDocs.Signature kan du säkerställa att dina Word-dokument bibehåller sin integritet och tillhandahåller verifierbar information under hela sin livscykel.

## Vanliga frågor

### Kan jag lägga till metadata i Word-dokument som redan har vissa definierade egenskaper?

Ja, du kan lägga till nya metadata eller uppdatera befintliga metadata i Word-dokument. GroupDocs.Signature hanterar integrationen, antingen genom att lägga till nya egenskaper eller uppdatera befintliga med samma namn.

### Vilka ordbehandlingsformat stöds för metadatasignering?

GroupDocs.Signature för .NET stöder metadatasignering för olika ordbehandlingsformat, inklusive DOCX, DOC, RTF, ODT med flera. För en komplett lista, se [dokumentation](https://docs.groupdocs.com/signature/net/).

### Är metadatasignaturer i Word-dokument synliga för läsarna?

Metadatasignaturer syns inte i själva dokumentinnehållet. De kan dock visas via dokumentegenskapspanelen i Microsoft Word eller andra kompatibla program.

### Kan jag programmatiskt validera om ett Word-dokument har manipulerats efter att jag har lagt till metadata?

Ja, GroupDocs.Signature tillhandahåller verifieringsfunktioner som kan hjälpa till att upptäcka om ett dokument har ändrats efter signering, inklusive ändringar av metadata.

### Är det möjligt att ta bort metadata från ett Word-dokument?

Ja, GroupDocs.Signature erbjuder alternativ för att ta bort metadatasignaturer från dokument om det behövs. Detta kan vara användbart för att rensa känslig information innan dokument delas externt.

### Var kan jag hitta fler resurser och stöd?

- [API-referens](https://reference.groupdocs.com/signature/net/)
- [Nedladdningar](https://releases.groupdocs.com/signature/net/)
- [Exempel](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [Dokumentation](https://docs.groupdocs.com/signature/net/)
- [Produktsida](https://products.groupdocs.com/signature/net/)
- [Blogg](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [Supportforum](https://forum.groupdocs.com/c/signature/13)
- [Tillfällig licens](https://purchase.groupdocs.com/temporary-license/)