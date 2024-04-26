---
title: Több aláírás törlése a dokumentumból
linktitle: Több aláírás törlése a dokumentumból
second_title: GroupDocs.Signature .NET API
description: Könnyedén törölhet több aláírást a dokumentumokból a GroupDocs.Signature for .NET segítségével. Egyszerűsítse a dokumentumkezelési munkafolyamatot.
type: docs
weight: 15
url: /hu/net/delete-operations/delete-multiple-signatures/
---
## Bevezetés
A digitális világban a dokumentumkezelés gyakran magában foglalja a különféle aláírások kezelését. Több aláírás programozott törlése egy dokumentumból leegyszerűsítheti a munkafolyamatokat és növelheti a hatékonyságot. A GroupDocs.Signature for .NET segítségével ez a feladat zökkenőmentessé és egyszerűvé válik. Ez az oktatóanyag lépésről lépésre végigvezeti Önt a több aláírás törlésének folyamatán egy dokumentumból.
## Előfeltételek
Mielőtt belevágna az oktatóanyagba, győződjön meg arról, hogy rendelkezik a következő előfeltételekkel:
- A C# programozási nyelv alapvető ismerete.
- Telepített GroupDocs.Signature for .NET könyvtár.
- Mintadokumentum több aláírással teszteléshez.

## Névterek importálása
Kezdje a szükséges névterek importálásával a GroupDocs.Signature for .NET funkcióinak eléréséhez:
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## 1. lépés: Határozza meg a dokumentum elérési útját és fájlnevét
Állítsa be a több aláírást tartalmazó dokumentum fájl elérési útját. Győződjön meg arról, hogy rendelkezik a megfelelő fájl elérési úttal és fájlnévvel:
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
```
## 2. lépés: Másolja ki a dokumentumot feldolgozásra
Az eredeti dokumentum módosításának elkerülése érdekében hozzon létre egy másolatot feldolgozásra:
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "DeleteMultiple", fileName);
File.Copy(filePath, outputFilePath, true);
```
## 3. lépés: Az aláírási objektum inicializálása
Aláírási objektum példányosítása a kimeneti fájl elérési útjával:
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // Az aláírás-feldolgozási kód ide kerül
}
```
## 4. lépés: Adja meg a keresési beállításokat
Különféle keresési beállításokat határozhat meg a dokumentumon belüli aláírások azonosításához. A lehetőségek közé tartozik a szöveges keresés, a képkeresés, a vonalkódos keresés és a QR-kódos keresés:
```csharp
TextSearchOptions textSearchOptions = new TextSearchOptions();
ImageSearchOptions imageSearchOptions = new ImageSearchOptions();
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions();
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions();
// Beállítások hozzáadása a listához
List<SearchOptions> listOptions = new List<SearchOptions>();
listOptions.Add(textSearchOptions);
listOptions.Add(imageSearchOptions);
listOptions.Add(barcodeOptions);
listOptions.Add(qrCodeOptions);
```
## 5. lépés: Keressen aláírásokat
Hajtsa végre a keresési műveletet, hogy megtalálja az összes aláírást a dokumentumon belül a megadott keresési beállítások alapján:
```csharp
SearchResult result = signature.Search(listOptions);
```
## 6. lépés: Az aláírások törlése
Ha aláírásokat talál, folytassa azok törlésével:
```csharp
if (result.Signatures.Count > 0)
{
    // Próbálja meg törölni az összes aláírást
    DeleteResult deleteResult = signature.Delete(result.Signatures);
    //Ellenőrizze, hogy a törlés sikeres volt-e
    if(deleteResult.Succeeded.Count == result.Signatures.Count)
    {
        Console.WriteLine("\nAll signatures were successfully deleted!");                        
    }
    else
    {
        Console.WriteLine($"Successfully deleted signatures : {deleteResult.Succeeded.Count}");
        Helper.WriteError($"Not deleted signatures : {deleteResult.Failed.Count}");
    }
    // Információk megjelenítése a törölt aláírásokról
    Console.WriteLine("\nList of deleted signatures:");
    int number = 1;
    foreach(BaseSignature temp in deleteResult.Succeeded)
    {
        Console.WriteLine($"Signature #{number++}: Type: {temp.SignatureType} Id:{temp.SignatureId}, Location: {temp.Left}x{temp.Top}. Size: {temp.Width}x{temp.Height}");
    }
}
else
{
    Helper.WriteError("No one signature was found.");
}
```

## Következtetés
Több aláírás programozott törlése egy dokumentumból kulcsfontosságú feladat a dokumentumkezelésben. A GroupDocs.Signature for .NET segítségével ez a folyamat hatékony és megbízható lesz. Az oktatóanyagban ismertetett lépések követésével könnyedén integrálhatja az aláírástörlési funkciókat .NET-alkalmazásaiba.
## GYIK
### Kezelheti a GroupDocs.Signature for .NET különféle dokumentumformátumokat?
Igen, a GroupDocs.Signature for .NET a dokumentumformátumok széles skáláját támogatja, beleértve a DOCX, PDF, PPTX, XLSX és egyebeket.
### Lehetséges-e személyre szabni az aláírás-észlelés keresési beállításait?
A keresési lehetőségeket, például a szöveges keresést, a képkeresést, a vonalkódos keresést és a QR-kódos keresést teljesen az Ön egyedi igényei szerint alakíthatja.
### A GroupDocs.Signature for .NET biztosít hibakezelési mechanizmusokat?
Igen, a könyvtár robusztus hibakezelési képességeket kínál a dokumentumfeldolgozási feladatok zökkenőmentes végrehajtása érdekében.
### Integrálhatom a GroupDocs.Signature for .NET-et más, harmadik féltől származó könyvtárakkal?
A GroupDocs.Signature for .NET természetesen úgy lett kialakítva, hogy zökkenőmentesen integrálódjon más .NET-könyvtárakba, rugalmasságot és bővíthetőséget biztosítva.
### Hol találok további támogatást és erőforrásokat a GroupDocs.Signature for .NET számára?
 Látogassa meg a GroupDocs-t[fórum](https://forum.groupdocs.com/c/signature/13) elkötelezett az aláírással kapcsolatos megbeszéléseken, és kérjen segítséget a közösségtől és a szakértőktől.