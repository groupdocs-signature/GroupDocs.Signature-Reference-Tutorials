---
"description": "Tanulja meg, hogyan kereshet több aláírástípust dokumentumokban a GroupDocs.Signature for .NET segítségével. Átfogó útmutató kódpéldákkal a fokozott dokumentumbiztonság érdekében."
"linktitle": "Több aláírás keresése"
"second_title": "GroupDocs.Signature .NET API"
"title": "Több aláírástípus keresése dokumentumokban"
"url": "/hu/net/signature-searching/search-for-multiple-signatures/"
"weight": 14
type: docs
---
## Bevezetés

modern dokumentumkezelő rendszerekben egyre fontosabbá válik, hogy egyetlen dokumentumon belül több aláírástípus is kereshető és validálható legyen. A szervezetek gyakran alkalmaznak különféle aláírástípusokat – például digitális aláírásokat, szöveges aláírásokat, vonalkódokat, QR-kódokat és egyebeket – a dokumentumok biztonságának fokozása és az ellenőrzési folyamatok egyszerűsítése érdekében. A GroupDocs.Signature for .NET egy hatékony keretrendszert biztosít, amely lehetővé teszi a fejlesztők számára, hogy átfogó aláírás-keresési funkciókat valósítsanak meg különböző dokumentumformátumokban.

Ez az oktatóanyag részletes magyarázatokat és gyakorlati kódpéldákat kínál, és végigvezeti Önt a GroupDocs.Signature for .NET használatával történő dokumentumokon belüli több aláírástípus keresésének folyamatán.

## Előfeltételek

Mielőtt belevágna a több aláírás keresési funkciójának megvalósításába, győződjön meg arról, hogy a következő előfeltételek teljesülnek:

1. Fejlesztői környezet: Visual Studio vagy bármely, a rendszerére telepített előnyben részesített .NET fejlesztői környezet.
  
2. GroupDocs.Signature for .NET: Töltse le és telepítse a GroupDocs.Signature for .NET könyvtárat innen: [itt](https://releases.groupdocs.com/signature/net/).

3. C# alapismeretek: Jártasság a C# programozási nyelvben és a .NET keretrendszer koncepcióiban.

4. Mintadokumentumok: Készítsen tesztdokumentumokat, amelyek különféle típusú aláírásokat tartalmaznak tesztelési célokra.

## Névterek importálása

Kezdje a GroupDocs.Signature funkció eléréséhez szükséges névterek importálásával:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Most bontsuk le világos és könnyen kezelhető lépésekre a több aláírástípus keresésének folyamatát:

## 1. lépés: A dokumentum betöltése

Először töltse be a keresni kívánt aláírásokat tartalmazó dokumentumot:

```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // Többszörös aláírású keresési kód kerül ide hozzáadásra
}
```

## 2. lépés: Keresési beállítások meghatározása különböző aláírástípusokhoz

Hozzon létre keresési beállításokat minden egyes keresni kívánt aláírástípushoz:

```csharp
// Szöveges aláírások keresési beállításainak meghatározása
TextSearchOptions textOptions = new TextSearchOptions
{
    AllPages = true,  // Keresés az összes oldalon
    Text = "Signature",  // Opcionális: keresendő szöveg
    MatchType = TextMatchType.Contains  // Egyezési kritériumok
};

// Digitális aláírások keresési beállításainak meghatározása
DigitalSearchOptions digitalOptions = new DigitalSearchOptions
{
    AllPages = true
};

// Vonalkód-aláírások keresési beállításainak meghatározása
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions
{
    AllPages = true,
    Text = "123456",  // Opcionális: vonalkód szövegének egyeztetése
    MatchType = TextMatchType.Exact  // Egyezési kritériumok
};

// QR-kód aláírások keresési beállításainak meghatározása
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions
{
    AllPages = true,
    Text = "John",  // Opcionális: QR-kód szövegének egyeztetése
    MatchType = TextMatchType.Contains  // Egyezési kritériumok
};

// Metaadat-aláírások keresési beállításainak meghatározása
MetadataSearchOptions metadataOptions = new MetadataSearchOptions();
```

## 3. lépés: Opciók hozzáadása egy gyűjteményhez

Az összes keresési lehetőség hozzáadása egy gyűjteményhez:

```csharp
// Hozz létre egy listát az összes keresési lehetőséghez
List<SearchOptions> searchOptions = new List<SearchOptions>
{
    textOptions,
    digitalOptions,
    barcodeOptions,
    qrCodeOptions,
    metadataOptions
};
```

## 4. lépés: Keresés végrehajtása és az eredmények feldolgozása

Végezze el a keresést a kombinált keresési beállításokkal, és dolgozza fel az eredményeket:

```csharp
// Az összes aláírástípus keresése a megadott beállításokkal
SearchResult result = signature.Search(searchOptions);

// Ellenőrizze, hogy találtak-e aláírásokat
if (result.Signatures.Count > 0)
{
    Console.WriteLine($"\nSource document ['{filePath}'] contains {result.Signatures.Count} signature(s):");
    
    // Ismételje át a talált aláírásokat
    foreach (var foundSignature in result.Signatures)
    {
        Console.WriteLine($"Signature found: Type: {foundSignature.SignatureType}, Page: {foundSignature.PageNumber}, ID: {foundSignature.SignatureId}");
        
        // Folyamatspecifikus aláírástípusok
        if (foundSignature is TextSignature textSignature)
        {
            Console.WriteLine($"Text: '{textSignature.Text}'");
        }
        else if (foundSignature is BarcodeSignature barcodeSignature)
        {
            Console.WriteLine($"Barcode Type: {barcodeSignature.EncodeType.TypeName}, Text: '{barcodeSignature.Text}'");
        }
        else if (foundSignature is QrCodeSignature qrCodeSignature)
        {
            Console.WriteLine($"QR Code Type: {qrCodeSignature.EncodeType.TypeName}, Text: '{qrCodeSignature.Text}'");
        }
        else if (foundSignature is DigitalSignature digitalSignature)
        {
            Console.WriteLine($"Certificate: {digitalSignature.Certificate?.SubjectName}, Valid: {digitalSignature.IsValid}");
        }
        else if (foundSignature is MetadataSignature metadataSignature)
        {
            Console.WriteLine($"Metadata: Name: {metadataSignature.Name}, Value: {metadataSignature.Value}");
        }
    }
}
else
{
    Console.WriteLine("No signatures were found in the document.");
}
```

## Teljes példa

Íme egy teljes, működő példa, amely bemutatja, hogyan kereshetünk több aláírástípust egy dokumentumban:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace MultiSignatureSearch
{
    class Program
    {
        static void Main(string[] args)
        {
            // Dokumentum elérési útja
            string filePath = "sample_multiple_signatures.docx";
            
            // Aláíráspéldány inicializálása
            using (Signature signature = new Signature(filePath))
            {
                try
                {
                    // Szöveges aláírások keresési beállításainak meghatározása
                    TextSearchOptions textOptions = new TextSearchOptions
                    {
                        AllPages = true,
                        MatchType = TextMatchType.Contains
                    };

                    // Digitális aláírások keresési beállításainak meghatározása
                    DigitalSearchOptions digitalOptions = new DigitalSearchOptions
                    {
                        AllPages = true
                    };

                    // Vonalkód-aláírások keresési beállításainak meghatározása
                    BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions
                    {
                        AllPages = true
                    };

                    // QR-kód aláírások keresési beállításainak meghatározása
                    QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions
                    {
                        AllPages = true
                    };

                    // Metaadat-aláírások keresési beállításainak meghatározása
                    MetadataSearchOptions metadataOptions = new MetadataSearchOptions();

                    // Hozz létre egy listát az összes keresési lehetőséghez
                    List<SearchOptions> searchOptions = new List<SearchOptions>
                    {
                        textOptions,
                        digitalOptions,
                        barcodeOptions,
                        qrCodeOptions,
                        metadataOptions
                    };

                    // Az összes aláírástípus keresése
                    SearchResult result = signature.Search(searchOptions);

                    // Ellenőrizze, hogy találtak-e aláírásokat
                    if (result.Signatures.Count > 0)
                    {
                        Console.WriteLine($"\nSource document ['{filePath}'] contains {result.Signatures.Count} signature(s):");
                        
                        // Eredmények feldolgozása aláírás típus szerint
                        foreach (var foundSignature in result.Signatures)
                        {
                            Console.WriteLine($"Signature found: Type: {foundSignature.SignatureType}, Page: {foundSignature.PageNumber}");
                            
                            // Folyamatspecifikus aláírástípusok
                            switch (foundSignature.SignatureType)
                            {
                                case SignatureType.Text:
                                    var textSignature = foundSignature as TextSignature;
                                    Console.WriteLine($"Text: '{textSignature.Text}'");
                                    break;
                                    
                                case SignatureType.Barcode:
                                    var barcodeSignature = foundSignature as BarcodeSignature;
                                    Console.WriteLine($"Barcode Type: {barcodeSignature.EncodeType.TypeName}, Text: '{barcodeSignature.Text}'");
                                    break;
                                    
                                case SignatureType.QrCode:
                                    var qrCodeSignature = foundSignature as QrCodeSignature;
                                    Console.WriteLine($"QR Code Type: {qrCodeSignature.EncodeType.TypeName}, Text: '{qrCodeSignature.Text}'");
                                    break;
                                    
                                case SignatureType.Digital:
                                    var digitalSignature = foundSignature as DigitalSignature;
                                    Console.WriteLine($"Certificate: {digitalSignature.Certificate?.SubjectName}, Valid: {digitalSignature.IsValid}");
                                    break;
                                    
                                case SignatureType.Metadata:
                                    var metadataSignature = foundSignature as MetadataSignature;
                                    Console.WriteLine($"Metadata: Name: {metadataSignature.Name}, Value: {metadataSignature.Value}");
                                    break;
                            }
                            
                            Console.WriteLine(); // Sortörés hozzáadása az aláírások között
                        }
                    }
                    else
                    {
                        Console.WriteLine("No signatures were found in the document.");
                    }
                }
                catch (Exception ex)
                {
                    Console.WriteLine($"Error occurred: {ex.Message}");
                }
            }
            
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

## Fejlett többaláírásos keresési technikák

### Keresési eredmények szűrése

Speciális szűrést alkalmazhat a keresési eredmények szűkítéséhez:

```csharp
// Eredmények szűrése oldalszám szerint
var signaturesOnFirstPage = result.Signatures.FindAll(s => s.PageNumber == 1);

// Eredmények szűrése aláírás típusa szerint
var digitalSignatures = result.Signatures.FindAll(s => s.SignatureType == SignatureType.Digital);
var qrCodeSignatures = result.Signatures.FindAll(s => s.SignatureType == SignatureType.QrCode);

// Adott tartalmat tartalmazó szöveges aláírások szűrése
var approvalSignatures = result.Signatures
    .FindAll(s => s is TextSignature && ((TextSignature)s).Text.Contains("Approved"));
```

### Többszörös aláírások érvényesítése

Validációs logika megvalósítása különböző aláírás-típusokhoz:

```csharp
bool ValidateAllSignatures(SearchResult result)
{
    bool isDocumentValid = true;
    
    // Ellenőrizze, hogy a dokumentum rendelkezik-e érvényes digitális aláírással
    bool hasValidDigitalSignature = result.Signatures
        .Any(s => s is DigitalSignature && ((DigitalSignature)s).IsValid);
    
    if (!hasValidDigitalSignature)
    {
        Console.WriteLine("Warning: Document does not contain a valid digital signature");
        isDocumentValid = false;
    }
    
    // Ellenőrizze, hogy a dokumentumhoz tartozik-e QR-kód
    bool hasRequiredQRCode = result.Signatures
        .Any(s => s is QrCodeSignature && ((QrCodeSignature)s).Text.Contains("Auth-Code"));
    
    if (!hasRequiredQRCode)
    {
        Console.WriteLine("Warning: Document does not contain the required authentication QR code");
        isDocumentValid = false;
    }
    
    return isDocumentValid;
}
```

### Keresés egyéni feldolgozással

Egyéni feldolgozási logikát definiálhat a keresési műveletekhez:

```csharp
// Keresési beállítások létrehozása egyéni feldolgozással
TextSearchOptions textOptions = new TextSearchOptions
{
    AllPages = true,
    
    // Egyéni feldolgozás definiálása delegált használatával
    ProcessCompleted = (signature) =>
    {
        // Egyéni érvényesítési logika – csak a megadott oldalakon lévő aláírásokat fogadja el
        TextSignature textSignature = signature as TextSignature;
        return textSignature != null && (textSignature.PageNumber == 1 || textSignature.PageNumber == 2);
    }
};
```

## Következtetés

Ebben az átfogó útmutatóban azt vizsgáltuk meg, hogyan kereshet több aláírástípust dokumentumokon belül a GroupDocs.Signature for .NET segítségével. A különböző aláírástípusok keresési beállításainak beállításától az eredmények feldolgozásáig és validálásáig most már rendelkezik azzal a tudással, hogy robusztus aláírás-keresési funkciót valósítson meg .NET-alkalmazásaiban.

A több aláírástípus egyidejű keresésének képessége javítja a dokumentum-ellenőrzési folyamatokat, erősíti a biztonsági intézkedéseket és egyszerűsíti a dokumentum-érvényesítési munkafolyamatokat. A GroupDocs.Signature egy hatékony és rugalmas keretrendszert biztosít a különféle aláírástípusok kezeléséhez különböző dokumentumformátumokban, így kiváló választás dokumentumfeldolgozó alkalmazásokhoz.

## GYIK

### Kereshetek aláírásokat jelszóval védett dokumentumokban?

Igen, a GroupDocs.Signature támogatja az aláírások keresését jelszóval védett dokumentumokban. A jelszót megadhatja az inicializáláskor. `Signature` objektum:

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // Aláírások keresése
}
```

### Mely dokumentumformátumok támogatottak az aláíráskereséshez?

A GroupDocs.Signature számos dokumentumformátumot támogat, beleértve a PDF-et, a Microsoft Office dokumentumokat (Word, Excel, PowerPoint), az OpenOffice formátumokat, a képeket és egyebeket.

### Korlátozhatom a keresést egy dokumentum adott oldalaira?

Igen, minden keresési beállítástípus rendelkezik olyan tulajdonságokkal, amelyek lehetővé teszik a keresést végző oldalak megadását:

```csharp
TextSearchOptions options = new TextSearchOptions
{
    AllPages = false,  // Ne keressen az összes oldalon
    PageNumber = 1,    // Csak az 1. oldalon keres
    
    // Vagy adjon meg több oldalt
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } }
};
```

### Hogyan optimalizálhatom a teljesítményt nagy dokumentumokban való kereséskor?

Nagy dokumentumok esetén a teljesítményt a következőképpen optimalizálhatja:

1. A keresés korlátozása adott oldalakra vagy oldaltartományokra
2. Pontosabb keresési feltételek használata a lehetséges találatok számának csökkentése érdekében
3. Lapozás implementálása az eredmények megjelenítésében
4. Egyszerre egy aláírástípus keresése, ha nincs szüksége egyidejű eredményekre

### Kiterjeszthetek a GroupDocs.Signature-t, hogy támogassa az egyéni aláírástípusokat?

Bár a GroupDocs.Signature beépített támogatást nyújt a gyakori aláírástípusokhoz, a funkcionalitása a következőkkel bővíthető:

1. Egyéni keresési beállításosztályok létrehozása a következőből származtatva: `SearchOptions`
2. Egyéni feldolgozási logika megvalósítása a `ProcessCompleted` küldött
3. Többszörös aláírás-keresést fejlett üzleti logikával kombináló burkolóosztályok fejlesztése

## Lásd még

* [API-referencia](https://reference.groupdocs.com/signature/net/)
* [Kódpéldák a GitHubon](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Termékdokumentáció](https://docs.groupdocs.com/signature/net/)
* [Termékoldal](https://products.groupdocs.com/signature/net/)
* [Legújabb verzió letöltése](https://releases.groupdocs.com/signature/net/)
* [Blogcikkek](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Ingyenes Támogatási Fórum](https://forum.groupdocs.com/c/signature/13)
* [Ideiglenes engedély](https://purchase.groupdocs.com/temporary-license/)