---
title: Dokumentuminformációk lekérése
linktitle: Dokumentuminformációk lekérése
second_title: GroupDocs.Signature .NET API
description: Javítsa a dokumentumkezelést a .NET-ben a GroupDocs.Signature segítségével. A dokumentumadatok lekérése lépésről lépésre. Különféle formátumokat támogat.
type: docs
weight: 11
url: /hu/net/document-preview-operations/retrieve-document-information/
---
## Bevezetés
A digitális dokumentáció területén a hitelesség és az integritás biztosítása a legfontosabb. A GroupDocs.Signature for .NET robusztus megoldást kínál a dokumentumok aláírásainak kezelésére a .NET környezetben. Ebben az oktatóanyagban a GroupDocs.Signature for .NET használatával történő dokumentuminformációk lekérésének folyamatát mutatjuk be, az egyes lépéseket lebontva az átfogó megértés érdekében.
## Előfeltételek
Mielőtt belevágna az oktatóanyagba, győződjön meg arról, hogy a következő előfeltételek teljesülnek:
1.  Telepítés: Telepítse a GroupDocs.Signature for .NET-et a webhelyről való letöltéssel[itt](https://releases.groupdocs.com/signature/net/).
2. .NET-környezet: rendelkezzen a .NET-keretrendszer gyakorlati ismereteivel.
3. Dokumentum: Készítsen mintadokumentumot (pl. "sample_multiple_signatures.docx") tesztelési célokra.

## Névterek importálása
Mielőtt folytatná a dokumentumaláírás-lekérési folyamatot, importálja a szükséges névtereket:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
```

## 1. lépés: Állítsa be a dokumentumfájl elérési útját:
Határozza meg annak a dokumentumnak a fájl elérési útját, amelyből információkat kíván lekérni.
```csharp
string filePath = "sample_multiple_signatures.docx";
```
## 2. lépés: Az aláírási objektum példányosítása:
 Hozzon létre egy példányt a`Signature` osztályt a dokumentumfájl elérési útjának átadásával.
```csharp
using (Signature signature = new Signature(filePath))
{

}
```
## 3. lépés: A dokumentum információinak lekérése:
 Használja ki a`GetDocumentInfo()` módszer átfogó információk lekérésére a dokumentumról.
```csharp
IDocumentInfo documentInfo = signature.GetDocumentInfo();
```
## 4. lépés: Jelenítse meg a dokumentum tulajdonságait:
Kiadja a dokumentum különféle tulajdonságait, például formátumot, kiterjesztést, méretet, oldalszámot stb.
```csharp
Console.WriteLine($"Document properties {Path.GetFileName(filePath)}:");
Console.WriteLine($" - format : {documentInfo.FileType.FileFormat}");
Console.WriteLine($" - extension : {documentInfo.FileType.Extension}");
Console.WriteLine($" - size : {documentInfo.Size}");
Console.WriteLine($" - page count : {documentInfo.PageCount}");
Console.WriteLine($" - Form Fields count : {documentInfo.FormFields.Count}");
Console.WriteLine($" - Text signatures count : {documentInfo.TextSignatures.Count}");
Console.WriteLine($" - Image signatures count : {documentInfo.ImageSignatures.Count}");
Console.WriteLine($" - Digital signatures count : {documentInfo.DigitalSignatures.Count}");
Console.WriteLine($" - Barcode signatures count : {documentInfo.BarcodeSignatures.Count}");
Console.WriteLine($" - QrCode signatures count : {documentInfo.QrCodeSignatures.Count}");
Console.WriteLine($" - FormField signatures count : {documentInfo.FormFieldSignatures.Count}");
foreach (PageInfo pageInfo in documentInfo.Pages)
{
   Console.WriteLine($" - page-{pageInfo.PageNumber} Width {pageInfo.Width}, Height {pageInfo.Height}");
}
```


## Következtetés
GroupDocs.Signature for .NET hatékony eszközcsomagot kínál a dokumentumok aláírásainak zökkenőmentes kezeléséhez a .NET keretrendszeren belül. Az ebben az útmutatóban ismertetett lépések követésével hatékonyan nyerhet le átfogó információkat a dokumentumokról, ami megkönnyíti a továbbfejlesztett dokumentumkezelési lehetőségeket.

## GYIK
### A GroupDocs.Signature for .NET kezelhet több dokumentumformátumot?
Igen, a GroupDocs.Signature a dokumentumformátumok széles skáláját támogatja, többek között, de nem kizárólagosan a DOCX, PDF, PNG és JPEG.
### Elérhető a GroupDocs.Signature for .NET próbaverziója?
 Igen, a próbaverziót innen érheti el[itt](https://releases.groupdocs.com/).
### A GroupDocs.Signature for .NET támogatja a digitális aláírásokat?
A GroupDocs.Signature határozottan támogatja a digitális aláírásokat, biztosítva a dokumentumok hitelességét és integritását.
### Hol találok további dokumentációt és támogatást a GroupDocs.Signature for .NET-hez?
 Olvassa el az átfogó dokumentációt[itt](https://reference.groupdocs.com/signature/net/) , támogatásért pedig látogassa meg a GroupDocs fórumot[itt](https://forum.groupdocs.com/c/signature/13).
### Kaphatók-e ideiglenes licencek a GroupDocs.Signature for .NET számára?
 Igen, az ideiglenes licencek megvásárolhatók[itt](https://purchase.groupdocs.com/temporary-license/).