---
title: Képaláírás törlése
linktitle: Képaláírás törlése
second_title: GroupDocs.Signature .NET API
description: Ismerje meg, hogyan törölhet képaláírásokat dokumentumokból a GroupDocs.Signature for .NET segítségével. Kövesse lépésenkénti útmutatónkat a hatékony aláíráskezeléshez.
weight: 14
url: /hu/net/delete-operations/delete-image-signature/
---
## Bevezetés
Ebben az oktatóanyagban azt vizsgáljuk meg, hogyan törölhetők képaláírások a dokumentumokból a GroupDocs.Signature for .NET segítségével. A GroupDocs.Signature egy hatékony könyvtár, amely lehetővé teszi a fejlesztők számára, hogy digitális aláírásokkal, bélyegzőkkel és űrlapmezőkkel dolgozzanak különféle dokumentumformátumokon belül.
## Előfeltételek
Mielőtt elkezdené, győződjön meg arról, hogy rendelkezik az alábbiakkal:
### 1. GroupDocs.Signature for .NET
 Töltse le és telepítse a GroupDocs.Signature for .NET alkalmazást a[weboldal](https://releases.groupdocs.com/signature/net/). Kövesse a dokumentációban található telepítési utasításokat.
### 2. .NET-keretrendszer
Győződjön meg arról, hogy a .NET-keretrendszer telepítve van a gépére.
## Névterek importálása
Helyezze be a szükséges névtereket a projektbe:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
Bontsuk le a képaláírások törlésének folyamatát több lépésre:
## 1. lépés: Határozza meg a fájl elérési útját
Először adja meg a bemeneti és a kimeneti dokumentum elérési útját az aláírás törlése után:
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteImage", fileName);
```
## 2. lépés: Másolja a forrásfájlt
 Mivel a`Delete`módszer ugyanazzal a dokumentummal működik, elengedhetetlen a forrásfájl másolása egy másik helyre:
```csharp
File.Copy(filePath, outputFilePath, true);
```
## 3. lépés: Az aláírási objektum inicializálása
 Hozzon létre egy példányt a`Signature` osztályt, és adja meg a kimeneti dokumentum elérési útját:
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // A kód ide kerül
}
```
## 4. lépés: Keressen képaláírásokat
Adja meg a keresési beállításokat és keressen képaláírásokat a dokumentumban:
```csharp
ImageSearchOptions options = new ImageSearchOptions();
List<ImageSignature> signatures = signature.Search<ImageSignature>(options);
```
## 5. lépés: Törölje a képaláírást
Ha a rendszer képaláírásokat talál, törölje az elsőt:
```csharp
if (signatures.Count > 0)
{
    ImageSignature imageSignature = signatures[0];
    bool result = signature.Delete(imageSignature);
    if (result)
    {
        Console.WriteLine($"Image signature at location {imageSignature.Left}x{imageSignature.Top} and Size {imageSignature.Size} was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature at location {imageSignature.Left}x{imageSignature.Top} and Size {imageSignature.Size} was not found!");
    }
}
```
## Következtetés
Ebben az oktatóanyagban megtanultuk, hogyan törölheti a képaláírásokat a dokumentumokból a GroupDocs.Signature for .NET segítségével. A lépésenkénti útmutató követésével a fejlesztők hatékonyan kezelhetik a digitális aláírásokat alkalmazásaikban.
## GYIK
### Törölhetek több képaláírást egy dokumentumból?
 Igen, módosíthatja a kódot úgy, hogy több képaláírást is töröljön, ha ismételgeti a kódot`signatures` lista.
### A GroupDocs.Signature a DOCX-en kívül más dokumentumformátumokat is támogat?
Igen, a GroupDocs.Signature a dokumentumformátumok széles skáláját támogatja, beleértve a PDF, PPT, XLS stb.
### Elérhető a GroupDocs.Signature for .NET próbaverziója?
 Igen, letölthet egy ingyenes próbaverziót a webhelyről[weboldal](https://releases.groupdocs.com/).
### Hogyan kaphatok támogatást a GroupDocs.Signature-hez?
 Meglátogathatja a[GroupDocs.Signature fórum](https://forum.groupdocs.com/c/signature/13) segítségért és támogatásért.
### Vásárolhatok ideiglenes licencet a GroupDocs.Signature számára?
 Igen, vásárolhat ideiglenes licencet a[vásárlási oldal](https://purchase.groupdocs.com/temporary-license/).