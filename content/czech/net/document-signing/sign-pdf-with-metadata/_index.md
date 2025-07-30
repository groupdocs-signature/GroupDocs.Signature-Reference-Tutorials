---
"description": "Integrujte podpisy metadat do PDF dokumentů pomocí GroupDocs.Signature pro .NET. Naučte se vkládat informace o autorovi, časová razítka a vlastní data pro zvýšení autenticity a sledovatelnosti PDF."
"linktitle": "Podepsat PDF pomocí metadat"
"second_title": "GroupDocs.Signature .NET API"
"title": "Přidání podpisů metadat do dokumentů PDF v C# .NET"
"url": "/cs/net/document-signing/sign-pdf-with-metadata/"
"weight": 11
---

## Zavedení

Dokumenty PDF (Portable Document Format) jsou široce používány napříč odvětvími díky své konzistenci a nezávislosti na platformě. Zajištění autenticity a sledovatelnosti těchto dokumentů je v mnoha profesionálních prostředích klíčové. Jedním z účinných způsobů, jak toho dosáhnout, je vložení metadat do samotných souborů PDF.

V tomto komplexním tutoriálu se podíváme na to, jak podepisovat dokumenty PDF metadaty pomocí nástroje GroupDocs.Signature pro .NET. Podpisy metadat umožňují vkládat do dokumentu další informace, jako jsou údaje o autorovi, časová razítka vytvoření, identifikátory dokumentu a vlastní hodnoty, aniž by se viditelně změnil vzhled dokumentu.

## Předpoklady

Než začneme, ujistěte se, že máte připraveno následující:

1. [GroupDocs.Signature pro .NET](https://releases.groupdocs.com/signature/net/) - Stáhněte a nainstalujte knihovnu
2. Vývojové prostředí - Visual Studio nebo jakékoli jiné IDE kompatibilní s .NET
3. PDF dokument - Ukázkový PDF soubor k podepsání
4. Základní znalost C# - znalost programovacího jazyka C#

## Importovat jmenné prostory

Začněte importem potřebných jmenných prostorů pro přístup k funkci GroupDocs.Signature:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## Krok 1: Nastavení cest k souborům

Nejprve definujte cestu k dokumentu PDF a určete, kam chcete uložit podepsaný výstup:

```csharp
// Zadejte cestu k vašemu PDF dokumentu
string filePath = "sample.pdf";

// Definujte výstupní adresář a cestu k souboru
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignPdfWithMetadata", "SignedWithMetadata.pdf");

// Ujistěte se, že výstupní adresář existuje.
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## Krok 2: Inicializace objektu Signature

Vytvořte instanci třídy Signature se zdrojovým PDF dokumentem:

```csharp
using (Signature signature = new Signature(filePath))
{
    // Kód pro podpis bude zde
}
```

## Krok 3: Definování možností metadat

Vytvořte a nakonfigurujte možnosti metadat a přidejte různé typy podpisů metadat:

```csharp
// Vytvořit objekt možností metadat
MetadataSignOptions options = new MetadataSignOptions();

// Přidávání různých typů metadat pomocí rozhraní Fluent
options
    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // Řetězcová hodnota
    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // Hodnota data a času
    .Add(new PdfMetadataSignature("DocumentId", 123456))            // Celočíselná hodnota
    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // Dvojitá hodnota
    .Add(new PdfMetadataSignature("Amount", 123.456M))              // Desetinná hodnota
    .Add(new PdfMetadataSignature("Total", 123.456F));              // Hodnota s plovoucí desetinnou čárkou
```

## Krok 4: Podepište PDF pomocí metadat

Použijte podpisy metadat na dokument PDF a uložte výsledek:

```csharp
// Podepište dokument a uložte ho do výstupní cesty
SignResult result = signature.Sign(outputFilePath, options);

// Zobrazit zprávu o úspěchu
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed document saved at: {outputFilePath}");
```

## Kompletní příklad

Zde je kompletní příklad kódu, který shrnuje všechny kroky dohromady:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignPdfWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // Zadejte cesty k souborům
            string filePath = "sample.pdf";
            string outputFilePath = Path.Combine("Your Document Directory", "SignPdfWithMetadata", "SignedWithMetadata.pdf");
            
            // Ujistěte se, že výstupní adresář existuje.
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // Podepište PDF metadaty
            using (Signature signature = new Signature(filePath))
            {
                // Vytvořit objekt možností metadat
                MetadataSignOptions options = new MetadataSignOptions();
                
                // Přidání různých typů podpisů metadat
                options
                    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // Řetězcová hodnota
                    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // Hodnota data a času
                    .Add(new PdfMetadataSignature("DocumentId", 123456))            // Celočíselná hodnota
                    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // Dvojitá hodnota
                    .Add(new PdfMetadataSignature("Amount", 123.456M))              // Desetinná hodnota
                    .Add(new PdfMetadataSignature("Total", 123.456F));              // Hodnota s plovoucí desetinnou čárkou
                
                // Podepsat dokument a uložit do souboru
                SignResult result = signature.Sign(outputFilePath, options);
                
                // Zobrazit výsledky
                Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## Pokročilé operace s metadaty PDF

### Přidávání vlastních metadat s podporou jmenných prostorů

Dokumenty PDF podporují vlastní metadata s podporou jmenného prostoru XML:

```csharp
// Přidání vlastních metadat s jmenným prostorem
options.Add(new PdfMetadataSignature("CustomProperty", "Custom Value")
{
    NamespaceUri = "http://váš-jmenný_prostor.com/schéma
});
```

### Vyhledávání metadat v podepsaných PDF souborech

Po podepsání můžete chtít ověřit nebo extrahovat metadata:

```csharp
// Vytvořte možnosti vyhledávání pro metadata
MetadataSearchOptions searchOptions = new MetadataSearchOptions();

// Hledání podpisů metadat
SearchResult searchResult = signature.Search(searchOptions);

// Zobrazit nalezené podpisy
Console.WriteLine($"Found {searchResult.Signatures.Count} metadata signatures:");
foreach (var foundSignature in searchResult.Signatures)
{
    MetadataSignature metadataSignature = foundSignature as MetadataSignature;
    if (metadataSignature != null)
    {
        Console.WriteLine($"- {metadataSignature.Name}: {metadataSignature.Value} ({metadataSignature.Value.GetType().Name})");
    }
}
```

### Práce se standardními metadaty PDF

Dokumenty PDF mají standardní pole metadat, ke kterým lze přistupovat a upravovat je:

```csharp
// Nastavení standardních polí metadat PDF
options
    .Add(new PdfMetadataSignature("Title", "Important Contract"))
    .Add(new PdfMetadataSignature("Subject", "Legal Agreement"))
    .Add(new PdfMetadataSignature("Keywords", "contract, agreement, legal, binding"))
    .Add(new PdfMetadataSignature("Creator", "Legal Department"))
    .Add(new PdfMetadataSignature("Producer", "GroupDocs.Signature"));
```

## Závěr

V tomto tutoriálu jste se naučili, jak podepisovat dokumenty PDF metadaty pomocí nástroje GroupDocs.Signature pro .NET. Vkládání metadat do souborů PDF představuje vynikající způsob, jak zvýšit autenticitu dokumentů, přidat důležité informace a vylepšit pracovní postupy správy dokumentů.

Metadata v PDF souborech jsou obzvláště cenná v obchodním prostředí, kde je nezbytná sledovatelnost dokumentů a ověření jejich pravosti. Vložená metadata mohou zahrnovat informace o původu dokumentu, autorovi, čase vytvoření, verzi a uživatelských vlastnostech relevantních pro pracovní postup vaší organizace.

Implementací podpisů metadat pomocí GroupDocs.Signature si můžete zajistit, aby si vaše PDF dokumenty zachovaly integritu a poskytovaly ověřitelné informace po celou dobu svého životního cyklu.

## Často kladené otázky

### Mohu upravit existující metadata v dokumentu PDF?

Ano, existující metadata v dokumentech PDF můžete upravovat. Když použijete nové podpisy metadat se stejnými názvy jako stávající, hodnoty se odpovídajícím způsobem aktualizují.

### Jsou podpisy metadat v dokumentech PDF viditelné pro koncového uživatele?

Podpisy metadat nejsou viditelné v samotném obsahu dokumentu. Lze je však zobrazit prostřednictvím panelu vlastností dokumentu v čtečkách PDF, jako je Adobe Acrobat, nebo pomocí specializovaných nástrojů pro zobrazení metadat.

### Mohu šifrovat nebo chránit metadata v souborech PDF?

GroupDocs.Signature nabízí možnosti zabezpečení dokumentů, včetně šifrování. Šifrování na úrovni dokumentu můžete použít k ochraně celého PDF souboru, včetně jeho metadat.

### Existuje omezení, kolik metadat mohu do PDF přidat?

I když specifikace PDF nestanovuje žádné striktní omezení, přidání nadměrného množství metadat může zvětšit velikost souboru. Doporučuje se do metadat zahrnout pouze relevantní a nezbytné informace.

### Mohu programově ověřit, zda byl PDF soubor po přidání metadat upraven?

Ano, GroupDocs.Signature poskytuje ověřovací funkce, které mohou pomoci zjistit, zda byl dokument po podepsání upraven, včetně změn metadat.

### Kde mohu najít další zdroje a podporu?

- [Referenční informace k API](https://reference.groupdocs.com/signature/net/)
- [Soubory ke stažení](https://releases.groupdocs.com/signature/net/)
- [Příklady](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [Dokumentace](https://docs.groupdocs.com/signature/net/)
- [Stránka produktu](https://products.groupdocs.com/signature/net/)
- [Blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [Fórum podpory](https://forum.groupdocs.com/c/signature/13)
- [Dočasná licence](https://purchase.groupdocs.com/temporary-license/)