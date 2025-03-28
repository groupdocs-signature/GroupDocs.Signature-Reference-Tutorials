---
title: Aláírás törlése azonosító alapján
linktitle: Aláírás törlése azonosító alapján
second_title: GroupDocs.Signature .NET API
description: Ismerje meg, hogyan törölhet aláírást azonosító alapján .NET-dokumentumokban a GroupDocs.Signature könyvtár használatával. Könnyű, lépésenkénti útmutató.
weight: 11
url: /hu/net/delete-operations/delete-signature-by-id/
---

# Aláírás törlése azonosító alapján

## Bevezetés
Ebben az oktatóanyagban megvizsgáljuk, hogyan törölhet aláírást az azonosítója alapján a GroupDocs.Signature for .NET segítségével. A GroupDocs.Signature for .NET egy hatékony könyvtár, amely lehetővé teszi a fejlesztők számára digitális aláírások hozzáadását, eltávolítását vagy ellenőrzését különféle dokumentumformátumokban .NET-alkalmazások segítségével.
## Előfeltételek
Mielőtt elkezdené, győződjön meg arról, hogy rendelkezik a következő előfeltételekkel:
1.  GroupDocs.Signature for .NET Library: Töltse le és telepítse a könyvtárat innen[itt](https://releases.groupdocs.com/signature/net/).
2. .NET-keretrendszer: Győződjön meg arról, hogy a .NET-keretrendszer telepítve van a rendszeren.
3. Dokumentum aláírással: Készítsen egy dokumentumot (pl. DOCX, PDF) olyan aláírással, amelyet törölni szeretne.

## Névterek importálása
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## 1. lépés: Határozza meg a fájl elérési útját
Először adja meg az aláírást tartalmazó dokumentum fájl elérési útját, és a kimeneti fájl elérési útját, ahová a módosított dokumentumot menti.
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteById", fileName);
```
## 2. lépés: Másolja ki a dokumentumot
 Mivel a`Delete` módszer módosítja a dokumentumot a helyén, a legjobb, ha másolatot készít az eredeti dokumentumról.
```csharp
File.Copy(filePath, outputFilePath, true);
```
## 3. lépés: Aláírás törlése azonosító alapján
 Inicializálja a`Signature` objektumot a dokumentumfájl elérési útjával, és használja a`Delete` módszer az aláírás eltávolítására az azonosítójával.
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    string id = @"eff64a14-dad9-47b0-88e5-2ee4e3604e71";
    bool result = signature.Delete(id);
    if (result)
    {
        Console.WriteLine($"Signature with Id# '{id}' was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature with id# '{id}' was not found!");
    }
}
```

## Következtetés
Ebben az oktatóanyagban megtanultuk, hogyan törölhet aláírást az azonosítója alapján a GroupDocs.Signature for .NET használatával. Ez a könyvtár kényelmes módot biztosít a különféle dokumentumformátumú digitális aláírások programozott kezelésére.
## GYIK
### Törölhetek több aláírást egyszerre?
 Igen, több aláírást is törölhet úgy, hogy ismételgeti az azonosítóikat, és meghívja a`Delete` módszer minden azonosítóhoz.
### A GroupDocs.Signature for .NET kompatibilis az összes dokumentumformátummal?
GroupDocs.Signature for .NET a dokumentumformátumok széles skáláját támogatja, beleértve a PDF, DOCX, XLSX és egyebeket.
### Testreszabhatom az aláírás megjelenését?
Igen, testreszabhatja az aláírás megjelenését, beleértve a helyzetét, méretét, betűtípusát és színét.
### Létezik próbaverzió?
 Igen, letölthet egy ingyenes próbaverziót a webhelyről[itt](https://releases.groupdocs.com/).
### Hol találok segítséget vagy támogatást a GroupDocs.Signature for .NET-hez?
 Látogassa meg a támogatási fórumot[itt](https://forum.groupdocs.com/c/signature/13) segítségért.