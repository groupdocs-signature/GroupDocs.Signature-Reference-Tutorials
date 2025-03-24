---
title: Vyhledejte více podpisů
linktitle: Vyhledejte více podpisů
second_title: GroupDocs.Signature .NET API
description: Naučte se vyhledávat více podpisů v dokumentech .NET pomocí GroupDocs.Signature pro efektivní zabezpečení a integritu dokumentů.
weight: 14
url: /cs/net/signature-searching/search-for-multiple-signatures/
---
## Úvod
GroupDocs.Signature for .NET je výkonná knihovna, která umožňuje vývojářům přidávat, vyhledávat a odstraňovat různé typy podpisů v oblíbených formátech dokumentů pomocí aplikací .NET. V tomto tutoriálu se zaměříme na vyhledávání více podpisů v dokumentu pomocí GroupDocs.Signature for .NET.
## Předpoklady
Než začneme, ujistěte se, že máte následující předpoklady:
- Visual Studio nainstalované ve vašem systému.
- Základní znalost programovacího jazyka C#.
- Knihovna GroupDocs.Signature for .NET nainstalovaná ve vašem projektu. Můžete si jej stáhnout z[tady](https://releases.groupdocs.com/signature/net/).

## Import jmenných prostorů
Nejprve musíte importovat potřebné jmenné prostory pro přístup ke třídám a metodám poskytovaným GroupDocs.Signature pro .NET.
```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Krok 1: Vložte dokument
Vložte dokument tam, kde chcete hledat více podpisů. Ujistěte se, že zadáváte správnou cestu k souboru.
```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // Váš kód je zde
}
```
## Krok 2: Definujte možnosti vyhledávání
Definujte možnosti vyhledávání pro různé typy podpisů, jako jsou textové, digitální, čárové kódy, QR kódy a metadata. Můžete zadat kritéria vyhledávání, jako je text, který se má shodovat, typ shody a vyhledávání na všech stránkách.
```csharp
// Definujte možnosti vyhledávání
TextSearchOptions textOptions = new TextSearchOptions()
{
    AllPages = true
};
DigitalSearchOptions digitalOptions = new DigitalSearchOptions()
{
    AllPages = true
};
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions()
{
    AllPages = true,
    Text = "123456",
    MatchType = TextMatchType.Exact
};
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions()
{
    AllPages = true,
    Text = "John",
    MatchType = TextMatchType.Contains
};
MetadataSearchOptions metadataOptions = new MetadataSearchOptions();
```
## Krok 3: Přidejte možnosti hledání do seznamu
Přidejte definované možnosti vyhledávání do seznamu.
```csharp
// Přidejte možnosti do seznamu
List<SearchOptions> listOptions = new List<SearchOptions>();
listOptions.Add(textOptions);
listOptions.Add(barcodeOptions);
listOptions.Add(qrCodeOptions);
listOptions.Add(metadataOptions);
listOptions.Add(digitalOptions);
```
## Krok 4: Vyhledejte podpisy
Vyhledejte podpisy v dokumentu pomocí definovaných možností vyhledávání.
```csharp
// Vyhledejte podpisy v dokumentu
SearchResult result = signature.Search(listOptions);
if (result.Signatures.Count > 0)
{
    Console.WriteLine($"\nSource document ['{filePath}'] contains following signatures.");
    foreach (var resSignature in result.Signatures)
    {
        Console.WriteLine($"Signature found at page {resSignature.PageNumber} with type {resSignature.SignatureType} and Id#: {resSignature.SignatureId}");
    }
}
else
{
    Helper.WriteError("No one signature was found.");
}
```

## Závěr
tomto tutoriálu jsme se naučili, jak vyhledávat více podpisů v dokumentu pomocí GroupDocs.Signature for .NET. Dodržováním uvedených kroků můžete efektivně najít různé typy podpisů ve svých dokumentech, čímž se zvýší bezpečnost a integrita dokumentů.
## FAQ
### Mohu vyhledávat podpisy v různých formátech dokumentů?
Ano, GroupDocs.Signature for .NET podporuje širokou škálu formátů dokumentů včetně Wordu, PDF, Excelu a dalších.
### Je možné upravit kritéria vyhledávání pro podpisy?
Kritéria vyhledávání můžete samozřejmě přizpůsobit svým požadavkům, jako je zadání přesné shody textu nebo vyhledávání na všech stránkách.
### Nabízí GroupDocs.Signature for .NET podporu pro digitální podpisy?
Ano, můžete vyhledávat digitální podpisy i jiné typy, jako jsou podpisy s textem, čárovým kódem a QR kódem.
### Mohu snadno integrovat funkci vyhledávání podpisů do svých aplikací .NET?
Ano, GroupDocs.Signature for .NET poskytuje přímočaré rozhraní API, které zjednodušuje proces integrace.
### Kde najdu další podporu nebo pomoc?
 Můžete navštívit fórum GroupDocs.Signature[tady](https://forum.groupdocs.com/c/signature/13) pro jakékoli dotazy nebo pomoc.