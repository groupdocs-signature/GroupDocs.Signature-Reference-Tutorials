---
title: Podepisování dokumentů pomocí QR kódu pomocí GroupDocs.Signature
linktitle: Podepisování pomocí QR kódu
second_title: GroupDocs.Signature .NET API
description: Naučte se přidávat podpisy QR kódů do dokumentů pomocí GroupDocs.Signature pro .NET. Zvyšte zabezpečení a ověřování bez námahy.
weight: 15
url: /cs/net/advanced-signature-techniques/sign-with-qr-code/
---
## Úvod
tomto tutoriálu si projdeme procesem podepisování dokumentů pomocí QR kódu pomocí GroupDocs.Signature for .NET. GroupDocs.Signature for .NET je výkonné API, které umožňuje vývojářům přidávat různé typy podpisů do digitálních dokumentů programově. Podepisování dokumentů pomocí QR kódů může poskytnout další vrstvu zabezpečení a ověřování vašich dokumentů.
## Předpoklady
Než začneme, ujistěte se, že máte nainstalované následující předpoklady:
1.  GroupDocs.Signature for .NET: Knihovnu si můžete stáhnout z[webová stránka](https://releases.groupdocs.com/signature/net/).
2. Vývojové prostředí: Ujistěte se, že máte na svém počítači nastavené vývojové prostředí .NET.
3. Vzorový dokument: Připravte si vzorový dokument (např. PDF), který chcete podepsat pomocí QR kódu.

## Import nezbytných jmenných prostorů
Než se ponoříme do kódu, importujme potřebné jmenné prostory:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## Krok 1: Definujte cesty k souboru
```csharp
string filePath = "sample.pdf";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "SignWithQRCode", fileName);
```
 Zajistěte výměnu`"Your Document Directory"` s cestou k adresáři, kam chcete podepsaný dokument uložit.
## Krok 2: Inicializujte objekt podpisu
```csharp
using (Signature signature = new Signature(filePath))
{
    //Kód pro podpis je zde
}
```
 Inicializovat a`Signature` objekt s cestou k dokumentu, který chcete podepsat.
## Krok 3: Vytvořte QRCodeSignOptions
```csharp
QrCodeSignOptions options = new QrCodeSignOptions("JohnSmith")
{
    EncodeType = QrCodeTypes.QR,
    Left = 50,
    Top = 150,
    Width = 200,
    Height = 200
};
```
 Vytvořit`QrCodeSignOptions` objekt s požadovaným nastavením podpisu QR kódu. Můžete přizpůsobit parametry, jako je kódování textu, umístění a rozměry QR kódu.
## Krok 4: Podepište dokument
```csharp
SignResult result = signature.Sign(outputFilePath, options);
```
 Použijte`Sign` metoda`Signature` objekt podepsat dokument se zadanými možnostmi. Tato metoda vrací a`SignResult` objekt obsahující informace o procesu podepisování.
## Krok 5: Zobrazení výsledku
```csharp
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```
Zobrazte zprávu o úspěchu procesu podepisování a umístění, kde je podepsaný dokument uložen.

## Závěr
V tomto tutoriálu jsme se naučili podepisovat dokumenty pomocí QR kódu pomocí GroupDocs.Signature for .NET. Pomocí těchto jednoduchých kroků můžete do svých digitálních dokumentů přidat podpisy s QR kódem, čímž zvýšíte zabezpečení a autentizaci.

## FAQ
### Mohu upravit vzhled QR kódu?
Ano, můžete přizpůsobit různé parametry, jako je velikost, pozice a typ kódování QR kódu podle vašich požadavků.
### Které formáty dokumentů jsou podporovány pro podepisování pomocí QR kódů?
GroupDocs.Signature for .NET podporuje širokou škálu formátů dokumentů, včetně PDF, Word, Excel, PowerPoint a dalších.
### Je možné podepsat více dokumentů v dávkovém procesu?
Rozhodně můžete použít GroupDocs.Signature for .NET k podepisování více dokumentů současně, čímž se zjednoduší váš pracovní postup.
### Mohu ověřit pravost dokumentu podepsaného QR kódem?
Ano, GroupDocs.Signature for .NET poskytuje ověřovací mechanismy k zajištění integrity a pravosti podepsaných dokumentů.
### Je k dispozici zkušební verze pro otestování funkčnosti před zakoupením?
 Ano, můžete si stáhnout bezplatnou zkušební verzi z[webová stránka](https://releases.groupdocs.com/) vyhodnotit funkce a možnosti GroupDocs.Signature pro .NET.