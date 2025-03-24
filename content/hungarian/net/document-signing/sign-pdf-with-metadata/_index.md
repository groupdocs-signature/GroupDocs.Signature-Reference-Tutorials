---
title: PDF aláírása metaadatokkal
linktitle: PDF aláírása metaadatokkal
second_title: GroupDocs.Signature .NET API
description: Ismerje meg, hogyan írhat alá PDF-dokumentumokat metaadatokkal a GroupDocs.Signature for .NET használatával. Egyszerűen javíthatja a dokumentumok nyomon követhetőségét és hitelességét.
weight: 11
url: /hu/net/document-signing/sign-pdf-with-metadata/
---
## Bevezetés
Ebből az oktatóanyagból megtudjuk, hogyan írhat alá egy PDF-dokumentumot metaadatokkal a GroupDocs.Signature for .NET használatával. Ha metaadatokat ad hozzá a PDF-hez, további információkkal szolgálhat a dokumentumról, például szerzőségről, létrehozási dátumról, dokumentumazonosítóról stb.
## Előfeltételek
Mielőtt elkezdené, győződjön meg arról, hogy rendelkezik a következőkkel:
1.  GroupDocs.Signature for .NET: Letöltheti innen[itt](https://releases.groupdocs.com/signature/net/).
2. PDF-dokumentum: Készítsen PDF-mintafájlt aláírásra.
3. C# programozási alapismeretek: A kódpéldák megértéséhez a C# szintaxis ismerete szükséges.
## Névterek importálása
Először győződjön meg arról, hogy importálja a szükséges névtereket a szükséges osztályok és metódusok eléréséhez:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## 1. lépés: Töltse be a PDF-dokumentumot
Töltse be az aláírni kívánt PDF dokumentumot:
```csharp
string filePath = "sample.pdf";
```
## 2. lépés: Adja meg a kimeneti fájl elérési útját
Határozza meg a kimeneti fájl elérési útját, ahová a metaadatokkal aláírt PDF mentésre kerül:
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignPdfWithMetadata", "SignedWithMetadata.pdf");
```
## 3. lépés: Hozzon létre aláírási példányt
Aláírás-példány inicializálása a PDF-dokumentum elérési útjának megadásával:
```csharp
using (Signature signature = new Signature(filePath))
{
    // Az aláírással kapcsolatos kód ide kerül
}
```
## 4. lépés: Határozza meg a metaadat-beállításokat
Hozzon létre MetadataSignOptions, és adjon hozzá metaadatmezőket a megfelelő értékekkel:
```csharp
MetadataSignOptions options = new MetadataSignOptions();
options
    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // Karakterlánc értéke
    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // DateTime értékek
    .Add(new PdfMetadataSignature("DocumentId", 123456))            // Egész érték
    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // Dupla érték
    .Add(new PdfMetadataSignature("Amount", 123.456M))              // Tizedes érték
    .Add(new PdfMetadataSignature("Total", 123.456F));              // Lebegő érték
```
## 5. lépés: Aláírja a dokumentumot
Aláírja a PDF-dokumentumot a megadott metaadat-beállításokkal, és mentse az aláírt dokumentumot:
```csharp
SignResult result = signature.Sign(outputFilePath, options);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## Következtetés
Ebben az oktatóanyagban bemutattuk, hogyan írhat alá egy PDF-dokumentumot metaadatokkal a GroupDocs.Signature for .NET használatával. A lépésenkénti útmutatót követve könnyedén hozzáadhat metaadat-információkat, például szerzőséget, létrehozási dátumot és egyebeket PDF-fájljaihoz, javítva azok hasznosságát és nyomon követhetőségét.
## GYIK
### Hozzáadhatok egyéni metaadatmezőket PDF-dokumentumaimhoz?
Igen, hozzáadhat egyéni metaadatmezőket a mező nevének és a hozzá tartozó értéknek a GroupDocs.Signature for .NET segítségével történő megadásával.
### A GroupDocs.Signature for .NET kompatibilis a .NET Framework összes verziójával?
A GroupDocs.Signature for .NET kompatibilis a .NET-keretrendszer különféle verzióival, rugalmasságot és egyszerű integrációt biztosítva.
### A GroupDocs.Signature támogatja a PDF-en kívül más dokumentumformátumok aláírását is?
Igen, a GroupDocs.Signature a dokumentumformátumok széles skáláját támogatja, beleértve a Word, Excel, PowerPoint és egyebeket.
### Aláírhatok több dokumentumot tömegesen a GroupDocs.Signature for .NET használatával?
Igen, több dokumentumot is aláírhat tömegesen, ha végignézi a fájllistát, és programozottan alkalmazza az aláírási folyamatot.
### Elérhető technikai támogatás a GroupDocs.Signature felhasználók számára?
 Igen, a GroupDocs dedikált technikai támogatást nyújt fórumain keresztül. Hozzáférhet a támogatási fórumhoz[itt](https://forum.groupdocs.com/c/signature/13).