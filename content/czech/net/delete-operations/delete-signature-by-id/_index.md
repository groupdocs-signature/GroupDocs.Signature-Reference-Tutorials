---
title: Smazat podpis podle ID
linktitle: Smazat podpis podle ID
second_title: GroupDocs.Signature .NET API
description: Přečtěte si, jak odstranit podpis podle ID v dokumentech .NET pomocí knihovny GroupDocs.Signature. Snadný průvodce krok za krokem.
type: docs
weight: 11
url: /cs/net/delete-operations/delete-signature-by-id/
---
## Úvod
V tomto tutoriálu prozkoumáme, jak odstranit podpis podle jeho ID pomocí GroupDocs.Signature for .NET. GroupDocs.Signature for .NET je výkonná knihovna, která umožňuje vývojářům přidávat, odebírat nebo ověřovat digitální podpisy v různých formátech dokumentů pomocí aplikací .NET.
## Předpoklady
Než začneme, ujistěte se, že máte následující předpoklady:
1.  GroupDocs.Signature for .NET Library: Stáhněte a nainstalujte knihovnu z[tady](https://releases.groupdocs.com/signature/net/).
2. .NET Framework: Ujistěte se, že máte v systému nainstalované rozhraní .NET Framework.
3. Dokument s podpisem: Připravte dokument (např. DOCX, PDF) s podpisem, který chcete odstranit.

## Import jmenných prostorů
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Krok 1: Definujte cesty k souboru
Nejprve zadejte cestu k souboru pro dokument obsahující podpis a cestu k výstupnímu souboru, kam bude upravený dokument uložen.
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteById", fileName);
```
## Krok 2: Zkopírujte dokument
 Vzhledem k tomu,`Delete` metoda upraví dokument na místě, je nejlepší vytvořit kopii původního dokumentu.
```csharp
File.Copy(filePath, outputFilePath, true);
```
## Krok 3: Vymažte podpis podle ID
 Inicializujte`Signature` objekt s cestou k souboru dokumentu a použijte`Delete` způsob odstranění podpisu podle jeho ID.
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    string id = @"eff64a14-dad9-47b0-88e5-2ee4e3604e71";
    bool result = signature.Delete(id);
    if (result)
    {
        Console.WriteLine($"Signature with Id# '{id}' was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature with id# '{id}' was not found!");
    }
}
```

## Závěr
V tomto tutoriálu jsme se naučili, jak odstranit podpis podle jeho ID pomocí GroupDocs.Signature for .NET. Tato knihovna poskytuje pohodlný způsob, jak programově spravovat digitální podpisy v různých formátech dokumentů.
## FAQ
### Mohu smazat více podpisů najednou?
 Ano, můžete odstranit více podpisů tím, že projdete jejich ID a zavoláte na`Delete` metoda pro každé ID.
### Je GroupDocs.Signature for .NET kompatibilní se všemi formáty dokumentů?
GroupDocs.Signature for .NET podporuje širokou škálu formátů dokumentů, včetně PDF, DOCX, XLSX a dalších.
### Mohu upravit vzhled podpisu?
Ano, můžete upravit vzhled podpisu, včetně jeho polohy, velikosti, písma a barvy.
### Je k dispozici zkušební verze?
 Ano, můžete si stáhnout bezplatnou zkušební verzi z[tady](https://releases.groupdocs.com/).
### Kde najdu nápovědu nebo podporu pro GroupDocs.Signature pro .NET?
 Můžete navštívit fórum podpory[tady](https://forum.groupdocs.com/c/signature/13) pro pomoc.