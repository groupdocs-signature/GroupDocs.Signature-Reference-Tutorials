---
"description": "Naučte se, jak vyhledávat více typů podpisů v dokumentech pomocí GroupDocs.Signature pro .NET. Komplexní průvodce s příklady kódu pro vylepšené zabezpečení dokumentů."
"linktitle": "Hledat více podpisů"
"second_title": "GroupDocs.Signature .NET API"
"title": "Hledání více typů podpisů v dokumentech"
"url": "/cs/net/signature-searching/search-for-multiple-signatures/"
"weight": 14
---

## Zavedení

moderních systémech správy dokumentů je stále důležitější možnost vyhledávat a ověřovat více typů podpisů v rámci jednoho dokumentu. Organizace často používají různé typy podpisů – například digitální podpisy, textové podpisy, čárové kódy, QR kódy a další – ke zvýšení zabezpečení dokumentů a zefektivnění procesů ověřování. GroupDocs.Signature pro .NET poskytuje výkonný framework, který umožňuje vývojářům implementovat komplexní funkce vyhledávání podpisů v různých formátech dokumentů.

Tento tutoriál vás provede procesem vyhledávání více typů podpisů v dokumentech pomocí GroupDocs.Signature pro .NET a nabídne podrobná vysvětlení a praktické příklady kódu.

## Předpoklady

Než se pustíte do implementace funkce vyhledávání více podpisů, ujistěte se, že máte následující předpoklady:

1. Vývojové prostředí: Visual Studio nebo jakékoli preferované vývojové prostředí .NET nainstalované ve vašem systému.
  
2. GroupDocs.Signature pro .NET: Stáhněte a nainstalujte knihovnu GroupDocs.Signature pro .NET z [zde](https://releases.groupdocs.com/signature/net/).

3. Základní znalost C#: Znalost programovacího jazyka C# a konceptů .NET frameworku.

4. Ukázkové dokumenty: Připravte testovací dokumenty obsahující různé typy podpisů pro testovací účely.

## Importovat jmenné prostory

Začněte importem potřebných jmenných prostorů pro přístup k funkcím GroupDocs.Signature:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Nyní si rozdělme proces vyhledávání více typů podpisů do jasných a zvládnutelných kroků:

## Krok 1: Vložení dokumentu

Nejprve načtěte dokument obsahující podpisy, které chcete vyhledat:

```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // Zde bude přidán vyhledávací kód pro více podpisů
}
```

## Krok 2: Definování možností vyhledávání pro různé typy podpisů

Vytvořte možnosti vyhledávání pro každý typ podpisu, který chcete vyhledat:

```csharp
// Definování možností vyhledávání pro textové podpisy
TextSearchOptions textOptions = new TextSearchOptions
{
    AllPages = true,  // Hledat na všech stránkách
    Text = "Signature",  // Volitelné: text k nalezení
    MatchType = TextMatchType.Contains  // Kritéria shody
};

// Definování možností vyhledávání pro digitální podpisy
DigitalSearchOptions digitalOptions = new DigitalSearchOptions
{
    AllPages = true
};

// Definování možností vyhledávání pro podpisy čárových kódů
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions
{
    AllPages = true,
    Text = "123456",  // Volitelné: odpovídající text čárového kódu
    MatchType = TextMatchType.Exact  // Kritéria shody
};

// Definování možností vyhledávání pro podpisy QR kódů
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions
{
    AllPages = true,
    Text = "John",  // Volitelné: Text QR kódu pro shodu
    MatchType = TextMatchType.Contains  // Kritéria shody
};

// Definování možností vyhledávání pro podpisy metadat
MetadataSearchOptions metadataOptions = new MetadataSearchOptions();
```

## Krok 3: Přidání možností do kolekce

Přidejte všechny možnosti vyhledávání do kolekce:

```csharp
// Vytvořte seznam, který bude obsahovat všechny možnosti vyhledávání
List<SearchOptions> searchOptions = new List<SearchOptions>
{
    textOptions,
    digitalOptions,
    barcodeOptions,
    qrCodeOptions,
    metadataOptions
};
```

## Krok 4: Proveďte vyhledávání a zpracujte výsledky

Proveďte vyhledávání pomocí kombinovaných možností vyhledávání a zpracujte výsledky:

```csharp
// Vyhledat všechny typy podpisů pomocí definovaných možností
SearchResult result = signature.Search(searchOptions);

// Zkontrolujte, zda byly nalezeny podpisy
if (result.Signatures.Count > 0)
{
    Console.WriteLine($"\nSource document ['{filePath}'] contains {result.Signatures.Count} signature(s):");
    
    // Projděte nalezené podpisy
    foreach (var foundSignature in result.Signatures)
    {
        Console.WriteLine($"Signature found: Type: {foundSignature.SignatureType}, Page: {foundSignature.PageNumber}, ID: {foundSignature.SignatureId}");
        
        // Typy podpisů specifických pro proces
        if (foundSignature is TextSignature textSignature)
        {
            Console.WriteLine($"Text: '{textSignature.Text}'");
        }
        else if (foundSignature is BarcodeSignature barcodeSignature)
        {
            Console.WriteLine($"Barcode Type: {barcodeSignature.EncodeType.TypeName}, Text: '{barcodeSignature.Text}'");
        }
        else if (foundSignature is QrCodeSignature qrCodeSignature)
        {
            Console.WriteLine($"QR Code Type: {qrCodeSignature.EncodeType.TypeName}, Text: '{qrCodeSignature.Text}'");
        }
        else if (foundSignature is DigitalSignature digitalSignature)
        {
            Console.WriteLine($"Certificate: {digitalSignature.Certificate?.SubjectName}, Valid: {digitalSignature.IsValid}");
        }
        else if (foundSignature is MetadataSignature metadataSignature)
        {
            Console.WriteLine($"Metadata: Name: {metadataSignature.Name}, Value: {metadataSignature.Value}");
        }
    }
}
else
{
    Console.WriteLine("No signatures were found in the document.");
}
```

## Kompletní příklad

Zde je kompletní, funkční příklad, který demonstruje vyhledávání více typů podpisů v dokumentu:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace MultiSignatureSearch
{
    class Program
    {
        static void Main(string[] args)
        {
            // Cesta k dokumentu
            string filePath = "sample_multiple_signatures.docx";
            
            // Inicializovat instanci podpisu
            using (Signature signature = new Signature(filePath))
            {
                try
                {
                    // Definování možností vyhledávání pro textové podpisy
                    TextSearchOptions textOptions = new TextSearchOptions
                    {
                        AllPages = true,
                        MatchType = TextMatchType.Contains
                    };

                    // Definování možností vyhledávání pro digitální podpisy
                    DigitalSearchOptions digitalOptions = new DigitalSearchOptions
                    {
                        AllPages = true
                    };

                    // Definování možností vyhledávání pro podpisy čárových kódů
                    BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions
                    {
                        AllPages = true
                    };

                    // Definování možností vyhledávání pro podpisy QR kódů
                    QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions
                    {
                        AllPages = true
                    };

                    // Definování možností vyhledávání pro podpisy metadat
                    MetadataSearchOptions metadataOptions = new MetadataSearchOptions();

                    // Vytvořte seznam, který bude obsahovat všechny možnosti vyhledávání
                    List<SearchOptions> searchOptions = new List<SearchOptions>
                    {
                        textOptions,
                        digitalOptions,
                        barcodeOptions,
                        qrCodeOptions,
                        metadataOptions
                    };

                    // Hledat všechny typy podpisů
                    SearchResult result = signature.Search(searchOptions);

                    // Zkontrolujte, zda byly nalezeny podpisy
                    if (result.Signatures.Count > 0)
                    {
                        Console.WriteLine($"\nSource document ['{filePath}'] contains {result.Signatures.Count} signature(s):");
                        
                        // Výsledky zpracování podle typu podpisu
                        foreach (var foundSignature in result.Signatures)
                        {
                            Console.WriteLine($"Signature found: Type: {foundSignature.SignatureType}, Page: {foundSignature.PageNumber}");
                            
                            // Typy podpisů specifických pro proces
                            switch (foundSignature.SignatureType)
                            {
                                case SignatureType.Text:
                                    var textSignature = foundSignature as TextSignature;
                                    Console.WriteLine($"Text: '{textSignature.Text}'");
                                    break;
                                    
                                case SignatureType.Barcode:
                                    var barcodeSignature = foundSignature as BarcodeSignature;
                                    Console.WriteLine($"Barcode Type: {barcodeSignature.EncodeType.TypeName}, Text: '{barcodeSignature.Text}'");
                                    break;
                                    
                                case SignatureType.QrCode:
                                    var qrCodeSignature = foundSignature as QrCodeSignature;
                                    Console.WriteLine($"QR Code Type: {qrCodeSignature.EncodeType.TypeName}, Text: '{qrCodeSignature.Text}'");
                                    break;
                                    
                                case SignatureType.Digital:
                                    var digitalSignature = foundSignature as DigitalSignature;
                                    Console.WriteLine($"Certificate: {digitalSignature.Certificate?.SubjectName}, Valid: {digitalSignature.IsValid}");
                                    break;
                                    
                                case SignatureType.Metadata:
                                    var metadataSignature = foundSignature as MetadataSignature;
                                    Console.WriteLine($"Metadata: Name: {metadataSignature.Name}, Value: {metadataSignature.Value}");
                                    break;
                            }
                            
                            Console.WriteLine(); // Přidat zalomení řádku mezi podpisy
                        }
                    }
                    else
                    {
                        Console.WriteLine("No signatures were found in the document.");
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

## Pokročilé techniky vyhledávání více podpisů

### Filtrování výsledků vyhledávání

Pro zúžení výsledků vyhledávání můžete implementovat pokročilé filtrování:

```csharp
// Filtrovat výsledky podle čísla stránky
var signaturesOnFirstPage = result.Signatures.FindAll(s => s.PageNumber == 1);

// Filtrovat výsledky podle typu podpisu
var digitalSignatures = result.Signatures.FindAll(s => s.SignatureType == SignatureType.Digital);
var qrCodeSignatures = result.Signatures.FindAll(s => s.SignatureType == SignatureType.QrCode);

// Filtrovat textové podpisy obsahující specifický obsah
var approvalSignatures = result.Signatures
    .FindAll(s => s is TextSignature && ((TextSignature)s).Text.Contains("Approved"));
```

### Ověřování více podpisů

Implementujte logiku ověřování pro různé typy podpisů:

```csharp
bool ValidateAllSignatures(SearchResult result)
{
    bool isDocumentValid = true;
    
    // Zkontrolujte, zda má dokument platný digitální podpis
    bool hasValidDigitalSignature = result.Signatures
        .Any(s => s is DigitalSignature && ((DigitalSignature)s).IsValid);
    
    if (!hasValidDigitalSignature)
    {
        Console.WriteLine("Warning: Document does not contain a valid digital signature");
        isDocumentValid = false;
    }
    
    // Zkontrolujte, zda dokument obsahuje požadovaný QR kód
    bool hasRequiredQRCode = result.Signatures
        .Any(s => s is QrCodeSignature && ((QrCodeSignature)s).Text.Contains("Auth-Code"));
    
    if (!hasRequiredQRCode)
    {
        Console.WriteLine("Warning: Document does not contain the required authentication QR code");
        isDocumentValid = false;
    }
    
    return isDocumentValid;
}
```

### Vyhledávání s vlastním zpracováním

Pro vyhledávací operace můžete definovat vlastní logiku zpracování:

```csharp
// Vytvořte možnosti vyhledávání s vlastním zpracováním
TextSearchOptions textOptions = new TextSearchOptions
{
    AllPages = true,
    
    // Definování vlastního zpracování pomocí delegáta
    ProcessCompleted = (signature) =>
    {
        // Vlastní logika ověřování – přijímání podpisů pouze na zadaných stránkách
        TextSignature textSignature = signature as TextSignature;
        return textSignature != null && (textSignature.PageNumber == 1 || textSignature.PageNumber == 2);
    }
};
```

## Závěr

V této komplexní příručce jsme prozkoumali, jak vyhledávat více typů podpisů v dokumentech pomocí GroupDocs.Signature pro .NET. Od nastavení možností vyhledávání pro různé typy podpisů až po zpracování a ověřování výsledků – nyní máte znalosti potřebné k implementaci robustní funkce vyhledávání podpisů ve vašich .NET aplikacích.

Možnost vyhledávat více typů podpisů současně vylepšuje procesy ověřování dokumentů, posiluje bezpečnostní opatření a zefektivňuje pracovní postupy ověřování dokumentů. GroupDocs.Signature poskytuje výkonný a flexibilní rámec pro práci s různými typy podpisů v různých formátech dokumentů, což z něj činí vynikající volbu pro aplikace pro zpracování dokumentů.

## Často kladené otázky

### Mohu vyhledávat podpisy v dokumentech chráněných heslem?

Ano, GroupDocs.Signature podporuje vyhledávání podpisů v dokumentech chráněných heslem. Heslo můžete zadat při inicializaci. `Signature` objekt:

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // Hledat podpisy
}
```

### Které formáty dokumentů jsou podporovány pro vyhledávání podpisů?

GroupDocs.Signature podporuje širokou škálu formátů dokumentů, včetně PDF, dokumentů Microsoft Office (Word, Excel, PowerPoint), formátů OpenOffice, obrázků a dalších.

### Mohu omezit vyhledávání na konkrétní stránky v dokumentu?

Ano, každý typ možnosti vyhledávání má vlastnosti, které vám umožňují určit, které stránky chcete prohledávat:

```csharp
TextSearchOptions options = new TextSearchOptions
{
    AllPages = false,  // Neprohledávat všechny stránky
    PageNumber = 1,    // Hledat pouze na straně 1
    
    // Nebo zadejte více stránek
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } }
};
```

### Jak mohu optimalizovat výkon při vyhledávání ve velkých dokumentech?

U velkých dokumentů můžete optimalizovat výkon pomocí:

1. Omezení vyhledávání na konkrétní stránky nebo rozsahy stránek
2. Použití konkrétnějších vyhledávacích kritérií pro snížení počtu potenciálních shod
3. Implementace stránkování ve výsledcích vyhledávání
4. Hledání jednoho typu podpisu najednou, pokud nepotřebujete simultánní výsledky

### Mohu rozšířit GroupDocs.Signature o podporu vlastních typů podpisů?

I když GroupDocs.Signature poskytuje vestavěnou podporu pro běžné typy podpisů, můžete jeho funkčnost rozšířit pomocí:

1. Vytváření vlastních tříd možností vyhledávání odvozených z `SearchOptions`
2. Implementace vlastní logiky zpracování pomocí `ProcessCompleted` delegát
3. Vývoj obalových tříd, které kombinují vyhledávání více signatur s pokročilou obchodní logikou

## Viz také

* [Referenční informace k API](https://reference.groupdocs.com/signature/net/)
* [Příklady kódu na GitHubu](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Dokumentace k produktu](https://docs.groupdocs.com/signature/net/)
* [Stránka produktu](https://products.groupdocs.com/signature/net/)
* [Stáhnout nejnovější verzi](https://releases.groupdocs.com/signature/net/)
* [Články na blogu](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Bezplatné fórum podpory](https://forum.groupdocs.com/c/signature/13)
* [Dočasná licence](https://purchase.groupdocs.com/temporary-license/)