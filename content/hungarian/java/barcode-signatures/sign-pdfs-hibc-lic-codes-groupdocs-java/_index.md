---
categories:
- Document Signing
- Healthcare Integration
date: '2026-05-16'
description: Ismerje meg, hogyan hozhat létre Data Matrix PDF-et, és adhat hozzá QR
  code PDF-et a GroupDocs.Signature for Java segítségével. Lépésről‑lépésre útmutató
  az egészségügyi dokumentumok aláírásához.
keywords:
- create data matrix pdf
- add qr code pdf
- HIBC barcode Java
lastmod: '2026-05-16'
linktitle: HIBC PDF aláírás Java útmutató
schemas:
- author: GroupDocs
  dateModified: '2026-05-16'
  description: Learn how to create data matrix PDF and add QR code PDF using GroupDocs.Signature
    for Java. Step‑by‑step guide for healthcare document signing.
  headline: Create Data Matrix PDF with HIBC Barcode in Java
  type: TechArticle
- description: Learn how to create data matrix PDF and add QR code PDF using GroupDocs.Signature
    for Java. Step‑by‑step guide for healthcare document signing.
  name: Create Data Matrix PDF with HIBC Barcode in Java
  steps:
  - name: '**Import the required classes** – these give you access to the signature
      engine and Data Matrix options.'
    text: '**Import the required classes** – these give you access to the signature
      engine and Data Matrix options.'
  - name: '**Instantiate the `Signature` object** with absolute paths for source and
      destination files.'
    text: '**Instantiate the `Signature` object** with absolute paths for source and
      destination files.'
  - name: '**Configure the Data Matrix options** – set the HIBC string, choose `QrCodeTypes.HIBCLICDataMatrix`,
      and define placement coordinates. `QrCodeTypes` enumerates the supported barcode
      formats for HIBC signatures.'
    text: '**Configure the Data Matrix options** – set the HIBC string, choose `QrCodeTypes.HIBCLICDataMatrix`,
      and define placement coordinates. `QrCodeTypes` enumerates the supported barcode
      formats for HIBC signatures.'
  - name: '**Apply the signature** to the PDF.'
    text: '**Apply the signature** to the PDF.'
  - name: '**Dispose of resources** to free file handles and avoid memory leaks.'
    text: '**Dispose of resources** to free file handles and avoid memory leaks.'
  - name: '**Import QR‑specific classes**'
    text: '**Import QR‑specific classes**'
  - name: '**Create and configure QR options** – note the use of `QrCodeTypes.HIBCLICQR`.'
    text: '**Create and configure QR options** – note the use of `QrCodeTypes.HIBCLICQR`.'
  - name: '**Sign the document**'
    text: '**Sign the document**'
  type: HowTo
- questions:
  - answer: Yes, it also supports DOCX, XLSX, PPTX, PNG, JPEG, and TIFF with the same
      barcode‑signing API.
    question: Can GroupDocs.Signature sign file types other than PDF?
  - answer: Verify that your HIBC string follows the exact HIBCC syntax, use the online
      validator, and ensure you’re using the correct `QrCodeTypes` constant for the
      chosen format.
    question: How do I troubleshoot “Invalid barcode content” errors?
  - answer: QR ≈ 4,296 alphanumeric characters, Aztec ≈ 3,832 numeric / 3,067 alphanumeric,
      Data Matrix ≈ 3,116 numeric / 2,335 alphanumeric. Keep codes under 200 characters
      for optimal scan reliability.
    question: What is the maximum data capacity for each HIBC format?
  - answer: Absolutely. Create separate `QrCodeSignOptions` objects with different
      positions and call `signature.sign()` for each. Just ensure they don’t overlap.
    question: Is it possible to embed multiple barcode types in one PDF?
  - answer: No. After the JAR is on the classpath and the license is activated, all
      operations are performed locally.
    question: Do I need an internet connection for signing at runtime?
  type: FAQPage
tags:
- java
- pdf-signing
- hibc
- healthcare
- barcode
- pharmaceutical
title: Data Matrix PDF létrehozása HIBC Barcode használatával Java-ban
type: docs
url: /hu/java/barcode-signatures/sign-pdfs-hibc-lic-codes-groupdocs-java/
weight: 1
---

# Data Matrix PDF létrehozása HIBC vonalkóddal Java-ban

Ha gyógyszeripari vagy egészségügyi logisztikai szoftvert fejlesztesz, valószínűleg már szembesültél a papír alapú nyomon követés, elveszett aláírások és audit rémtámák problémáival. **Data Matrix PDF létrehozása**, amely HIBC LIC vonalkódot ágyaz be, megoldja ezeket a problémákat azáltal, hogy egy manipulációra érzékeny, géppel olvasható nyomot biztosít, amely túlél a nyomtatást, szkennelést és a szabályozói felülvizsgálatot. Ebben az útmutatóban pontosan megmutatjuk, hogyan **add hozzá a QR kód PDF** támogatást, valamint az Aztec és Data Matrix formátumokat a GroupDocs.Signature for Java használatával.

## Gyors válaszok
- **Melyik könyvtár kezeli a HIBC vonalkódokat Java-ban?** GroupDocs.Signature for Java.  
- **Melyik vonalkód formátum a legkisebb?** Data Matrix – ideális kis címkékhez.  
- **Hozzáadhatok mind QR, mind Data Matrix kódot ugyanahhoz a PDF-hez?** Igen, csak hozz létre külön `QrCodeSignOptions`-t.  
- **Szükség van internetkapcsolatra futásidőben?** Nem, a könyvtár teljesen offline működik a telepítés után.  
- **Melyik Java verzió ajánlott?** Java 11+ a termelési szintű teljesítményhez.

## Mi az a HIBC vonalkód PDF aláírás?
`Signature` osztály a GroupDocs.Signature for Java-ban PDF dokumentumot képvisel, és módszereket biztosít a HIBC vonalkódok digitális aláírásként történő beágyazásához. Egy PDF aláírásával HIBC vonalkóddal ellenőrizhető, manipulációra érzékeny rekordot hozol létre, amely a szállítási lánc bármely pontján szkennelhető.

## Miért használjunk egyszerre Data Matrix és QR kódokat?
A GroupDocs.Signature támogatja a **50+ bemeneti és kimeneti formátumot**, és képes több száz oldalas PDF-eket feldolgozni anélkül, hogy az egész fájlt a memóriába töltené. A Data Matrix használata sűrű, kis területű címkékhez és a QR a tágasabb dokumentumokhoz a legjobb egyensúlyt biztosítja az olvashatóság, az adatkapacitás (akár 4 296 karakter QR esetén) és a nyomtatási hely hatékonysága között.

## Előkövetelmények
- **JDK 11 vagy újabb** (Java 8 működik, de a Java 11+ ajánlott az optimális teljesítményhez).  
- **IDE**, például IntelliJ IDEA, Eclipse vagy VS Code Java kiegészítőkkel.  
- **Maven vagy Gradle** a függőségkezeléshez (példák alább).  
- **Minta PDF** (például `sample.pdf`) a megvalósítás teszteléséhez.  
- **Érvényes GroupDocs.Signature licenc** (ingyenes próba a fejlesztéshez, fizetett licenc a termeléshez).

## A GroupDocs.Signature beállítása Java-hoz

### Maven konfiguráció
Add the dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Gradle konfiguráció
Gradle projektekhez add ezt a `build.gradle`-hoz:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### Közvetlen letöltési lehetőség
A JAR fájlt közvetlenül letöltheted a [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) oldalról, és manuálisan hozzáadhatod a projekt osztályútvonalához. Ez a megközelítés jól működik korlátozott hálózati környezetben.

### Licenc beszerzése
Kérj ingyenes próba vagy ideiglenes licencet a GroupDocs-tól a vízjelek eltávolításához és az összes funkció feloldásához. A termelési telepítésekhez megvásárolt licenc szükséges.

### Alap inicializálás
A `Signature` osztály az összes aláírási művelet belépési pontja. Betölti a PDF-et, alkalmazza a vonalkódot, és kiírja az aláírt fájlt.

```java
import com.groupdocs.signature.Signature;

class InitializeSignature {
    public static void main(String[] args) {
        Signature signature = new Signature("sample.pdf");
        // Proceed with signing operations...
    }
}
```

## Hogyan hozzunk létre Data Matrix PDF-et HIBC vonalkóddal?
Töltsd be a forrás PDF-et, konfigurálj egy `QrCodeSignOptions` objektumot a Data Matrix formátumhoz, és hívd meg a `sign()`‑t – ennyi szükséges a megfelelő HIBC Data Matrix vonalkód beágyazásához. A következő lépések pontosan végigvezetnek a szükséges kódon. A `QrCodeSignOptions` határozza meg a vonalkód aláírás beállításait, például a típust, a tartalmat, a méretet és a pozíciót.

1. **Importáld a szükséges osztályokat** – ezek biztosítják a hozzáférést az aláírási motorhoz és a Data Matrix beállításokhoz.  

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
```

2. **Példányosítsd a `Signature` objektumot** abszolút útvonalakkal a forrás és a cél fájlokhoz.  

```java
String sourceFilePath = "YOUR_DOCUMENT_DIRECTORY";
String destinFilePath = "YOUR_OUTPUT_DIRECTORY/SignWithHIBCLICQR.pdf";

final Signature signature = new Signature(sourceFilePath);
```

3. **Konfiguráld a Data Matrix beállításokat** – állítsd be a HIBC karakterláncot, válaszd a `QrCodeTypes.HIBCLICDataMatrix`‑t, és definiáld a elhelyezési koordinátákat. A `QrCodeTypes` felsorolja a HIBC aláírásokhoz támogatott vonalkód formátumokat.  

```java
QrCodeSignOptions hibcLic_QR = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICQR);
hibcLic_QR.setLeft(1); // Set the position from left
hibcLic_QR.setTop(1);   // Set the position from top
hibcLic_QR.setReturnContent(true); // Return content after signing
hibcLic_QR.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

4. **Alkalmazd az aláírást** a PDF-re.  

```java
signature.sign(destinFilePath, hibcLic_QR);
```

5. **Szabadítsd fel az erőforrásokat** a fájlkezelők és a memória szivárgások elkerülése érdekében.  

```java
finally {
    if (signature != null) signature.dispose();
}
```

### Teljes működő példa
Itt a teljes folyamat egyetlen blokkban (a helyőrzők a korábbi részletekből másolt pontos kódot jelölik):

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;

public class HibcQrSigning {
    public static void main(String[] args) {
        String sourceFilePath = "sample.pdf";
        String destinFilePath = "output/SignWithHIBCLICQR.pdf";
        
        Signature signature = null;
        try {
            signature = new Signature(sourceFilePath);
            
            QrCodeSignOptions hibcLic_QR = new QrCodeSignOptions(
                "A123PROD30917/75#422011907#GP293", 
                QrCodeTypes.HIBCLICQR
            );
            hibcLic_QR.setLeft(1);
            hibcLic_QR.setTop(1);
            hibcLic_QR.setReturnContent(true);
            hibcLic_QR.setReturnContentType(FileType.PNG);
            
            signature.sign(destinFilePath, hibcLic_QR);
            System.out.println("PDF signed successfully with HIBC QR code");
            
        } catch (Exception e) {
            System.err.println("Error signing PDF: " + e.getMessage());
            e.printStackTrace();
        } finally {
            if (signature != null) signature.dispose();
        }
    }
}
```

#### Közvetlen válasz (40–70 szó)
A **Data Matrix PDF létrehozásához** példányosítsd a `Signature`‑t a forrás PDF‑eddel, állítsd be a `QrCodeSignOptions`‑t `QrCodeTypes.HIBCLICDataMatrix`‑re, és adj meg egy helyesen formázott HIBC karakterláncot, majd hívd meg a `signature.sign(outputPath, options)`‑t. A könyvtár a aláírt PDF‑et a célhelyre írja, megőrizve a elrendezést és a vonalkódot manipulációra érzékeny aláírásként ágyazva be.

## Hogyan adjunk hozzá QR kód PDF-et a GroupDocs.Signature használatával?
Töltsd be a PDF-et, konfiguráld a `QrCodeSignOptions`‑t a QR formátumhoz, és hívd meg a `sign()`‑t. Ez a két soros minta bármilyen PDF méretnél működik, és automatikusan méretezi a QR képet az optimális olvashatóság érdekében. A `QrCodeSignOptions` beállítja a QR vonalkód aláírást, beleértve a tartalmát és a vizuális tulajdonságait. A kódot a megadott koordináták alapján helyezi el, biztosítva, hogy ne fedje át a meglévő tartalmat, és nyomtatás után is beolvasható maradjon.

1. **Importáld a QR‑specifikus osztályokat**  

```java
QrCodeSignOptions hibcLic_AZ = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICAztec);
hibcLic_AZ.setLeft(1); // Set the position from left
hibcLic_AZ.setTop(200); // Set the position from top
hibcLic_AZ.setReturnContent(true); // Return content after signing
hibcLic_AZ.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

2. **Hozd létre és konfiguráld a QR beállításokat** – vedd figyelembe a `QrCodeTypes.HIBCLICQR` használatát.  

```java
signature.sign(destinFilePath, hibcLic_AZ);
```

3. **Aláírd a dokumentumot**  

```java
QrCodeSignOptions hibcLic_DM = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICDataMatrix);
hibcLic_DM.setLeft(1); // Set the position from left
hibcLic_DM.setTop(400); // Set the position from top
hibcLic_DM.setReturnContent(true); // Return content after signing
hibcLic_DM.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

> **Közvetlen válasz:** Használd a `QrCodeTypes.HIBCLICQR`‑t a `QrCodeSignOptions`‑ban, állítsd be a HIBC tartalom karakterláncot, helyezd el a kódot a `setLeft()` és `setTop()`‑al, majd hívd meg a `signature.sign(outputPath, options)`‑t. A QR vonalkód azonnal beágyazódik, készen áll a okostelefon vagy szkenner általi olvasásra.

## Gyakori hibák, amelyeket kerüljünk

### 1. Erőforrások felszabadításának elfelejtése
**Helytelen:**  
```java
Signature signature = new Signature("sample.pdf");
signature.sign(destinFilePath, options);
// Oops, no dispose() call
```  
**Javítás:** Tedd a `Signature` használatát try‑with‑resources blokkba, vagy explicit módon hívd meg a `close()`‑t egy finally ágazatban.

### 2. Helytelen HIBC formátumú karakterláncok használata
**Helytelen:** Általános karakterláncok használata, mint például “12345”.  
**Javítás:** Kövesd a HIBCC szabványt (például `A123PROD30917/75#422011907#GP293`). Ellenőrizd a [HIBCC online validator](https://www.hibcc.org/) segítségével.

### 3. Fájlútvonalak hard‑kódolása
**Helytelen:**  
```java
String sourceFilePath = "C:/Users/John/Documents/test.pdf";
```  
**Javítás:** Tárold az útvonalakat egy konfigurációs fájlban vagy környezeti változóban, és olvasd be futásidőben.

### 4. A vonalkód pozícióütközések figyelmen kívül hagyása
Helyezd a vonalkódokat a meglévő szövegtől vagy aláírásoktól távol. Használj PDF koordinátákat (a kiindulópont bal alsó), és tesztelj egy nyomtatott mintával.

### 5. Valódi szkennerekkel való tesztelés hiánya
Nyomtasd ki az aláírt PDF-et, és szkenneld le a munkafolyamatodban használt pontos hardverrel. Ellenőrizd az olvashatóságot különböző nyomtatási minőségeknél.

## Gyakorlati alkalmazások az egészségügyben

| Forgatókönyv | Ajánlott vonalkód | Miért megfelelő |
|--------------|-------------------|------------------|
| **Gyógyszerelosztás** | QR Code | Nagy adatkapacitás, széles körben szkennelhető okostelefonokkal. |
| **Készletkezelés** | Data Matrix | Kis helyigény, ideális sűrű polc címkékhez. |
| **Szabályozási megfelelés (FDA 21 CFR Part 11)** | QR + Data Matrix | A kettős formátum redundanciát és auditálhatóságot biztosít. |
| **Orvosi eszköz nyomon követése** | Aztec Code | Kompakt méret működik a korlátozott helyű csomagoláson. |

## Teljesítménybeli megfontolások és legjobb gyakorlatok

### Kötetes feldolgozási minta
```java
List<String> filesToSign = getFileList();
for (String filePath : filesToSign) {
    Signature signature = null;
    try {
        signature = new Signature(filePath);
        // Sign and save
    } finally {
        if (signature != null) signature.dispose();
    }
}
```

- Hozz létre egy új `Signature` példányt fájlonként a memóriahasználat alacsonyan tartásához.  
- Használj fix szálkészletet (`Executors.newFixedThreadPool(Runtime.getRuntime().availableProcessors() - 1)`) a párhuzamos feldolgozáshoz, de figyeld a heap méretét, mivel minden `Signature` a teljes PDF-et a memóriában tartja.

### Könyvtárak naprakészen tartása
A GroupDocs kiadások a feldolgozási sebességet akár **20 %**‑kal is javítják, és új HIBC megfelelőségi funkciókat adnak hozzá. Ütemezz negyedéves függőség-ellenőrzéseket.

### Sablonok gyorsítótárazása
Tölts be egy PDF sablont egyszer, klónozd minden vonalkód változathoz, és írd alá a klónokat. Ez csökkenti az I/O-t és felgyorsítja a nagy mennyiségű munkafolyamatokat.

## Gyakran feltett kérdések

**Q: Alá tudja-e írni a GroupDocs.Signature a PDF-en kívül más fájltípusokat?**  
A: Igen, támogatja a DOCX, XLSX, PPTX, PNG, JPEG és TIFF formátumokat is ugyanazzal a vonalkód‑aláírási API‑val.

**Q: Hogyan háríthatom el a “Invalid barcode content” hibákat?**  
A: Ellenőrizd, hogy a HIBC karakterláncod pontosan követi-e a HIBCC szintaxist, használd az online validátort, és győződj meg róla, hogy a megfelelő `QrCodeTypes` konstans van használatban a választott formátumhoz.

**Q: Mi a maximális adatkapacitás minden HIBC formátum esetén?**  
A: QR ≈ 4 296 alfanumerikus karakter, Aztec ≈ 3 832 numerikus / 3 067 alfanumerikus, Data Matrix ≈ 3 116 numerikus / 2 335 alfanumerikus. A megbízható beolvasás érdekében tartsd a kódokat 200 karakter alatt.

**Q: Lehet-e egy PDF-be több vonalkód típust beágyazni?**  
A: Teljesen lehetséges. Hozz létre külön `QrCodeSignOptions` objektumokat különböző pozíciókkal, és minden egyeshez hívd meg a `signature.sign()`‑t. Csak ügyelj arra, hogy ne fedjék egymást.

**Q: Szükség van internetkapcsolatra aláíráskor futásidőben?**  
A: Nem. Miután a JAR a classpath‑on van és a licenc aktiválva, minden művelet helyben, offline történik.

## További források

- [GroupDocs.Signature for Java Documentation](https://docs.groupdocs.com/signature/java/)  
- [API Reference Guide](https://reference.groupdocs.com/signature/java/)  
- [Latest Release Downloads](https://releases.groupdocs.com/signature/java/)  
- [Purchase License](https://purchase.groupdocs.com/buy)  
- [Get Free Trial](https://releases.groupdocs.com/signature/java/)  
- [Request Temporary License](https://purchase.groupdocs.com/temporary-license/)  
- [GroupDocs Forum](https://forum.groupdocs.com/c/signature/)

---

**Utolsó frissítés:** 2026-05-16  
**Tesztelve ezzel:** GroupDocs.Signature 23.12 for Java  
**Szerző:** GroupDocs  

---

```java
signature.sign(destinFilePath, hibcLic_DM);
```

## Kapcsolódó oktatóanyagok

- [Create Barcode Signature PDF in Java – GroupDocs Guide](/signature/java/barcode-signatures/create-sign-pdfs-groupdocs-barcode-java/)  
- [Create Barcode Signature in Java – Update PDF Barcodes](/signature/java/barcode-signatures/java-groupdocs-signature-barcode-initialize-update/)  
- [How to read QR code PDF using Java and GroupDocs.Signature](/signature/java/barcode-signatures/java-pdf-barcode-search-groupdocs-signature-api/)