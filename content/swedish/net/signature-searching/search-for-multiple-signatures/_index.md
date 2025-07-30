---
"description": "Lär dig hur du söker efter flera signaturtyper i dokument med GroupDocs.Signature för .NET. Omfattande guide med kodexempel för förbättrad dokumentsäkerhet."
"linktitle": "Sök efter flera signaturer"
"second_title": "GroupDocs.Signature .NET API"
"title": "Sök efter flera signaturtyper i dokument"
"url": "/sv/net/signature-searching/search-for-multiple-signatures/"
"weight": 14
---

## Introduktion

moderna dokumenthanteringssystem blir möjligheten att söka efter och validera flera signaturtyper inom ett enda dokument allt viktigare. Organisationer använder ofta olika signaturtyper – såsom digitala signaturer, textsignaturer, streckkoder, QR-koder med mera – för att förbättra dokumentsäkerheten och effektivisera verifieringsprocesser. GroupDocs.Signature för .NET tillhandahåller ett kraftfullt ramverk som gör det möjligt för utvecklare att implementera omfattande sökfunktioner för signaturer i olika dokumentformat.

Den här handledningen guidar dig genom processen att söka efter flera signaturtyper i dokument med GroupDocs.Signature för .NET, och erbjuder detaljerade förklaringar och praktiska kodexempel.

## Förkunskapskrav

Innan du börjar implementera en funktion för sökning med flera signaturer, se till att du har följande förutsättningar:

1. Utvecklingsmiljö: Visual Studio eller annan föredragen .NET-utvecklingsmiljö installerad på ditt system.
  
2. GroupDocs.Signature för .NET: Ladda ner och installera GroupDocs.Signature för .NET-biblioteket från [här](https://releases.groupdocs.com/signature/net/).

3. Grundläggande C#-kunskaper: Bekantskap med programmeringsspråket C# och .NET framework-koncept.

4. Exempeldokument: Förbered testdokument som innehåller olika typer av signaturer för teständamål.

## Importera namnrymder

Börja med att importera de namnrymder som behövs för att komma åt GroupDocs.Signature-funktionen:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Nu ska vi dela upp processen att söka efter flera signaturtyper i tydliga, hanterbara steg:

## Steg 1: Ladda dokumentet

Ladda först dokumentet som innehåller de signaturer du vill söka efter:

```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // Sökkod för flera signaturer kommer att läggas till här
}
```

## Steg 2: Definiera sökalternativ för olika signaturtyper

Skapa sökalternativ för varje signaturtyp du vill söka efter:

```csharp
// Definiera sökalternativ för textsignaturer
TextSearchOptions textOptions = new TextSearchOptions
{
    AllPages = true,  // Sök på alla sidor
    Text = "Signature",  // Valfritt: text att söka
    MatchType = TextMatchType.Contains  // Matchande kriterier
};

// Definiera sökalternativ för digitala signaturer
DigitalSearchOptions digitalOptions = new DigitalSearchOptions
{
    AllPages = true
};

// Definiera sökalternativ för streckkodssignaturer
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions
{
    AllPages = true,
    Text = "123456",  // Valfritt: matchande streckkodstext
    MatchType = TextMatchType.Exact  // Matchande kriterier
};

// Definiera sökalternativ för QR-kodsignaturer
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions
{
    AllPages = true,
    Text = "John",  // Valfritt: QR-kodstext som matchar
    MatchType = TextMatchType.Contains  // Matchande kriterier
};

// Definiera sökalternativ för metadatasignaturer
MetadataSearchOptions metadataOptions = new MetadataSearchOptions();
```

## Steg 3: Lägg till alternativ i en samling

Lägg till alla sökalternativ i en samling:

```csharp
// Skapa en lista för att innehålla alla sökalternativ
List<SearchOptions> searchOptions = new List<SearchOptions>
{
    textOptions,
    digitalOptions,
    barcodeOptions,
    qrCodeOptions,
    metadataOptions
};
```

## Steg 4: Utför sökningen och bearbeta resultaten

Utför sökningen med de kombinerade sökalternativen och bearbeta resultaten:

```csharp
// Sök efter alla signaturtyper med hjälp av de definierade alternativen
SearchResult result = signature.Search(searchOptions);

// Kontrollera om signaturer hittades
if (result.Signatures.Count > 0)
{
    Console.WriteLine($"\nSource document ['{filePath}'] contains {result.Signatures.Count} signature(s):");
    
    // Iterera igenom de funna signaturerna
    foreach (var foundSignature in result.Signatures)
    {
        Console.WriteLine($"Signature found: Type: {foundSignature.SignatureType}, Page: {foundSignature.PageNumber}, ID: {foundSignature.SignatureId}");
        
        // Processspecifika signaturtyper
        if (foundSignature is TextSignature textSignature)
        {
            Console.WriteLine($"Text: '{textSignature.Text}'");
        }
        else if (foundSignature is BarcodeSignature barcodeSignature)
        {
            Console.WriteLine($"Barcode Type: {barcodeSignature.EncodeType.TypeName}, Text: '{barcodeSignature.Text}'");
        }
        else if (foundSignature is QrCodeSignature qrCodeSignature)
        {
            Console.WriteLine($"QR Code Type: {qrCodeSignature.EncodeType.TypeName}, Text: '{qrCodeSignature.Text}'");
        }
        else if (foundSignature is DigitalSignature digitalSignature)
        {
            Console.WriteLine($"Certificate: {digitalSignature.Certificate?.SubjectName}, Valid: {digitalSignature.IsValid}");
        }
        else if (foundSignature is MetadataSignature metadataSignature)
        {
            Console.WriteLine($"Metadata: Name: {metadataSignature.Name}, Value: {metadataSignature.Value}");
        }
    }
}
else
{
    Console.WriteLine("No signatures were found in the document.");
}
```

## Komplett exempel

Här är ett komplett, fungerande exempel som visar hur man söker efter flera signaturtyper i ett dokument:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace MultiSignatureSearch
{
    class Program
    {
        static void Main(string[] args)
        {
            // Dokumentsökväg
            string filePath = "sample_multiple_signatures.docx";
            
            // Initiera signaturinstansen
            using (Signature signature = new Signature(filePath))
            {
                try
                {
                    // Definiera sökalternativ för textsignaturer
                    TextSearchOptions textOptions = new TextSearchOptions
                    {
                        AllPages = true,
                        MatchType = TextMatchType.Contains
                    };

                    // Definiera sökalternativ för digitala signaturer
                    DigitalSearchOptions digitalOptions = new DigitalSearchOptions
                    {
                        AllPages = true
                    };

                    // Definiera sökalternativ för streckkodssignaturer
                    BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions
                    {
                        AllPages = true
                    };

                    // Definiera sökalternativ för QR-kodsignaturer
                    QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions
                    {
                        AllPages = true
                    };

                    // Definiera sökalternativ för metadatasignaturer
                    MetadataSearchOptions metadataOptions = new MetadataSearchOptions();

                    // Skapa en lista för att innehålla alla sökalternativ
                    List<SearchOptions> searchOptions = new List<SearchOptions>
                    {
                        textOptions,
                        digitalOptions,
                        barcodeOptions,
                        qrCodeOptions,
                        metadataOptions
                    };

                    // Sök efter alla signaturtyper
                    SearchResult result = signature.Search(searchOptions);

                    // Kontrollera om signaturer hittades
                    if (result.Signatures.Count > 0)
                    {
                        Console.WriteLine($"\nSource document ['{filePath}'] contains {result.Signatures.Count} signature(s):");
                        
                        // Bearbeta resultat efter signaturtyp
                        foreach (var foundSignature in result.Signatures)
                        {
                            Console.WriteLine($"Signature found: Type: {foundSignature.SignatureType}, Page: {foundSignature.PageNumber}");
                            
                            // Processspecifika signaturtyper
                            switch (foundSignature.SignatureType)
                            {
                                case SignatureType.Text:
                                    var textSignature = foundSignature as TextSignature;
                                    Console.WriteLine($"Text: '{textSignature.Text}'");
                                    break;
                                    
                                case SignatureType.Barcode:
                                    var barcodeSignature = foundSignature as BarcodeSignature;
                                    Console.WriteLine($"Barcode Type: {barcodeSignature.EncodeType.TypeName}, Text: '{barcodeSignature.Text}'");
                                    break;
                                    
                                case SignatureType.QrCode:
                                    var qrCodeSignature = foundSignature as QrCodeSignature;
                                    Console.WriteLine($"QR Code Type: {qrCodeSignature.EncodeType.TypeName}, Text: '{qrCodeSignature.Text}'");
                                    break;
                                    
                                case SignatureType.Digital:
                                    var digitalSignature = foundSignature as DigitalSignature;
                                    Console.WriteLine($"Certificate: {digitalSignature.Certificate?.SubjectName}, Valid: {digitalSignature.IsValid}");
                                    break;
                                    
                                case SignatureType.Metadata:
                                    var metadataSignature = foundSignature as MetadataSignature;
                                    Console.WriteLine($"Metadata: Name: {metadataSignature.Name}, Value: {metadataSignature.Value}");
                                    break;
                            }
                            
                            Console.WriteLine(); // Lägg till radbrytning mellan signaturer
                        }
                    }
                    else
                    {
                        Console.WriteLine("No signatures were found in the document.");
                    }
                }
                catch (Exception ex)
                {
                    Console.WriteLine($"Error occurred: {ex.Message}");
                }
            }
            
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

## Avancerade söktekniker för flera signaturer

### Filtrera sökresultat

Du kan implementera avancerad filtrering för att begränsa sökresultaten:

```csharp
// Filtrera resultat efter sidnummer
var signaturesOnFirstPage = result.Signatures.FindAll(s => s.PageNumber == 1);

// Filtrera resultat efter signaturtyp
var digitalSignatures = result.Signatures.FindAll(s => s.SignatureType == SignatureType.Digital);
var qrCodeSignatures = result.Signatures.FindAll(s => s.SignatureType == SignatureType.QrCode);

// Filtrera textsignaturer som innehåller specifikt innehåll
var approvalSignatures = result.Signatures
    .FindAll(s => s is TextSignature && ((TextSignature)s).Text.Contains("Approved"));
```

### Validera flera signaturer

Implementera valideringslogik för olika signaturtyper:

```csharp
bool ValidateAllSignatures(SearchResult result)
{
    bool isDocumentValid = true;
    
    // Kontrollera om dokumentet har en giltig digital signatur
    bool hasValidDigitalSignature = result.Signatures
        .Any(s => s is DigitalSignature && ((DigitalSignature)s).IsValid);
    
    if (!hasValidDigitalSignature)
    {
        Console.WriteLine("Warning: Document does not contain a valid digital signature");
        isDocumentValid = false;
    }
    
    // Kontrollera om dokumentet har en QR-kod som krävs
    bool hasRequiredQRCode = result.Signatures
        .Any(s => s is QrCodeSignature && ((QrCodeSignature)s).Text.Contains("Auth-Code"));
    
    if (!hasRequiredQRCode)
    {
        Console.WriteLine("Warning: Document does not contain the required authentication QR code");
        isDocumentValid = false;
    }
    
    return isDocumentValid;
}
```

### Sökning med anpassad bearbetning

Du kan definiera anpassad bearbetningslogik för sökåtgärder:

```csharp
// Skapa sökalternativ med anpassad bearbetning
TextSearchOptions textOptions = new TextSearchOptions
{
    AllPages = true,
    
    // Definiera anpassad bearbetning med hjälp av en delegat
    ProcessCompleted = (signature) =>
    {
        // Anpassad valideringslogik - acceptera endast signaturer på angivna sidor
        TextSignature textSignature = signature as TextSignature;
        return textSignature != null && (textSignature.PageNumber == 1 || textSignature.PageNumber == 2);
    }
};
```

## Slutsats

I den här omfattande guiden har vi utforskat hur man söker efter flera signaturtyper i dokument med GroupDocs.Signature för .NET. Från att konfigurera sökalternativ för olika signaturtyper till att bearbeta och validera resultaten, har du nu kunskapen för att implementera robusta signatursökningsfunktioner i dina .NET-applikationer.

Möjligheten att söka efter flera signaturtyper samtidigt förbättrar dokumentverifieringsprocesser, stärker säkerhetsåtgärder och effektiviserar arbetsflöden för dokumentvalidering. GroupDocs.Signature tillhandahåller ett kraftfullt och flexibelt ramverk för att arbeta med olika signaturtyper i olika dokumentformat, vilket gör det till ett utmärkt val för dokumentbehandlingsprogram.

## Vanliga frågor

### Kan jag söka efter signaturer i lösenordsskyddade dokument?

Ja, GroupDocs.Signature stöder sökning efter signaturer i lösenordsskyddade dokument. Du kan ange lösenordet när du initialiserar `Signature` objekt:

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // Sök efter signaturer
}
```

### Vilka dokumentformat stöds för signatursökning?

GroupDocs.Signature stöder ett brett utbud av dokumentformat, inklusive PDF, Microsoft Office-dokument (Word, Excel, PowerPoint), OpenOffice-format, bilder och mer.

### Kan jag begränsa sökningen till specifika sidor i ett dokument?

Ja, varje sökalternativstyp har egenskaper som låter dig ange vilka sidor som ska sökas på:

```csharp
TextSearchOptions options = new TextSearchOptions
{
    AllPages = false,  // Sök inte på alla sidor
    PageNumber = 1,    // Sök endast på sidan 1
    
    // Eller ange flera sidor
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } }
};
```

### Hur kan jag optimera prestandan vid sökning i stora dokument?

För stora dokument kan du optimera prestandan genom att:

1. Begränsa sökningen till specifika sidor eller sidintervall
2. Använda mer specifika sökkriterier för att minska antalet potentiella träffar
3. Implementera paginering i din resultatvisning
4. Söka efter en signaturtyp åt gången om du inte behöver samtidiga resultat

### Kan jag utöka GroupDocs.Signature för att stödja anpassade signaturtyper?

Även om GroupDocs.Signature har inbyggt stöd för vanliga signaturtyper, kan du utöka dess funktionalitet genom att:

1. Skapa anpassade sökalternativsklasser härledda från `SearchOptions`
2. Implementera anpassad bearbetningslogik med hjälp av `ProcessCompleted` delegera
3. Utveckla wrapper-klasser som kombinerar flera signatursökningar med avancerad affärslogik

## Se även

* [API-referens](https://reference.groupdocs.com/signature/net/)
* [Kodexempel på GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Produktdokumentation](https://docs.groupdocs.com/signature/net/)
* [Produktsida](https://products.groupdocs.com/signature/net/)
* [Ladda ner senaste versionen](https://releases.groupdocs.com/signature/net/)
* [Bloggartiklar](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Gratis supportforum](https://forum.groupdocs.com/c/signature/13)
* [Tillfällig licens](https://purchase.groupdocs.com/temporary-license/)