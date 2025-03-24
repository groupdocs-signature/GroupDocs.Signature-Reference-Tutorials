---
title: Documentinformatie ophalen
linktitle: Documentinformatie ophalen
second_title: GroupDocs.Signature .NET API
description: Verbeter documentbeheer in .NET met GroupDocs.Signature. Haal stap voor stap documentinformatie op. Ondersteunt verschillende formaten.
weight: 11
url: /nl/net/document-preview-operations/retrieve-document-information/
---

# Documentinformatie ophalen

## Invoering
Op het gebied van digitale documentatie is het waarborgen van authenticiteit en integriteit van het allergrootste belang. GroupDocs.Signature voor .NET biedt een robuuste oplossing voor het beheren van documenthandtekeningen binnen de .NET-omgeving. In deze zelfstudie verdiepen we ons in het proces van het ophalen van documentinformatie met behulp van GroupDocs.Signature voor .NET, waarbij we elke stap opsplitsen voor een uitgebreid begrip.
## Vereisten
Voordat u in de zelfstudie duikt, moet u ervoor zorgen dat u aan de volgende vereisten voldoet:
1.  Installatie: Installeer GroupDocs.Signature voor .NET door het te downloaden van[hier](https://releases.groupdocs.com/signature/net/).
2. .NET-omgeving: heb praktische kennis van het .NET-framework.
3. Document: bereid een voorbeelddocument voor (bijvoorbeeld "sample_multiple_signatures.docx") voor testdoeleinden.

## Naamruimten importeren
Voordat u doorgaat met het ophalen van documenthandtekeningen, importeert u de benodigde naamruimten:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
```

## Stap 1: Stel het documentbestandspad in:
Definieer het bestandspad voor het document waaruit u informatie wilt ophalen.
```csharp
string filePath = "sample_multiple_signatures.docx";
```
## Stap 2: Handtekeningobject instantiëren:
 Maak een exemplaar van de`Signature` klasse door het documentbestandspad door te geven.
```csharp
using (Signature signature = new Signature(filePath))
{

}
```
## Stap 3: Documentinformatie ophalen:
 Maak gebruik van de`GetDocumentInfo()` methode om uitgebreide informatie over het document op te halen.
```csharp
IDocumentInfo documentInfo = signature.GetDocumentInfo();
```
## Stap 4: Documenteigenschappen weergeven:
Voer verschillende eigenschappen van het document uit, zoals formaat, extensie, grootte, aantal pagina's, enz.
```csharp
Console.WriteLine($"Document properties {Path.GetFileName(filePath)}:");
Console.WriteLine($" - format : {documentInfo.FileType.FileFormat}");
Console.WriteLine($" - extension : {documentInfo.FileType.Extension}");
Console.WriteLine($" - size : {documentInfo.Size}");
Console.WriteLine($" - page count : {documentInfo.PageCount}");
Console.WriteLine($" - Form Fields count : {documentInfo.FormFields.Count}");
Console.WriteLine($" - Text signatures count : {documentInfo.TextSignatures.Count}");
Console.WriteLine($" - Image signatures count : {documentInfo.ImageSignatures.Count}");
Console.WriteLine($" - Digital signatures count : {documentInfo.DigitalSignatures.Count}");
Console.WriteLine($" - Barcode signatures count : {documentInfo.BarcodeSignatures.Count}");
Console.WriteLine($" - QrCode signatures count : {documentInfo.QrCodeSignatures.Count}");
Console.WriteLine($" - FormField signatures count : {documentInfo.FormFieldSignatures.Count}");
foreach (PageInfo pageInfo in documentInfo.Pages)
{
   Console.WriteLine($" - page-{pageInfo.PageNumber} Width {pageInfo.Width}, Height {pageInfo.Height}");
}
```


## Conclusie
GroupDocs.Signature voor .NET biedt een krachtig pakket tools voor het naadloos beheren van documenthandtekeningen binnen het .NET-framework. Door de stappen in deze handleiding te volgen, kunt u op efficiënte wijze uitgebreide informatie over uw documenten ophalen, waardoor u verbeterde mogelijkheden voor documentbeheer krijgt.

## Veelgestelde vragen
### Kan GroupDocs.Signature voor .NET meerdere documentformaten verwerken?
Ja, GroupDocs.Signature ondersteunt een breed scala aan documentformaten, inclusief maar niet beperkt tot DOCX, PDF, PNG en JPEG.
### Is er een proefversie beschikbaar voor GroupDocs.Signature voor .NET?
 Ja, u kunt toegang krijgen tot de proefversie vanaf[hier](https://releases.groupdocs.com/).
### Biedt GroupDocs.Signature voor .NET ondersteuning voor digitale handtekeningen?
Absoluut, GroupDocs.Signature biedt robuuste ondersteuning voor digitale handtekeningen, waardoor de authenticiteit en integriteit van documenten wordt gegarandeerd.
### Waar kan ik aanvullende documentatie en ondersteuning vinden voor GroupDocs.Signature voor .NET?
 U kunt de uitgebreide documentatie raadplegen[hier](https://tutorials.groupdocs.com/signature/net/) en ga voor ondersteuning naar het GroupDocs-forum[hier](https://forum.groupdocs.com/c/signature/13).
### Kunnen tijdelijke licenties worden verkregen voor GroupDocs.Signature voor .NET?
 Ja, tijdelijke licenties zijn te koop[hier](https://purchase.groupdocs.com/temporary-license/).