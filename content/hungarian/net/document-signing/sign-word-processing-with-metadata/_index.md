---
"description": "Metaadat-aláírások hozzáadása Word-dokumentumokhoz a GroupDocs.Signature for .NET segítségével. Szerzői adatok, időbélyegek és egyéni tulajdonságok beágyazása a dokumentumok biztonságának és nyomon követhetőségének fokozása érdekében."
"linktitle": "Aláírásos szövegszerkesztés metaadatokkal"
"second_title": "GroupDocs.Signature .NET API"
"title": "Word-dokumentumok fejlesztése metaadat-aláírásokkal C# .NET-ben"
"url": "/hu/net/document-signing/sign-word-processing-with-metadata/"
"weight": 14
---

## Bevezetés

A szövegszerkesztési dokumentumok a leggyakrabban használt fájltípusok közé tartoznak az üzleti életben, az oktatásban és a személyes kommunikációban. Ezen dokumentumok hitelességének biztosítása, eredetük nyomon követése és integritásuk megőrzése számos szakmai környezetben kulcsfontosságú. A dokumentumok biztonságának és nyomon követhetőségének fokozásának egyik hatékony módja a metaadat-aláírások beágyazása.

Ez az átfogó oktatóanyag végigvezeti Önt a szövegszerkesztő dokumentumok metaadatokkal történő aláírásának folyamatán a GroupDocs.Signature for .NET használatával. Metaadat-aláírások hozzáadásával értékes információkat, például szerzői adatokat, létrehozási időbélyegeket, dokumentumazonosítókat és egyéb egyéni tulajdonságokat ágyazhat be közvetlenül a dokumentumfájl-struktúrába.

## Előfeltételek

Mielőtt folytatná ezt az oktatóanyagot, győződjön meg arról, hogy rendelkezik a következőkkel:

1. [GroupDocs.Signature .NET-hez](https://releases.groupdocs.com/signature/net/) - Töltse le és telepítse a könyvtárat
2. Fejlesztői környezet - Visual Studio vagy bármilyen más .NET-kompatibilis IDE
3. Word dokumentum – Mintadokumentumfájl (DOCX, DOC stb.)
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

Adja meg a forrás Word-dokumentum elérési útját, és azt, hogy hová kell menteni az aláírt kimenetet:

```csharp
// Adja meg a Word-dokumentum elérési útját
string filePath = "sample.docx";

// Adja meg az aláírt dokumentum kimeneti könyvtárát és fájlnevét
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignWordProcessingWithMetadata", "SignedWithMetadata.docx");

// Győződjön meg arról, hogy a kimeneti könyvtár létezik
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## 2. lépés: Az aláírásobjektum inicializálása

Hozz létre egy példányt a Signature osztályból a forrás Word dokumentumoddal:

```csharp
using (Signature signature = new Signature(filePath))
{
    // A kód többi része ide fog kerülni
}
```

## 3. lépés: Metaadat-aláírások létrehozása és konfigurálása

Ezután határozza meg a metaadat-beállításokat, és adjon hozzá különböző típusú metaadat-aláírásokat:

```csharp
// Metaadat-beállítások objektum létrehozása
MetadataSignOptions options = new MetadataSignOptions();

// Különböző típusú metaadatok hozzáadása a Fluent felület használatával
options
    .Add(new WordProcessingMetadataSignature("Author", "Mr.Sherlock Holmes")) // Karakterlánc érték
    .Add(new WordProcessingMetadataSignature("CreatedOn", DateTime.Now))      // Dátum/Idő érték
    .Add(new WordProcessingMetadataSignature("DocumentId", 123456))           // Egész érték
    .Add(new WordProcessingMetadataSignature("SignatureId", 123.456D))        // Dupla érték
    .Add(new WordProcessingMetadataSignature("Amount", 123.456M))             // Decimális érték
    .Add(new WordProcessingMetadataSignature("Total", 123.456F));             // Lebegőpontos érték
```

## 4. lépés: A dokumentum aláírása metaadatokkal

Alkalmazd a metaadat-aláírásokat a Word-dokumentumra, és mentsd el az eredményt:

```csharp
// Írja alá a dokumentumot, és mentse el a kimeneti fájl elérési útjára
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

namespace SignWordProcessingWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // Fájlútvonalak megadása
            string filePath = "sample.docx";
            string outputFilePath = Path.Combine("Your Document Directory", "SignWordProcessingWithMetadata", "SignedWithMetadata.docx");
            
            // Győződjön meg arról, hogy a kimeneti könyvtár létezik
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // Word-dokumentum aláírása metaadatokkal
            using (Signature signature = new Signature(filePath))
            {
                // Metaadat-beállítások objektum létrehozása
                MetadataSignOptions options = new MetadataSignOptions();
                
                // Különböző típusú metaadat-aláírások hozzáadása
                options
                    .Add(new WordProcessingMetadataSignature("Author", "Mr.Sherlock Holmes")) // Karakterlánc érték
                    .Add(new WordProcessingMetadataSignature("CreatedOn", DateTime.Now))      // Dátum/Idő érték
                    .Add(new WordProcessingMetadataSignature("DocumentId", 123456))           // Egész érték
                    .Add(new WordProcessingMetadataSignature("SignatureId", 123.456D))        // Dupla érték
                    .Add(new WordProcessingMetadataSignature("Amount", 123.456M))             // Decimális érték
                    .Add(new WordProcessingMetadataSignature("Total", 123.456F));             // Lebegőpontos érték
                
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

## Speciális Word dokumentum metaadat-technikák

### Egyéni és beépített dokumentumtulajdonságok használata

A Word dokumentumok beépített és egyéni tulajdonságokkal is rendelkeznek, amelyek a dokumentum tulajdonságai panelen keresztül érhetők el. A GroupDocs.Signature lehetővé teszi mindkettővel való munkát:

```csharp
// Beépített tulajdonságok hozzáadása
options
    .Add(new WordProcessingMetadataSignature("Company", "Sherlock Holmes Consulting"))
    .Add(new WordProcessingMetadataSignature("Category", "Legal Document"))
    .Add(new WordProcessingMetadataSignature("Keywords", "contract,agreement,legal"))
    .Add(new WordProcessingMetadataSignature("Comments", "This document is confidential"))
    .Add(new WordProcessingMetadataSignature("Manager", "John Watson"));

// Egyéni tulajdonságok hozzáadása
options.Add(new WordProcessingMetadataSignature("Department", "Legal"));
options.Add(new WordProcessingMetadataSignature("SecurityLevel", "Confidential"));
```

### Metaadatok keresése aláírt Word dokumentumokban

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

### Dokumentumváltozók használata

Word dokumentumok támogatják a dokumentumváltozókat is, amelyek a metaadatok egy másik formáját jelentik:

```csharp
// Dokumentumváltozók hozzáadása
options.Add(new WordProcessingMetadataSignature("DocVariable1", "Custom Value 1", true));
options.Add(new WordProcessingMetadataSignature("DocVariable2", DateTime.Now, true));
```

## Következtetés

Ebben az átfogó oktatóanyagban megtanulta, hogyan írhat alá metaadatokkal Word-dokumentumokat a GroupDocs.Signature for .NET használatával. A metaadatok Word-dokumentumokba ágyazása javítja a dokumentumok nyomon követhetőségét, értékes kontextust biztosít, és segít a hitelesség megállapításában.

A Word-dokumentumokban található metaadat-aláírások különösen hasznosak üzleti és jogi környezetben, ahol a dokumentum eredete, szerzősége és verziókövetése fontos. A beágyazott metaadatok tartalmazhatnak információkat a szerzőről, a létrehozási időről, a dokumentum azonosítóiról és a szervezet igényeinek megfelelő egyéni tulajdonságokról.

A GroupDocs.Signature segítségével metaadat-aláírások megvalósításával biztosíthatja, hogy Word-dokumentumai megőrzik integritásukat, és ellenőrizhető információkat biztosítsanak életciklusuk során.

## GYIK

### Hozzáadhatok metaadatokat olyan Word-dokumentumokhoz, amelyekhez már vannak definiált tulajdonságok?

Igen, hozzáadhat új metaadatokat, vagy frissítheti a meglévő metaadatokat a Word-dokumentumokban. A GroupDocs.Signature kezeli az integrációt, akár új tulajdonságok hozzáadásával, akár a meglévők azonos nevű frissítésével.

### Mely szövegszerkesztő formátumok támogatottak a metaadat-aláíráshoz?

A GroupDocs.Signature for .NET támogatja a metaadat-aláírást különféle szövegszerkesztési formátumokhoz, beleértve a DOCX, DOC, RTF, ODT és egyebeket. A teljes listát lásd a következőben: [dokumentáció](https://docs.groupdocs.com/signature/net/).

### Láthatók az olvasók számára a Word-dokumentumokban található metaadat-aláírások?

A metaadat-aláírások nem láthatók magában a dokumentum tartalmában. Azonban megtekinthetők a dokumentum tulajdonságai panelen a Microsoft Wordben vagy más kompatibilis alkalmazásokban.

### Programozottan ellenőrizhetem, hogy egy Word-dokumentumot manipuláltak-e a metaadatok hozzáadása után?

Igen, a GroupDocs.Signature olyan ellenőrzési funkciókat biztosít, amelyek segítenek észlelni, hogy egy dokumentumot módosítottak-e az aláírás után, beleértve a metaadatok változásait is.

### Lehetséges metaadatokat eltávolítani egy Word dokumentumból?

Igen, a GroupDocs.Signature lehetőséget biztosít a metaadat-aláírások eltávolítására a dokumentumokból, ha szükséges. Ez hasznos lehet az érzékeny információk megtisztításához a dokumentumok külső megosztása előtt.

### Hol találok további forrásokat és támogatást?

- [API-referencia](https://reference.groupdocs.com/signature/net/)
- [Letöltések](https://releases.groupdocs.com/signature/net/)
- [Példák](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [Dokumentáció](https://docs.groupdocs.com/signature/net/)
- [Termékoldal](https://products.groupdocs.com/signature/net/)
- [Blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [Támogatási fórum](https://forum.groupdocs.com/c/signature/13)
- [Ideiglenes engedély](https://purchase.groupdocs.com/temporary-license/)