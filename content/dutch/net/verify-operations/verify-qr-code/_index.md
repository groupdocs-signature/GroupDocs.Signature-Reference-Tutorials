---
"description": "Leer hoe u QR-codes in documenten kunt verifiëren met GroupDocs.Signature voor .NET. Complete handleiding met codevoorbeelden en best practices voor documentauthenticatie."
"linktitle": "QR-code verifiëren"
"second_title": "GroupDocs.Signature .NET API"
"title": "QR-code in documenten verifiëren"
"url": "/nl/net/verify-operations/verify-qr-code/"
"weight": 12
type: docs
---
## Invoering

Documentbeveiliging is een cruciaal aspect van moderne bedrijfsvoering. QR-codes zijn een steeds populairdere methode geworden om informatie in documenten te integreren die op authenticiteit kan worden geverifieerd. GroupDocs.Signature voor .NET biedt een krachtige en flexibele oplossing voor het verifiëren van QR-codes die in documenten in verschillende formaten zijn opgenomen.

Deze uitgebreide tutorial begeleidt u door het proces van het implementeren van QR-codeverificatie in uw .NET-toepassingen. Zo zorgt u ervoor dat uw documenten hun integriteit en authenticiteit behouden.

## Vereisten

Voordat u de QR-codeverificatiefunctionaliteit implementeert, moet u ervoor zorgen dat u aan de volgende vereisten voldoet:

1. GroupDocs.Signature voor .NET: Download en installeer de bibliotheek van de [downloadpagina](https://releases.groupdocs.com/signature/net/).
2. Ontwikkelomgeving: Visual Studio of een andere compatibele .NET-ontwikkelomgeving.
3. Testdocument: Een document met QR-codehandtekeningen voor verificatiedoeleinden.
4. Basiskennis: Kennis van C#-programmering en .NET Framework-concepten.

## Naamruimten importeren

Begin met het importeren van de vereiste naamruimten om toegang te krijgen tot de GroupDocs.Signature-functionaliteit:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## Stapsgewijs QR-codeverificatieproces

Volg deze gedetailleerde stappen om QR-codes in uw documenten te verifiëren:

### Stap 1: Geef het documentpad op

```csharp
// Geef het pad op naar het document met QR-codehandtekeningen
string filePath = "sample_multiple_signatures.docx";
```

Zorg ervoor dat u het voorbeeldpad vervangt door het daadwerkelijke pad naar uw document.

### Stap 2: Initialiseer het handtekeningobject

```csharp
// Maak een Signature-instantie door het documentpad door te geven
using (Signature signature = new Signature(filePath))
{
    // Verificatiecode wordt hier geïmplementeerd
}
```

De Signature-klasse is het belangrijkste toegangspunt voor alle bewerkingen in de GroupDocs.Signature API.

### Stap 3: Configureer QR-codeverificatieopties

```csharp
// Definieer QR-codeverificatieopties
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = true, // Controleer alle pagina's van het document
    Text = "John",   // Tekst ter verificatie binnen de QR-code
    MatchType = TextMatchType.Contains // Geef de tekstmatchcriteria op
};
```

Met de verificatieopties kunt u specifieke criteria voor het verificatieproces definiëren:
- `AllPages`: Instellen op true om alle documentpagina's te controleren (standaardgedrag)
- `Text`: De tekstinhoud die moet overeenkomen met de QR-code
- `MatchType`: De methode voor tekstmatching (Bevat, Exact, Begint met, enz.)

### Stap 4: Verificatieproces uitvoeren

```csharp
// Verificatie uitvoeren
VerificationResult result = signature.Verify(options);
```

Hiermee wordt het verificatieproces uitgevoerd op basis van de opties die u hebt opgegeven.

### Stap 5: Verificatieresultaten verwerken

```csharp
// Controleer het verificatieresultaat en voer de procedure dienovereenkomstig uit
if (result.IsValid)
{
    Console.WriteLine($"Document {filePath} contains valid QR code signature!");
    
    // Informatie weergeven over succesvolle handtekeningen
    foreach (QrCodeSignature signature in result.Succeeded)
    {
        Console.WriteLine($"Found valid QR Code signature with text: {signature.Text}");
        Console.WriteLine($"QR Code type: {signature.EncodeType.TypeName}");
        Console.WriteLine($"Location: Page {signature.PageNumber}, {signature.Left}x{signature.Top}");
    }
}
else
{
    Console.WriteLine($"Document {filePath} failed verification process.");
    Console.WriteLine($"Number of failed signatures: {result.Failed.Count}");
}
```

Als u de verificatieresultaten correct verwerkt, kan uw applicatie op basis van de verificatie-uitkomst de juiste maatregelen nemen.

## Volledig voorbeeld

Hier is een volledig, werkend voorbeeld dat QR-codeverificatie demonstreert:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace GroupDocs.Signature.Examples
{
    class Program
    {
        static void Main(string[] args)
        {
            // Documentpad
            string filePath = "sample_multiple_signatures.docx";
            
            // Initialiseer Signature-instantie
            using (Signature signature = new Signature(filePath))
            {
                // Verificatieopties instellen
                QrCodeVerifyOptions options = new QrCodeVerifyOptions()
                {
                    AllPages = true,
                    Text = "John",
                    MatchType = TextMatchType.Contains
                };
                
                // Controleer documenthandtekeningen
                VerificationResult result = signature.Verify(options);
                
                // Resultaten van procesverificatie
                if (result.IsValid)
                {
                    Console.WriteLine($"Document {filePath} contains valid QR code signature!");
                    
                    foreach (QrCodeSignature qrSignature in result.Succeeded)
                    {
                        Console.WriteLine($"Found valid QR Code with text: {qrSignature.Text}");
                    }
                }
                else
                {
                    Console.WriteLine($"Document {filePath} failed verification process.");
                }
            }
        }
    }
}
```

## Geavanceerde verificatieopties

GroupDocs.Signature biedt extra opties voor complexere verificatiescenario's:

### Specifieke QR-codetypen verifiëren

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    EncodeType = QrCodeTypes.QR,  // Verifieer alleen standaard QR-codes
    Text = "Confidential",
    MatchType = TextMatchType.Exact
};
```

### Verifiëren op specifieke pagina's

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = false,
    PageNumber = 2,  // Alleen verifiëren op pagina 2
    Text = "Approved"
};
```

### Reguliere expressies gebruiken voor verificatie

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    Text = "INV-\\d{6}",  // Factuurnummers matchen (bijv. INV-123456)
    MatchType = TextMatchType.Regex
};
```

## Aanbevolen procedures voor QR-codeverificatie

1. Valideer invoer altijd: zorg ervoor dat documentpaden en verificatiecriteria geldig zijn voordat u de invoer verwerkt.
2. Foutverwerking implementeren: gebruik try-catch-blokken om potentiële uitzonderingen tijdens verificatie af te handelen.
3. Houd rekening met de prestaties: bij grote documenten kunt u beter specifieke pagina's controleren dan het hele document.
4. Verificatieresultaten vastleggen: houd logboeken van verificatieprocessen bij voor auditdoeleinden.
5. Test met verschillende documentformaten: zorg ervoor dat uw verificatie werkt voor alle vereiste documentformaten.

## Conclusie

Het verifiëren van QR-codes in documenten is essentieel voor het waarborgen van de authenticiteit en integriteit van documenten. GroupDocs.Signature voor .NET biedt een uitgebreide en gebruiksvriendelijke API voor het implementeren van QR-codeverificatie in uw .NET-applicaties.

Door deze tutorial te volgen, hebt u geleerd hoe u:
- Het verificatieproces configureren en initialiseren
- Geef verschillende verificatiecriteria op
- Verificatieresultaten verwerken en interpreteren
- Geavanceerde verificatieopties implementeren

Met deze kennis kunt u de beveiliging en betrouwbaarheid van uw documentbeheersystemen verbeteren.

## Veelgestelde vragen

### Kan GroupDocs.Signature meerdere QR-codes in één document verifiëren?
Ja, GroupDocs.Signature kan meerdere QR-codes in één document verifiëren. De verificatieresultaten bevatten alle overeenkomende QR-codes.

### Welke documentformaten worden ondersteund voor QR-codeverificatie?
GroupDocs.Signature ondersteunt een breed scala aan documentformaten, waaronder PDF, Word (DOC, DOCX), Excel (XLS, XLSX), PowerPoint (PPT, PPTX), afbeeldingen en meer.

### Kan ik QR-codes verifiëren met een specifieke encryptie of opmaak?
Ja, GroupDocs.Signature biedt opties om QR-codes te verifiëren met specifieke coderingstypen en opmaakpatronen voor inhoud.

### Is het mogelijk om QR-codes te verifiëren die zijn gemaakt door applicaties van derden?
Ja, GroupDocs.Signature kan standaard QR-codes verifiëren die door de meeste applicaties worden gegenereerd, zolang ze de standaard QR-codeformaten volgen.

### Hoe ga ik om met QR-codes die binaire gegevens bevatten in plaats van tekst?
GroupDocs.Signature biedt opties voor het verifiëren van QR-codes met binaire gegevens via de `BinaryData` eigenschap van de verificatieopties.

### Gerelateerde bronnen
* [GroupDocs.Signature API-referentie](https://reference.groupdocs.com/signature/net/)
* [GroupDocs.Signature-downloads](https://releases.groupdocs.com/signature/net/)
* [Codevoorbeelden op GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Documentatie](https://docs.groupdocs.com/signature/net/)
* [Productpagina](https://products.groupdocs.com/signature/net/)
* [Blogartikelen](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Ondersteuningsforum](https://forum.groupdocs.com/c/signature/13)
* [Tijdelijke licentie](https://purchase.groupdocs.com/temporary-license/)