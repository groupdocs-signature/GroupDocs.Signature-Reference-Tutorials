---
title: Onderteken PDF met metadata
linktitle: Onderteken PDF met metadata
second_title: GroupDocs.Signature .NET API
description: Leer hoe u PDF-documenten met metagegevens kunt ondertekenen met GroupDocs.Signature voor .NET. Verbeter eenvoudig de traceerbaarheid en authenticiteit van documenten.
weight: 11
url: /nl/net/document-signing/sign-pdf-with-metadata/
---

# Onderteken PDF met metadata

## Invoering
In deze zelfstudie leren we hoe u een PDF-document met metagegevens kunt ondertekenen met GroupDocs.Signature voor .NET. Het toevoegen van metagegevens aan een PDF kan aanvullende informatie over het document opleveren, zoals auteurschap, aanmaakdatum, document-ID en meer.
## Vereisten
Voordat we beginnen, zorg ervoor dat u over het volgende beschikt:
1.  GroupDocs.Signature voor .NET: u kunt het downloaden van[hier](https://releases.groupdocs.com/signature/net/).
2. Een PDF-document: Zorg ervoor dat u een voorbeeld-PDF-bestand gereed heeft om te ondertekenen.
3. Basiskennis van C#-programmering: Bekendheid met de C#-syntaxis is vereist om de codevoorbeelden te begrijpen.
## Naamruimten importeren
Zorg er eerst voor dat u de benodigde naamruimten importeert om toegang te krijgen tot de vereiste klassen en methoden:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Stap 1: Laad het PDF-document
Laad het PDF-document dat u wilt ondertekenen:
```csharp
string filePath = "sample.pdf";
```
## Stap 2: Geef het uitvoerbestandspad op
Definieer het pad van het uitvoerbestand waar de ondertekende PDF met metagegevens wordt opgeslagen:
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignPdfWithMetadata", "SignedWithMetadata.pdf");
```
## Stap 3: Maak een handtekeninginstantie
Initialiseer een Signature-instantie door het pad naar het PDF-document op te geven:
```csharp
using (Signature signature = new Signature(filePath))
{
    // Handtekeninggerelateerde code komt hier terecht
}
```
## Stap 4: Definieer metadata-opties
Maak MetadataSignOptions aan en voeg metadatavelden toe met hun respectievelijke waarden:
```csharp
MetadataSignOptions options = new MetadataSignOptions();
options
    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // Tekenreekswaarde
    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // DateTime-waarden
    .Add(new PdfMetadataSignature("DocumentId", 123456))            // Integere waarde
    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // Dubbele waarde
    .Add(new PdfMetadataSignature("Amount", 123.456M))              // Decimale waarde
    .Add(new PdfMetadataSignature("Total", 123.456F));              // Zwevende waarde
```
## Stap 5: Onderteken het document
Onderteken het PDF-document met de opgegeven metadata-opties en sla het ondertekende document op:
```csharp
SignResult result = signature.Sign(outputFilePath, options);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## Conclusie
In deze zelfstudie hebben we besproken hoe u een PDF-document met metagegevens kunt ondertekenen met GroupDocs.Signature voor .NET. Door de stapsgewijze handleiding te volgen, kunt u eenvoudig metadata-informatie, zoals auteurschap, aanmaakdatum en meer, aan uw PDF-bestanden toevoegen, waardoor de bruikbaarheid en traceerbaarheid ervan wordt vergroot.
## Veelgestelde vragen
### Kan ik aangepaste metagegevensvelden toevoegen aan mijn PDF-documenten?
Ja, u kunt aangepaste metagegevensvelden toevoegen door de veldnaam en de bijbehorende waarde op te geven met GroupDocs.Signature voor .NET.
### Is GroupDocs.Signature voor .NET compatibel met alle versies van .NET Framework?
GroupDocs.Signature voor .NET is compatibel met verschillende versies van .NET Framework, wat flexibiliteit en integratiegemak garandeert.
### Ondersteunt GroupDocs.Signature het ondertekenen van andere documentformaten dan PDF?
Ja, GroupDocs.Signature ondersteunt een breed scala aan documentformaten, waaronder Word, Excel, PowerPoint en meer.
### Kan ik meerdere documenten bulksgewijs ondertekenen met GroupDocs.Signature voor .NET?
Ja, u kunt meerdere documenten in bulk ondertekenen door een lijst met bestanden te doorlopen en het ondertekeningsproces programmatisch toe te passen.
### Is er technische ondersteuning beschikbaar voor GroupDocs.Signature-gebruikers?
 Ja, GroupDocs biedt speciale technische ondersteuning via zijn forums. U kunt toegang krijgen tot het ondersteuningsforum[hier](https://forum.groupdocs.com/c/signature/13).