---
"description": "Ismerje meg, hogyan írhat alá és ágyazhat be metaadatokat képekbe a GroupDocs.Signature for .NET segítségével. Adjon hozzá szerzői információkat, időbélyegeket és egyéni adatokat a képek hitelességének és nyomon követhetőségének javítása érdekében."
"linktitle": "Kép aláírása metaadatokkal"
"second_title": "GroupDocs.Signature .NET API"
"title": "Képek aláírása metaadatokkal C# .NET-ben"
"url": "/hu/net/document-signing/sign-image-with-metadata/"
"weight": 10
type: docs
---
## Bevezetés

metaadatokkal ellátott digitális képaláírás egyre fontosabbá válik a hitelesség, a tulajdonjog és a nyomon követhetőség megállapítása szempontjából. A GroupDocs.Signature for .NET egy hatékony, mégis könnyen használható megoldást kínál metaadat-aláírások hozzáadására különféle képformátumokhoz. Ez az oktatóanyag végigvezeti Önt a képek metaadatokkal történő aláírásának teljes folyamatán C# használatával.

A metaadat-aláírások lehetővé teszik értékes információk, például szerzői adatok, létrehozási időbélyegek, egyedi azonosítók és egyebek közvetlen beágyazását a képfájlokba. Ezek az információk a képfájl részévé válnak, megbízható módszert biztosítva a kép hitelességének nyomon követésére és ellenőrzésére.

## Előfeltételek

Mielőtt folytatná ezt az oktatóanyagot, győződjön meg arról, hogy rendelkezik a következőkkel:

1. [GroupDocs.Signature .NET-hez](https://releases.groupdocs.com/signature/net/) - Töltse le és telepítse a könyvtárat
2. Fejlesztői környezet - Visual Studio vagy bármilyen kompatibilis IDE .NET támogatással
3. Képfájl – Minta képfájl támogatott formátumban (PNG, JPG, TIFF stb.)
4. Alapvető C# programozási ismeretek - Ismerkedés a C# programozási alapfogalmakkal

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

Adja meg a forráskép elérési útját és azt, hogy hová kell menteni az aláírt kimenetet:

```csharp
// Adja meg a forrásképfájl elérési útját
string filePath = "sample.png";

// Adja meg az aláírt kép kimeneti könyvtárát és fájlnevét
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignImageWithMetadata", "SignedWithMetadata.png");

// Győződjön meg arról, hogy a kimeneti könyvtár létezik
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## 2. lépés: Az aláírásobjektum inicializálása

Hozz létre egy példányt a Signature osztályból a forrásképfájloddal:

```csharp
using (Signature signature = new Signature(filePath))
{
    // A kód többi része ide fog kerülni
}
```

## 3. lépés: Metaadat-aláírások létrehozása és konfigurálása

Ezután határozza meg a képbe beágyazni kívánt metaadatokat. A GroupDocs.Signature a metaadatokhoz különféle adattípusokat támogat:

```csharp
// Metaadat-azonosító inicializálása (képformátum-specifikus)
ushort imgsMetadataId = 41996;

// Metaadat-beállítások objektum létrehozása
MetadataSignOptions options = new MetadataSignOptions();

// Különböző típusú metaadat-aláírások hozzáadása
options
    .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Sherlock Holmes"))  // Karakterlánc érték
    .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // Dátum/Idő érték
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // Egész érték
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // Dupla érték
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // Decimális érték
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // Lebegőpontos érték
```

## 4. lépés: A kép aláírása metaadatokkal

Alkalmazd a metaadat-aláírásokat a képre, és mentsd el az eredményt:

```csharp
// Írja alá a dokumentumot, és mentse el a kimeneti fájl elérési útjára
SignResult result = signature.Sign(outputFilePath, options);

// Sikeres üzenet megjelenítése
Console.WriteLine($"\nSource image signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed image saved at: {outputFilePath}");
```

## Teljes példa

Íme a teljes kódpélda, amely az összes lépést összefoglalja:

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
            // Fájlútvonalak megadása
            string filePath = "sample.png";            
            string outputFilePath = Path.Combine("Your Document Directory", "SignImageWithMetadata", "SignedWithMetadata.png");
            
            // Győződjön meg arról, hogy a kimeneti könyvtár létezik
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // Aláírja a képet metaadatokkal
            using (Signature signature = new Signature(filePath))
            {
                // Metaadat-azonosító inicializálása (képformátum-specifikus)
                ushort imgsMetadataId = 41996;
                
                // Metaadat-beállítások létrehozása
                MetadataSignOptions options = new MetadataSignOptions();
                
                // Különböző típusú metaadat-aláírások hozzáadása
                options
                    .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Sherlock Holmes")) // Karakterlánc érték
                    .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // Dátum/Idő érték
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // Egész érték
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // Dupla érték
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // Decimális érték
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // Lebegőpontos érték
                
                // Dokumentum aláírása és mentése fájlba
                SignResult result = signature.Sign(outputFilePath, options);
                
                // Eredmények megjelenítése
                Console.WriteLine($"\nSource image signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## Speciális metaadat-aláírási technikák

### Egyéni metaadatokkal való munka

Egyéni metaadatmezőket is létrehozhat adott azonosítókkal:

```csharp
// Egyéni metaadatok létrehozása adott azonosítóval
options.Add(new ImageMetadataSignature(42000, "CustomValue"));
```

### Metaadat-aláírások ellenőrzése

Aláírás után érdemes lehet ellenőrizni a metaadat-aláírásokat:

```csharp
// Ellenőrzési lehetőségek létrehozása
MetadataSearchOptions searchOptions = new MetadataSearchOptions();

// Metaadat-aláírások keresése
SearchResult result = signature.Search(searchOptions);

// Talált aláírások megjelenítése
Console.WriteLine($"Found {result.Signatures.Count} metadata signatures:");
foreach(var metadataSignature in result.Signatures)
{
    Console.WriteLine($"- {metadataSignature.Name}: {metadataSignature.Value}");
}
```

## Következtetés

Ebben az oktatóanyagban megtanulta, hogyan írhat alá metaadatokkal képeket a GroupDocs.Signature for .NET használatával. A metaadatok képekbe ágyazása kiváló módot kínál a képek hitelességének növelésére, fontos információk hozzáadására és a dokumentumkezelési munkafolyamatok javítására. A folyamat egyszerű, mégis hatékony, és lehetővé teszi a testreszabást az Ön egyedi igényei alapján.

A képfájlba ágyazott metaadatok különféle célokra használhatók, például szerzői jogvédelemre, a kép eredetének nyomon követésére, leíró információk hozzáadására és a digitális felügyeleti lánc létrehozására. Metaadat-aláírások bevezetésével biztosíthatja, hogy képei életciklusuk során megőrizzék integritásukat és hitelességüket.

## GYIK

### Hozzáadhatok metaadatokat a meglévő aláírt képekhez?

Igen, hozzáadhat további metaadatokat azokhoz a képekhez, amelyek már tartalmaznak metaadat-aláírásokat. A meglévő metaadatok megmaradnak, és az új metaadatok ennek megfelelően kerülnek hozzáadásra.

### Milyen képformátumok támogatottak a metaadat-aláíráshoz?

A GroupDocs.Signature for .NET támogatja a metaadat-aláírást különféle képformátumok esetén, beleértve a PNG, JPEG, TIFF, BMP, GIF és egyebeket. A teljes listát lásd a következőben: [hivatalos dokumentáció](https://docs.groupdocs.com/signature/net/).

### Lehetséges a képek metaadatainak titkosítása?

Igen, a GroupDocs.Signature lehetőséget biztosít a metaadatok titkosítására a fokozott biztonság érdekében. A könyvtár által biztosított titkosítási beállításokkal védheti a bizalmas metaadat-információkat.

### Programozottan ellenőrizhetem az aláírt képek hitelességét?

Teljesen. A GroupDocs.Signature ellenőrzési metódusaival ellenőrizheti a metaadat-aláírásokat és megerősítheti az aláírt képek hitelességét.

### Van fájlméret-korlátozás metaadatokkal ellátott képek aláírásakor?

Maga a könyvtár nem szab meg konkrét fájlméret-korlátozást, de a nagyon nagy fájlok több feldolgozási időt és memóriát igényelhetnek. Javasoljuk, hogy vegye figyelembe a rendszererőforrásokat, amikor rendkívül nagy képekkel dolgozik.

### Hogyan szerezhetek ideiglenes jogosítványt tesztelési célokra?

Szerezhetsz egy [ideiglenes engedély](https://purchase.groupdocs.com/temporary-license/) a GroupDocs.Signature tesztelésére vásárlás előtt.

### Hol találok további forrásokat és támogatást?

- [API-referencia](https://reference.groupdocs.com/signature/net/)
- [Letöltések](https://releases.groupdocs.com/signature/net/)
- [Példák](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [Dokumentáció](https://docs.groupdocs.com/signature/net/)
- [Termékoldal](https://products.groupdocs.com/signature/net/)
- [Blog](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [Támogatási fórum](https://forum.groupdocs.com/c/signature/13)