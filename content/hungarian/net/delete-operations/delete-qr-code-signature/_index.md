---
title: Törölje a QR-kód aláírását a dokumentumból
linktitle: Törölje a QR-kód aláírását a dokumentumból
second_title: GroupDocs.Signature .NET API
description: Ismerje meg, hogyan törölhet QR-kód aláírásokat dokumentumokból a GroupDocs.Signature for .NET segítségével. Kövesse lépésenkénti útmutatónkat a hatékony aláíráskezeléshez.
weight: 16
url: /hu/net/delete-operations/delete-qr-code-signature/
---
## Bevezetés
Ebben az oktatóanyagban végigvezetjük a QR-kód aláírásának a dokumentumból való eltávolításának folyamatán a GroupDocs.Signature for .NET segítségével. Kövesse ezeket a lépésenkénti utasításokat a QR-kód aláírások hatékony törléséhez.
## Előfeltételek
Mielőtt elkezdené, győződjön meg arról, hogy rendelkezik a következő előfeltételekkel:
-  GroupDocs.Signature for .NET: Győződjön meg arról, hogy a GroupDocs.Signature könyvtár telepítve van a .NET-projektben. Letöltheti innen[itt](https://releases.groupdocs.com/signature/net/).
- QR-kód aláírással ellátott dokumentum: Készítsen egy dokumentumot, amely QR-kód aláírásokat tartalmaz, amelyet törölni szeretne.
- C# alapismeretek: Ismerkedjen meg a C# programozási nyelv alapjaival.

## Névterek importálása
Mielőtt belemerülne a kódba, importálja a szükséges névtereket a C# fájlba:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## 1. lépés: Határozza meg a fájl elérési útját
```csharp
// A dokumentumok könyvtárának elérési útja.
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
// Határozza meg a módosított dokumentum kimeneti fájl elérési útját.
string outputFilePath = Path.Combine("Your Document Directory", "DeleteQRCode", fileName);
// Másolja a forrásfájlt, mivel a Törlés módszer ugyanazzal a dokumentummal működik.
File.Copy(filePath, outputFilePath, true);
```
## 2. lépés: Az aláírási objektum inicializálása
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // Hozzon létre lehetőségeket a QR-kód aláírások kereséséhez.
    QrCodeSearchOptions options = new QrCodeSearchOptions();
    // Keressen QR-kód aláírásokat a dokumentumban.
    List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(options);
```
## 3. lépés: Ellenőrizze a QR-kód aláírását
```csharp
    if (signatures.Count > 0)
    {
        // Szerezze meg a dokumentumban található első QR-kód aláírást.
        QrCodeSignature qrCodeSignature = signatures[0];
```
## 4. lépés: Törölje a QR-kód aláírását
```csharp
        // Törölje a QR-kód aláírását a dokumentumból.
        bool result = signature.Delete(qrCodeSignature);
        if (result)
        {
            Console.WriteLine($"Signature with QR-Code '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was deleted from document ['{fileName}'].");
        }
        else
        {
            Helper.WriteError($"Signature was not deleted from the document! Signature with Barcode '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was not found!");
        }
    }
}
```
Gratulálunk! Sikeresen eltávolította a QR-kód aláírását a dokumentumból a GroupDocs.Signature for .NET segítségével.

## Következtetés
Ebben az oktatóanyagban megtanultuk, hogyan lehet QR-kód aláírást törölni egy dokumentumból a GroupDocs.Signature for .NET segítségével. A megadott lépések követésével hatékonyan kezelheti és kezelheti az aláírásokat .NET-alkalmazásaiban.
## GYIK
### Törölhetek több QR-kód aláírást egy dokumentumból?
Igen, módosíthatja a kódot, hogy az összes QR-kód-aláíráson keresztül ismétlődjön, és ennek megfelelően törölje azokat.
### A GroupDocs.Signature támogatja a QR-kódokon kívül más típusú aláírásokat is?
Igen, a GroupDocs.Signature különféle aláírástípusokat támogat, például szöveget, képet, vonalkódot stb.
### A GroupDocs.Signature kompatibilis az összes dokumentumformátummal?
GroupDocs.Signature a dokumentumformátumok széles skáláját támogatja, beleértve a PDF, Microsoft Word, Excel, PowerPoint és egyebeket.
### Testreszabhatom az aláírások keresési beállításait?
Igen, igényei szerint testreszabhatja a keresési beállításokat, hogy megkeresse a dokumentumon belüli konkrét aláírásokat.
### Elérhető a GroupDocs.Signature próbaverziója?
 Igen, elérheti a GroupDocs.Signature ingyenes próbaverzióját innen[itt](https://releases.groupdocs.com/).