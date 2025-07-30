---
"description": "Integráljon metaadat-aláírásokat PDF-dokumentumokba a GroupDocs.Signature for .NET segítségével. Ismerje meg, hogyan ágyazhat be szerzői információkat, időbélyegeket és egyéni adatokat a PDF-ek hitelességének és nyomon követhetőségének javítása érdekében."
"linktitle": "PDF aláírása metaadatokkal"
"second_title": "GroupDocs.Signature .NET API"
"title": "Metaadat-aláírások hozzáadása PDF-dokumentumokhoz C# .NET-ben"
"url": "/hu/net/document-signing/sign-pdf-with-metadata/"
"weight": 11
---

## Bevezetés

PDF (Portable Document Format) dokumentumokat széles körben használják az iparágakban a konzisztenciájuk és platformfüggetlenségük miatt. Ezen dokumentumok hitelességének és nyomon követhetőségének biztosítása kulcsfontosságú számos szakmai környezetben. Ennek egyik hatékony módja a metaadatok beágyazása magukba a PDF fájlokba.

Ebben az átfogó oktatóanyagban megvizsgáljuk, hogyan írhatunk alá metaadatokkal PDF dokumentumokat a GroupDocs.Signature for .NET használatával. A metaadat-aláírások lehetővé teszik további információk, például szerzői adatok, létrehozási időbélyegek, dokumentumazonosítók és egyéni értékek beágyazását a dokumentumba anélkül, hogy láthatóan megváltoztatnánk a dokumentum megjelenését.

## Előfeltételek

Mielőtt elkezdenénk, győződjünk meg róla, hogy a következők megvannak:

1. [GroupDocs.Signature .NET-hez](https://releases.groupdocs.com/signature/net/) - Töltse le és telepítse a könyvtárat
2. Fejlesztői környezet - Visual Studio vagy bármilyen más .NET-kompatibilis IDE
3. PDF dokumentum – Minta PDF fájl aláíráshoz
4. C# alapismeretek - Ismeri a C# programozási nyelvet

## Névterek importálása

Kezdje a GroupDocs.Signature funkció eléréséhez szükséges névterek importálásával:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## 1. lépés: Fájlútvonalak beállítása

Először is, adja meg a PDF dokumentum elérési útját, és adja meg, hová szeretné menteni az aláírt kimenetet:

```csharp
// Adja meg a PDF dokumentum elérési útját
string filePath = "sample.pdf";

// Kimeneti könyvtár és fájlútvonal megadása
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignPdfWithMetadata", "SignedWithMetadata.pdf");

// Győződjön meg arról, hogy a kimeneti könyvtár létezik
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## 2. lépés: Az aláírásobjektum inicializálása

Hozz létre egy példányt a Signature osztályból a forrás PDF dokumentumoddal:

```csharp
using (Signature signature = new Signature(filePath))
{
    // Az aláíráshoz szükséges kód ide fog kerülni.
}
```

## 3. lépés: Metaadat-beállítások meghatározása

Hozza létre és konfigurálja a metaadat-beállításokat, különféle típusú metaadat-aláírások hozzáadásával:

```csharp
// Metaadat-beállítások objektum létrehozása
MetadataSignOptions options = new MetadataSignOptions();

// Különböző típusú metaadatok hozzáadása a Fluent felület használatával
options
    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // Karakterlánc érték
    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // Dátum/Idő érték
    .Add(new PdfMetadataSignature("DocumentId", 123456))            // Egész érték
    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // Dupla érték
    .Add(new PdfMetadataSignature("Amount", 123.456M))              // Decimális érték
    .Add(new PdfMetadataSignature("Total", 123.456F));              // Lebegőpontos érték
```

## 4. lépés: PDF aláírása metaadatokkal

Alkalmazza a metaadat-aláírásokat a PDF dokumentumra, és mentse az eredményt:

```csharp
// Aláírja a dokumentumot, és mentse el a kimeneti útvonalra.
SignResult result = signature.Sign(outputFilePath, options);

// Sikeres üzenet megjelenítése
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed document saved at: {outputFilePath}");
```

## Teljes példa

Íme a teljes kódpélda, amely az összes lépést összefoglalja:

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
            // Fájlútvonalak megadása
            string filePath = "sample.pdf";
            string outputFilePath = Path.Combine("Your Document Directory", "SignPdfWithMetadata", "SignedWithMetadata.pdf");
            
            // Győződjön meg arról, hogy a kimeneti könyvtár létezik
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // PDF aláírása metaadatokkal
            using (Signature signature = new Signature(filePath))
            {
                // Metaadat-beállítások objektum létrehozása
                MetadataSignOptions options = new MetadataSignOptions();
                
                // Különböző típusú metaadat-aláírások hozzáadása
                options
                    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // Karakterlánc érték
                    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // Dátum/Idő érték
                    .Add(new PdfMetadataSignature("DocumentId", 123456))            // Egész érték
                    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // Dupla érték
                    .Add(new PdfMetadataSignature("Amount", 123.456M))              // Decimális érték
                    .Add(new PdfMetadataSignature("Total", 123.456F));              // Lebegőpontos érték
                
                // Dokumentum aláírása és mentése fájlba
                SignResult result = signature.Sign(outputFilePath, options);
                
                // Eredmények megjelenítése
                Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## Speciális PDF metaadat-műveletek

### Egyéni metaadatok hozzáadása névtér-támogatással

A PDF dokumentumok támogatják az egyéni metaadatokat XML névtér-támogatással:

```csharp
// Egyéni metaadatok hozzáadása névtérrel
options.Add(new PdfMetadataSignature("CustomProperty", "Custom Value")
{
    NamespaceUri = "http://your-namespace.com/schema"
});
```

### Metaadatok keresése aláírt PDF-ekben

Aláírás után érdemes lehet ellenőrizni vagy kinyerni a metaadatokat:

```csharp
// Metaadatok keresési beállításainak létrehozása
MetadataSearchOptions searchOptions = new MetadataSearchOptions();

// Metaadat-aláírások keresése
SearchResult searchResult = signature.Search(searchOptions);

// Talált aláírások megjelenítése
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

### Standard PDF metaadatokkal való munka

A PDF dokumentumok szabványos metaadat-mezőket tartalmaznak, amelyekhez hozzáférhetünk és módosíthatunk:

```csharp
// Standard PDF metaadatmezők beállítása
options
    .Add(new PdfMetadataSignature("Title", "Important Contract"))
    .Add(new PdfMetadataSignature("Subject", "Legal Agreement"))
    .Add(new PdfMetadataSignature("Keywords", "contract, agreement, legal, binding"))
    .Add(new PdfMetadataSignature("Creator", "Legal Department"))
    .Add(new PdfMetadataSignature("Producer", "GroupDocs.Signature"));
```

## Következtetés

Ebben az oktatóanyagban megtanulta, hogyan írhat alá PDF dokumentumokat metaadatokkal a GroupDocs.Signature for .NET használatával. A metaadatok PDF fájlokba ágyazása kiváló módot kínál a dokumentumok hitelességének javítására, fontos információk hozzáadására és a dokumentumkezelési munkafolyamatok javítására.

A PDF-ekben található metaadat-aláírások különösen értékesek azokban az üzleti környezetekben, ahol a dokumentumok nyomon követhetősége és hitelességének ellenőrzése elengedhetetlen. A beágyazott metaadatok tartalmazhatnak információkat a dokumentum eredetéről, szerzőjéről, létrehozási idejéről, verziójáról és a szervezet munkafolyamatához kapcsolódó egyéni tulajdonságokról.

GroupDocs.Signature segítségével metaadat-aláírások megvalósításával biztosíthatja, hogy PDF-dokumentumai megőrzik integritásukat, és ellenőrizhető információkat nyújtsanak életciklusuk során.

## GYIK

### Módosíthatom a meglévő metaadatokat egy PDF dokumentumban?

Igen, módosíthatja a meglévő metaadatokat a PDF dokumentumokban. Amikor új metaadat-aláírásokat alkalmaz a meglévőkkel megegyező nevekkel, az értékek ennek megfelelően frissülnek.

### Láthatók a végfelhasználó számára a PDF dokumentumokban található metaadat-aláírások?

A metaadat-aláírások nem láthatók magában a dokumentum tartalmában. Azonban megtekinthetők a dokumentum tulajdonságai panelen a PDF-olvasókban, például az Adobe Acrobatban, vagy a metaadatok megtekintésére szolgáló speciális eszközök használatával.

### Titkosíthatom vagy védhetem a PDF-ekben található metaadatokat?

A GroupDocs.Signature dokumentumok védelmére szolgáló lehetőségeket kínál, beleértve a titkosítást is. Dokumentumszintű titkosítást alkalmazhat a teljes PDF-fájl, beleértve a metaadatait is, védelmére.

### Van-e korlátozás arra vonatkozóan, hogy mennyi metaadatot adhatok hozzá egy PDF-hez?

Bár a PDF specifikáció nem szab szigorú korlátot, a metaadatok túlzott mennyiségének hozzáadása növelheti a fájlméretet. Javasoljuk, hogy a metaadatokban csak a releváns és szükséges információkat szerepeltesse.

### Programozottan ellenőrizhetem, hogy egy PDF-et manipuláltak-e a metaadatok hozzáadása után?

Igen, a GroupDocs.Signature olyan ellenőrzési funkciókat biztosít, amelyek segítenek észlelni, hogy egy dokumentumot módosítottak-e az aláírás után, beleértve a metaadatok változásait is.

### Hol találok további forrásokat és támogatást?

- [API-referencia](https://reference.groupdocs.com/signature/net/)
- [Letöltések](https://releases.groupdocs.com/signature/net/)
- [Példák](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [Dokumentáció](https://docs.groupdocs.com/signature/net/)
- [Termékoldal](https://products.groupdocs.com/signature/net/)
- [Blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [Támogatási fórum](https://forum.groupdocs.com/c/signature/13)
- [Ideiglenes engedély](https://purchase.groupdocs.com/temporary-license/)