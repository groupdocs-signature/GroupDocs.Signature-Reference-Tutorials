---
"description": "Naučte se, jak podepisovat a vkládat metadata do obrázků pomocí nástroje GroupDocs.Signature pro .NET. Přidejte informace o autorovi, časová razítka a vlastní data pro zvýšení autenticity a sledovatelnosti obrázků."
"linktitle": "Podepsat obrázek metadaty"
"second_title": "GroupDocs.Signature .NET API"
"title": "Podepisování obrázků metadaty v C# .NET"
"url": "/cs/net/document-signing/sign-image-with-metadata/"
"weight": 10
---

## Zavedení

Digitální podepisování obrázků pomocí metadat se stává stále důležitějším pro stanovení autenticity, vlastnictví a sledovatelnosti. GroupDocs.Signature pro .NET poskytuje výkonné a zároveň snadno použitelné řešení pro přidávání podpisů metadat k různým formátům obrázků. Tento tutoriál vás provede celým procesem podepisování obrázků metadaty pomocí jazyka C#.

Metadatové podpisy umožňují vkládat cenné informace přímo do obrazových souborů, jako jsou informace o autorovi, časová razítka vytvoření, jedinečné identifikátory a další. Tyto informace se stávají součástí samotného obrazového souboru a poskytují spolehlivou metodu pro sledování a ověřování pravosti obrazu.

## Předpoklady

Než budete pokračovat v tomto tutoriálu, ujistěte se, že máte následující:

1. [GroupDocs.Signature pro .NET](https://releases.groupdocs.com/signature/net/) - Stáhněte a nainstalujte knihovnu
2. Vývojové prostředí - Visual Studio nebo jakékoli kompatibilní IDE s podporou .NET
3. Soubor obrázku – Ukázkový soubor obrázku v podporovaném formátu (PNG, JPG, TIFF atd.)
4. Základní znalosti programování v C# - Seznámení s koncepty programování v C#

## Importovat jmenné prostory

Začněte importem potřebných jmenných prostorů pro přístup k funkcím GroupDocs.Signature:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## Krok 1: Nastavení cest k souborům

Definujte cesty ke zdrojovému obrazu a kam se má uložit podepsaný výstup:

```csharp
// Zadejte cestu ke zdrojovému souboru s obrázkem
string filePath = "sample.png";

// Definujte výstupní adresář a název souboru pro podepsaný obraz
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignImageWithMetadata", "SignedWithMetadata.png");

// Ujistěte se, že výstupní adresář existuje.
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## Krok 2: Inicializace objektu Signature

Vytvořte instanci třídy Signature se zdrojovým souborem obrázku:

```csharp
using (Signature signature = new Signature(filePath))
{
    // Zbytek kódu půjde sem
}
```

## Krok 3: Vytvoření a konfigurace podpisů metadat

Dále definujte metadata, která chcete vložit do obrázku. GroupDocs.Signature podporuje různé datové typy pro metadata:

```csharp
// Inicializovat ID metadat (specifické pro formát obrázku)
ushort imgsMetadataId = 41996;

// Vytvořit objekt možností metadat
MetadataSignOptions options = new MetadataSignOptions();

// Přidání různých typů podpisů metadat
options
    .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Sherlock Holmes"))  // Řetězcová hodnota
    .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // Hodnota data a času
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // Celočíselná hodnota
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // Dvojitá hodnota
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // Desetinná hodnota
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // Hodnota s plovoucí desetinnou čárkou
```

## Krok 4: Podepište obrázek metadaty

Aplikujte podpisy metadat na obrázek a uložte výsledek:

```csharp
// Podepište dokument a uložte ho do cesty k výstupnímu souboru.
SignResult result = signature.Sign(outputFilePath, options);

// Zobrazit zprávu o úspěchu
Console.WriteLine($"\nSource image signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed image saved at: {outputFilePath}");
```

## Kompletní příklad

Zde je kompletní příklad kódu, který shrnuje všechny kroky dohromady:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignImageWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // Zadejte cesty k souborům
            string filePath = "sample.png";            
            string outputFilePath = Path.Combine("Your Document Directory", "SignImageWithMetadata", "SignedWithMetadata.png");
            
            // Ujistěte se, že výstupní adresář existuje.
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // Podepište obrázek metadaty
            using (Signature signature = new Signature(filePath))
            {
                // Inicializovat ID metadat (specifické pro formát obrázku)
                ushort imgsMetadataId = 41996;
                
                // Vytvořit možnosti metadat
                MetadataSignOptions options = new MetadataSignOptions();
                
                // Přidání různých typů podpisů metadat
                options
                    .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Sherlock Holmes")) // Řetězcová hodnota
                    .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // Hodnota data a času
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // Celočíselná hodnota
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // Dvojitá hodnota
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // Desetinná hodnota
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // Hodnota s plovoucí desetinnou čárkou
                
                // Podepsat dokument a uložit do souboru
                SignResult result = signature.Sign(outputFilePath, options);
                
                // Zobrazit výsledky
                Console.WriteLine($"\nSource image signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## Pokročilé techniky podepisování metadat

### Práce s vlastními metadaty

Můžete také vytvořit vlastní pole metadat se specifickými ID:

```csharp
// Vytvořte vlastní metadata se specifickým ID
options.Add(new ImageMetadataSignature(42000, "CustomValue"));
```

### Ověřování podpisů metadat

Po podepsání můžete chtít ověřit podpisy metadat:

```csharp
// Vytvořit možnosti ověření
MetadataSearchOptions searchOptions = new MetadataSearchOptions();

// Hledání podpisů metadat
SearchResult result = signature.Search(searchOptions);

// Zobrazit nalezené podpisy
Console.WriteLine($"Found {result.Signatures.Count} metadata signatures:");
foreach(var metadataSignature in result.Signatures)
{
    Console.WriteLine($"- {metadataSignature.Name}: {metadataSignature.Value}");
}
```

## Závěr

V tomto tutoriálu jste se naučili, jak podepisovat obrázky metadaty pomocí nástroje GroupDocs.Signature pro .NET. Vkládání metadat do obrázků představuje vynikající způsob, jak zvýšit autenticitu obrázků, přidat důležité informace a vylepšit pracovní postupy správy dokumentů. Tento proces je přímočarý, ale zároveň výkonný a umožňuje přizpůsobení na základě vašich specifických požadavků.

Metadata vložená do obrazového souboru lze použít k různým účelům, jako je ochrana autorských práv, sledování původu obrázku, přidávání popisných informací a vytváření digitálního řetězce úschovy. Implementací podpisů metadat můžete zajistit, že si vaše obrázky zachovají integritu a autenticitu po celou dobu svého životního cyklu.

## Často kladené otázky

### Mohu přidat metadata k existujícím podepsaným obrázkům?

Ano, k obrázkům, které již obsahují podpisy metadat, můžete přidat další metadata. Stávající metadata budou zachována a nová metadata budou odpovídajícím způsobem přidána.

### Které formáty obrázků jsou podporovány pro podepisování metadat?

GroupDocs.Signature pro .NET podporuje podepisování metadat pro různé obrazové formáty, včetně PNG, JPEG, TIFF, BMP, GIF a dalších. Úplný seznam naleznete v [oficiální dokumentace](https://docs.groupdocs.com/signature/net/).

### Je možné šifrovat metadata v obrázcích?

Ano, GroupDocs.Signature nabízí možnosti šifrování metadat pro zvýšení zabezpečení. Možnosti šifrování poskytované knihovnou můžete použít k ochraně citlivých metadat.

### Mohu programově ověřit pravost podepsaných obrázků?

Rozhodně. K ověření podpisů metadat a potvrzení pravosti podepsaných obrázků můžete použít ověřovací metody v GroupDocs.Signature.

### Existuje omezení velikosti souboru při podepisování obrázků metadaty?

Samotná knihovna nemá žádné konkrétní omezení velikosti souboru, ale velmi velké soubory mohou vyžadovat více času na zpracování a paměti. Při práci s extrémně velkými obrázky se doporučuje zvážit systémové prostředky.

### Jak mohu získat dočasnou licenci pro účely testování?

Můžete získat [dočasná licence](https://purchase.groupdocs.com/temporary-license/) pro testování GroupDocs.Signature před provedením nákupu.

### Kde mohu najít další zdroje a podporu?

- [Referenční informace k API](https://reference.groupdocs.com/signature/net/)
- [Soubory ke stažení](https://releases.groupdocs.com/signature/net/)
- [Příklady](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [Dokumentace](https://docs.groupdocs.com/signature/net/)
- [Stránka produktu](https://products.groupdocs.com/signature/net/)
- [Blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [Fórum podpory](https://forum.groupdocs.com/c/signature/13)