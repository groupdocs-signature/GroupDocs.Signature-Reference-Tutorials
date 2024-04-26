---
title: Aláírja a képet metaadatokkal
linktitle: Aláírja a képet metaadatokkal
second_title: GroupDocs.Signature .NET API
description: Ismerje meg, hogyan írhat alá képeket metaadatokkal a .NET-ben a GroupDocs.Signature használatával. Egyszerű, hatékony és testreszabható metaadat-aláírási megoldás.
type: docs
weight: 10
url: /hu/net/document-signing/sign-image-with-metadata/
---
## Bevezetés
A GroupDocs.Signature for .NET lehetővé teszi a fejlesztők számára, hogy hatékonyan írják alá a képeket metaadatokkal. Ez az oktatóanyag lépésről lépésre végigvezeti a folyamaton.
## Előfeltételek
Mielőtt elkezdené, győződjön meg arról, hogy rendelkezik a következőkkel:
1. GroupDocs.Signature for .NET: Telepítse a GroupDocs.Signature csomagot .NET-projektjébe. Letöltheti innen[itt](https://releases.groupdocs.com/signature/net/).   
2. Képfájl: Készítse elő a metaadatokkal aláírni kívánt képfájlt.

## Névterek importálása
Ügyeljen arra, hogy importálja a szükséges névtereket a C# kódban:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## 1. lépés: Töltse be a képfájlt
Először adja meg a képfájl elérési útját és a metaadatokkal aláírt kép kimeneti könyvtárát:
```csharp
string filePath = "sample.png";            
string outputFilePath = Path.Combine("Your Document Directory", "SignImageWithMetadata", "SignedWithMetadata.png");
```
## 2. lépés: Hozzon létre metaadat-aláírásokat
Ezután hozzon létre különböző metaadat-aláírásokat, és adja hozzá őket az opciók aláírásgyűjteményéhez:
```csharp
using (Signature signature = new Signature(filePath))
{
    ushort imgsMetadataId = 41996;
    MetadataSignOptions options = new MetadataSignOptions();
    options
        .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Scherlock Holmes")) // Karakterlánc értéke
        .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // Dátum Idő érték
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // Egész érték
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // Dupla érték
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // Tizedes érték
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // Lebegő érték
    
    // aláírja a dokumentumot a fájlba
    SignResult result = signature.Sign(outputFilePath, options);
    Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
}
```

## Következtetés
Ebben az oktatóanyagban megtanulta, hogyan írhat alá egy képet metaadatokkal a GroupDocs.Signature for .NET segítségével. Az alábbi lépések követésével könnyedén beépítheti a metaadat-aláírásokat .NET-alkalmazásaiba.

## GYIK
### Aláírhatok több képet metaadatokkal a GroupDocs.Signature for .NET segítségével?
Igen, több képet is aláírhat metaadatokkal az egyes képfájlok iterációjával és a metaadat-aláírások alkalmazásával.
### Elérhető a GroupDocs.Signature for .NET próbaverziója?
 Igen, letöltheti a próbaverziót innen[itt](https://releases.groupdocs.com/).
### A GroupDocs.Signature for .NET támogatja a képeken kívül más fájlformátumokat is?
Igen, a GroupDocs.Signature különféle fájlformátumokat támogat, beleértve a PDF, Word, Excel és egyebeket.
### Testreszabhatom a metaadat-aláírás megjelenését?
Igen, testreszabhatja a metaadat-aláírás megjelenését, például a betűméretet, a színt és a pozíciót.
### Hol kaphatok támogatást a GroupDocs.Signature for .NET-hez?
 Támogatást kaphat a GroupDocs.Signature fórumon[itt](https://forum.groupdocs.com/c/signature/13).