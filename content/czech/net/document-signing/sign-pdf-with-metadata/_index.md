---
title: Podepište PDF pomocí metadat
linktitle: Podepište PDF pomocí metadat
second_title: GroupDocs.Signature .NET API
description: Naučte se podepisovat dokumenty PDF pomocí metadat pomocí GroupDocs.Signature for .NET. Snadno vylepšete sledovatelnost a pravost dokumentů.
weight: 11
url: /cs/net/document-signing/sign-pdf-with-metadata/
---
## Úvod
tomto tutoriálu se naučíme, jak podepsat dokument PDF s metadaty pomocí GroupDocs.Signature for .NET. Přidání metadat do PDF může poskytnout další informace o dokumentu, jako je autorství, datum vytvoření, ID dokumentu a další.
## Předpoklady
Než začneme, ujistěte se, že máte následující:
1.  GroupDocs.Signature for .NET: Můžete si jej stáhnout z[tady](https://releases.groupdocs.com/signature/net/).
2. Dokument PDF: Připravte si vzorový soubor PDF k podpisu.
3. Základní znalost programování v C#: Pro pochopení příkladů kódu je nutná znalost syntaxe C#.
## Import jmenných prostorů
Nejprve se ujistěte, že importujete potřebné jmenné prostory pro přístup k požadovaným třídám a metodám:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Krok 1: Načtěte dokument PDF
Načtěte dokument PDF, který chcete podepsat:
```csharp
string filePath = "sample.pdf";
```
## Krok 2: Zadejte cestu k výstupnímu souboru
Definujte cestu k výstupnímu souboru, kam bude podepsaný PDF s metadaty uložen:
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignPdfWithMetadata", "SignedWithMetadata.pdf");
```
## Krok 3: Vytvořte instanci podpisu
Inicializujte instanci podpisu zadáním cesty k dokumentu PDF:
```csharp
using (Signature signature = new Signature(filePath))
{
    // Sem bude umístěn kód související s podpisem
}
```
## Krok 4: Definujte možnosti metadat
Vytvořte možnosti MetadataSignOptions a přidejte pole metadat s jejich příslušnými hodnotami:
```csharp
MetadataSignOptions options = new MetadataSignOptions();
options
    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // Hodnota řetězce
    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // Hodnoty DateTime
    .Add(new PdfMetadataSignature("DocumentId", 123456))            // Celočíselná hodnota
    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // Dvojnásobná hodnota
    .Add(new PdfMetadataSignature("Amount", 123.456M))              // Desetinná hodnota
    .Add(new PdfMetadataSignature("Total", 123.456F));              // Plovoucí hodnota
```
## Krok 5: Podepište dokument
Podepište dokument PDF pomocí zadaných možností metadat a uložte podepsaný dokument:
```csharp
SignResult result = signature.Sign(outputFilePath, options);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## Závěr
V tomto tutoriálu jsme probrali, jak podepsat dokument PDF s metadaty pomocí GroupDocs.Signature for .NET. Podle podrobného průvodce můžete do souborů PDF snadno přidat metadata, jako je autorství, datum vytvoření a další, a zlepšit tak jejich užitečnost a sledovatelnost.
## FAQ
### Mohu do svých dokumentů PDF přidat vlastní pole metadat?
Ano, můžete přidat vlastní pole metadat zadáním názvu pole a jeho odpovídající hodnoty pomocí GroupDocs.Signature for .NET.
### Je GroupDocs.Signature for .NET kompatibilní se všemi verzemi .NET Framework?
GroupDocs.Signature for .NET je kompatibilní s různými verzemi .NET Framework, což zajišťuje flexibilitu a snadnou integraci.
### Podporuje GroupDocs.Signature podepisování jiných formátů dokumentů kromě PDF?
Ano, GroupDocs.Signature podporuje širokou škálu formátů dokumentů, včetně Wordu, Excelu, PowerPointu a dalších.
### Mohu hromadně podepsat více dokumentů pomocí GroupDocs.Signature for .NET?
Ano, můžete hromadně podepsat více dokumentů procházením seznamu souborů a programovým použitím procesu podpisu.
### Je pro uživatele GroupDocs.Signature k dispozici technická podpora?
 Ano, GroupDocs poskytuje specializovanou technickou podporu prostřednictvím svých fór. Můžete vstoupit do fóra podpory[tady](https://forum.groupdocs.com/c/signature/13).