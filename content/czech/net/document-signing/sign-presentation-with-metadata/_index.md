---
title: Podepsat prezentaci s metadaty
linktitle: Podepsat prezentaci s metadaty
second_title: GroupDocs.Signature .NET API
description: Naučte se podepisovat prezentační soubory pomocí metadat pomocí GroupDocs.Signature for .NET. Vylepšete integritu dokumentů a přidejte cenné informace.
type: docs
weight: 12
url: /cs/net/document-signing/sign-presentation-with-metadata/
---
## Úvod
tomto tutoriálu se naučíme, jak podepsat prezentační soubor (PPTX) s metadaty pomocí knihovny GroupDocs.Signature for .NET. Podepisování prezentací pomocí metadat dodává dokumentu cenné informace, jako je jméno autora, datum vytvoření, ID dokumentu, ID podpisu a různé číselné hodnoty.
## Předpoklady
Než začneme, ujistěte se, že máte následující:
1.  GroupDocs.Signature for .NET Library: Stáhněte a nainstalujte knihovnu z[tady](https://releases.groupdocs.com/signature/net/).
2. Vývojové prostředí: Ujistěte se, že máte nastavené vývojové prostředí .NET.
3. Soubor prezentace: Připravte si vzorový soubor prezentace (formát PPTX) k podpisu.
4. Základní porozumění C#: Výhodou bude znalost programovacího jazyka C#.

## Import jmenných prostorů
Než se ponoříme do kódu, importujme potřebné jmenné prostory:
```csharp
using System;
using System.IO;
    using GroupDocs.Signature;
    using GroupDocs.Signature.Domain;
    using GroupDocs.Signature.Options;
```
## Krok 1: Načtěte soubor prezentace
```csharp
string filePath = "sample.pptx";
```
 Nahradit`"sample.pptx"` s cestou k souboru prezentace.
## Krok 2: Zadejte cestu k výstupnímu souboru
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignPresentationWithMetadata", "SignedWithMetadata.pptx");
```
Zadejte adresář, kam chcete uložit podepsaný soubor prezentace spolu s názvem souboru.
## Krok 3: Inicializujte objekt podpisu
```csharp
using (Signature signature = new Signature(filePath))
```
Inicializujte objekt Signature zadáním cesty k souboru prezentace.
## Krok 4: Definujte možnosti označení metadat
```csharp
MetadataSignOptions options = new MetadataSignOptions();
```
Chcete-li definovat možnosti podepisování metadat, vytvořte instanci MetadataSignOptions.
## Krok 5: Vytvořte podpisy metadat
```csharp
PresentationMetadataSignature[] signatures = new PresentationMetadataSignature[]
{
    new PresentationMetadataSignature("Author", "Mr.Scherlock Holmes"),
    new PresentationMetadataSignature("CreatedOn", DateTime.Now),
    new PresentationMetadataSignature("DocumentId", 123456),
    new PresentationMetadataSignature("SignatureId", 123.456D),
    new PresentationMetadataSignature("Amount", 123.456M),
    new PresentationMetadataSignature("Total", 123.456F)
};
```
Vytvořte pole objektů PresentationMetadataSignature, z nichž každý představuje podpis metadat. Můžete přidat různé typy metadat, včetně řetězce, data a času, celého čísla, dvojitého, desítkového a float.
## Krok 6: Přidejte podpisy do možností
```csharp
options.Signatures.AddRange(signatures);
```
Přidejte vytvořené podpisy metadat do objektu MetadataSignOptions.
## Krok 7: Podepište dokument
```csharp
SignResult result = signature.Sign(outputFilePath, options);
```
Podepište soubor prezentace s metadaty pomocí zadaných možností a uložte podepsaný soubor do výstupní cesty.
## Krok 8: Zobrazení výsledku
```csharp
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```
Zobrazí zprávu o úspěchu spolu s počtem použitých podpisů a cestou, kam je podepsaný soubor uložen.

## Závěr
V tomto tutoriálu jsme se naučili, jak podepsat prezentační soubor s metadaty pomocí knihovny GroupDocs.Signature for .NET. Přidání podpisů metadat zvyšuje integritu dokumentu a poskytuje cenné informace o jeho obsahu.

## FAQ
### Mohu podepsat jiné formáty dokumentů kromě PPTX pomocí metadat pomocí GroupDocs.Signature for .NET?
Ano, GroupDocs.Signature podporuje různé formáty dokumentů, včetně Wordu, Excelu, PDF a dalších, pro podepisování pomocí metadat.
### Je GroupDocs.Signature for .NET kompatibilní s .NET Core?
Ano, knihovna je kompatibilní s .NET Framework i .NET Core.
### Mohu přizpůsobit vzhled podpisů metadat?
Ano, vzhled, pozici a další vlastnosti podpisů metadat si můžete přizpůsobit podle svých požadavků.
### Poskytuje GroupDocs.Signature for .NET šifrování podepsaných dokumentů?
Ano, GroupDocs.Signature nabízí možnosti šifrování pro zabezpečení podepsaných dokumentů před neoprávněným přístupem.
### Je k dispozici zkušební verze pro testování před zakoupením?
 Ano, můžete využít bezplatnou zkušební verzi GroupDocs.Signature for .NET od[tady](https://releases.groupdocs.com/).