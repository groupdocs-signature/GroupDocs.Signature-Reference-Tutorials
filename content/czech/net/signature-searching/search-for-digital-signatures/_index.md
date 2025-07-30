---
"description": "Zvládněte vyhledávání digitálních podpisů v dokumentech s GroupDocs.Signature pro .NET. Zvyšte zabezpečení a ověřování dokumentů s naším podrobným návodem krok za krokem."
"linktitle": "Hledat digitální podpisy"
"second_title": "GroupDocs.Signature .NET API"
"title": "Hledání digitálních podpisů v dokumentech"
"url": "/cs/net/signature-searching/search-for-digital-signatures/"
"weight": 11
---

## Zavedení

V dnešní digitální krajině je zajištění pravosti a integrity dokumentů pro firmy a organizace klíčové. Digitální podpisy poskytují robustní mechanismus pro ověřování pravosti dokumentů a detekci neoprávněných úprav. GroupDocs.Signature for .NET nabízí komplexní řešení pro práci s digitálními podpisy v různých formátech dokumentů, což vývojářům umožňuje bezproblémově integrovat funkce podpisu do jejich .NET aplikací.

Tento tutoriál vás provede procesem vyhledávání digitálních podpisů v dokumentech pomocí GroupDocs.Signature pro .NET a poskytne vám podrobná vysvětlení a praktické příklady kódu.

## Předpoklady

Než se ponoříme do detailů implementace, ujistěte se, že máte splněny následující předpoklady:

1. GroupDocs.Signature pro .NET: Stáhněte a nainstalujte knihovnu z [zde](https://releases.groupdocs.com/signature/net/).
   
2. Vývojové prostředí: Nastavte si vývojové prostředí .NET pomocí Visual Studia nebo vámi preferovaného IDE.
   
3. Ukázkové dokumenty: Připravte si ukázkové dokumenty obsahující digitální podpisy pro účely testování.

4. Základní znalosti: Znalost programovacího jazyka C# a základů .NET frameworku.

## Importovat jmenné prostory

Začněte importem požadovaných jmenných prostorů pro přístup k funkcím poskytovaným GroupDocs.Signature pro .NET:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Nyní si rozdělme proces vyhledávání digitálních podpisů na jasné a zvládnutelné kroky:

## Krok 1: Inicializace objektu podpisu

Začněte vytvořením instance `Signature` třída s předáním cesty k vašemu dokumentu:

```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // Zde bude přidán kód pro vyhledávání digitálních podpisů.
}
```

## Krok 2: Vyhledejte digitální podpisy

Dále použijte `Search` metoda s `SignatureType.Digital` parametr pro vyhledávání digitálních podpisů v dokumentu:

```csharp
// Hledání digitálních podpisů v dokumentu
List<DigitalSignature> signatures = signature.Search<DigitalSignature>(SignatureType.Digital);
```

## Krok 3: Zpracování a zobrazení výsledků

Nakonec zpracujte výsledky vyhledávání a zobrazte relevantní informace o nalezených digitálních podpisech:

```csharp
Console.WriteLine($"\nSource document ['{filePath}'] contains the following digital signatures:");
foreach (var digitalSignature in signatures)
{
    Console.WriteLine($"Digital signature found from {digitalSignature.SignTime} with validation status: {digitalSignature.IsValid}");
    Console.WriteLine($"Certificate: Subject: {digitalSignature.Certificate?.SubjectName}");
    Console.WriteLine($"Certificate: Issuer: {digitalSignature.Certificate?.IssuerName}");
    Console.WriteLine($"Certificate: Serial Number: {digitalSignature.Certificate?.SerialNumber}");
    Console.WriteLine();
}
```

## Kompletní příklad

Zde je kompletní, funkční příklad, který ukazuje, jak v dokumentu vyhledávat digitální podpisy:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SearchDigitalSignatures
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
                // Hledání digitálních podpisů v dokumentu
                List<DigitalSignature> signatures = signature.Search<DigitalSignature>(SignatureType.Digital);
                
                // Zobrazit výsledky vyhledávání
                Console.WriteLine($"\nSource document ['{filePath}'] contains the following digital signatures:");
                
                if (signatures.Count > 0)
                {
                    foreach (var digitalSignature in signatures)
                    {
                        Console.WriteLine($"Digital signature found from {digitalSignature.SignTime} with validation status: {digitalSignature.IsValid}");
                        Console.WriteLine($"Certificate: Subject: {digitalSignature.Certificate?.SubjectName}");
                        Console.WriteLine($"Certificate: Issuer: {digitalSignature.Certificate?.IssuerName}");
                        Console.WriteLine($"Certificate: Serial Number: {digitalSignature.Certificate?.SerialNumber}");
                        Console.WriteLine();
                    }
                }
                else
                {
                    Console.WriteLine("No digital signatures found in the document.");
                }
            }
        }
    }
}
```

## Možnosti rozšířeného vyhledávání

Pro cílenější vyhledávání můžete použít `DigitalSearchOptions` Chcete-li přizpůsobit kritéria vyhledávání:

```csharp
// Vytvořte možnosti digitálního vyhledávání
DigitalSearchOptions options = new DigitalSearchOptions()
{
    // Hledat pouze na konkrétních stránkách (např. stránky 1 a 2)
    PageNumber = 1,
    PagesSetup = new PagesSetup() { Pages = new List<int> { 1, 2 } },
    
    // Filtrovat podle komentářů v digitálních podpisech
    Comments = "Approved",
    
    // Nastavení rozsahu data a času pro vyhledávání
    SignDateTimeFrom = new DateTime(2022, 1, 1),
    SignDateTimeTo = DateTime.Now
};

// Hledat s konkrétními možnostmi
List<DigitalSignature> signatures = signature.Search<DigitalSignature>(options);
```

## Práce s informacemi o certifikátu

Digitální podpisy obsahují cenné informace o certifikátu, ke kterým máte přístup a které můžete ověřit:

```csharp
foreach (var digitalSignature in signatures)
{
    if (digitalSignature.Certificate != null)
    {
        // Vlastnosti certifikátu přístupu
        Console.WriteLine($"Certificate Valid From: {digitalSignature.Certificate.NotBefore}");
        Console.WriteLine($"Certificate Valid To: {digitalSignature.Certificate.NotAfter}");
        
        // Zkontrolujte, zda je certifikát v platném rozsahu dat
        bool isDateValid = DateTime.Now >= digitalSignature.Certificate.NotBefore && 
                          DateTime.Now <= digitalSignature.Certificate.NotAfter;
        
        Console.WriteLine($"Certificate Date Validity: {isDateValid}");
        
        // Podrobnosti o vydavateli certifikátu přístupu
        Console.WriteLine($"Certificate Issuer: {digitalSignature.Certificate.IssuerName}");
    }
}
```

## Závěr

GroupDocs.Signature pro .NET poskytuje výkonné a flexibilní řešení pro vyhledávání a ověřování digitálních podpisů v dokumentech. V tomto tutoriálu jsme prozkoumali podrobný proces implementace funkce vyhledávání digitálních podpisů v aplikacích .NET a poskytli vám znalosti pro zvýšení zabezpečení a ověřování integrity dokumentů.

Využitím GroupDocs.Signature můžete vybudovat robustní systémy správy dokumentů, které zajistí autenticitu a integritu vašich digitálních dokumentů a podpoří důvěru a dodržování předpisů ve vašich obchodních procesech.

## Často kladené otázky

### Může GroupDocs.Signature ověřit platnost digitálních podpisů?

Ano, GroupDocs.Signature automaticky ověřuje digitální podpisy během procesu vyhledávání a poskytuje stav ověření prostřednictvím `IsValid` majetek `DigitalSignature` třída.

### Které formáty dokumentů podporují vyhledávání digitálních podpisů?

GroupDocs.Signature podporuje vyhledávání digitálních podpisů v různých formátech, včetně PDF, dokumentů Microsoft Office (Word, Excel, PowerPoint), formátů OpenOffice a dalších.

### Mohu vyhledávat digitální podpisy v dokumentech chráněných heslem?

Ano, digitální podpisy můžete vyhledávat v dokumentech chráněných heslem zadáním hesla při inicializaci `Signature` objekt:

```csharp
LoadOptions loadOptions = new LoadOptions() { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // Hledat digitální podpisy
}
```

### Jak mohu ověřit, zda digitální podpis vytvořila konkrétní osoba?

Identitu podepisujícího můžete ověřit podle názvu subjektu certifikátu a dalších jeho vlastností:

```csharp
foreach (var signature in signatures)
{
    if (signature.Certificate?.SubjectName?.Contains("John Doe") == true)
    {
        Console.WriteLine("Found signature by John Doe");
    }
}
```

### Mohu extrahovat veřejný klíč z certifikátu digitálního podpisu?

Ano, k informacím o veřejném klíči máte přístup prostřednictvím vlastností certifikátu:

```csharp
if (signature.Certificate != null)
{
    // Přístup k informacím o veřejném klíči
    Console.WriteLine($"Public Key: {signature.Certificate.GetPublicKeyString()}");
}
```

## Viz také

* [Referenční informace k API](https://reference.groupdocs.com/signature/net/)
* [Příklady kódu](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Dokumentace k produktu](https://docs.groupdocs.com/signature/net/)
* [Stránka produktu](https://products.groupdocs.com/signature/net/)
* [Stáhnout nejnovější verzi](https://releases.groupdocs.com/signature/net/)
* [Články na blogu](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Fórum podpory](https://forum.groupdocs.com/c/signature/13)
* [Dočasná licence](https://purchase.groupdocs.com/temporary-license/)