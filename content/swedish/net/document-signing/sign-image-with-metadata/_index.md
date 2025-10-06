---
"description": "Lär dig hur du signerar och bäddar in metadata i bilder med GroupDocs.Signature för .NET. Lägg till författarinformation, tidsstämplar och anpassade data för att förbättra bildens äkthet och spårbarhet."
"linktitle": "Signera bild med metadata"
"second_title": "GroupDocs.Signature .NET API"
"title": "Signera bilder med metadata i C# .NET"
"url": "/sv/net/document-signing/sign-image-with-metadata/"
"weight": 10
type: docs
---
## Introduktion

Digital bildsignering med metadata blir allt viktigare för att fastställa autenticitet, ägarskap och spårbarhet. GroupDocs.Signature för .NET tillhandahåller en kraftfull men ändå lättanvänd lösning för att lägga till metadatasignaturer i olika bildformat. Den här handledningen guidar dig genom hela processen att signera bilder med metadata med hjälp av C#.

Metadatasignaturer låter dig bädda in värdefull information direkt i bildfiler, såsom författarinformation, tidsstämplar för skapande, unika identifierare med mera. Denna information blir en del av själva bildfilen, vilket ger en tillförlitlig metod för att spåra och verifiera bildens äkthet.

## Förkunskapskrav

Innan du fortsätter med den här handledningen, se till att du har följande:

1. [GroupDocs.Signature för .NET](https://releases.groupdocs.com/signature/net/) - Ladda ner och installera biblioteket
2. Utvecklingsmiljö - Visual Studio eller annan kompatibel IDE med .NET-stöd
3. Bildfil - En exempelbildfil i ett format som stöds (PNG, JPG, TIFF, etc.)
4. Grundläggande C#-programmeringskunskaper - Bekantskap med C#-programmeringskoncept

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

Definiera sökvägarna för din källbild och var den signerade utdatan ska sparas:

```csharp
// Ange sökvägen till din källbildfil
string filePath = "sample.png";

// Definiera utdatakatalogen och filnamnet för den signerade bilden
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignImageWithMetadata", "SignedWithMetadata.png");

// Se till att utdatakatalogen finns
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## Steg 2: Initiera signaturobjektet

Skapa en instans av Signature-klassen med din källbildsfil:

```csharp
using (Signature signature = new Signature(filePath))
{
    // Resten av koden kommer att hamna här
}
```

## Steg 3: Skapa och konfigurera metadatasignaturer

Definiera sedan de metadata som du vill bädda in i bilden. GroupDocs.Signature stöder olika datatyper för metadata:

```csharp
// Initiera metadata-ID (specifikt för bildformat)
ushort imgsMetadataId = 41996;

// Skapa metadataalternativobjekt
MetadataSignOptions options = new MetadataSignOptions();

// Lägg till olika typer av metadatasignaturer
options
    .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Sherlock Holmes"))  // Strängvärde
    .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // Datum Tid värde
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // Heltalsvärde
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // Dubbelt värde
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // Decimalvärde
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // Flytvärde
```

## Steg 4: Signera bilden med metadata

Tillämpa metadatasignaturerna på bilden och spara resultatet:

```csharp
// Signera dokumentet och spara det i sökvägen för utdatafilen
SignResult result = signature.Sign(outputFilePath, options);

// Visa meddelande om framgång
Console.WriteLine($"\nSource image signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed image saved at: {outputFilePath}");
```

## Komplett exempel

Här är det kompletta kodexemplet som sammanför alla steg:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignImageWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // Ange sökvägar för filer
            string filePath = "sample.png";            
            string outputFilePath = Path.Combine("Your Document Directory", "SignImageWithMetadata", "SignedWithMetadata.png");
            
            // Se till att utdatakatalogen finns
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // Signera bilden med metadata
            using (Signature signature = new Signature(filePath))
            {
                // Initiera metadata-ID (specifikt för bildformat)
                ushort imgsMetadataId = 41996;
                
                // Skapa metadataalternativ
                MetadataSignOptions options = new MetadataSignOptions();
                
                // Lägg till olika typer av metadatasignaturer
                options
                    .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Sherlock Holmes")) // Strängvärde
                    .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // Datum Tid värde
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // Heltalsvärde
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // Dubbelt värde
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // Decimalvärde
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // Flytvärde
                
                // Signera dokumentet och spara det i filen
                SignResult result = signature.Sign(outputFilePath, options);
                
                // Visa resultat
                Console.WriteLine($"\nSource image signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## Avancerade metadatasigneringstekniker

### Arbeta med anpassade metadata

Du kan också skapa anpassade metadatafält med specifika ID:n:

```csharp
// Skapa anpassade metadata med specifikt ID
options.Add(new ImageMetadataSignature(42000, "CustomValue"));
```

### Verifiera metadatasignaturer

Efter signeringen kan du verifiera metadatasignaturerna:

```csharp
// Skapa verifieringsalternativ
MetadataSearchOptions searchOptions = new MetadataSearchOptions();

// Sök efter metadatasignaturer
SearchResult result = signature.Search(searchOptions);

// Visa funna signaturer
Console.WriteLine($"Found {result.Signatures.Count} metadata signatures:");
foreach(var metadataSignature in result.Signatures)
{
    Console.WriteLine($"- {metadataSignature.Name}: {metadataSignature.Value}");
}
```

## Slutsats

I den här handledningen har du lärt dig hur du signerar bilder med metadata med GroupDocs.Signature för .NET. Att bädda in metadata i bilder är ett utmärkt sätt att förbättra bilders autenticitet, lägga till viktig information och förbättra arbetsflöden för dokumenthantering. Processen är enkel men kraftfull och möjliggör anpassning baserat på dina specifika behov.

Metadata som är inbäddade i bildfilen kan användas för olika ändamål, såsom upphovsrättsskydd, spårning av bildens ursprung, tillägg av beskrivande information och upprättande av digital spårbarhetskedja. Genom att implementera metadatasignaturer kan du säkerställa att dina bilder bibehåller sin integritet och autenticitet under hela sin livscykel.

## Vanliga frågor

### Kan jag lägga till metadata till befintliga signerade bilder?

Ja, du kan lägga till ytterligare metadata till bilder som redan innehåller metadatasignaturer. Befintliga metadata kommer att bevaras och nya metadata kommer att läggas till i enlighet därmed.

### Vilka bildformat stöds för metadatasignering?

GroupDocs.Signature för .NET stöder metadatasignering för olika bildformat, inklusive PNG, JPEG, TIFF, BMP, GIF med flera. För en komplett lista, se [officiell dokumentation](https://docs.groupdocs.com/signature/net/).

### Är det möjligt att kryptera metadata i bilder?

Ja, GroupDocs.Signature erbjuder alternativ för att kryptera metadata för ökad säkerhet. Du kan använda krypteringsalternativen som biblioteket tillhandahåller för att skydda känslig metadatainformation.

### Kan jag programmatiskt validera äktheten hos signerade bilder?

Absolut. Du kan använda verifieringsmetoderna i GroupDocs.Signature för att validera metadatasignaturer och bekräfta äktheten hos signerade bilder.

### Finns det en begränsning på filstorleken när man signerar bilder med metadata?

Det finns ingen specifik begränsning för filstorleken som införs av själva biblioteket, men mycket stora filer kan kräva mer bearbetningstid och minne. Det rekommenderas att man tar hänsyn till systemresurser när man arbetar med extremt stora bilder.

### Hur kan jag få en tillfällig licens för teständamål?

Du kan få en [tillfällig licens](https://purchase.groupdocs.com/temporary-license/) för att testa GroupDocs.Signature innan ett köp görs.

### Var kan jag hitta fler resurser och stöd?

- [API-referens](https://reference.groupdocs.com/signature/net/)
- [Nedladdningar](https://releases.groupdocs.com/signature/net/)
- [Exempel](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [Dokumentation](https://docs.groupdocs.com/signature/net/)
- [Produktsida](https://products.groupdocs.com/signature/net/)
- [Blogg](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [Supportforum](https://forum.groupdocs.com/c/signature/13)