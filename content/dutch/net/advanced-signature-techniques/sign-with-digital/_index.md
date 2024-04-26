---
title: Ondertekenen met digitale handtekening
linktitle: Ondertekenen met digitale handtekening
second_title: GroupDocs.Signature .NET API
description: Leer hoe u documenten digitaal kunt ondertekenen in .NET met behulp van GroupDocs.Signature. Verbeter de beveiliging en authenticiteit met deze uitgebreide tutorial.
type: docs
weight: 12
url: /nl/net/advanced-signature-techniques/sign-with-digital/
---
## Invoering
Digitale handtekeningen spelen een cruciale rol bij het waarborgen van de authenticiteit en integriteit van elektronische documenten. Op het gebied van .NET-ontwikkeling biedt GroupDocs.Signature een krachtige oplossing voor het naadloos integreren van digitale handtekeningen in uw toepassingen. Deze tutorial leidt u door het proces van het ondertekenen van een document met behulp van een digitale handtekening met GroupDocs.Signature voor .NET.
## Vereisten
Voordat we ingaan op de implementatie, moet u ervoor zorgen dat u aan de volgende vereisten voldoet:
1.  GroupDocs.Signature voor .NET: Download en installeer GroupDocs.Signature voor .NET vanaf de[downloadpagina](https://releases.groupdocs.com/signature/net/).
2. Digitaal certificaat: verkrijg een digitaal certificaat (.pfx) dat wordt gebruikt voor het ondertekenen van het document. Als u er geen heeft, kunt u een zelfondertekend certificaat maken of dit verkrijgen bij een vertrouwde certificeringsinstantie.
3. Te ondertekenen document: Bereid het document (bijvoorbeeld PDF) voor dat u digitaal wilt ondertekenen. Zorg ervoor dat u over de benodigde machtigingen beschikt om het document te openen en te wijzigen.
4. Handtekeningafbeelding: Optioneel kunt u een afbeelding van uw handtekening opgeven die in het document wordt ingesloten. Dit voegt een persoonlijk tintje toe aan de digitale handtekening.

## Naamruimten importeren
Laten we eerst de benodigde naamruimten in onze C#-code importeren:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Stap 1: Geef bestandspaden en opties op
Definieer de bestandspaden voor het te ondertekenen document, de handtekeningafbeelding (indien van toepassing) en het digitale certificaat.
```csharp
string filePath = "sample.pdf";
string fileName = Path.GetFileName(filePath);
string imagePath = "signature_handwrite.jpg";
string certificatePath = "YourSignature.pfx";
string outputFilePath = Path.Combine("Your Document Directory", "SignWithDigital", fileName);
```
## Stap 2: Initialiseer het handtekeningobject
 Maak een exemplaar van de`Signature` klasse door het pad van het te ondertekenen document door te geven.
```csharp
using (Signature signature = new Signature(filePath))
{
    // Opties voor digitale handtekeningen definiëren
    DigitalSignOptions options = new DigitalSignOptions(certificatePath)
    {
        ImageFilePath = imagePath, // Afbeeldingsbestandspad instellen (optioneel)
        Left = 50,                 //Stel de X-coördinaat van de handtekeningpositie in
        Top = 50,                  // Stel de Y-coördinaat van de handtekeningpositie in
        PageNumber = 1,            // Geef het paginanummer op dat u wilt ondertekenen
        Password = "1234567890"    // Wachtwoord voor certificaat instellen (indien nodig)
    };
    // Stap 3: Onderteken het document
    SignResult result = signature.Sign(outputFilePath, options);
    // Stap 4: Resultaat weergeven
    Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
}
```

## Conclusie
In deze zelfstudie hebben we onderzocht hoe u een document kunt ondertekenen met een digitale handtekening met GroupDocs.Signature voor .NET. Door deze eenvoudige stappen te volgen, kunt u de veiligheid en authenticiteit van uw elektronische documenten verbeteren, zodat ze fraudebestendig en juridisch bindend blijven.
## Veelgestelde vragen
### Wat is een digitale handtekening?
Een digitale handtekening is een cryptografische techniek die wordt gebruikt om de authenticiteit en integriteit van digitale documenten of berichten te verifiëren.
### Kan ik documenten ondertekenen met GroupDocs.Signature met een zelfondertekend certificaat?
Ja, u kunt documenten ondertekenen met een zelfondertekend certificaat dat is gegenereerd door tools zoals OpenSSL of MakeCert van Microsoft.
### Is GroupDocs.Signature compatibel met verschillende documentformaten?
Ja, GroupDocs.Signature ondersteunt een breed scala aan documentformaten, waaronder PDF, Word, Excel, PowerPoint en meer.
### Kan ik het uiterlijk van mijn digitale handtekening aanpassen?
Absoluut! Met GroupDocs.Signature kunt u verschillende aspecten van uw digitale handtekening aanpassen, zoals de positie, de grootte en het uiterlijk.
### Is GroupDocs.Signature geschikt voor toepassingen op ondernemingsniveau?
Ja, GroupDocs.Signature biedt robuuste functies en schaalbaarheid, waardoor het een ideale keuze is voor toepassingen voor documentondertekening op bedrijfsniveau.