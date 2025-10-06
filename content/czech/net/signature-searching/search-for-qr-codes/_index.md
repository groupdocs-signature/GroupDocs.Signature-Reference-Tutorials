---
"description": "Naučte se, jak efektivně vyhledávat QR kódy v dokumentech pomocí GroupDocs.Signature pro .NET s tímto komplexním podrobným návodem a příklady kódu."
"linktitle": "Hledat QR kódy"
"second_title": "GroupDocs.Signature .NET API"
"title": "Hledání podpisů QR kódů v dokumentech"
"url": "/cs/net/signature-searching/search-for-qr-codes/"
"weight": 15
type: docs
---
## Zavedení

V dnešním ekosystému digitálních dokumentů se podpisy QR kódy staly neocenitelným nástrojem pro vkládání informací, ověřování a zvyšování zabezpečení dokumentů. GroupDocs.Signature for .NET poskytuje vývojářům výkonné API pro vyhledávání a extrakci QR kódů z různých formátů dokumentů, což umožňuje pokročilou analýzu a ověřování dokumentů v aplikacích .NET.

Tento komplexní tutoriál vás provede procesem implementace funkce vyhledávání QR kódů pomocí GroupDocs.Signature pro .NET a poskytne vám srozumitelné vysvětlení, podrobné pokyny a praktické příklady kódu, které můžete integrovat do vlastních aplikací.

## Předpoklady

Než se pustíte do vyhledávání podpisů QR kódů, ujistěte se, že máte následující předpoklady:

1. GroupDocs.Signature pro .NET SDK: Stáhněte a nainstalujte sadu SDK z [stránka ke stažení](https://releases.groupdocs.com/signature/net/).

2. Vývojové prostředí: Nastavte vývojové prostředí .NET, například Visual Studio, s nainstalovaným .NET Framework nebo .NET Core.

3. Základní znalosti: Znalost programování v C# a konceptů vývoje v .NET.

4. Ukázkové dokumenty: Připravte testovací dokumenty obsahující QR kódy pro ověření a testování.

## Importovat jmenné prostory

Začněte importem potřebných jmenných prostorů pro přístup k funkcím GroupDocs.Signature:

```csharp
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
using System;
using System.Collections.Generic;
```

Nyní si rozdělme proces vyhledávání QR kódů do jasných a snadno sledovatelných kroků:

## Krok 1: Definování cesty k dokumentu

Nejprve zadejte cestu k dokumentu obsahujícímu QR kódy, které chcete vyhledat:

```csharp
string filePath = "sample_multiple_signatures.docx";
```

## Krok 2: Inicializace objektu Signature

Vytvořte instanci `Signature` třída předáním cesty k dokumentu:

```csharp
using (Signature signature = new Signature(filePath))
{
    // Zde bude přidán vyhledávací kód QR kódu
}
```

## Krok 3: Vyhledejte podpisy QR kódů

Použijte `Search` metoda s příslušným typem podpisu pro nalezení QR kódů v dokumentu:

```csharp
// Vyhledávání podpisů QR kódů v dokumentu
List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
```

## Krok 4: Zpracování a zobrazení výsledků

Projděte si nalezené podpisy QR kódů a získejte přístup k jejich vlastnostem:

```csharp
// Zobrazit informace o nalezených QR kódech
Console.WriteLine($"\nSource document contains {signatures.Count} QR code signature(s):");

foreach (var qrCodeSignature in signatures)
{
    Console.WriteLine($"QR Code found at page {qrCodeSignature.PageNumber} with type {qrCodeSignature.EncodeType.TypeName}");
    Console.WriteLine($"Content: {qrCodeSignature.Text}");
    Console.WriteLine($"Location: X={qrCodeSignature.Left}, Y={qrCodeSignature.Top}, Width={qrCodeSignature.Width}, Height={qrCodeSignature.Height}");
    Console.WriteLine();
}
```

## Kompletní příklad

Zde je komplexní pracovní příklad, který demonstruje kompletní proces vyhledávání QR kódů v dokumentu:

```csharp
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
using System;
using System.Collections.Generic;

namespace QrCodeSignatureSearch
{
    class Program
    {
        static void Main(string[] args)
        {
            // Cesta k dokumentu – aktualizujte cestou k souboru
            string filePath = "sample_multiple_signatures.docx";
            
            // Inicializovat instanci podpisu
            using (Signature signature = new Signature(filePath))
            {
                try
                {
                    // Vyhledávání podpisů QR kódů v dokumentu
                    List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
                    
                    // Zobrazit výsledky vyhledávání
                    Console.WriteLine($"\nSource document ['{filePath}'] contains {signatures.Count} QR code signature(s):");
                    
                    foreach (var qrCodeSignature in signatures)
                    {
                        Console.WriteLine($"QR Code found at page {qrCodeSignature.PageNumber} with type {qrCodeSignature.EncodeType.TypeName}");
                        Console.WriteLine($"Content: {qrCodeSignature.Text}");
                        Console.WriteLine($"Location: X={qrCodeSignature.Left}, Y={qrCodeSignature.Top}, Width={qrCodeSignature.Width}, Height={qrCodeSignature.Height}");
                        Console.WriteLine();
                    }
                }
                catch (Exception ex)
                {
                    Console.WriteLine($"Error occurred: {ex.Message}");
                }
            }
            
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

## Pokročilé techniky vyhledávání QR kódů

### Vyhledávání podle specifických kritérií

Pro cílenější vyhledávání můžete použít `QrCodeSearchOptions` pro přizpůsobení kritérií vyhledávání:

```csharp
// Vytvořte možnosti vyhledávání QR kódů s konkrétními kritérii
QrCodeSearchOptions options = new QrCodeSearchOptions
{
    // Hledat pouze na konkrétních stránkách
    AllPages = false,
    PageNumber = 1,
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } },
    
    // Filtrovat podle obsahu QR kódu
    Text = "Invoice",
    MatchType = TextMatchType.Contains,
    
    // Filtrovat podle konkrétních typů QR kódů
    EncodeType = QrCodeTypes.QR,
    
    // Definujte konkrétní oblast, ve které chcete vyhledávat
    Rectangle = new Rectangle(100, 100, 400, 400)
};

// Hledat s konkrétními možnostmi
List<QrCodeSignature> filteredSignatures = signature.Search<QrCodeSignature>(options);
```

### Zpracování dat QR kódu

Můžete implementovat vlastní zpracování dat QR kódů na základě požadavků vaší aplikace:

```csharp
foreach (var qrCode in signatures)
{
    // Extrahování a zpracování dat QR kódu na základě obsahu
    string qrContent = qrCode.Text;
    
    if (qrContent.StartsWith("URL:"))
    {
        // Zpracovat data URL
        string url = qrContent.Substring(4);
        Console.WriteLine($"Found URL in QR code: {url}");
    }
    else if (qrContent.StartsWith("CONTACT:"))
    {
        // Zpracovat kontaktní informace
        string contact = qrContent.Substring(8);
        Console.WriteLine($"Found contact information in QR code: {contact}");
    }
    else if (qrContent.StartsWith("INVOICE:"))
    {
        // Zpracovat informace o fakturách
        string invoiceData = qrContent.Substring(8);
        Console.WriteLine($"Found invoice information in QR code: {invoiceData}");
        
        // Analyzovat a ověřit data faktur
        if (ValidateInvoiceData(invoiceData))
        {
            Console.WriteLine("Invoice data is valid!");
        }
        else
        {
            Console.WriteLine("Warning: Invalid invoice data detected!");
        }
    }
}

// Příklad metody validace
static bool ValidateInvoiceData(string data)
{
    // Implementujte svou ověřovací logiku
    return !string.IsNullOrEmpty(data) && data.Contains("ID") && data.Contains("Amount");
}
```

### Implementace bezpečnostního ověřování

QR kódy se často používají k ověřování. Zde je návod, jak implementovat základní bezpečnostní ověření:

```csharp
// Zkontrolujte, zda dokument obsahuje platný ověřovací QR kód
bool hasValidAuthQrCode = false;

foreach (var qrCode in signatures)
{
    if (qrCode.Text.StartsWith("AUTH:"))
    {
        string authCode = qrCode.Text.Substring(5);
        
        // Ověření ověřovacího kódu (např. oproti databázi nebo předdefinovanému seznamu)
        if (VerifyAuthCode(authCode))
        {
            hasValidAuthQrCode = true;
            Console.WriteLine("Document contains valid authentication QR code!");
            break;
        }
    }
}

if (!hasValidAuthQrCode)
{
    Console.WriteLine("Warning: Document does not contain a valid authentication QR code!");
}

// Příklad metody ověření
static bool VerifyAuthCode(string code)
{
    // Implementujte svou ověřovací logiku
    // Může se jednat o vyhledávání v databázi, volání API nebo porovnání s předdefinovanými hodnotami.
    return code == "A7B82C3D" || code == "X9Y8Z7W6";
}
```

### Extrakce obrázků QR kódů

Obrázky QR kódů můžete z dokumentů extrahovat pro další zpracování nebo zobrazení:

```csharp
// Uložení obrázků QR kódů na disk
foreach (var qrCode in signatures)
{
    if (qrCode.Content != null)
    {
        // Vytvořte jedinečný název souboru na základě čísla stránky a pozice
        string outputPath = $"QrCode_P{qrCode.PageNumber}_X{qrCode.Left}_Y{qrCode.Top}.png";
        
        // Uložte obrazová data
        File.WriteAllBytes(outputPath, qrCode.Content);
        Console.WriteLine($"Saved QR code image to {outputPath}");
    }
}
```

## Závěr

V této komplexní příručce jsme prozkoumali, jak vyhledávat podpisy QR kódů v dokumentech pomocí nástroje GroupDocs.Signature pro .NET. Od základního vyhledávání až po pokročilé techniky – nyní máte znalosti pro implementaci robustní práce s QR kódy ve vašich .NET aplikacích. Rozhraní GroupDocs.Signature API poskytuje výkonný a flexibilní rámec pro práci s různými typy podpisů, včetně QR kódů, v různých formátech dokumentů.

Využitím těchto funkcí můžete vylepšit procesy ověřování dokumentů, implementovat systémy ověřování a extrahovat cenné informace vložené do QR kódů, a to vše v rámci vašich .NET aplikací.

## Často kladené otázky

### Které formáty QR kódů podporuje GroupDocs.Signature?

GroupDocs.Signature podporuje různé formáty QR kódů, včetně standardních QR kódů, mikro QR kódů a dalších běžných standardů QR kódů. Konkrétní formát je přístupný prostřednictvím `EncodeType` majetek `QrCodeSignature` objekt.

### Mohu vyhledávat QR kódy v dokumentech chráněných heslem?

Ano, GroupDocs.Signature podporuje vyhledávání QR kódů v dokumentech chráněných heslem zadáním hesla při inicializaci `Signature` objekt:

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // Hledat QR kódy
}
```

### Jak mohu filtrovat QR kódy na základě jejich obsahu?

QR kódy můžete filtrovat podle jejich obsahu pomocí `Text` a `MatchType` vlastnosti `QrCodeSearchOptions`:

```csharp
QrCodeSearchOptions options = new QrCodeSearchOptions
{
    Text = "Invoice",
    MatchType = TextMatchType.Contains // Další možnosti: Přesné, Začíná na, Končí na
};
```

### Dokáže GroupDocs.Signature detekovat poškozené nebo částečně viditelné QR kódy?

GroupDocs.Signature má určitou schopnost detekovat částečně viditelné QR kódy, ale silně poškozené QR kódy nemusí být rozpoznány. Přesnost detekce závisí na kvalitě a viditelnosti QR kódu v dokumentu.

### Jaké formáty dokumentů jsou podporovány pro vyhledávání QR kódů?

GroupDocs.Signature podporuje vyhledávání QR kódů v různých formátech dokumentů, včetně PDF, dokumentů Microsoft Office (Word, Excel, PowerPoint), obrázků (JPEG, PNG, TIFF) a mnoha dalších.

## Viz také

* [Referenční informace k API](https://reference.groupdocs.com/signature/net/)
* [Příklady kódu na GitHubu](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Dokumentace k produktu](https://docs.groupdocs.com/signature/net/)
* [Stránka produktu](https://products.groupdocs.com/signature/net/)
* [Stáhnout nejnovější verzi](https://releases.groupdocs.com/signature/net/)
* [Články na blogu](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Bezplatné fórum podpory](https://forum.groupdocs.com/c/signature/13)
* [Dočasná licence](https://purchase.groupdocs.com/temporary-license/)