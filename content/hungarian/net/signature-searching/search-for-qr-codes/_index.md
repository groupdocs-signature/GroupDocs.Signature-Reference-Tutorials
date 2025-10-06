---
"description": "Tanulja meg, hogyan kereshet hatékonyan QR-kódokat dokumentumokban a GroupDocs.Signature for .NET segítségével ezzel az átfogó, lépésről lépésre bemutató útmutatóval és kódpéldákkal."
"linktitle": "QR-kódok keresése"
"second_title": "GroupDocs.Signature .NET API"
"title": "QR-kód aláírások keresése dokumentumokban"
"url": "/hu/net/signature-searching/search-for-qr-codes/"
"weight": 15
type: docs
---
## Bevezetés

A mai digitális dokumentum-ökoszisztémában a QR-kód aláírások felbecsülhetetlen értékű eszközzé váltak az információk beágyazásához, a hitelesítéshez és a dokumentumok biztonságának fokozásához. A GroupDocs.Signature for .NET egy hatékony API-t biztosít a fejlesztők számára, amellyel QR-kódokat kereshetnek és kinyerhetnek különböző dokumentumformátumokból, lehetővé téve a fejlett dokumentumelemzési és -ellenőrzési képességeket a .NET alkalmazásokban.

Ez az átfogó oktatóanyag végigvezeti Önt a QR-kód keresési funkció GroupDocs.Signature for .NET használatával történő megvalósításának folyamatán, világos magyarázatokat, lépésről lépésre bemutatott utasításokat és gyakorlati kódpéldákat nyújtva, amelyeket integrálhat saját alkalmazásaiba.

## Előfeltételek

Mielőtt belevágna a QR-kód aláírás keresésébe, győződjön meg arról, hogy a következő előfeltételek teljesülnek:

1. GroupDocs.Signature for .NET SDK: Töltse le és telepítse az SDK-t a következő helyről: [letöltési oldal](https://releases.groupdocs.com/signature/net/).

2. Fejlesztői környezet: Állítson be egy .NET fejlesztői környezetet, például a Visual Studio-t, telepített .NET Framework vagy .NET Core rendszerrel.

3. Alapismeretek: Jártasság a C# programozásban és a .NET fejlesztési koncepciókban.

4. Mintadokumentumok: Készítsen QR-kódokat tartalmazó tesztdokumentumokat ellenőrzéshez és teszteléshez.

## Névterek importálása

Kezdje a GroupDocs.Signature funkció eléréséhez szükséges névterek importálásával:

```csharp
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
using System;
using System.Collections.Generic;
```

Most bontsuk le a QR-kódok keresésének folyamatát világos, könnyen követhető lépésekre:

## 1. lépés: A dokumentum elérési útjának meghatározása

Először adja meg a keresni kívánt QR-kódokat tartalmazó dokumentum elérési útját:

```csharp
string filePath = "sample_multiple_signatures.docx";
```

## 2. lépés: Az aláírásobjektum inicializálása

Hozz létre egy példányt a `Signature` osztály a dokumentum elérési útjának átadásával:

```csharp
using (Signature signature = new Signature(filePath))
{
    // QR-kód keresőkód kerül ide hozzáadásra
}
```

## 3. lépés: QR-kód aláírások keresése

Használd a `Search` metódus a megfelelő aláírástípussal QR-kódok kereséséhez a dokumentumban:

```csharp
// QR-kód aláírások keresése a dokumentumban
List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
```

## 4. lépés: Az eredmények feldolgozása és megjelenítése

Járja végig a megtalált QR-kód aláírásokat, és érje el a tulajdonságaikat:

```csharp
// Információk megjelenítése a talált QR-kódokról
Console.WriteLine($"\nSource document contains {signatures.Count} QR code signature(s):");

foreach (var qrCodeSignature in signatures)
{
    Console.WriteLine($"QR Code found at page {qrCodeSignature.PageNumber} with type {qrCodeSignature.EncodeType.TypeName}");
    Console.WriteLine($"Content: {qrCodeSignature.Text}");
    Console.WriteLine($"Location: X={qrCodeSignature.Left}, Y={qrCodeSignature.Top}, Width={qrCodeSignature.Width}, Height={qrCodeSignature.Height}");
    Console.WriteLine();
}
```

## Teljes példa

Íme egy átfogó működő példa, amely bemutatja a QR-kódok keresésének teljes folyamatát egy dokumentumban:

```csharp
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
using System;
using System.Collections.Generic;

namespace QrCodeSignatureSearch
{
    class Program
    {
        static void Main(string[] args)
        {
            // Dokumentum elérési útja – frissítse a fájl elérési útjával
            string filePath = "sample_multiple_signatures.docx";
            
            // Aláíráspéldány inicializálása
            using (Signature signature = new Signature(filePath))
            {
                try
                {
                    // QR-kód aláírások keresése a dokumentumban
                    List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
                    
                    // Keresési eredmények megjelenítése
                    Console.WriteLine($"\nSource document ['{filePath}'] contains {signatures.Count} QR code signature(s):");
                    
                    foreach (var qrCodeSignature in signatures)
                    {
                        Console.WriteLine($"QR Code found at page {qrCodeSignature.PageNumber} with type {qrCodeSignature.EncodeType.TypeName}");
                        Console.WriteLine($"Content: {qrCodeSignature.Text}");
                        Console.WriteLine($"Location: X={qrCodeSignature.Left}, Y={qrCodeSignature.Top}, Width={qrCodeSignature.Width}, Height={qrCodeSignature.Height}");
                        Console.WriteLine();
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

## Speciális QR-kód keresési technikák

### Keresés meghatározott feltételek alapján

Célzottabb keresésekhez használhatod a `QrCodeSearchOptions` a keresési feltételek testreszabásához:

```csharp
// QR-kód keresési beállítások létrehozása meghatározott feltételekkel
QrCodeSearchOptions options = new QrCodeSearchOptions
{
    // Csak adott oldalakon kereshet
    AllPages = false,
    PageNumber = 1,
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } },
    
    // Szűrés QR-kód tartalma alapján
    Text = "Invoice",
    MatchType = TextMatchType.Contains,
    
    // Szűrés adott QR-kód típusok szerint
    EncodeType = QrCodeTypes.QR,
    
    // Adjon meg egy adott területet a kereséshez
    Rectangle = new Rectangle(100, 100, 400, 400)
};

// Keresés adott beállításokkal
List<QrCodeSignature> filteredSignatures = signature.Search<QrCodeSignature>(options);
```

### QR-kód adatok feldolgozása

Az alkalmazás követelményei alapján egyéni QR-kód-adatok feldolgozását is megvalósíthatja:

```csharp
foreach (var qrCode in signatures)
{
    // QR-kód adatok kinyerése és feldolgozása tartalom alapján
    string qrContent = qrCode.Text;
    
    if (qrContent.StartsWith("URL:"))
    {
        // URL-adatok feldolgozása
        string url = qrContent.Substring(4);
        Console.WriteLine($"Found URL in QR code: {url}");
    }
    else if (qrContent.StartsWith("CONTACT:"))
    {
        // Kapcsolattartási adatok feldolgozása
        string contact = qrContent.Substring(8);
        Console.WriteLine($"Found contact information in QR code: {contact}");
    }
    else if (qrContent.StartsWith("INVOICE:"))
    {
        // Számlaadatok feldolgozása
        string invoiceData = qrContent.Substring(8);
        Console.WriteLine($"Found invoice information in QR code: {invoiceData}");
        
        // Számlaadatok elemzése és ellenőrzése
        if (ValidateInvoiceData(invoiceData))
        {
            Console.WriteLine("Invoice data is valid!");
        }
        else
        {
            Console.WriteLine("Warning: Invalid invoice data detected!");
        }
    }
}

// Példa validációs módszerre
static bool ValidateInvoiceData(string data)
{
    // Validációs logika megvalósítása
    return !string.IsNullOrEmpty(data) && data.Contains("ID") && data.Contains("Amount");
}
```

### Biztonsági ellenőrzés megvalósítása

A QR-kódokat gyakran használják hitelesítési célokra. Így valósíthatja meg az alapvető biztonsági ellenőrzést:

```csharp
// Ellenőrizze, hogy a dokumentum tartalmaz-e érvényes hitelesítési QR-kódot
bool hasValidAuthQrCode = false;

foreach (var qrCode in signatures)
{
    if (qrCode.Text.StartsWith("AUTH:"))
    {
        string authCode = qrCode.Text.Substring(5);
        
        // Hitelesítési kód ellenőrzése (pl. adatbázis vagy előre definiált lista alapján)
        if (VerifyAuthCode(authCode))
        {
            hasValidAuthQrCode = true;
            Console.WriteLine("Document contains valid authentication QR code!");
            break;
        }
    }
}

if (!hasValidAuthQrCode)
{
    Console.WriteLine("Warning: Document does not contain a valid authentication QR code!");
}

// Példa ellenőrzési módszerre
static bool VerifyAuthCode(string code)
{
    // Implementálja az ellenőrzési logikáját
    // Ez lehet adatbázis-keresés, API-hívás vagy összehasonlítás előre definiált értékekkel.
    return code == "A7B82C3D" || code == "X9Y8Z7W6";
}
```

### QR-kód képek kinyerése

QR-kód képeket kinyerhet dokumentumokból további feldolgozás vagy megjelenítés céljából:

```csharp
// QR-kód képek mentése lemezre
foreach (var qrCode in signatures)
{
    if (qrCode.Content != null)
    {
        // Hozzon létre egyedi fájlnevet az oldalszám és a pozíció alapján
        string outputPath = $"QrCode_P{qrCode.PageNumber}_X{qrCode.Left}_Y{qrCode.Top}.png";
        
        // Mentse el a képadatokat
        File.WriteAllBytes(outputPath, qrCode.Content);
        Console.WriteLine($"Saved QR code image to {outputPath}");
    }
}
```

## Következtetés

Ebben az átfogó útmutatóban azt vizsgáltuk meg, hogyan kereshet QR-kód aláírásokat dokumentumokban a GroupDocs.Signature for .NET segítségével. Az alapvető kereséstől a haladó technikákig most már rendelkezik azzal a tudással, hogy robusztus QR-kód kezelést valósítson meg .NET alkalmazásaiban. A GroupDocs.Signature API egy hatékony és rugalmas keretrendszert biztosít a különféle aláírástípusok, többek között a QR-kódok kezeléséhez különböző dokumentumformátumokban.

Ezen képességek kihasználásával javíthatja a dokumentum-ellenőrzési folyamatokat, hitelesítési rendszereket valósíthat meg, és kinyerheti a QR-kódokba ágyazott értékes információkat, mindezt a .NET-alkalmazásain belül.

## GYIK

### Milyen QR-kód formátumokat támogat a GroupDocs.Signature?

GroupDocs.Signature különféle QR-kód formátumokat támogat, beleértve a szabványos QR-kódot, a mikro QR-kódot és más elterjedt QR-kód szabványokat. Az adott formátum a következőn keresztül érhető el: `EncodeType` a tulajdona `QrCodeSignature` objektum.

### Kereshetek QR-kódokat jelszóval védett dokumentumokban?

Igen, a GroupDocs.Signature támogatja a QR-kódok keresését jelszóval védett dokumentumokban azáltal, hogy megadja a jelszót az inicializáláskor. `Signature` objektum:

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // QR-kódok keresése
}
```

### Hogyan szűrhetem a QR-kódokat a tartalmuk alapján?

A QR-kódokat tartalmuk alapján szűrheti a következővel: `Text` és `MatchType` tulajdonságai `QrCodeSearchOptions`:

```csharp
QrCodeSearchOptions options = new QrCodeSearchOptions
{
    Text = "Invoice",
    MatchType = TextMatchType.Contains // További lehetőségek: Pontos, Ezzel kezdődik, Ezzel végződik
};
```

### Képes a GroupDocs.Signature sérült vagy részben látható QR-kódokat észlelni?

A GroupDocs.Signature képes részben látható QR-kódok észlelésére, de a súlyosan sérült QR-kódokat esetleg nem ismeri fel. Az észlelés pontossága a QR-kód minőségétől és láthatóságától függ a dokumentumban.

### Milyen dokumentumformátumok támogatottak a QR-kód kereséshez?

A GroupDocs.Signature támogatja a QR-kód keresését különféle dokumentumformátumokban, beleértve a PDF-et, a Microsoft Office dokumentumokat (Word, Excel, PowerPoint), a képeket (JPEG, PNG, TIFF) és sok mást.

## Lásd még

* [API-referencia](https://reference.groupdocs.com/signature/net/)
* [Kódpéldák a GitHubon](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Termékdokumentáció](https://docs.groupdocs.com/signature/net/)
* [Termékoldal](https://products.groupdocs.com/signature/net/)
* [Legújabb verzió letöltése](https://releases.groupdocs.com/signature/net/)
* [Blogcikkek](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Ingyenes Támogatási Fórum](https://forum.groupdocs.com/c/signature/13)
* [Ideiglenes engedély](https://purchase.groupdocs.com/temporary-license/)