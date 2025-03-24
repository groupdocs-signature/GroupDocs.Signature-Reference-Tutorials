---
title: Signering med digital signatur
linktitle: Signering med digital signatur
second_title: GroupDocs.Signature .NET API
description: Lär dig hur du signerar dokument digitalt i .NET med GroupDocs.Signature. Förbättra säkerheten och autenticiteten med denna omfattande handledning.
weight: 12
url: /sv/net/advanced-signature-techniques/sign-with-digital/
---

# Signering med digital signatur

## Introduktion
Digitala signaturer spelar en avgörande roll för att säkerställa elektroniska dokuments äkthet och integritet. Inom området för .NET-utveckling erbjuder GroupDocs.Signature en kraftfull lösning för att sömlöst integrera digitala signaturer i dina applikationer. Denna handledning guidar dig genom processen att signera ett dokument med en digital signatur med GroupDocs.Signature för .NET.
## Förutsättningar
Innan vi dyker in i implementeringen, se till att du har följande förutsättningar på plats:
1.  GroupDocs.Signature för .NET: Ladda ner och installera GroupDocs.Signature för .NET från[nedladdningssida](https://releases.groupdocs.com/signature/net/).
2. Digitalt certifikat: Skaffa ett digitalt certifikat (.pfx) som kommer att användas för att signera dokumentet. Om du inte har ett kan du skapa ett självsignerat certifikat eller skaffa det från en betrodd certifikatutfärdare.
3. Dokument att signera: Förbered dokumentet (t.ex. PDF) som du vill signera digitalt. Se till att du har nödvändiga behörigheter för att komma åt och ändra dokumentet.
4. Signaturbild: Alternativt kan du tillhandahålla en bild av din signatur som kommer att bäddas in i dokumentet. Detta ger en personlig touch till den digitala signaturen.

## Importera namnområden
Låt oss först importera de nödvändiga namnrymden till vår C#-kod:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Steg 1: Ange filsökvägar och alternativ
Definiera filsökvägarna för dokumentet som ska signeras, signaturbilden (om tillämpligt) och det digitala certifikatet.
```csharp
string filePath = "sample.pdf";
string fileName = Path.GetFileName(filePath);
string imagePath = "signature_handwrite.jpg";
string certificatePath = "YourSignature.pfx";
string outputFilePath = Path.Combine("Your Document Directory", "SignWithDigital", fileName);
```
## Steg 2: Initiera signaturobjekt
 Skapa en instans av`Signature` klass genom att passera sökvägen till dokumentet som ska undertecknas.
```csharp
using (Signature signature = new Signature(filePath))
{
    // Definiera alternativ för digitala signaturer
    DigitalSignOptions options = new DigitalSignOptions(certificatePath)
    {
        ImageFilePath = imagePath, // Ställ in sökväg för bildfil (valfritt)
        Left = 50,                 //Ställ in X-koordinaten för signaturpositionen
        Top = 50,                  // Ställ in Y-koordinat för signaturposition
        PageNumber = 1,            // Ange sidnumret som ska signeras
        Password = "1234567890"    // Ange lösenord för certifikat (om det krävs)
    };
    // Steg 3: Signera dokumentet
    SignResult result = signature.Sign(outputFilePath, options);
    // Steg 4: Visa resultat
    Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
}
```

## Slutsats
I den här handledningen har vi utforskat hur man signerar ett dokument med en digital signatur med GroupDocs.Signature för .NET. Genom att följa dessa enkla steg kan du förbättra säkerheten och äktheten för dina elektroniska dokument, och se till att de förblir manipuleringssäkra och juridiskt bindande.
## FAQ's
### Vad är en digital signatur?
En digital signatur är en kryptografisk teknik som används för att verifiera äktheten och integriteten hos digitala dokument eller meddelanden.
### Kan jag signera dokument med GroupDocs.Signature med ett självsignerat certifikat?
Ja, du kan signera dokument med ett självsignerat certifikat som genereras av verktyg som OpenSSL eller Microsofts MakeCert.
### Är GroupDocs.Signature kompatibel med olika dokumentformat?
Ja, GroupDocs.Signature stöder ett brett utbud av dokumentformat, inklusive PDF, Word, Excel, PowerPoint och mer.
### Kan jag anpassa utseendet på min digitala signatur?
Absolut! Med GroupDocs.Signature kan du anpassa olika aspekter av din digitala signatur, såsom dess position, storlek och utseende.
### Är GroupDocs.Signature lämplig för applikationer på företagsnivå?
Ja, GroupDocs.Signature erbjuder robusta funktioner och skalbarhet, vilket gör det till ett idealiskt val för dokumentsigneringsapplikationer på företagsnivå.