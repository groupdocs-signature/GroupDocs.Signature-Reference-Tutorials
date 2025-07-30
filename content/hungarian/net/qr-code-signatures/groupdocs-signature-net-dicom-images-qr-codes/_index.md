---
"date": "2025-05-07"
"description": "Ismerje meg, hogyan írhat alá DICOM képeket QR-kódokkal a GroupDocs.Signature for .NET használatával. Ez az útmutató a QR-kód aláírások beállítását, megvalósítását és ellenőrzését ismerteti az orvosi képalkotásban."
"title": "DICOM képek aláírása QR-kódokkal a GroupDocs.Signature for .NET használatával – Átfogó útmutató"
"url": "/hu/net/qr-code-signatures/groupdocs-signature-net-dicom-images-qr-codes/"
"weight": 1
---

# DICOM képek aláírása QR-kódokkal a GroupDocs.Signature for .NET használatával: Átfogó útmutató

Biztonságos módszert keres DICOM-fájljai hitelesítésére? Ez a részletes útmutató bemutatja, hogyan használhatja a GroupDocs.Signature for .NET-et QR-kód aláírások DICOM-képekbe integrálásához. Ideális egészségügyi szakemberek, fejlesztők és bárki számára, aki digitális orvosi dokumentumokkal dolgozik, ez az oktatóanyag a beállítástól a megvalósításig mindent lefed.

## Amit tanulni fogsz:
- Fejlesztői környezet beállítása a GroupDocs.Signature for .NET segítségével.
- Lépésről lépésre útmutató a DICOM képek QR-kódokkal történő aláírásához.
- Módszerek QR-kód aláírások ellenőrzésére és keresésére DICOM fájlokban.
- Technikák aláírt dokumentumok előnézetének létrehozására ellenőrzési célokra.
- Bevált gyakorlatok a teljesítmény optimalizálásához és az erőforrások hatékony kezeléséhez.

Kezdjük az előfeltételekkel!

## Előfeltételek

A GroupDocs.Signature for .NET használatához győződjön meg arról, hogy a környezete készen áll. Íme, amire szüksége lesz:

### Szükséges könyvtárak és verziók
- **GroupDocs.Signature .NET-hez**Győződjön meg a kompatibilitásról a .NET keretrendszerével.

### Környezeti beállítási követelmények
- Fejlesztői környezet Windows vagy Linux rendszeren.
- Visual Studio vagy más .NET-kompatibilis IDE telepítve.

### Ismereti előfeltételek
- C# programozás alapjainak ismerete.
- Jártasság a fájl I/O műveletekkel .NET alkalmazásokban.

## A GroupDocs.Signature beállítása .NET-hez

Telepítse a GroupDocs.Signature könyvtárat a kívánt módszerrel:

**.NET parancssori felület használata:**
```bash
dotnet add package GroupDocs.Signature
```

**Csomagkezelő:**
```powershell
Install-Package GroupDocs.Signature
```

**NuGet csomagkezelő felhasználói felület:**
- Keresd meg a „GroupDocs.Signature” fájlt, és telepítsd a legújabb verziót.

### Licencszerzés

Kezdj egy ingyenes próbaverzióval a funkciók felfedezéséhez. Hosszabb távú használat esetén érdemes lehet ideiglenes vagy teljes licencet vásárolni. [Csoportdokumentumok](https://purchase.groupdocs.com/buy).

A telepítés után inicializálja a könyvtárat:

```csharp
using GroupDocs.Signature;
// Inicializálja az Signature objektumot a DICOM fájl elérési útjával.
Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample.dicom");
```

## Megvalósítási útmutató

### DICOM kép aláírása QR-kóddal

#### Áttekintés
QR-kód aláírások hozzáadása az orvosi dokumentumok hitelességének és nyomon követhetőségének biztosítása érdekében.

**1. lépés: Aláírásobjektum inicializálása**

```csharp
string filePath = "YOUR_DOCUMENT_DIRECTORY\\sample.dicom";
using (Signature signature = new Signature(filePath))
{
    // Folytassa az aláírási műveleteket...
}
```

**2. lépés: QR-kód aláírási beállítások létrehozása**

Konfiguráljon olyan tulajdonságokat, mint a szöveg, a méret és az igazítás.

```csharp
QrCodeSignOptions options = new QrCodeSignOptions("Patient #36363393. R: No-Issues")
{
    AllPages = true,
    Width = 100,
    Height = 100,
    VerticalAlignment = VerticalAlignment.Bottom,
    HorizontalAlignment = HorizontalAlignment.Right,
    Margin = new Padding() { Right = 5, Left = 5 }
};
```

**3. lépés: XMP metaadatok hozzáadása**

További metaadatokkal gazdagíthatja a dokumentumot.

```csharp
DicomSaveOptions dicomSaveOptions = new DicomSaveOptions()
{
    XmpEntries = new List<DicomXmpEntry>() { new DicomXmpEntry(DicomXmpType.PatientName, "Patient #4") }
};
```

**4. lépés: A dokumentum aláírása**

Hajtsa végre az aláírást és mentse el.

```csharp
SignResult signResult = signature.Sign("YOUR_OUTPUT_DIRECTORY\\SignedDicom", options, dicomSaveOptions);
```

### Dokumentuminformációk lekérése

Metaadatok lekérése aláírt DICOM fájlokból az adatintegritás biztosítása érdekében.

**Áttekintés:**
Hozzáférés a dokumentuminformációkhoz és az XMP metaadat-aláírásokhoz ellenőrzés céljából.

**1. lépés: Dokumentuminformációk lekérése**

```csharp
using (Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample_signed.dicom"))
{
    IDocumentInfo signedDocumentInfo = signature.GetDocumentInfo();
}
```

**2. lépés: XMP adatok iterálása és nyomtatása**

Metaadatok részleteinek megjelenítése.

```csharp
foreach (var item in signedDocumentInfo.MetadataSignatures)
{
    Console.WriteLine(item.ToString());
}
```

### DICOM aláírások ellenőrzése

A DICOM képeken belüli QR-kód aláírások hitelességének ellenőrzése.

**Áttekintés:**
Győződjön meg arról, hogy az aláírások helyesek és hitelesek.

**1. lépés: QR-kód létrehozása Ellenőrzési beállítások**

A QR-kódokban található adott szövegnek megfelelő beállítások megadása.

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = true,
    Text = "Patient #36363393",
    MatchType = TextMatchType.Contains
};
```

**2. lépés: Aláírások ellenőrzése**

Ellenőrizd, hogy az aláírások megfelelnek-e a kritériumoknak.

```csharp
VerificationResult result = signature.Verify(options);

if (result.IsValid)
{
    Console.WriteLine($"DICOM {filePath} has {result.Succeeded.Count} successfully verified signatures!");
}
```

### Aláírások keresése DICOM-ban

QR-kód aláírások megkeresése az aláírt DICOM képeken.

**Áttekintés:**
Hatékonyan megtalálja az összes QR-kód aláírást a dokumentumok hitelességének kezelése érdekében.

**1. lépés: QR-kód aláírások keresése**

```csharp
List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
```

**2. lépés: Aláírás részleteinek ismétlése és nyomtatása**

Tekintse át az egyes talált aláírások részleteit.

```csharp
foreach (var QrCodeSignature in signatures)
{
    Console.WriteLine($"QRCode signature found at page {QrCodeSignature.PageNumber} with type {QrCodeSignature.EncodeType.TypeName} and text {QrCodeSignature.Text}");
}
```

### Aláírt DICOM előnézetének létrehozása

Vizuális előnézetek létrehozása az ellenőrzéshez.

**Áttekintés:**
Kép előnézetek generálása a tartalom ellenőrzéséhez speciális szoftver nélkül.

**1. lépés: Streammetódusok definiálása**

Fájlfolyam-kezelési metódusok beállítása az előnézet létrehozása során.

```csharp
Stream CreatePageStream(PreviewPageData pageData)
{
    string imageFilePath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignDicomImageAdvanced", $"preview-{pageData.PageNumber}.jpg");
    var folder = Path.GetDirectoryName(imageFilePath);
    if (!Directory.Exists(folder))
    {
        Directory.CreateDirectory(folder);
    }
    return new FileStream(imageFilePath, FileMode.Create);
}

void ReleasePageStream(PreviewPageData pageData, Stream pageStream)
{
    pageStream.Dispose();
}
```

**2. lépés: Előnézetek létrehozása**

Hajtsa végre az előnézeti verzió létrehozási folyamatát.

```csharp
using (Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample_signed.dicom"))
{
    PreviewOptions previewOption = new PreviewOptions(CreatePageStream, ReleasePageStream)
    {
        PreviewFormat = PreviewOptions.PreviewFormats.PNG,
    };

    signature.GeneratePreview(previewOption);
}
```

## Gyakorlati alkalmazások

1. **Orvosi nyilvántartás kezelése**A betegek adatainak hitelesítése QR-kódos aláírásokkal a megfelelőség érdekében.
2. **Auditnaplók az egészségügyi rendszerekben**: Dokumentummódosítások nyomon követése és hitelességének ellenőrzése QR-kódok segítségével.
3. **Biztonságos adatmegosztás**: Biztosítsa az orvosi képek biztonságos megosztását digitális aláírások beágyazásával.
4. **Megfelelőség-ellenőrzés**A DICOM fájlok integritását rendszeresen ellenőrizni kell a jogi követelményeknek való megfelelés érdekében.
5. **Integráció az elektronikus egészségügyi nyilvántartási rendszerekkel**Zökkenőmentesen integrálhatja az aláírt DICOM fájlokat az elektronikus egészségügyi nyilvántartási (EHR) rendszerekbe a gördülékenyebb működés érdekében.