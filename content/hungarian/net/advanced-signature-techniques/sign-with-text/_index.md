---
title: Aláírás szöveggel a GroupDocs.Signature for .NET használatával
linktitle: Aláírás szöveggel
second_title: GroupDocs.Signature .NET API
description: Ismerje meg, hogyan írhat alá dokumentumokat szöveggel a GroupDocs.Signature for .NET használatával. Lépésről lépésre szóló útmutató szöveges aláírások programozott hozzáadásához.
weight: 17
url: /hu/net/advanced-signature-techniques/sign-with-text/
---

# Aláírás szöveggel a GroupDocs.Signature for .NET használatával

## Bevezetés
A digitális korban a dokumentumok elektronikus aláírása általános gyakorlattá vált, ami időt és erőforrásokat takarít meg. A GroupDocs.Signature for .NET átfogó megoldást kínál szöveges aláírások programozott hozzáadására különböző dokumentumformátumokhoz. Ebben az oktatóanyagban végigvezetjük a dokumentum szöveges aláírásának folyamatán a GroupDocs.Signature for .NET használatával.
## Előfeltételek
Mielőtt belevágnánk az oktatóanyagba, győződjön meg arról, hogy rendelkezik a következő előfeltételekkel:
1.  GroupDocs.Signature for .NET: Győződjön meg arról, hogy telepítve van a GroupDocs.Signature for .NET könyvtár. Letöltheti innen[itt](https://releases.groupdocs.com/signature/net/).
2. Fejlesztési környezet: Készítsen munkakörnyezetet a .NET fejlesztéshez.
3. Dokumentum: Készítse elő a szöveggel aláírni kívánt dokumentumot (pl. PDF, Word).

## Névterek importálása
Először is importálnia kell a szükséges névtereket a .NET-projektbe a GroupDocs.Signature funkciók használatához.
```csharp
using System;
using System.IO;
using System.Drawing;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Bontsuk le a dokumentum szöveges aláírásának folyamatát több lépésre:
## 1. lépés: Töltse be a dokumentumot
Töltse be az aláírni kívánt dokumentumot szöveggel.
```csharp
string filePath = "sample.pdf"; // A dokumentum elérési útja
string fileName = Path.GetFileName(filePath);
```
## 2. lépés: Állítsa be a kimeneti fájl elérési útját
Határozza meg a kimeneti fájl elérési útját, ahová az aláírt dokumentum mentésre kerül.
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignWithText", fileName);
```
## 3. lépés: Aláírási beállítások létrehozása
Állítsa be a szöveges aláírás beállításait, beleértve a szöveg tartalmát, pozícióját, méretét, színét és betűtípusát.
```csharp
TextSignOptions options = new TextSignOptions("John Smith")
{
    Left = 50, // Állítsa be az aláírás pozícióját
    Top = 200,
    Width = 100, // Állítsa be az aláírási téglalapot
    Height = 30,
    ForeColor = Color.Red, // Állítsa be a szöveg színét
    Font = new SignatureFont { Size = 14, FamilyName = "Comic Sans MS" } // Betűtípus beállítása
};
```
## 4. lépés: Írja alá a dokumentumot
A GroupDocs.Signature használatával írja alá a dokumentumot a megadott beállításokkal, és mentse az aláírt dokumentumot a kimeneti fájl elérési útjára.
```csharp
using (Signature signature = new Signature(filePath))
{
    SignResult result = signature.Sign(outputFilePath, options); // Írja alá a dokumentumot
    Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
}
```

## Következtetés
Ebben az oktatóanyagban megtanultuk, hogyan írhat alá egy dokumentumot szöveggel a GroupDocs.Signature for .NET használatával. Ha követi ezeket a lépéseket, akkor hatékonyan adhat szöveges aláírásokat a dokumentumokhoz programozottan, növelve a biztonságot és a hitelességet.
## GYIK
### Testreszabhatom a szöveges aláírás megjelenését?
Igen, testreszabhatja a különböző paramétereket, például a színt, a betűtípust, a méretet és a szövegaláírás pozícióját saját igényei szerint.
### A GroupDocs.Signature kompatibilis több dokumentumformátummal?
Igen, a GroupDocs.Signature különféle dokumentumformátumokat támogat, beleértve a PDF, Word, Excel, PowerPoint és egyebeket.
### Hozzáadhatok több szöveges aláírást egyetlen dokumentumhoz?
Természetesen több szöveges aláírást is hozzáadhat egy dokumentumhoz, mindegyik saját testreszabási lehetőséggel.
### A GroupDocs.Signature biztosítja a dokumentum integritását az aláírás után?
Igen, a GroupDocs.Signature robusztus kriptográfiai algoritmusokat alkalmaz a dokumentumok sértetlenségének biztosítása és az aláírás utáni manipuláció megakadályozása érdekében.
### Vásárlás előtt kipróbálható-e próbaverzió?
 Igen, letölthet egy ingyenes próbaverziót a webhelyről[itt](https://releases.groupdocs.com/) hogy vásárlás előtt fedezze fel a funkciókat.