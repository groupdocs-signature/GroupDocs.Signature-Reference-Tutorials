---
"description": "Ověřování textových podpisů v .NET aplikacích pomocí GroupDocs.Signature. Podrobný návod k implementaci s kompletními příklady kódu a osvědčenými postupy."
"linktitle": "Ověření textu"
"second_title": "GroupDocs.Signature .NET API"
"title": "Ověřování textových podpisů v dokumentech"
"url": "/cs/net/verify-operations/verify-text/"
"weight": 13
type: docs
---
## Zavedení

Textové podpisy, ačkoli jsou často jednodušší než digitální nebo elektronické podpisy, hrají klíčovou roli ve správě a ověřování dokumentů. Ať už se jedná o vodoznaky, text zápatí nebo specifické vzory obsahu, ověření přítomnosti a integrity textových podpisů je důležitým aspektem procesů ověřování dokumentů.

GroupDocs.Signature pro .NET poskytuje výkonné API pro ověřování textových podpisů v dokumentech v široké škále formátů. Tento komplexní tutoriál vás provede implementací funkce ověřování textu ve vašich .NET aplikacích a zajistí, že si vaše dokumenty zachovají svou integritu a autenticitu.

## Předpoklady

Před implementací funkce ověřování textu se ujistěte, že máte splněny následující předpoklady:

1. GroupDocs.Signature pro .NET: Stáhněte a nainstalujte knihovnu z [stránka ke stažení](https://releases.groupdocs.com/signature/net/).
2. Vývojové prostředí .NET: Visual Studio nebo jakékoli kompatibilní vývojové prostředí .NET.
3. Základní znalosti: Znalost programování v C# a konceptů .NET frameworku.
4. Testovací dokument: Dokument obsahující textové podpisy pro účely ověření.

## Importovat požadované jmenné prostory

Začněte importem potřebných jmenných prostorů pro přístup k funkci GroupDocs.Signature:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Rozdělme si proces ověřování textu do jasných a snadno zvládnutelných kroků:

## Krok 1: Zadejte cestu k dokumentu

```csharp
// Cesta k dokumentu obsahujícímu textové podpisy
string filePath = "sample_multiple_signatures.docx";
```

Ujistěte se, že jste vzorovou cestu nahradili skutečnou cestou k dokumentu obsahujícímu textové podpisy.

## Krok 2: Inicializace objektu Signature

```csharp
// Vytvořte instanci třídy Signature předáním cesty k dokumentu
using (Signature signature = new Signature(filePath))
{
    // Ověřovací kód bude implementován zde
}
```

Třída Signature je hlavním vstupním bodem pro všechny operace v rozhraní GroupDocs.Signature API.

## Krok 3: Konfigurace možností ověření textu

```csharp
// Definování možností ověření textu
TextVerifyOptions options = new TextVerifyOptions()
{
    AllPages = true,                               // Zkontrolujte všechny stránky dokumentu
    SignatureImplementation = TextSignatureImplementation.Native,
    Text = "signature",                            // Text k ověření
    MatchType = TextMatchType.Contains             // Zadejte kritéria shody
};
```

Možnosti ověřování vám umožňují definovat specifická kritéria pro proces ověřování:
- `AllPages`Nastavením na hodnotu true zkontrolujete všechny stránky dokumentu.
- `SignatureImplementation`Zadejte, jak je text implementován (nativní nebo samolepka)
- `Text`Textový obsah, který se má v dokumentu shodovat
- `MatchType`Metoda pro porovnávání textu (Obsahuje, Přesný, Začíná na atd.)

## Krok 4: Proveďte ověřovací proces

```csharp
// Provést ověření
VerificationResult result = signature.Verify(options);
```

Tím se spustí proces ověření na základě vámi zadaných možností.

## Krok 5: Výsledky ověření procesu

```csharp
// Zkontrolujte výsledek ověření a postupujte podle něj
if (result.IsValid)
{
    Console.WriteLine($"Document {filePath} contains valid text signatures!");
    
    // Zobrazit informace o úspěšných podpisech
    foreach (TextSignature textSignature in result.Succeeded)
    {
        Console.WriteLine($"\nFound valid text signature:");
        Console.WriteLine($"Text: {textSignature.Text}");
        Console.WriteLine($"Location: Page {textSignature.PageNumber}, {textSignature.Left}x{textSignature.Top}");
    }
}
else
{
    Console.WriteLine($"Document {filePath} failed verification process.");
    Console.WriteLine($"Number of failed signatures: {result.Failed.Count}");
}
```

Tento kód kontroluje, zda bylo ověření úspěšné, a poskytuje podrobné informace o ověřených textových podpisech.

## Kompletní příklad

Zde je kompletní funkční příklad, který demonstruje ověření textového podpisu:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace GroupDocs.Signature.Examples
{
    class Program
    {
        static void Main(string[] args)
        {
            // Cesta k dokumentu
            string filePath = "sample_multiple_signatures.docx";
            
            try
            {
                // Inicializovat instanci podpisu
                using (Signature signature = new Signature(filePath))
                {
                    // Možnosti ověření nastavení
                    TextVerifyOptions options = new TextVerifyOptions()
                    {
                        AllPages = true,
                        SignatureImplementation = TextSignatureImplementation.Native,
                        Text = "signature",
                        MatchType = TextMatchType.Contains
                    };
                    
                    // Ověření podpisů dokumentů
                    VerificationResult result = signature.Verify(options);
                    
                    // Výsledky ověření procesu
                    if(result.IsValid)
                    {
                        Console.WriteLine($"\nDocument {filePath} was verified successfully!");
                        foreach (TextSignature item in result.Succeeded)
                        {
                            Console.WriteLine($"\nValid signature is found with text: {item.Text}");
                            Console.WriteLine($"Location: Page {item.PageNumber}, position {item.Left}x{item.Top}");
                        }
                    }
                    else
                    {
                        Console.WriteLine($"\nDocument {filePath} failed verification process.");
                    }
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error: {ex.Message}");
            }
        }
    }
}
```

## Scénáře pokročilého ověřování

GroupDocs.Signature nabízí další možnosti pro složitější scénáře ověřování:

### Použití regulárních výrazů pro ověřování

Pro flexibilnější porovnávání vzorů můžete použít regulární výrazy:

```csharp
TextVerifyOptions options = new TextVerifyOptions()
{
    Text = "Invoice\\s+#\\d{5,6}",  // Vzory shody jako „Faktura č. 12345“
    MatchType = TextMatchType.Regex
};
```

### Ověřování textu v určitých oblastech dokumentu

Ověření můžete omezit na konkrétní oblasti dokumentu:

```csharp
TextVerifyOptions options = new TextVerifyOptions()
{
    AllPages = false,
    PageNumber = 1,  // Ověřte pouze na první stránce
    
    // Definujte oblast pro vyhledávání (souřadnice v bodech)
    PagesSetup = new PagesSetup() 
    { 
        FirstPage = true,
        LastPage = false,
        OddPages = false,
        EvenPages = false 
    },
    
    // Plocha obdélníku v milimetrech
    Rectangle = new Rectangle(10, 10, 100, 30),
    
    Text = "Confidential"
};
```

### Současné ověřování více textových vzorů

Můžete vytvořit více možností ověřování pro kontrolu různých textových vzorů:

```csharp
// Vytvořte seznam možností ověření
List<VerifyOptions> listOptions = new List<VerifyOptions>();

// Přidat první ověření textem
listOptions.Add(new TextVerifyOptions()
{
    Text = "Confidential",
    MatchType = TextMatchType.Exact
});

// Přidat druhé ověření textem
listOptions.Add(new TextVerifyOptions()
{
    Text = "Do not copy",
    MatchType = TextMatchType.Contains
});

// Ověření s více možnostmi
VerificationResult result = signature.Verify(listOptions);
```

### Ověřování textu se specifickým vzhledem

Můžete také ověřit text se specifickými charakteristikami formátování:

```csharp
TextVerifyOptions options = new TextVerifyOptions()
{
    Text = "APPROVED",
    MatchType = TextMatchType.Exact,
    
    // Ověření specifických vlastností vzhledu
    ForegroundColorRGB = System.Drawing.Color.Green,
    Font = new SignatureFont() { FontFamily = "Arial", FontSize = 12, Bold = true }
};
```

## Nejlepší postupy pro ověřování textových zpráv

1. Vyberte vhodné typy shody: Vyberte správný typ shody (Obsahuje, Přesná, Regex) na základě vašich požadavků na ověření.
2. Optimalizace pro výkon: U rozsáhlých dokumentů zvažte ověření konkrétních stránek, nikoli celého dokumentu.
3. Ošetření chyb: Implementujte správné ošetření chyb pro elegantní zvládání neočekávaných scénářů.
4. Rozlišujte velká a malá písmena: Při porovnávání textu dbejte na rozlišování velkých a malých písmen, zejména při kritických ověřováních.
5. Důkladné otestování: Ověření proveďte s různými formáty dokumentů a textovými vzory, abyste zajistili kompatibilitu.

## Řešení běžných problémů

### Text nebyl rozpoznán
- Zkontrolujte, zda formátování nebo kódování textu ovlivňuje detekci.
- Ujistěte se, že text je v dokumentu skutečně přítomen jako běžný text (ne jako obrázek).
- Zkuste jiná kritéria shody (Obsahuje místo Přesné)

### Problémy s výkonem
- Optimalizujte ověřování cílením na konkrétní stránky nebo oblasti
- Používejte specifičtější textové vzory pro snížení falešně pozitivních výsledků

### Selhání ověření
- Zkontrolujte, zda shodu ovlivňují mezery, speciální znaky nebo formátování.
- Ověřte, zda text není součástí naskenovaného obrázku (což vyžaduje OCR).
- Ujistěte se, že dokument nebyl od přidání textu upraven.

## Závěr

Ověřování textu je všestranný a praktický přístup k ověřování dokumentů, který lze použít samostatně nebo v kombinaci s jinými metodami ověřování. GroupDocs.Signature pro .NET poskytuje komplexní a snadno použitelné API pro implementaci robustní funkce ověřování textu ve vašich .NET aplikacích.

Dodržováním tohoto podrobného návodu jste se naučili, jak:
- Konfigurace a inicializace procesu ověřování textu
- Zadejte různá ověřovací kritéria
- Zpracování a interpretace výsledků ověření
- Implementace pokročilých scénářů ověřování

Díky těmto funkcím můžete vytvářet bezpečné a spolehlivé systémy pro zpracování dokumentů, které dokáží ověřovat pravost textu v různých formátech dokumentů.

## Často kladené otázky

### Může GroupDocs.Signature ověřovat text v naskenovaných dokumentech?
GroupDocs.Signature je primárně určen pro digitální ověřování textu. U naskenovaných dokumentů byste nejprve museli použít technologii OCR (optické rozpoznávání znaků) k převodu naskenovaných obrázků do textu.

### Které formáty dokumentů jsou podporovány pro ověřování textu?
GroupDocs.Signature podporuje širokou škálu formátů dokumentů, včetně PDF, dokumentů Word (DOC, DOCX), tabulek Excel (XLS, XLSX), prezentací PowerPoint (PPT, PPTX), obrázků a dalších.

### Mohu ověřit formátovaný text (tučné písmo, kurzíva, specifická písma)?
Ano, GroupDocs.Signature nabízí možnosti pro ověření textu se specifickými charakteristikami formátování, včetně rodiny písma, velikosti, stylu (tučné, kurzíva) a barvy.

### Je možné ověřit text v dokumentech chráněných heslem?
Ano, GroupDocs.Signature nabízí možnosti pro zadání hesel k dokumentům při otevírání chráněných dokumentů za účelem ověření.

### Mohu ověřit vodoznaky a text na pozadí?
Ano, GroupDocs.Signature dokáže ověřovat různé typy textových podpisů, včetně vodoznaků a textu na pozadí, v závislosti na tom, jak byly v dokumentu implementovány.

### Související zdroje
* [Referenční příručka k rozhraní GroupDocs.Signature API](https://reference.groupdocs.com/signature/net/)
* [Soubory ke stažení GroupDocs.Signature](https://releases.groupdocs.com/signature/net/)
* [Příklady kódu na GitHubu](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Dokumentace](https://docs.groupdocs.com/signature/net/)
* [Stránka produktu](https://products.groupdocs.com/signature/net/)
* [Články na blogu](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Fórum podpory](https://forum.groupdocs.com/c/signature/13)
* [Dočasná licence](https://purchase.groupdocs.com/temporary-license/)