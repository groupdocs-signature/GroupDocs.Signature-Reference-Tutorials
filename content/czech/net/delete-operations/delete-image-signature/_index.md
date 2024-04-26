---
title: Smazat podpis obrázku
linktitle: Smazat podpis obrázku
second_title: GroupDocs.Signature .NET API
description: Přečtěte si, jak odstranit podpisy obrázků z dokumentů pomocí GroupDocs.Signature for .NET. Postupujte podle našeho podrobného průvodce pro efektivní správu podpisů.
type: docs
weight: 14
url: /cs/net/delete-operations/delete-image-signature/
---
## Úvod
V tomto tutoriálu prozkoumáme, jak odstranit podpisy obrázků z dokumentů pomocí GroupDocs.Signature for .NET. GroupDocs.Signature je výkonná knihovna, která umožňuje vývojářům pracovat s digitálními podpisy, razítky a poli formulářů v rámci různých formátů dokumentů.
## Předpoklady
Než začneme, ujistěte se, že máte následující:
### 1. GroupDocs.Signature pro .NET
 Stáhněte a nainstalujte GroupDocs.Signature for .NET z[webová stránka](https://releases.groupdocs.com/signature/net/). Postupujte podle pokynů k instalaci uvedených v dokumentaci.
### 2. .NET Framework
Ujistěte se, že máte na svém počítači nainstalované rozhraní .NET Framework.
## Import jmenných prostorů
Zahrňte do projektu potřebné jmenné prostory:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
Pojďme si proces mazání podpisů obrázků rozdělit do několika kroků:
## Krok 1: Definujte cesty k souboru
Nejprve určete cesty pro vstupní dokument a výstupní dokument po odstranění podpisu:
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteImage", fileName);
```
## Krok 2: Zkopírujte zdrojový soubor
 Vzhledem k tomu,`Delete`metoda pracuje se stejným dokumentem, je nezbytné zkopírovat zdrojový soubor na jiné místo:
```csharp
File.Copy(filePath, outputFilePath, true);
```
## Krok 3: Inicializujte objekt podpisu
 Vytvořte instanci souboru`Signature` třídy a zadejte cestu k výstupnímu dokumentu:
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // Kód jde sem
}
```
## Krok 4: Vyhledejte podpisy obrázků
Definujte možnosti vyhledávání a vyhledávejte podpisy obrázků v dokumentu:
```csharp
ImageSearchOptions options = new ImageSearchOptions();
List<ImageSignature> signatures = signature.Search<ImageSignature>(options);
```
## Krok 5: Odstraňte podpis obrázku
Pokud jsou nalezeny podpisy obrázků, odstraňte první:
```csharp
if (signatures.Count > 0)
{
    ImageSignature imageSignature = signatures[0];
    bool result = signature.Delete(imageSignature);
    if (result)
    {
        Console.WriteLine($"Image signature at location {imageSignature.Left}x{imageSignature.Top} and Size {imageSignature.Size} was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature at location {imageSignature.Left}x{imageSignature.Top} and Size {imageSignature.Size} was not found!");
    }
}
```
## Závěr
V tomto tutoriálu jsme se naučili, jak odstranit podpisy obrázků z dokumentů pomocí GroupDocs.Signature for .NET. Podle tohoto podrobného průvodce mohou vývojáři efektivně spravovat digitální podpisy ve svých aplikacích.
## FAQ
### Mohu z dokumentu odstranit více podpisů obrázků?
 Ano, kód můžete upravit tak, aby smazal více podpisů obrázků iterací přes`signatures` seznam.
### Podporuje GroupDocs.Signature jiné formáty dokumentů kromě DOCX?
Ano, GroupDocs.Signature podporuje širokou škálu formátů dokumentů, včetně PDF, PPT, XLS a dalších.
### Je k dispozici zkušební verze pro GroupDocs.Signature pro .NET?
 Ano, můžete si stáhnout bezplatnou zkušební verzi z[webová stránka](https://releases.groupdocs.com/).
### Jak mohu získat podporu pro GroupDocs.Signature?
 Můžete navštívit[GroupDocs.Signature fórum](https://forum.groupdocs.com/c/signature/13) za pomoc a podporu.
### Mohu si zakoupit dočasnou licenci pro GroupDocs.Signature?
 Ano, můžete si zakoupit dočasnou licenci od[nákupní stránku](https://purchase.groupdocs.com/temporary-license/).