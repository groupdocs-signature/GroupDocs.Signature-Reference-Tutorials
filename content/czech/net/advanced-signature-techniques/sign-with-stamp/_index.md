---
title: Podepisování razítkem pomocí GroupDocs.Signature
linktitle: Podepisování razítkem
second_title: GroupDocs.Signature .NET API
description: Naučte se, jak snadno přidat podpisy razítek do dokumentů .NET pomocí GroupDocs.Signature pro .NET. Zvyšte zabezpečení dokumentů.
weight: 16
url: /cs/net/advanced-signature-techniques/sign-with-stamp/
---

# Podepisování razítkem pomocí GroupDocs.Signature

## Úvod
V tomto tutoriálu vás provedeme procesem podepisování dokumentu razítkem pomocí GroupDocs.Signature for .NET. Podle těchto podrobných pokynů budete moci snadno přidat podpis razítka do svých dokumentů.
## Předpoklady
Než začneme, ujistěte se, že máte následující předpoklady:
1.  GroupDocs.Signature for .NET SDK: Stáhněte a nainstalujte SDK z[webová stránka](https://releases.groupdocs.com/signature/net/).
2. Vývojové prostředí: Ujistěte se, že máte pro vývoj .NET nastaveno vhodné vývojové prostředí.
3. Dokument k podpisu: Připravte dokument (např. PDF), který chcete podepsat razítkem.

## Import jmenných prostorů
Začněte importováním potřebných jmenných prostorů do vašeho projektu:
```csharp
using System;
using System.IO;
using System.Drawing;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Krok 1: Vložte dokument
```csharp
string filePath = "sample.pdf";
using (Signature signature = new Signature(filePath))
{
    // Váš kód je zde
}
```
## Krok 2: Nastavte možnosti znaku razítka
```csharp
StampSignOptions options = new StampSignOptions()
{
    Left = 50,
    Top = 150,                    
    Width = 200,
    Height = 200
};
```
## Krok 3: Nakonfigurujte vzhled razítka
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
## Krok 4: Podepište dokument
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignWithStamp", fileName);
SignResult result = signature.Sign(outputFilePath, options);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## Závěr
Přidávání podpisů razítek do vašich dokumentů pomocí GroupDocs.Signature for .NET je jednoduchý proces, jak je ukázáno v tomto tutoriálu. Pomocí uvedených kroků můžete snadno zvýšit zabezpečení a autenticitu svých dokumentů.
## FAQ
### Mohu upravit vzhled podpisu razítka?
Ano, různé aspekty, jako je text, písmo, barva a umístění podpisu razítka, si můžete přizpůsobit podle svých požadavků.
### Podporuje GroupDocs.Signature podepisování více formátů dokumentů?
Ano, GroupDocs.Signature podporuje širokou škálu formátů dokumentů včetně PDF, Microsoft Word, Excel, PowerPoint a dalších.
### Je k dispozici zkušební verze pro GroupDocs.Signature?
 Ano, máte přístup k bezplatné zkušební verzi z[webová stránka](https://releases.groupdocs.com/).
### Mohu k jednomu dokumentu přidat více podpisů?
Rozhodně, GroupDocs.Signature umožňuje přidat více podpisů, včetně razítek, textu, obrázků a digitálních podpisů, do jednoho dokumentu.
### Kde najdu podporu, pokud během implementace narazím na nějaké problémy?
 Podporu a pomoc můžete najít na fóru komunity GroupDocs.Signature[tady](https://forum.groupdocs.com/c/signature/13).