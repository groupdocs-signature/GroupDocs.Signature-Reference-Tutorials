---
"description": "Leer digitale handtekeningen in documenten zoeken met GroupDocs.Signature voor .NET. Verbeter de beveiliging en verificatie van uw documenten met onze gedetailleerde stapsgewijze handleiding."
"linktitle": "Zoeken naar digitale handtekeningen"
"second_title": "GroupDocs.Signature .NET API"
"title": "Zoeken naar digitale handtekeningen in documenten"
"url": "/nl/net/signature-searching/search-for-digital-signatures/"
"weight": 11
---

## Invoering

In het huidige digitale landschap is het garanderen van de authenticiteit en integriteit van documenten cruciaal voor bedrijven en organisaties. Digitale handtekeningen bieden een robuust mechanisme om de authenticiteit van documenten te verifiëren en ongeautoriseerde wijzigingen te detecteren. GroupDocs.Signature voor .NET biedt een uitgebreide oplossing voor het werken met digitale handtekeningen in verschillende documentformaten, waardoor ontwikkelaars handtekeningfunctionaliteit naadloos kunnen integreren in hun .NET-applicaties.

In deze tutorial wordt u door het proces van het zoeken naar digitale handtekeningen in documenten met behulp van GroupDocs.Signature voor .NET geleid. De tutorial geeft gedetailleerde uitleg en praktische codevoorbeelden.

## Vereisten

Voordat u in de implementatiedetails duikt, moet u ervoor zorgen dat u aan de volgende vereisten voldoet:

1. GroupDocs.Signature voor .NET: Download en installeer de bibliotheek van [hier](https://releases.groupdocs.com/signature/net/).
   
2. Ontwikkelomgeving: Stel een .NET-ontwikkelomgeving in met Visual Studio of uw favoriete IDE.
   
3. Voorbeelddocumenten: bereid voorbeelddocumenten voor met digitale handtekeningen voor testdoeleinden.

4. Basiskennis: Kennis van de programmeertaal C# en de basisprincipes van het .NET Framework.

## Naamruimten importeren

Begin met het importeren van de vereiste naamruimten om toegang te krijgen tot de functionaliteit van GroupDocs.Signature voor .NET:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Laten we het proces van het zoeken naar digitale handtekeningen opsplitsen in duidelijke, beheersbare stappen:

## Stap 1: Initialiseer het handtekeningobject

Begin met het maken van een exemplaar van de `Signature` klasse, waarbij het pad naar uw document wordt doorgegeven:

```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // Hier wordt code toegevoegd voor het zoeken naar digitale handtekeningen
}
```

## Stap 2: Zoek naar digitale handtekeningen

Gebruik vervolgens de `Search` methode met de `SignatureType.Digital` parameter om te zoeken naar digitale handtekeningen in het document:

```csharp
// Zoeken naar digitale handtekeningen in het document
List<DigitalSignature> signatures = signature.Search<DigitalSignature>(SignatureType.Digital);
```

## Stap 3: Resultaten verwerken en weergeven

Verwerk ten slotte de zoekresultaten en geef relevante informatie weer over de gevonden digitale handtekeningen:

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

## Volledig voorbeeld

Hier is een volledig, werkend voorbeeld dat laat zien hoe u naar digitale handtekeningen in een document kunt zoeken:

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
            // Documentpad
            string filePath = "sample_multiple_signatures.docx";
            
            // Initialiseer Signature-instantie
            using (Signature signature = new Signature(filePath))
            {
                // Zoeken naar digitale handtekeningen in het document
                List<DigitalSignature> signatures = signature.Search<DigitalSignature>(SignatureType.Digital);
                
                // Zoekresultaten weergeven
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

## Geavanceerde zoekopties

Voor gerichtere zoekopdrachten kunt u gebruik maken van `DigitalSearchOptions` om de zoekcriteria aan te passen:

```csharp
// Creëer digitale zoekopties
DigitalSearchOptions options = new DigitalSearchOptions()
{
    // Zoek alleen op specifieke pagina's (bijvoorbeeld pagina 1 en 2)
    PageNumber = 1,
    PagesSetup = new PagesSetup() { Pages = new List<int> { 1, 2 } },
    
    // Filteren op opmerkingen in digitale handtekeningen
    Comments = "Approved",
    
    // Datum- en tijdsbereik voor zoeken instellen
    SignDateTimeFrom = new DateTime(2022, 1, 1),
    SignDateTimeTo = DateTime.Now
};

// Zoeken met specifieke opties
List<DigitalSignature> signatures = signature.Search<DigitalSignature>(options);
```

## Werken met certificaatinformatie

Digitale handtekeningen bevatten waardevolle certificaatinformatie die u kunt raadplegen en valideren:

```csharp
foreach (var digitalSignature in signatures)
{
    if (digitalSignature.Certificate != null)
    {
        // Toegang tot certificaateigenschappen
        Console.WriteLine($"Certificate Valid From: {digitalSignature.Certificate.NotBefore}");
        Console.WriteLine($"Certificate Valid To: {digitalSignature.Certificate.NotAfter}");
        
        // Controleren of het certificaat binnen een geldig datumbereik valt
        bool isDateValid = DateTime.Now >= digitalSignature.Certificate.NotBefore && 
                          DateTime.Now <= digitalSignature.Certificate.NotAfter;
        
        Console.WriteLine($"Certificate Date Validity: {isDateValid}");
        
        // Toegang tot certificaatuitgevergegevens
        Console.WriteLine($"Certificate Issuer: {digitalSignature.Certificate.IssuerName}");
    }
}
```

## Conclusie

GroupDocs.Signature voor .NET biedt een krachtige en flexibele oplossing voor het zoeken en valideren van digitale handtekeningen in documenten. In deze tutorial hebben we het stapsgewijze proces van het implementeren van zoekfunctionaliteit voor digitale handtekeningen in .NET-applicaties onderzocht, waardoor u de kennis krijgt om de beveiliging en integriteitsverificatie van documenten te verbeteren.

Met GroupDocs.Signature kunt u robuuste documentbeheersystemen opzetten die de authenticiteit en integriteit van uw digitale documenten garanderen en zo het vertrouwen en de naleving van wet- en regelgeving in uw bedrijfsprocessen bevorderen.

## Veelgestelde vragen

### Kan GroupDocs.Signature de geldigheid van digitale handtekeningen verifiëren?

Ja, GroupDocs.Signature valideert automatisch digitale handtekeningen tijdens het zoekproces en geeft de validatiestatus door via de `IsValid` eigendom van de `DigitalSignature` klas.

### Welke documentformaten ondersteunen het zoeken naar digitale handtekeningen?

GroupDocs.Signature ondersteunt het zoeken naar digitale handtekeningen in verschillende formaten, waaronder PDF, Microsoft Office-documenten (Word, Excel, PowerPoint), OpenOffice-formaten en meer.

### Kan ik zoeken naar digitale handtekeningen in documenten die met een wachtwoord zijn beveiligd?

Ja, u kunt zoeken naar digitale handtekeningen in met een wachtwoord beveiligde documenten door het wachtwoord op te geven bij het initialiseren van de `Signature` voorwerp:

```csharp
LoadOptions loadOptions = new LoadOptions() { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // Zoeken naar digitale handtekeningen
}
```

### Hoe kan ik controleren of een digitale handtekening door een specifieke persoon is gemaakt?

U kunt de onderwerpnaam en andere eigenschappen van het certificaat onderzoeken om de identiteit van de ondertekenaar te verifiëren:

```csharp
foreach (var signature in signatures)
{
    if (signature.Certificate?.SubjectName?.Contains("John Doe") == true)
    {
        Console.WriteLine("Found signature by John Doe");
    }
}
```

### Kan ik de openbare sleutel uit een digitaal handtekeningcertificaat halen?

Ja, u kunt de informatie over de openbare sleutel opvragen via de certificaateigenschappen:

```csharp
if (signature.Certificate != null)
{
    // Toegang tot openbare sleutelinformatie
    Console.WriteLine($"Public Key: {signature.Certificate.GetPublicKeyString()}");
}
```

## Zie ook

* [API-referentie](https://reference.groupdocs.com/signature/net/)
* [Codevoorbeelden](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Productdocumentatie](https://docs.groupdocs.com/signature/net/)
* [Productpagina](https://products.groupdocs.com/signature/net/)
* [Download de nieuwste versie](https://releases.groupdocs.com/signature/net/)
* [Blogartikelen](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Ondersteuningsforum](https://forum.groupdocs.com/c/signature/13)
* [Tijdelijke licentie](https://purchase.groupdocs.com/temporary-license/)