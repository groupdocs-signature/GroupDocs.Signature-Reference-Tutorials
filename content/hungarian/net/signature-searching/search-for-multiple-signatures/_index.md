---
title: Több aláírás keresése
linktitle: Több aláírás keresése
second_title: GroupDocs.Signature .NET API
description: Ismerje meg, hogyan kereshet több aláírást .NET-dokumentumokban a GroupDocs.Signature segítségével a hatékony dokumentumbiztonság és -integritás érdekében.
weight: 14
url: /hu/net/signature-searching/search-for-multiple-signatures/
---

# Több aláírás keresése

## Bevezetés
A GroupDocs.Signature for .NET egy hatékony könyvtár, amely lehetővé teszi a fejlesztők számára, hogy .NET-alkalmazásokkal különféle típusú aláírásokat adjanak hozzá, keressenek és távolítsanak el népszerű dokumentumformátumokban. Ebben az oktatóanyagban arra összpontosítunk, hogy egy dokumentumon belül több aláírást keressünk a GroupDocs.Signature for .NET használatával.
## Előfeltételek
Mielőtt elkezdené, győződjön meg arról, hogy rendelkezik a következő előfeltételekkel:
- A Visual Studio telepítve van a rendszerére.
- A C# programozási nyelv alapvető ismerete.
- GroupDocs.Signature for .NET könyvtár telepítve a projektben. Letöltheti innen[itt](https://releases.groupdocs.com/signature/net/).

## Névterek importálása
Először is importálnia kell a szükséges névtereket, hogy hozzáférjen a GroupDocs.Signature for .NET által biztosított osztályokhoz és metódusokhoz.
```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## 1. lépés: Töltse be a dokumentumot
Töltse be azt a dokumentumot, ahol több aláírást szeretne keresni. Győződjön meg arról, hogy a megfelelő fájl elérési utat adta meg.
```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // A kódod ide kerül
}
```
## 2. lépés: Adja meg a keresési beállításokat
Határozzon meg keresési beállításokat különféle típusú aláírásokhoz, például szöveges, digitális, vonalkódos, QR-kódhoz és metaadatokhoz. Megadhat keresési feltételeket, például szöveget, egyezési típust és keresést az összes oldalon.
```csharp
// Határozza meg a keresési beállításokat
TextSearchOptions textOptions = new TextSearchOptions()
{
    AllPages = true
};
DigitalSearchOptions digitalOptions = new DigitalSearchOptions()
{
    AllPages = true
};
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions()
{
    AllPages = true,
    Text = "123456",
    MatchType = TextMatchType.Exact
};
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions()
{
    AllPages = true,
    Text = "John",
    MatchType = TextMatchType.Contains
};
MetadataSearchOptions metadataOptions = new MetadataSearchOptions();
```
## 3. lépés: Keresési lehetőségek hozzáadása a listához
Adja hozzá a meghatározott keresési beállításokat egy listához.
```csharp
// Beállítások hozzáadása a listához
List<SearchOptions> listOptions = new List<SearchOptions>();
listOptions.Add(textOptions);
listOptions.Add(barcodeOptions);
listOptions.Add(qrCodeOptions);
listOptions.Add(metadataOptions);
listOptions.Add(digitalOptions);
```
## 4. lépés: Aláírások keresése
Aláírások keresése a dokumentumban a megadott keresési beállításokkal.
```csharp
// Aláírások keresése a dokumentumban
SearchResult result = signature.Search(listOptions);
if (result.Signatures.Count > 0)
{
    Console.WriteLine($"\nSource document ['{filePath}'] contains following signatures.");
    foreach (var resSignature in result.Signatures)
    {
        Console.WriteLine($"Signature found at page {resSignature.PageNumber} with type {resSignature.SignatureType} and Id#: {resSignature.SignatureId}");
    }
}
else
{
    Helper.WriteError("No one signature was found.");
}
```

## Következtetés
Ebben az oktatóanyagban megtanultuk, hogyan kereshet több aláírást egy dokumentumon belül a GroupDocs.Signature for .NET használatával. A megadott lépések követésével hatékonyan megtalálhatja a különböző típusú aláírásokat a dokumentumokban, javítva a dokumentumok biztonságát és integritását.
## GYIK
### Kereshetek aláírásokat különböző dokumentumformátumokban?
Igen, a GroupDocs.Signature for .NET a dokumentumformátumok széles skáláját támogatja, beleértve a Word, PDF, Excel és egyebeket.
### Lehetséges-e személyre szabni az aláírások keresési feltételeit?
A keresési feltételeket teljesen az igényei szerint szabhatja, például pontos szövegegyezéseket adhat meg, vagy az összes oldalon kereshet.
### A GroupDocs.Signature for .NET támogatja a digitális aláírásokat?
Igen, kereshet digitális aláírásokra, valamint más típusokra, például szöveges, vonalkódos és QR-kódos aláírásokra.
### Könnyen integrálhatom az aláíráskereső funkciót .NET-alkalmazásaimba?
Igen, a GroupDocs.Signature for .NET egy egyszerű API-t biztosít, amely leegyszerűsíti az integrációs folyamatot.
### Hol találhatok további támogatást vagy segítséget?
 Látogassa meg a GroupDocs.Signature fórumot[itt](https://forum.groupdocs.com/c/signature/13) bármilyen kérdésért vagy segítségért.