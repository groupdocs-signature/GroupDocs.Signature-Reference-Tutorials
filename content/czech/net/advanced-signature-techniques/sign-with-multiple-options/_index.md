---
title: Podepisování s více možnostmi
linktitle: Podepisování s více možnostmi
second_title: GroupDocs.Signature .NET API
description: Naučte se podepisovat dokumenty s více možnostmi pomocí GroupDocs.Signature for .NET. Zvyšte zabezpečení dokumentů pomocí textu, čárového kódu, QR kódu, digitálního a obrazového kódu.
weight: 14
url: /cs/net/advanced-signature-techniques/sign-with-multiple-options/
---

# Podepisování s více možnostmi

## Úvod
tomto tutoriálu prozkoumáme, jak podepsat dokument pomocí více možností podpisu pomocí knihovny GroupDocs.Signature pro .NET. Podepisování dokumentů pomocí různých možností, jako je text, čárový kód, QR kód, digitální podpisy, podpisy obrázků a metadat, může poskytnout všestrannost a zvýšit zabezpečení dokumentů.
## Předpoklady
Než začnete, ujistěte se, že máte následující předpoklady:
1.  Knihovna GroupDocs.Signature for .NET: Stáhněte a nainstalujte knihovnu GroupDocs.Signature for .NET z[tady](https://releases.groupdocs.com/signature/net/).
2. Vývojové prostředí: Nastavte vývojové prostředí s nainstalovaným rozhraním .NET Framework.
3. Dokument k podpisu: Připravte dokument (např. sample.docx), který chcete podepsat.
4. Certifikáty a obrázky: Připravte si všechny požadované certifikáty a obrázky pro digitální a obrazové podpisy.

## Import jmenných prostorů
Nejprve importujte potřebné obory názvů pro použití knihovny GroupDocs.Signature ve vaší aplikaci .NET:
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Krok 1: Vložte dokument
```csharp
string filePath = "sample.docx";
string outputFilePath = Path.Combine("Your Document Directory", "SignWithMultiple", "SignWithMultiple.docx");
using (Signature signature = new Signature(filePath))
{
    // Váš kód pokračuje...
}
```
## Krok 2: Definujte možnosti podpisu
Definujte několik možností podpisu různých typů a nastavení, jako je text, čárový kód, QR kód, digitální podpis, obrazový podpis a podpisy metadat:
```csharp
TextSignOptions textOptions = new TextSignOptions("Text signature")
{
    VerticalAlignment = VerticalAlignment.Top,
    HorizontalAlignment = HorizontalAlignment.Left
};
BarcodeSignOptions barcodeOptions = new BarcodeSignOptions("123456")
{
    EncodeType = BarcodeTypes.Code128,
    Left = 0,
    Top = 150,
    Height = 50,
    Width = 200
};
// Definujte další možnosti podpisu (např. QR kód, digitální, obrázek, metadata)...
```
## Krok 3: Vytvořte seznam možností podpisu
Definujte seznam možností podpisu obsahující všechny dříve definované možnosti:
```csharp
List<SignOptions> listOptions = new List<SignOptions>();
listOptions.Add(textOptions);
listOptions.Add(barcodeOptions);
// Přidat další možnosti podpisu do seznamu...
```
## Krok 4: Podepište dokument
Podepište dokument pomocí seznamu možností podpisu a uložte podepsaný dokument:
```csharp
SignResult result = signature.Sign(outputFilePath, listOptions);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## Závěr
Podepisování dokumentů s více možnostmi pomocí GroupDocs.Signature for .NET poskytuje robustní řešení pro zvýšení zabezpečení a všestrannosti dokumentů. Podle kroků uvedených v tomto kurzu můžete bez problémů integrovat různé typy podpisů do aplikací .NET.
## FAQ
### Mohu použít vlastní obrázky pro digitální podpisy?
Ano, pomocí knihovny GroupDocs.Signature můžete zadat vlastní obrázky pro digitální podpisy.
### Je GroupDocs.Signature kompatibilní s různými formáty dokumentů?
Ano, GroupDocs.Signature podporuje různé formáty dokumentů, včetně DOCX, PDF, PPTX a dalších.
### Mohu upravit vzhled textových podpisů?
Absolutně si můžete přizpůsobit vzhled textových podpisů, včetně velikosti písma, barvy a stylu.
### Poskytuje GroupDocs.Signature šifrování pro digitální podpisy?
Ano, GroupDocs.Signature nabízí možnosti šifrování pro digitální podpisy pro zajištění bezpečnosti dokumentů.
### Je k dispozici zkušební verze pro GroupDocs.Signature pro .NET?
 Ano, můžete si stáhnout bezplatnou zkušební verzi GroupDocs.Signature pro .NET z[tady](https://releases.groupdocs.com/).