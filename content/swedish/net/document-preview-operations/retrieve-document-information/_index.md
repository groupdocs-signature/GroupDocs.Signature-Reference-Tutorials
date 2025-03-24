---
title: Hämta dokumentinformation
linktitle: Hämta dokumentinformation
second_title: GroupDocs.Signature .NET API
description: Förbättra dokumenthanteringen i .NET med GroupDocs.Signature. Hämta dokumentinformation steg för steg. Stöder olika format.
weight: 11
url: /sv/net/document-preview-operations/retrieve-document-information/
---
## Introduktion
När det gäller digital dokumentation är det av största vikt att säkerställa autenticitet och integritet. GroupDocs.Signature för .NET tillhandahåller en robust lösning för att hantera dokumentsignaturer inom .NET-miljön. I den här handledningen går vi in i processen att hämta dokumentinformation med GroupDocs.Signature för .NET, och bryta ner varje steg för en heltäckande förståelse.
## Förutsättningar
Innan du dyker in i handledningen, se till att du har följande förutsättningar på plats:
1.  Installation: Installera GroupDocs.Signature för .NET genom att ladda ner det från[här](https://releases.groupdocs.com/signature/net/).
2. .NET-miljö: Ha praktiska kunskaper om .NET-ramverket.
3. Dokument: Förbered ett exempeldokument (t.ex. "sample_multiple_signatures.docx") för teständamål.

## Importera namnområden
Innan du fortsätter med processen för att hämta dokumentsignaturen, importera de nödvändiga namnrymden:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
```

## Steg 1: Ange sökväg för dokumentfil:
Definiera filsökvägen för dokumentet du tänker hämta information från.
```csharp
string filePath = "sample_multiple_signatures.docx";
```
## Steg 2: Instantiera signaturobjekt:
 Skapa en instans av`Signature` klass genom att skicka dokumentfilens sökväg.
```csharp
using (Signature signature = new Signature(filePath))
{

}
```
## Steg 3: Hämta dokumentinformation:
 Använd`GetDocumentInfo()` metod för att hämta omfattande information om dokumentet.
```csharp
IDocumentInfo documentInfo = signature.GetDocumentInfo();
```
## Steg 4: Visa dokumentegenskaper:
Skriv ut olika egenskaper för dokumentet såsom format, tillägg, storlek, sidantal, etc.
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


## Slutsats
GroupDocs.Signature för .NET erbjuder en kraftfull uppsättning verktyg för att hantera dokumentsignaturer sömlöst inom .NET-ramverket. Genom att följa stegen som beskrivs i den här guiden kan du effektivt hämta omfattande information om dina dokument, vilket underlättar förbättrade dokumenthanteringsmöjligheter.

## FAQ's
### Kan GroupDocs.Signature för .NET hantera flera dokumentformat?
Ja, GroupDocs.Signature stöder ett brett utbud av dokumentformat, inklusive men inte begränsat till DOCX, PDF, PNG och JPEG.
### Finns det en testversion tillgänglig för GroupDocs.Signature för .NET?
 Ja, du kan komma åt testversionen från[här](https://releases.groupdocs.com/).
### Ger GroupDocs.Signature för .NET stöd för digitala signaturer?
Absolut, GroupDocs.Signature erbjuder robust stöd för digitala signaturer, vilket säkerställer dokumentets autenticitet och integritet.
### Var kan jag hitta ytterligare dokumentation och support för GroupDocs.Signature för .NET?
 Du kan hänvisa till den omfattande dokumentationen[här](https://tutorials.groupdocs.com/signature/net/) , och för support, besök GroupDocs-forumet[här](https://forum.groupdocs.com/c/signature/13).
### Kan temporära licenser erhållas för GroupDocs.Signature för .NET?
 Ja, tillfälliga licenser finns att köpa[här](https://purchase.groupdocs.com/temporary-license/).