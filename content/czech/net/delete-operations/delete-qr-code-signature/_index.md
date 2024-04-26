---
title: Odstraňte podpis QR kódu z dokumentu
linktitle: Odstraňte podpis QR kódu z dokumentu
second_title: GroupDocs.Signature .NET API
description: Přečtěte si, jak odstranit podpisy QR kódu z dokumentů pomocí GroupDocs.Signature for .NET. Postupujte podle našeho podrobného průvodce pro efektivní správu podpisů.
type: docs
weight: 16
url: /cs/net/delete-operations/delete-qr-code-signature/
---
## Úvod
tomto tutoriálu vás provedeme procesem odstranění podpisu QR kódu z dokumentu pomocí GroupDocs.Signature for .NET. Chcete-li účinně odstranit podpisy QR kódu, postupujte podle těchto podrobných pokynů.
## Předpoklady
Než začnete, ujistěte se, že máte následující předpoklady:
-  GroupDocs.Signature pro .NET: Ujistěte se, že máte ve svém projektu .NET nainstalovanou knihovnu GroupDocs.Signature. Můžete si jej stáhnout z[tady](https://releases.groupdocs.com/signature/net/).
- Dokument s podpisem QR kódu: Připravte si dokument obsahující podpisy QR kódu, který chcete odstranit.
- Základní znalost C#: Seznamte se se základy programovacího jazyka C#.

## Import jmenných prostorů
Než se ponoříte do kódu, importujte potřebné jmenné prostory do souboru C#:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Krok 1: Definujte cesty k souboru
```csharp
// Cesta k adresáři dokumentů.
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
// Definujte cestu k výstupnímu souboru pro upravený dokument.
string outputFilePath = Path.Combine("Your Document Directory", "DeleteQRCode", fileName);
// Zkopírujte zdrojový soubor, protože metoda Delete funguje se stejným dokumentem.
File.Copy(filePath, outputFilePath, true);
```
## Krok 2: Inicializujte objekt podpisu
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // Vytvořte možnosti pro vyhledávání podpisů QR kódu.
    QrCodeSearchOptions options = new QrCodeSearchOptions();
    // Vyhledejte v dokumentu podpisy QR kódu.
    List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(options);
```
## Krok 3: Zkontrolujte existenci podpisu QR kódu
```csharp
    if (signatures.Count > 0)
    {
        // Získejte první podpis QR kódu nalezený v dokumentu.
        QrCodeSignature qrCodeSignature = signatures[0];
```
## Krok 4: Odstraňte podpis QR kódu
```csharp
        // Odstraňte podpis QR kódu z dokumentu.
        bool result = signature.Delete(qrCodeSignature);
        if (result)
        {
            Console.WriteLine($"Signature with QR-Code '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was deleted from document ['{fileName}'].");
        }
        else
        {
            Helper.WriteError($"Signature was not deleted from the document! Signature with Barcode '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was not found!");
        }
    }
}
```
Gratulujeme! Úspěšně jste odstranili podpis QR kódu z dokumentu pomocí GroupDocs.Signature for .NET.

## Závěr
V tomto tutoriálu jsme se naučili, jak odstranit podpis QR kódu z dokumentu pomocí GroupDocs.Signature for .NET. Dodržováním uvedených kroků můžete efektivně spravovat a manipulovat s podpisy ve svých aplikacích .NET.
## FAQ
### Mohu z dokumentu odstranit více podpisů s QR kódem?
Ano, kód můžete upravit tak, aby procházel všemi podpisy QR kódu a podle toho je smazat.
### Podporuje GroupDocs.Signature jiné typy podpisů kromě QR kódů?
Ano, GroupDocs.Signature podporuje různé typy podpisů, jako je text, obrázek, čárový kód a další.
### Je GroupDocs.Signature kompatibilní se všemi formáty dokumentů?
GroupDocs.Signature podporuje širokou škálu formátů dokumentů včetně PDF, Microsoft Word, Excel, PowerPoint a dalších.
### Mohu přizpůsobit možnosti vyhledávání podpisů?
Ano, můžete upravit možnosti vyhledávání podle svých požadavků, abyste našli konkrétní podpisy v dokumentu.
### Je k dispozici zkušební verze pro GroupDocs.Signature?
 Ano, máte přístup k bezplatné zkušební verzi GroupDocs.Signature z[tady](https://releases.groupdocs.com/).