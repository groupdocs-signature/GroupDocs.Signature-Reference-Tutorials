---
title: Aláírás több opcióval
linktitle: Aláírás több opcióval
second_title: GroupDocs.Signature .NET API
description: Ismerje meg, hogyan írhat alá dokumentumokat több lehetőséggel a GroupDocs.Signature for .NET használatával. Fokozza a dokumentumok biztonságát szöveggel, vonalkóddal, QR-kóddal, digitális és képpel.
type: docs
weight: 14
url: /hu/net/advanced-signature-techniques/sign-with-multiple-options/
---
## Bevezetés
Ebben az oktatóanyagban megvizsgáljuk, hogyan írhat alá egy dokumentumot több aláírási lehetőség használatával a .NET GroupDocs.Signature könyvtárával. A dokumentumok aláírása különféle lehetőségekkel, például szöveges, vonalkódos, QR-kódos, digitális, képi és metaadat-aláírásokkal sokoldalúságot biztosíthat és fokozhatja a dokumentumok biztonságát.
## Előfeltételek
Mielőtt elkezdené, győződjön meg arról, hogy rendelkezik a következő előfeltételekkel:
1.  GroupDocs.Signature for .NET Library: Töltse le és telepítse a GroupDocs.Signature for .NET könyvtárat innen:[itt](https://releases.groupdocs.com/signature/net/).
2. Fejlesztői környezet: Hozzon létre egy fejlesztői környezetet a .NET-keretrendszerrel.
3. Aláírandó dokumentum: Készítse elő az aláírni kívánt dokumentumot (pl. minta.docx).
4. Tanúsítványok és képek: Készítse elő a szükséges tanúsítványokat és képeket a digitális és képi aláírásokhoz.

## Névterek importálása
Először is importálja a szükséges névtereket a GroupDocs.Signature könyvtár használatához a .NET alkalmazásban:
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## 1. lépés: Töltse be a dokumentumot
```csharp
string filePath = "sample.docx";
string outputFilePath = Path.Combine("Your Document Directory", "SignWithMultiple", "SignWithMultiple.docx");
using (Signature signature = new Signature(filePath))
{
    // A kód folytatódik...
}
```
## 2. lépés: Adja meg az aláírási beállításokat
Határozzon meg több különböző típusú és beállítású aláírási lehetőséget, például szöveges, vonalkódos, QR-kódos, digitális, képi és metaadat-aláírásokat:
```csharp
TextSignOptions textOptions = new TextSignOptions("Text signature")
{
    VerticalAlignment = VerticalAlignment.Top,
    HorizontalAlignment = HorizontalAlignment.Left
};
BarcodeSignOptions barcodeOptions = new BarcodeSignOptions("123456")
{
    EncodeType = BarcodeTypes.Code128,
    Left = 0,
    Top = 150,
    Height = 50,
    Width = 200
};
// Egyéb aláírási lehetőségek meghatározása (pl. QR-kód, digitális, kép, metaadatok)...
```
## 3. lépés: Hozzon létre egy listát az aláírási lehetőségekről
Adja meg az aláírási lehetőségek listáját, amely tartalmazza az összes korábban meghatározott opciót:
```csharp
List<SignOptions> listOptions = new List<SignOptions>();
listOptions.Add(textOptions);
listOptions.Add(barcodeOptions);
// További aláírási lehetőségek hozzáadása a listához...
```
## 4. lépés: Aláírja a dokumentumot
Aláírja a dokumentumot az aláírási lehetőségek listájával, és mentse el az aláírt dokumentumot:
```csharp
SignResult result = signature.Sign(outputFilePath, listOptions);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## Következtetés
A dokumentumok több lehetőséggel történő aláírása a GroupDocs segítségével. A Signature for .NET robusztus megoldást kínál a dokumentumok biztonságának és sokoldalúságának fokozására. Az oktatóanyagban ismertetett lépések követésével zökkenőmentesen integrálhatja a különböző aláírástípusokat .NET-alkalmazásaiba.
## GYIK
### Használhatok egyéni képeket digitális aláíráshoz?
Igen, megadhat egyéni képeket digitális aláírásokhoz a GroupDocs.Signature könyvtár használatával.
### A GroupDocs.Signature kompatibilis a különböző dokumentumformátumokkal?
Igen, a GroupDocs.Signature különféle dokumentumformátumokat támogat, beleértve a DOCX, PDF, PPTX és egyebeket.
### Testreszabhatom a szöveges aláírások megjelenését?
Természetesen testreszabhatja a szöveges aláírások megjelenését, beleértve a betűméretet, a színt és a stílust.
### A GroupDocs.Signature biztosít titkosítást a digitális aláírásokhoz?
Igen, a GroupDocs.Signature titkosítási lehetőségeket kínál a digitális aláírásokhoz a dokumentumok biztonsága érdekében.
### Elérhető a GroupDocs.Signature for .NET próbaverziója?
 Igen, letöltheti a GroupDocs.Signature for .NET ingyenes próbaverzióját a webhelyről[itt](https://releases.groupdocs.com/).