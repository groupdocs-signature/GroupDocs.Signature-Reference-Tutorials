---
"description": "Bemästra sökning efter digitala signaturer i dokument med GroupDocs.Signature för .NET. Förbättra dokumentsäkerhet och verifiering med vår detaljerade steg-för-steg-guide."
"linktitle": "Sök efter digitala signaturer"
"second_title": "GroupDocs.Signature .NET API"
"title": "Sök efter digitala signaturer i dokument"
"url": "/sv/net/signature-searching/search-for-digital-signatures/"
"weight": 11
type: docs
---
## Introduktion

I dagens digitala landskap är det avgörande för företag och organisationer att säkerställa dokumentäkthet och integritet. Digitala signaturer ger en robust mekanism för att verifiera dokumentäkthet och upptäcka obehöriga ändringar. GroupDocs.Signature för .NET erbjuder en omfattande lösning för att arbeta med digitala signaturer i olika dokumentformat, vilket gör det möjligt för utvecklare att sömlöst integrera signaturfunktioner i sina .NET-applikationer.

Den här handledningen guidar dig genom processen att söka efter digitala signaturer i dokument med GroupDocs.Signature för .NET, och ger detaljerade förklaringar och praktiska kodexempel.

## Förkunskapskrav

Innan du går in på detaljerna kring implementeringen, se till att du har följande förutsättningar:

1. GroupDocs.Signature för .NET: Ladda ner och installera biblioteket från [här](https://releases.groupdocs.com/signature/net/).
   
2. Utvecklingsmiljö: Konfigurera en .NET-utvecklingsmiljö med Visual Studio eller din föredragna IDE.
   
3. Exempeldokument: Förbered exempeldokument som innehåller digitala signaturer för teständamål.

4. Grundläggande kunskaper: Bekantskap med programmeringsspråket C# och grunderna i .NET framework.

## Importera namnrymder

Börja med att importera de namnrymder som krävs för att komma åt funktionerna som tillhandahålls av GroupDocs.Signature för .NET:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Nu ska vi dela upp processen att söka efter digitala signaturer i tydliga, hanterbara steg:

## Steg 1: Initiera signaturobjektet

Börja med att skapa en instans av `Signature` klass, skickar sökvägen till ditt dokument:

```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // Kod för att söka efter digitala signaturer kommer att läggas till här
}
```

## Steg 2: Sök efter digitala signaturer

Använd sedan `Search` metod med `SignatureType.Digital` parameter för att söka efter digitala signaturer i dokumentet:

```csharp
// Sök efter digitala signaturer i dokumentet
List<DigitalSignature> signatures = signature.Search<DigitalSignature>(SignatureType.Digital);
```

## Steg 3: Bearbeta och visa resultat

Slutligen, bearbeta sökresultaten och visa relevant information om de digitala signaturerna som hittats:

```csharp
Console.WriteLine($"\nSource document ['{filePath}'] contains the following digital signatures:");
foreach (var digitalSignature in signatures)
{
    Console.WriteLine($"Digital signature found from {digitalSignature.SignTime} with validation status: {digitalSignature.IsValid}");
    Console.WriteLine($"Certificate: Subject: {digitalSignature.Certificate?.SubjectName}");
    Console.WriteLine($"Certificate: Issuer: {digitalSignature.Certificate?.IssuerName}");
    Console.WriteLine($"Certificate: Serial Number: {digitalSignature.Certificate?.SerialNumber}");
    Console.WriteLine();
}
```

## Komplett exempel

Här är ett komplett, fungerande exempel som visar hur man söker efter digitala signaturer i ett dokument:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SearchDigitalSignatures
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
                // Sök efter digitala signaturer i dokumentet
                List<DigitalSignature> signatures = signature.Search<DigitalSignature>(SignatureType.Digital);
                
                // Visa sökresultat
                Console.WriteLine($"\nSource document ['{filePath}'] contains the following digital signatures:");
                
                if (signatures.Count > 0)
                {
                    foreach (var digitalSignature in signatures)
                    {
                        Console.WriteLine($"Digital signature found from {digitalSignature.SignTime} with validation status: {digitalSignature.IsValid}");
                        Console.WriteLine($"Certificate: Subject: {digitalSignature.Certificate?.SubjectName}");
                        Console.WriteLine($"Certificate: Issuer: {digitalSignature.Certificate?.IssuerName}");
                        Console.WriteLine($"Certificate: Serial Number: {digitalSignature.Certificate?.SerialNumber}");
                        Console.WriteLine();
                    }
                }
                else
                {
                    Console.WriteLine("No digital signatures found in the document.");
                }
            }
        }
    }
}
```

## Avancerade sökalternativ

För mer riktade sökningar kan du använda `DigitalSearchOptions` för att anpassa sökkriterierna:

```csharp
// Skapa digitala sökalternativ
DigitalSearchOptions options = new DigitalSearchOptions()
{
    // Sök endast på specifika sidor (t.ex. sidorna 1 och 2)
    PageNumber = 1,
    PagesSetup = new PagesSetup() { Pages = new List<int> { 1, 2 } },
    
    // Filtrera efter kommentarer i digitala signaturer
    Comments = "Approved",
    
    // Ange datum- och tidsintervall för sökningen
    SignDateTimeFrom = new DateTime(2022, 1, 1),
    SignDateTimeTo = DateTime.Now
};

// Sök med specifika alternativ
List<DigitalSignature> signatures = signature.Search<DigitalSignature>(options);
```

## Arbeta med certifikatinformation

Digitala signaturer innehåller värdefull certifikatinformation som du kan komma åt och validera:

```csharp
foreach (var digitalSignature in signatures)
{
    if (digitalSignature.Certificate != null)
    {
        // Egenskaper för åtkomstcertifikat
        Console.WriteLine($"Certificate Valid From: {digitalSignature.Certificate.NotBefore}");
        Console.WriteLine($"Certificate Valid To: {digitalSignature.Certificate.NotAfter}");
        
        // Kontrollera om certifikatet är inom ett giltigt datumintervall
        bool isDateValid = DateTime.Now >= digitalSignature.Certificate.NotBefore && 
                          DateTime.Now <= digitalSignature.Certificate.NotAfter;
        
        Console.WriteLine($"Certificate Date Validity: {isDateValid}");
        
        // Åtkomst till certifikatutfärdarens uppgifter
        Console.WriteLine($"Certificate Issuer: {digitalSignature.Certificate.IssuerName}");
    }
}
```

## Slutsats

GroupDocs.Signature för .NET erbjuder en kraftfull och flexibel lösning för att söka och validera digitala signaturer i dokument. I den här handledningen utforskade vi steg-för-steg-processen för att implementera sökfunktioner för digitala signaturer i .NET-applikationer, vilket ger dig kunskapen för att förbättra dokumentsäkerhet och integritetsverifiering.

Genom att utnyttja GroupDocs.Signature kan du bygga robusta dokumenthanteringssystem som säkerställer äktheten och integriteten hos dina digitala dokument, vilket främjar förtroende och efterlevnad i dina affärsprocesser.

## Vanliga frågor

### Kan GroupDocs.Signature verifiera giltigheten av digitala signaturer?

Ja, GroupDocs.Signature validerar automatiskt digitala signaturer under sökprocessen och ger valideringsstatus via `IsValid` egendomen tillhörande `DigitalSignature` klass.

### Vilka dokumentformat stöder sökning efter digitala signaturer?

GroupDocs.Signature stöder sökning efter digitala signaturer i olika format, inklusive PDF, Microsoft Office-dokument (Word, Excel, PowerPoint), OpenOffice-format med mera.

### Kan jag söka efter digitala signaturer i lösenordsskyddade dokument?

Ja, du kan söka efter digitala signaturer i lösenordsskyddade dokument genom att ange lösenordet när du initialiserar `Signature` objekt:

```csharp
LoadOptions loadOptions = new LoadOptions() { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // Sök efter digitala signaturer
}
```

### Hur kan jag kontrollera om en digital signatur skapades av en specifik person?

Du kan granska certifikatets ämnesnamn och andra egenskaper för att verifiera undertecknarens identitet:

```csharp
foreach (var signature in signatures)
{
    if (signature.Certificate?.SubjectName?.Contains("John Doe") == true)
    {
        Console.WriteLine("Found signature by John Doe");
    }
}
```

### Kan jag extrahera den offentliga nyckeln från ett digitalt signaturcertifikat?

Ja, du kan komma åt informationen om den offentliga nyckeln via certifikategenskaperna:

```csharp
if (signature.Certificate != null)
{
    // Åtkomst till information om offentlig nyckel
    Console.WriteLine($"Public Key: {signature.Certificate.GetPublicKeyString()}");
}
```

## Se även

* [API-referens](https://reference.groupdocs.com/signature/net/)
* [Kodexempel](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Produktdokumentation](https://docs.groupdocs.com/signature/net/)
* [Produktsida](https://products.groupdocs.com/signature/net/)
* [Ladda ner senaste versionen](https://releases.groupdocs.com/signature/net/)
* [Bloggartiklar](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Supportforum](https://forum.groupdocs.com/c/signature/13)
* [Tillfällig licens](https://purchase.groupdocs.com/temporary-license/)