---
title: Signering med stämpel med GroupDocs.Signature
linktitle: Signering med stämpel
second_title: GroupDocs.Signature .NET API
description: Lär dig hur du enkelt lägger till stämpelsignaturer till dina .NET-dokument med GroupDocs.Signature for .NET. Förbättra dokumentsäkerheten.
weight: 16
url: /sv/net/advanced-signature-techniques/sign-with-stamp/
---
## Introduktion
I den här handledningen går vi igenom processen att signera ett dokument med en stämpel med GroupDocs.Signature för .NET. Genom att följa dessa steg-för-steg-instruktioner kommer du att kunna lägga till en stämpelsignatur till dina dokument med lätthet.
## Förutsättningar
Innan vi börjar, se till att du har följande förutsättningar:
1.  GroupDocs.Signature för .NET SDK: Ladda ner och installera SDK från[hemsida](https://releases.groupdocs.com/signature/net/).
2. Utvecklingsmiljö: Se till att du har en lämplig utvecklingsmiljö inrättad för .NET-utveckling.
3. Dokument att signera: Förbered dokumentet (t.ex. PDF) som du vill signera med en stämpel.

## Importera namnområden
Börja med att importera de nödvändiga namnrymden till ditt projekt:
```csharp
using System;
using System.IO;
using System.Drawing;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Steg 1: Ladda dokumentet
```csharp
string filePath = "sample.pdf";
using (Signature signature = new Signature(filePath))
{
    // Din kod kommer hit
}
```
## Steg 2: Ställ in stämpelskyltalternativ
```csharp
StampSignOptions options = new StampSignOptions()
{
    Left = 50,
    Top = 150,                    
    Width = 200,
    Height = 200
};
```
## Steg 3: Konfigurera stämpelns utseende
```csharp
StampLine outerLine = new StampLine();
outerLine.Text = " * European Union ";
outerLine.TextRepeatType = StampTextRepeatType.FullTextRepeat;
outerLine.Font.Size = 12;
outerLine.Height = 22;
outerLine.TextBottomIntent = 6;
outerLine.TextColor = Color.WhiteSmoke;
outerLine.BackgroundColor = Color.DarkSlateBlue;
options.OuterLines.Add(outerLine);
StampLine innerLine = new StampLine();
innerLine.Text = "John Smith";
innerLine.TextColor = Color.MediumVioletRed;
innerLine.Font.Size = 20;
innerLine.Font.Bold = true;
innerLine.Height = 40;
options.InnerLines.Add(innerLine);
```
## Steg 4: Signera dokumentet
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignWithStamp", fileName);
SignResult result = signature.Sign(outputFilePath, options);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## Slutsats
Att lägga till stämpelsignaturer till dina dokument med GroupDocs.Signature för .NET är en enkel process, vilket visas i den här handledningen. Med de medföljande stegen kan du enkelt förbättra säkerheten och äktheten för dina dokument.
## FAQ's
### Kan jag anpassa utseendet på stämpelsignaturen?
Ja, du kan anpassa olika aspekter som text, typsnitt, färg och placering av stämpelsignaturen enligt dina krav.
### Stöder GroupDocs.Signature signering av flera dokumentformat?
Ja, GroupDocs.Signature stöder ett brett utbud av dokumentformat inklusive PDF, Microsoft Word, Excel, PowerPoint och mer.
### Finns det en testversion tillgänglig för GroupDocs.Signature?
 Ja, du kan komma åt den kostnadsfria testversionen från[hemsida](https://releases.groupdocs.com/).
### Kan jag lägga till flera signaturer i ett enda dokument?
Absolut, GroupDocs.Signature låter dig lägga till flera signaturer, inklusive stämplar, text, bilder och digitala signaturer, till ett enda dokument.
### Var kan jag hitta support om jag stöter på några problem under implementeringen?
 Du kan hitta support och hjälp från GroupDocs.Signatures communityforum[här](https://forum.groupdocs.com/c/signature/13).