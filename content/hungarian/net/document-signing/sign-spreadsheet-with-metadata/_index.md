---
"description": "Védje és javítsa Excel-táblázatait metaadat-aláírások beágyazásával a GroupDocs.Signature for .NET segítségével. Adjon hozzá szerzői információkat, időbélyegeket és egyéni adatokat a dokumentumok nyomon követhetőségének és hitelességének javítása érdekében."
"linktitle": "Táblázat aláírása metaadatokkal"
"second_title": "GroupDocs.Signature .NET API"
"title": "Metaadat-aláírások hozzáadása Excel-táblázatokhoz C# .NET-ben"
"url": "/hu/net/document-signing/sign-spreadsheet-with-metadata/"
"weight": 13
type: docs
---
## Bevezetés

Az Excel-táblázatok gyakran tartalmaznak kritikus üzleti adatokat, pénzügyi információkat és fontos számításokat. Hitelességük biztosítása, eredetük nyomon követése és integritásuk védelme kulcsfontosságú számos szakmai környezetben. A táblázatok biztonságának és nyomon követhetőségének fokozásának egyik hatékony módja a metaadat-aláírások beágyazása.

Ez az átfogó oktatóanyag végigvezeti Önt az Excel-táblázatok metaadatokkal való aláírásának folyamatán a GroupDocs.Signature for .NET használatával. Metaadat-aláírások hozzáadásával értékes információkat, például szerzői adatokat, létrehozási időbélyegeket, dokumentumazonosítókat és egyéb egyéni tulajdonságokat ágyazhat be közvetlenül a táblázatfájl struktúrájába.

## Előfeltételek

Mielőtt folytatná ezt az oktatóanyagot, győződjön meg arról, hogy rendelkezik a következőkkel:

1. [GroupDocs.Signature .NET-hez](https://releases.groupdocs.com/signature/net/) - Töltse le és telepítse a könyvtárat
2. Fejlesztői környezet - Visual Studio vagy bármilyen más .NET-kompatibilis IDE
3. Excel táblázatkezelő – Minta táblázatkezelő fájl (XLSX, XLS stb.)
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

Adja meg a forrástáblázat elérési útját és az aláírt kimenet mentési helyét:

```csharp
// Adja meg az Excel-fájl elérési útját
string filePath = "sample.xlsx";

// Adja meg az aláírt táblázat kimeneti könyvtárát és fájlnevét
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignSpreadsheetWithMetadata", "SignedWithMetadata.xlsx");

// Győződjön meg arról, hogy a kimeneti könyvtár létezik
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## 2. lépés: Az aláírásobjektum inicializálása

Hozz létre egy példányt a Signature osztályból a forrás táblázatfájloddal:

```csharp
using (Signature signature = new Signature(filePath))
{
    // A kód többi része ide fog kerülni
}
```

## 3. lépés: Metaadat-aláírások létrehozása és konfigurálása

Ezután definiálja a metaadat-beállításokat, és hozzon létre egy táblázat metaadat-aláírásokból álló tömböt:

```csharp
// Metaadat-beállítások objektum létrehozása
MetadataSignOptions options = new MetadataSignOptions();

// Hozzon létre táblázat metaadat-aláírások tömbjét különböző adattípusokkal
SpreadsheetMetadataSignature[] signatures = new SpreadsheetMetadataSignature[]
{
    new SpreadsheetMetadataSignature("Author", "Mr.Sherlock Holmes"), // Karakterlánc érték
    new SpreadsheetMetadataSignature("CreatedOn", DateTime.Now),      // Dátum/Idő érték
    new SpreadsheetMetadataSignature("DocumentId", 123456),           // Egész érték
    new SpreadsheetMetadataSignature("SignatureId", 123.456D),        // Dupla érték
    new SpreadsheetMetadataSignature("Amount", 123.456M),             // Decimális érték
    new SpreadsheetMetadataSignature("Total", 123.456F)               // Lebegőpontos érték
};

// Aláírásgyűjtés hozzáadása a beállításokhoz
options.Signatures.AddRange(signatures);
```

## 4. lépés: A táblázat aláírása metaadatokkal

Alkalmazd a metaadat-aláírásokat a táblázatra, és mentsd el az eredményt:

```csharp
// Írja alá a dokumentumot, és mentse el a kimeneti fájl elérési útjára
SignResult result = signature.Sign(outputFilePath, options);

// Sikeres üzenet megjelenítése
Console.WriteLine($"\nSource spreadsheet signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed spreadsheet saved at: {outputFilePath}");
```

## Teljes példa

Íme a teljes kódpélda, amely az összes lépést összefoglalja:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignSpreadsheetWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // Fájlútvonalak megadása
            string filePath = "sample.xlsx";
            string outputFilePath = Path.Combine("Your Document Directory", "SignSpreadsheetWithMetadata", "SignedWithMetadata.xlsx");
            
            // Győződjön meg arról, hogy a kimeneti könyvtár létezik
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // Aláírja a táblázatot metaadatokkal
            using (Signature signature = new Signature(filePath))
            {
                // Metaadat-beállítások objektum létrehozása
                MetadataSignOptions options = new MetadataSignOptions();
                
                // Hozzon létre táblázat metaadat-aláírások tömbjét különböző adattípusokkal
                SpreadsheetMetadataSignature[] signatures = new SpreadsheetMetadataSignature[]
                {
                    new SpreadsheetMetadataSignature("Author", "Mr.Sherlock Holmes"), // Karakterlánc érték
                    new SpreadsheetMetadataSignature("CreatedOn", DateTime.Now),      // Dátum/Idő érték
                    new SpreadsheetMetadataSignature("DocumentId", 123456),           // Egész érték
                    new SpreadsheetMetadataSignature("SignatureId", 123.456D),        // Dupla érték
                    new SpreadsheetMetadataSignature("Amount", 123.456M),             // Decimális érték
                    new SpreadsheetMetadataSignature("Total", 123.456F)               // Lebegőpontos érték
                };
                
                // Aláírásgyűjtés hozzáadása a beállításokhoz
                options.Signatures.AddRange(signatures);
                
                // Dokumentum aláírása és mentése fájlba
                SignResult result = signature.Sign(outputFilePath, options);
                
                // Eredmények megjelenítése
                Console.WriteLine($"\nSource spreadsheet signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## Speciális táblázatkezelő metaadat-technikák

### Egyéni és beépített táblázattulajdonságok használata

Az Excel-táblázatok beépített és egyéni tulajdonságokkal is rendelkeznek, amelyek a fájltulajdonságok párbeszédpanelen keresztül érhetők el. A GroupDocs.Signature lehetővé teszi mindkettővel való munkát:

```csharp
// Beépített tulajdonságok hozzáadása
signatures = new SpreadsheetMetadataSignature[]
{
    new SpreadsheetMetadataSignature("Company", "Sherlock Holmes Consulting"),
    new SpreadsheetMetadataSignature("Category", "Financial"),
    new SpreadsheetMetadataSignature("Keywords", "budget,forecast,analysis"),
    new SpreadsheetMetadataSignature("Comments", "This spreadsheet contains confidential information"),
    new SpreadsheetMetadataSignature("Manager", "John Watson")
};
options.Signatures.AddRange(signatures);

// Egyéni tulajdonságok hozzáadása
options.Signatures.Add(new SpreadsheetMetadataSignature("Department", "Finance"));
options.Signatures.Add(new SpreadsheetMetadataSignature("SecurityLevel", "Confidential"));
```

### Metaadatok keresése aláírt táblázatokban

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

### Meglévő metaadatok frissítése

A táblázatokban található meglévő metaadatokat ugyanazon tulajdonságnevek használatával frissítheti:

```csharp
// Meglévő metaadatok frissítése
options.Signatures.Add(new SpreadsheetMetadataSignature("Author", "Updated Author Name"));
```

## Következtetés

Ebben az átfogó oktatóanyagban megtanulta, hogyan írhat alá Excel-táblázatokat metaadatokkal a GroupDocs.Signature for .NET használatával. A metaadatok táblázatfájlokba ágyazása javítja a dokumentumok nyomon követhetőségét, értékes kontextust biztosít, és segít a hitelesség megállapításában.

táblázatokban található metaadat-aláírások különösen hasznosak azokban az üzleti környezetekben, ahol a dokumentum eredete, szerzősége és verziókövetése fontos. A beágyazott metaadatok tartalmazhatnak információkat a szerzőről, a létrehozás idejéről, a dokumentum azonosítóiról és a szervezet igényeinek megfelelő egyéni tulajdonságokról.

A GroupDocs.Signature segítségével metaadat-aláírások megvalósításával biztosíthatja, hogy Excel-táblázatai megőrizzék integritásukat, és ellenőrizhető információkat szolgáltassanak teljes életciklusuk során.

## GYIK

### Hozzáadhatok metaadatokat olyan táblázatokhoz, amelyekhez már vannak definiált tulajdonságok?

Igen, hozzáadhat új metaadatokat, vagy frissítheti a meglévő metaadatokat a táblázatokban. A GroupDocs.Signature kezeli az integrációt, akár új tulajdonságok hozzáadásával, akár a meglévők azonos nevű frissítésével.

### Mely táblázatformátumok támogatottak a metaadat-aláíráshoz?

GroupDocs.Signature for .NET támogatja a metaadat-aláírást különféle táblázatformátumokhoz, beleértve az XLSX, XLS, XLSM, ODS és egyebeket. A teljes listát lásd a következőben: [hivatalos dokumentáció](https://docs.groupdocs.com/signature/net/).

### Láthatók a felhasználók számára a táblázatokban található metaadat-aláírások?

A metaadat-aláírások nem láthatók magában a táblázat tartalmában. Azonban megtekinthetők a dokumentum tulajdonságai panelen az Excelben vagy más kompatibilis alkalmazásokban.

### Programozottan ellenőrizhetem, hogy egy táblázatot manipuláltak-e a metaadatok hozzáadása után?

Igen, a GroupDocs.Signature olyan ellenőrzési funkciókat biztosít, amelyek segítenek észlelni, hogy egy dokumentumot módosítottak-e az aláírás után, beleértve a metaadatok változásait is.

### A metaadatok hozzáadása befolyásolja a táblázatkezelő működését?

A metaadatok hozzáadása minimális hatással van a fájlméretre, és nincs hatással a táblázatkezelő funkcionalitására. Ez egy egyszerű módja a dokumentum tulajdonságainak javítására a számítások, képletek vagy más Excel-funkciók befolyásolása nélkül.

### Hol találok további forrásokat és támogatást?

- [API-referencia](https://reference.groupdocs.com/signature/net/)
- [Letöltések](https://releases.groupdocs.com/signature/net/)
- [Példák](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [Dokumentáció](https://docs.groupdocs.com/signature/net/)
- [Termékoldal](https://products.groupdocs.com/signature/net/)
- [Blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [Támogatási fórum](https://forum.groupdocs.com/c/signature/13)
- [Ideiglenes engedély](https://purchase.groupdocs.com/temporary-license/)