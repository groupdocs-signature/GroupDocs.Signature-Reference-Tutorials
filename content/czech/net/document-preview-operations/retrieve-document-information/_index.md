---
title: Načíst informace o dokumentu
linktitle: Načíst informace o dokumentu
second_title: GroupDocs.Signature .NET API
description: Vylepšete správu dokumentů v .NET pomocí GroupDocs.Signature. Získejte informace o dokumentu krok za krokem. Podporuje různé formáty.
type: docs
weight: 11
url: /cs/net/document-preview-operations/retrieve-document-information/
---
## Úvod
V oblasti digitální dokumentace je prvořadé zajištění autenticity a integrity. GroupDocs.Signature for .NET poskytuje robustní řešení pro správu podpisů dokumentů v prostředí .NET. V tomto tutoriálu se ponoříme do procesu získávání informací o dokumentech pomocí GroupDocs.Signature for .NET a rozebereme každý krok pro komplexní pochopení.
## Předpoklady
Než se pustíte do výukového programu, ujistěte se, že máte splněny následující předpoklady:
1.  Instalace: Nainstalujte GroupDocs.Signature for .NET stažením z[tady](https://releases.groupdocs.com/signature/net/).
2. Prostředí .NET: Mít pracovní znalost rámce .NET.
3. Dokument: Připravte vzorový dokument (např. "sample_multiple_signatures.docx") pro testovací účely.

## Import jmenných prostorů
Než budete pokračovat v procesu získávání podpisu dokumentu, importujte potřebné jmenné prostory:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
```

## Krok 1: Nastavte cestu k souboru dokumentu:
Definujte cestu k souboru pro dokument, ze kterého chcete načíst informace.
```csharp
string filePath = "sample_multiple_signatures.docx";
```
## Krok 2: Objekt okamžitého podpisu:
 Vytvořte instanci souboru`Signature` třídy předáním cesty k souboru dokumentu.
```csharp
using (Signature signature = new Signature(filePath))
{

}
```
## Krok 3: Načtení informací o dokumentu:
 Využijte`GetDocumentInfo()` metoda k načtení komplexních informací o dokumentu.
```csharp
IDocumentInfo documentInfo = signature.GetDocumentInfo();
```
## Krok 4: Zobrazení vlastností dokumentu:
Výstup různých vlastností dokumentu, jako je formát, přípona, velikost, počet stránek atd.
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


## Závěr
GroupDocs.Signature for .NET nabízí výkonnou sadu nástrojů pro bezproblémovou správu podpisů dokumentů v rámci .NET. Podle kroků uvedených v této příručce můžete efektivně získat komplexní informace o svých dokumentech, což usnadní vylepšené možnosti správy dokumentů.

## FAQ
### Dokáže GroupDocs.Signature for .NET zpracovat více formátů dokumentů?
Ano, GroupDocs.Signature podporuje širokou škálu formátů dokumentů, včetně, ale bez omezení na DOCX, PDF, PNG a JPEG.
### Je k dispozici zkušební verze pro GroupDocs.Signature pro .NET?
 Ano, ke zkušební verzi máte přístup z[tady](https://releases.groupdocs.com/).
### Poskytuje GroupDocs.Signature for .NET podporu pro digitální podpisy?
GroupDocs.Signature rozhodně nabízí robustní podporu pro digitální podpisy, což zajišťuje pravost a integritu dokumentu.
### Kde najdu další dokumentaci a podporu pro GroupDocs.Signature pro .NET?
 Můžete se podívat na komplexní dokumentaci[tady](https://reference.groupdocs.com/signature/net/) a pro podporu navštivte fórum GroupDocs[tady](https://forum.groupdocs.com/c/signature/13).
### Lze získat dočasné licence pro GroupDocs.Signature for .NET?
 Ano, dočasné licence je možné zakoupit[tady](https://purchase.groupdocs.com/temporary-license/).