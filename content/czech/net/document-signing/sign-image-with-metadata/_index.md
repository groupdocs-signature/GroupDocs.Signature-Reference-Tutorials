---
title: Podepsat obrázek s metadaty
linktitle: Podepsat obrázek s metadaty
second_title: GroupDocs.Signature .NET API
description: Naučte se podepisovat obrázky pomocí metadat v .NET pomocí GroupDocs.Signature. Snadné, efektivní a přizpůsobitelné řešení podepisování metadat.
weight: 10
url: /cs/net/document-signing/sign-image-with-metadata/
---

# Podepsat obrázek s metadaty

## Úvod
GroupDocs.Signature for .NET umožňuje vývojářům efektivně podepisovat obrázky pomocí metadat. Tento tutoriál vás provede procesem krok za krokem.
## Předpoklady
Než začnete, ujistěte se, že máte následující:
1. GroupDocs.Signature for .NET: Nainstalujte balíček GroupDocs.Signature do svého projektu .NET. Můžete si jej stáhnout z[tady](https://releases.groupdocs.com/signature/net/).   
2. Soubor obrázku: Připravte soubor obrázku, který chcete podepsat pomocí metadat.

## Import jmenných prostorů
Ujistěte se, že jste do kódu C# importovali potřebné jmenné prostory:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Krok 1: Načtěte soubor obrázku
Nejprve zadejte cestu k souboru obrázku a výstupní adresář pro podepsaný obrázek s metadaty:
```csharp
string filePath = "sample.png";            
string outputFilePath = Path.Combine("Your Document Directory", "SignImageWithMetadata", "SignedWithMetadata.png");
```
## Krok 2: Vytvořte podpisy metadat
Dále vytvořte různé podpisy metadat a přidejte je do kolekce podpisů voleb:
```csharp
using (Signature signature = new Signature(filePath))
{
    ushort imgsMetadataId = 41996;
    MetadataSignOptions options = new MetadataSignOptions();
    options
        .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Scherlock Holmes")) // Hodnota řetězce
        .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // Datum Hodnota času
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // Celočíselná hodnota
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // Dvojnásobná hodnota
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // Desetinná hodnota
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // Plovoucí hodnota
    
    // podepsat dokument do souboru
    SignResult result = signature.Sign(outputFilePath, options);
    Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
}
```

## Závěr
V tomto kurzu jste se naučili, jak podepsat obrázek pomocí metadat pomocí GroupDocs.Signature for .NET. Pomocí těchto kroků můžete snadno začlenit podpisy metadat do svých aplikací .NET.

## FAQ
### Mohu podepsat více obrázků pomocí metadat pomocí GroupDocs.Signature for .NET?
Ano, můžete podepsat více obrázků pomocí metadat tím, že projdete každý soubor obrázku a použijete podpisy metadat.
### Je k dispozici zkušební verze pro GroupDocs.Signature pro .NET?
 Ano, zkušební verzi si můžete stáhnout z[tady](https://releases.groupdocs.com/).
### Podporuje GroupDocs.Signature for .NET jiné formáty souborů kromě obrázků?
Ano, GroupDocs.Signature podporuje různé formáty souborů, včetně PDF, Wordu, Excelu a dalších.
### Mohu přizpůsobit vzhled podpisu metadat?
Ano, můžete upravit vzhled podpisu metadat, jako je velikost písma, barva a poloha.
### Kde mohu získat podporu pro GroupDocs.Signature pro .NET?
 Podporu můžete získat na fóru GroupDocs.Signature[tady](https://forum.groupdocs.com/c/signature/13).