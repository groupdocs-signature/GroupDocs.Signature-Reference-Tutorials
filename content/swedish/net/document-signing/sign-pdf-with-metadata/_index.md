---
"description": "Integrera metadatasignaturer i PDF-dokument med GroupDocs.Signature för .NET. Lär dig bädda in författarinformation, tidsstämplar och anpassade data för att förbättra PDF-autentitet och spårbarhet."
"linktitle": "Signera PDF med metadata"
"second_title": "GroupDocs.Signature .NET API"
"title": "Lägg till metadatasignaturer till PDF-dokument i C# .NET"
"url": "/sv/net/document-signing/sign-pdf-with-metadata/"
"weight": 11
type: docs
---
## Introduktion

PDF-dokument (Portable Document Format) används flitigt inom olika branscher tack vare deras konsistens och plattformsoberoende. Att säkerställa dessa dokuments äkthet och spårbarhet är avgörande i många professionella miljöer. Ett effektivt sätt att uppnå detta är att bädda in metadata i själva PDF-filerna.

I den här omfattande handledningen utforskar vi hur man signerar PDF-dokument med metadata med GroupDocs.Signature för .NET. Metadatasignaturer låter dig bädda in ytterligare information i dokumentet, till exempel författaruppgifter, tidsstämplar för skapande, dokumentidentifierare och anpassade värden, utan att synligt ändra dokumentets utseende.

## Förkunskapskrav

Innan vi börjar, se till att du har följande på plats:

1. [GroupDocs.Signature för .NET](https://releases.groupdocs.com/signature/net/) - Ladda ner och installera biblioteket
2. Utvecklingsmiljö - Visual Studio eller annan .NET-kompatibel IDE
3. PDF-dokument - Ett exempel på en PDF-fil för signering
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

Först, definiera sökvägen till ditt PDF-dokument och ange var du vill spara den signerade utdata:

```csharp
// Ange sökvägen till ditt PDF-dokument
string filePath = "sample.pdf";

// Definiera utdatakatalog och filsökväg
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignPdfWithMetadata", "SignedWithMetadata.pdf");

// Se till att utdatakatalogen finns
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## Steg 2: Initiera signaturobjektet

Skapa en instans av Signature-klassen med ditt käll-PDF-dokument:

```csharp
using (Signature signature = new Signature(filePath))
{
    // Koden för signering kommer att placeras här
}
```

## Steg 3: Definiera metadataalternativ

Skapa och konfigurera metadataalternativen och lägg till olika typer av metadatasignaturer:

```csharp
// Skapa metadataalternativobjekt
MetadataSignOptions options = new MetadataSignOptions();

// Lägg till olika typer av metadata med hjälp av det smidiga gränssnittet
options
    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // Strängvärde
    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // DateTime-värde
    .Add(new PdfMetadataSignature("DocumentId", 123456))            // Heltalsvärde
    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // Dubbelt värde
    .Add(new PdfMetadataSignature("Amount", 123.456M))              // Decimalvärde
    .Add(new PdfMetadataSignature("Total", 123.456F));              // Flytvärde
```

## Steg 4: Signera PDF-filen med metadata

Tillämpa metadatasignaturerna på PDF-dokumentet och spara resultatet:

```csharp
// Signera dokumentet och spara det i utdatasökvägen
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

namespace SignPdfWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // Ange sökvägar för filer
            string filePath = "sample.pdf";
            string outputFilePath = Path.Combine("Your Document Directory", "SignPdfWithMetadata", "SignedWithMetadata.pdf");
            
            // Se till att utdatakatalogen finns
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // Signera PDF-filen med metadata
            using (Signature signature = new Signature(filePath))
            {
                // Skapa metadataalternativobjekt
                MetadataSignOptions options = new MetadataSignOptions();
                
                // Lägg till olika typer av metadatasignaturer
                options
                    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // Strängvärde
                    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // DateTime-värde
                    .Add(new PdfMetadataSignature("DocumentId", 123456))            // Heltalsvärde
                    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // Dubbelt värde
                    .Add(new PdfMetadataSignature("Amount", 123.456M))              // Decimalvärde
                    .Add(new PdfMetadataSignature("Total", 123.456F));              // Flytvärde
                
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

## Avancerade PDF-metadataoperationer

### Lägga till anpassade metadata med namnrymdsstöd

PDF-dokument stöder anpassade metadata med stöd för XML-namnrymd:

```csharp
// Lägg till anpassade metadata med namnrymd
options.Add(new PdfMetadataSignature("CustomProperty", "Custom Value")
{
    NamespaceUri = "http://ditt-namnutrymme.com/schema"
});
```

### Söka efter metadata i signerade PDF-filer

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

### Arbeta med standard PDF-metadata

PDF-dokument har standardiserade metadatafält som kan nås och ändras:

```csharp
// Ange standardfält för PDF-metadata
options
    .Add(new PdfMetadataSignature("Title", "Important Contract"))
    .Add(new PdfMetadataSignature("Subject", "Legal Agreement"))
    .Add(new PdfMetadataSignature("Keywords", "contract, agreement, legal, binding"))
    .Add(new PdfMetadataSignature("Creator", "Legal Department"))
    .Add(new PdfMetadataSignature("Producer", "GroupDocs.Signature"));
```

## Slutsats

I den här handledningen har du lärt dig hur du signerar PDF-dokument med metadata med GroupDocs.Signature för .NET. Att bädda in metadata i PDF-filer är ett utmärkt sätt att förbättra dokumentautenticitet, lägga till viktig information och förbättra arbetsflöden för dokumenthantering.

Metadatasignaturer i PDF-filer är särskilt värdefulla i affärsmiljöer där dokumentspårbarhet och äkthetsverifiering är avgörande. De inbäddade metadata kan innehålla information om dokumentets ursprung, författare, skapandetid, version och anpassade egenskaper som är relevanta för din organisations arbetsflöde.

Genom att implementera metadatasignaturer med GroupDocs.Signature kan du säkerställa att dina PDF-dokument bibehåller sin integritet och tillhandahåller verifierbar information under hela sin livscykel.

## Vanliga frågor

### Kan jag ändra befintliga metadata i ett PDF-dokument?

Ja, du kan ändra befintliga metadata i PDF-dokument. När du använder nya metadatasignaturer med samma namn som befintliga, kommer värdena att uppdateras i enlighet därmed.

### Är metadatasignaturer i PDF-dokument synliga för slutanvändaren?

Metadatasignaturer syns inte i själva dokumentinnehållet. De kan dock visas via dokumentegenskapspanelen i PDF-läsare som Adobe Acrobat eller med hjälp av specialverktyg för att visa metadata.

### Kan jag kryptera eller skydda metadata i PDF-filer?

GroupDocs.Signature erbjuder alternativ för att säkra dokument, inklusive kryptering. Du kan använda kryptering på dokumentnivå för att skydda hela PDF-filen, inklusive dess metadata.

### Finns det en gräns för hur mycket metadata jag kan lägga till i en PDF?

Även om det inte finns någon strikt gräns i PDF-specifikationen, kan det öka filstorleken om man lägger till för många metadata. Det rekommenderas att endast inkludera relevant och nödvändig information i metadata.

### Kan jag programmatiskt validera om en PDF har manipulerats efter att jag lagt till metadata?

Ja, GroupDocs.Signature tillhandahåller verifieringsfunktioner som kan hjälpa till att upptäcka om ett dokument har ändrats efter signering, inklusive ändringar av metadata.

### Var kan jag hitta fler resurser och stöd?

- [API-referens](https://reference.groupdocs.com/signature/net/)
- [Nedladdningar](https://releases.groupdocs.com/signature/net/)
- [Exempel](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [Dokumentation](https://docs.groupdocs.com/signature/net/)
- [Produktsida](https://products.groupdocs.com/signature/net/)
- [Blogg](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [Supportforum](https://forum.groupdocs.com/c/signature/13)
- [Tillfällig licens](https://purchase.groupdocs.com/temporary-license/)