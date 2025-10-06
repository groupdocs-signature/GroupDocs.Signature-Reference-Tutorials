---
"date": "2025-05-08"
"description": "Ismerje meg, hogyan védheti a kép metaadatait titkosítással a GroupDocs.Signature for Java segítségével. Lépésről lépésre útmutatóval biztosíthatja az adatok integritását és hitelességét."
"title": "Képmetaadatok aláírásának és titkosításának megvalósítása Java-ban a GroupDocs.Signature segítségével"
"url": "/hu/java/metadata-signatures/groupdocs-signature-java-image-metadata-encryption/"
"weight": 1
type: docs
---
# Kép metaadat-aláírás titkosítással megvalósítása Java-ban a GroupDocs.Signature használatával

## Bevezetés

A mai digitális környezetben a dokumentumok metaadataiban található bizalmas információk védelme kiemelkedő fontosságú. Akár bizalmas üzleti szerződésekről, akár személyazonosító fényképekről van szó, a képmetaadatok integritásának és hitelességének megőrzése segít megelőzni a jogosulatlan hozzáférést és manipulációt. **GroupDocs.Signature Java-hoz** robusztus megoldást kínál a kép metaadatainak biztonságos aláírására és titkosítására.

Ez az oktatóanyag bemutatja, hogyan valósíthat meg képmetaadatok aláírását titkosítással Java nyelven a GroupDocs.Signature hatékony funkcióinak használatával. A következő lépéseket követve hatékonyan integrálhatja ezt a funkciót Java alkalmazásaiba.

**Amit tanulni fogsz:**
- Dokumentum metaadatainak aláírása a GroupDocs.Signature for Java használatával
- Egyéni objektumaláírások megvalósítása titkosítással
- Biztonságos környezet létrehozása szimmetrikus kulcsú titkosítással

## Előfeltételek

Kezdés előtt győződjön meg arról, hogy a következő előfeltételek teljesülnek:

### Szükséges könyvtárak és függőségek:
- **GroupDocs.Signature Java-hoz**Győződjön meg róla, hogy a 23.12-es vagy újabb verzióval rendelkezik.

### Környezeti beállítási követelmények:
- Telepítsd a Java Development Kitet (JDK) a gépedre.
- Használjon integrált fejlesztői környezetet (IDE), például IntelliJ IDEA-t, Eclipse-t vagy NetBeans-t.

### Előfeltételek a tudáshoz:
- Java programozási alapismeretek.
- Maven vagy Gradle ismeretek függőségkezelés terén.

## GroupDocs.Signature beállítása Java-hoz

A GroupDocs.Signature projektben való használatához a következőképpen kell megadni a szükséges függőségeket:

### Maven használata
Add hozzá ezt a `pom.xml` fájl:
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Gradle használata
Vedd bele ezt a `build.gradle` fájl:
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### Közvetlen letöltés
Vagy töltse le a legújabb verziót innen: [GroupDocs.Signature Java kiadásokhoz](https://releases.groupdocs.com/signature/java/).

#### Licencbeszerzés lépései
- **Ingyenes próbaverzió**: Kezdje egy próbaverzióval a funkciók megismeréséhez.
- **Ideiglenes engedély**Szükség esetén kérjen átfogó vizsgálatot.
- **Vásárlás**: Szerezzen be egy licencet termelési célra a következőtől: [Csoportdokumentumok](https://purchase.groupdocs.com/buy).

## Alapvető inicializálás és beállítás

Így inicializálhatja a GroupDocs.Signature-t a Java alkalmazásában:

```java
import com.groupdocs.signature.Signature;

public class InitializeSignature {
    public static void main(String[] args) {
        // A dokumentum elérési útja
        String filePath = "path/to/your/document.jpg";
        
        // Hozzon létre egy új Signature-példányt
        Signature signature = new Signature(filePath);

        System.out.println("GroupDocs.Signature initialized successfully.");
    }
}
```

## Megvalósítási útmutató

### Funkció: Metaadat-aláírás egyéni objektummal

#### Áttekintés
Ez a funkció lehetővé teszi a kép metaadatainak aláírását egyéni objektum használatával, és titkosítását a fokozott biztonság érdekében, biztosítva, hogy csak a jogosult felek férhessenek hozzá a metaadatokhoz, vagy módosíthassák azokat.

#### Lépésről lépésre történő megvalósítás

##### 1. Határozza meg a dokumentum aláírási adatosztályát
Hozz létre egy osztályt a metaadataid tárolásához:

```java
import java.math.BigDecimal;
import java.util.Date;

class DocumentSignatureData {
    private String ID;
    private String Author;
    private Date Signed = new Date();
    private BigDecimal DataFactor = new BigDecimal(0.01);

    public String getID() { return ID; }
    public void setID(String value) { ID = value; }

    @FormatAttribute(propertyName = "SignID")
    public final String getAuthor() { return Author; }
    public final void setAuthor(String value) { Author = value; }

    @FormatAttribute(propertyName = "SAuth")
    public final Date getSigned() { return Signed; }
    public final void setSigned(Date value) { Signed = value; }

    @FormatAttribute(propertyName = "SDate", propertyFormat = "yyyy-MM-dd")
    public final BigDecimal getDataFactor() { return DataFactor; }
    public final void setDataFactor(BigDecimal value) { DataFactor = value; }
}
```

##### 2. Az aláírási logika megvalósítása
A metaadatok titkosítással történő aláírásának módja:

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;
import com.groupdocs.signature.domain.extensions.encryption.SymmetricAlgorithmType;
import com.groupdocs.signature.domain.extensions.encryption.SymmetricEncryption;
import com.groupdocs.signature.domain.signatures.metadata.ImageMetadataSignature;
import com.groupdocs.signature.exception.GroupDocsSignatureException;
import com.groupdocs.signature.options.sign.MetadataSignOptions;

import java.io.File;
import java.nio.file.Paths;
import java.util.UUID;

public class SignMetadataWithCustomObject {
    // Fájlútvonalak inicializálása helyőrzőkkel
    String filePath = "YOUR_DOCUMENT_DIRECTORY/SampleImage.jpg";
    String outputFilePath = new File("YOUR_OUTPUT_DIRECTORY", 
                                       "SignedImageWithCustomMetadata/SampleImage_signed.jpg").getPath();

    public void run() throws Exception {
        Signature signature = new Signature(filePath);

        // Titkosítási kulcs és jelszó beállítása
        String key = "1234567890";
        String salt = "1234567890";
        IDataEncryption encryption = new SymmetricEncryption(
            SymmetricAlgorithmType.Rijndael, key, salt);

        MetadataSignOptions options = new MetadataSignOptions();
        DocumentSignatureData documentSignature = new DocumentSignatureData();
        
        // Egyéni metaadat-tulajdonságok beállítása
        documentSignature.setID(UUID.randomUUID().toString());
        documentSignature.setAuthor(System.getenv("USERNAME"));
        documentSignature.setSigned(new Date());
        documentSignature.setDataFactor(new BigDecimal("11.22"));

        ImageMetadataSignature mdDocument = new ImageMetadataSignature(41996, documentSignature);
        mdDocument.setDataEncryption(encryption);

        // Metaadat-aláírások hozzáadása a beállításokhoz
        options.getSignatures().add(mdDocument);

        signature.sign(outputFilePath, options);
    }
}
```

#### Kulcskonfigurációs beállítások
- **Szimmetrikus titkosítás**Rijndael algoritmust használ a titkosításhoz.
- **Metaadat-aláírási beállítások**: Konfigurálja az aláírási folyamatot, és meghatározza, hogy mely metaadatokat kell aláírni.

##### Hibaelhárítási tippek
- Győződjön meg arról, hogy a fájlelérési utak helyesek és elérhetők.
- Ellenőrizd, hogy a környezeti változó `USERNAME` megfelelően van beállítva.
- Ellenőrizze, hogy a GroupDocs.Signature függvénytár verziója megegyezik-e a kód függőségeivel.

### Funkció: Metaadat-aláírás titkosítással

#### Áttekintés
Ez a funkció a metaadat-aláírások titkosítására összpontosít, hogy megvédje a képfájlokban található érzékeny információkat.

#### Lépésről lépésre történő megvalósítás
##### 1. Implementálja a titkosítási logikát
A metaadatok titkosítással történő aláírásának módja:
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;
import com.groupdocs.signature.domain.extensions.encryption.SymmetricAlgorithmType;
import com.groupdocs.signature.domain.extensions.encryption.SymmetricEncryption;
import com.groupdocs.signature.exception.GroupDocsSignatureException;
import com.groupdocs.signature.options.sign.MetadataSignOptions;

import java.io.File;
import java.nio.file.Paths;
import java.util.UUID;

public class SignMetadataWithEncryption {
    // Fájlútvonalak inicializálása helyőrzőkkel
    String filePath = "YOUR_DOCUMENT_DIRECTORY/SampleImage.jpg";
    String outputFilePath = new File("YOUR_OUTPUT_DIRECTORY", 
                                       "SignedImageWithEncryption/SampleImage_signed.jpg").getPath();

    public void run() throws Exception {
        Signature signature = new Signature(filePath);

        // Titkosítási kulcs és jelszó beállítása
        String key = "1234567890";
        String salt = "1234567890";
        IDataEncryption encryption = new SymmetricEncryption(
            SymmetricAlgorithmType.Rijndael, key, salt);

        MetadataSignOptions options = new MetadataSignOptions();
        DocumentSignatureData documentSignature = new DocumentSignatureData();
        
        // Egyéni metaadat-tulajdonságok beállítása
        documentSignature.setID(UUID.randomUUID().toString());
        documentSignature.setAuthor(System.getenv("USERNAME"));
        documentSignature.setSigned(new Date());
        documentSignature.setDataFactor(new BigDecimal("11.22"));

        ImageMetadataSignature mdDocument = new ImageMetadataSignature(41996, documentSignature);
        mdDocument.setDataEncryption(encryption);

        // Metaadat-aláírások hozzáadása a beállításokhoz
        options.getSignatures().add(mdDocument);

        signature.sign(outputFilePath, options);
    }
}
```