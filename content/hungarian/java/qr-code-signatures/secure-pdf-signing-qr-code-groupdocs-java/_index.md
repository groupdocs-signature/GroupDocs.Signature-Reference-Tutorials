---
"date": "2025-05-08"
"description": "Ismerje meg, hogyan teheti biztonságossá PDF-fájljait QR-kód titkosítással és digitális aláírásokkal a GroupDocs.Signature for Java segítségével. Növelje dokumentumai biztonságát hatékonyan."
"title": "Biztonságos PDF-aláírás megvalósítása QR-kód titkosítással Java-ban a GroupDocs.Signature használatával"
"url": "/hu/java/qr-code-signatures/secure-pdf-signing-qr-code-groupdocs-java/"
"weight": 1
---

# Biztonságos PDF-aláírás megvalósítása QR-kód titkosítással Java-ban a GroupDocs.Signature használatával

mai digitális korban a dokumentumokban található bizalmas információk védelme kiemelkedő fontosságú. A kiberfenyegetések számának növekedése miatt az adattitkosítás a dokumentumkezelés elengedhetetlen részévé vált. Ez az oktatóanyag végigvezeti Önt a biztonságos PDF-aláírás megvalósításán QR-kód titkosítással a GroupDocs.Signature for Java segítségével. A cikk végére felkészült lesz arra, hogy robusztus biztonsági funkciókat integráljon alkalmazásaiba.

## Amit tanulni fogsz:
- A szimmetrikus adattitkosítás megértése Java nyelven
- Egyéni aláírási osztály létrehozása
- QR-kód aláírások konfigurálása egyéni adatokkal és igazítással
- GroupDocs.Signature integrálása a biztonságos PDF-aláíráshoz

Készen állsz a belevágásra? Kezdjük is!

## Előfeltételek
Mielőtt elkezdenénk, győződjünk meg arról, hogy a következőkkel rendelkezünk:
- **Java fejlesztőkészlet (JDK):** 8-as vagy újabb verzió.
- **Maven vagy Gradle:** Függőségek kezeléséhez. Válasszon a projekt beállításai alapján.
- **Java programozási ismeretek:** Az objektumorientált programozás alapjai Java nyelven.

## GroupDocs.Signature beállítása Java-hoz
A GroupDocs.Signature használatának megkezdéséhez hozzá kell adnia azt függőségként a projektjéhez. Ez a könyvtár hatékony eszközöket kínál a digitális aláírások és a dokumentumok titkosításának kezeléséhez.

### Maven beállítás
Adja hozzá a következő függőséget a `pom.xml` fájl:
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Gradle beállítása
Gradle felhasználóknak ezt is bele kell foglalniuk a listájukba. `build.gradle` fájl:
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### Közvetlen letöltés
Vagy töltse le a legújabb verziót innen: [GroupDocs.Signature Java kiadásokhoz](https://releases.groupdocs.com/signature/java/).

### Licencszerzés
A GroupDocs.Signature ingyenes próbaverziójával értékelheti a funkcióit. Hosszabb távú használat esetén érdemes lehet licencet vásárolni, vagy ideiglenes licencet igényelni a weboldalukon keresztül.

## Megvalósítási útmutató
Ez az útmutató főbb részekre oszlik, amelyek az adattitkosítást, az egyéni aláírás létrehozását és a QR-kód aláírás konfigurálását tárgyalják.

### Adattitkosítás szimmetrikus algoritmussal
Az adatok titkosítása biztosítja, hogy azok biztonságban maradjanak az átvitel és a tárolás során. A szimmetrikus titkosítás beállítása a GroupDocs.Signature használatával:

#### Szimmetrikus titkosítás beállítása
1. **Szükséges csomagok importálása:**
   ```java
   import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;
   import com.groupdocs.signature.domain.extensions.encryption.SymmetricAlgorithmType;
   import com.groupdocs.signature.domain.extensions.encryption.SymmetricEncryption;
   ```
2. **A titkosítási objektum inicializálása:**
   Használjon biztonságos kulcsot és sót a titkosításhoz. `"YOUR_SECURE_KEY"` a saját kulcsaiddal.
   ```java
   String key = "YOUR_SECURE_KEY";
   String salt = "YOUR_SECURE_SALT";

   IDataEncryption encryption = new SymmetricEncryption(
       SymmetricAlgorithmType.Rijndael, 
       key, 
       salt
   );
   ```
   - **SzimmetrikusAlgoritmusTípus.Rijndael:** Ez határozza meg a használandó szimmetrikus algoritmus típusát.
   - **Kulcs és só:** Győződjön meg arról, hogy ezek egyediek és biztonságosak az alkalmazásához.

### Egyéni adataláírási osztály
Egyéni osztály létrehozásával hatékonyan kezelheti az aláírás tulajdonságait. Így teheti meg:

#### A meghatározása `DocumentSignatureData` Osztály
```java
class DocumentSignatureData {
    private String ID;
    private String Author;
    private Date Signed = new Date();
    private BigDecimal DataFactor = new BigDecimal(0.01);

    public String getID() { return ID; }
    public void setID(String value) { ID = value; }

    public final String getAuthor() { return Author; }
    public final void setAuthor(String value) { Author = value; }

    public final Date getSigned() { return Signed; }
    public final void setSigned(Date value) { Signed = value; }

    public final BigDecimal getDataFactor() { return DataFactor; }
    public final void setDataFactor(BigDecimal value) { DataFactor = value; }
}
```
- **Azonosító, Szerző, Aláírás:** Ezek a mezők tárolják az aláírás metaadatait.
- **Adattényező:** Az alkalmazás logikájához kapcsolódó numerikus értéket tartalmaz.

### QR-kód aláírási beállítások
A QR-kódok kompakt módon beágyazhatják az információkat. Konfigurálja őket egyéni adatokkal és titkosítással:

#### QR-kód aláírások beállítása
1. **Inicializálás `Signature` Objektum:**
   ```java
   import com.groupdocs.signature.Signature;
   
   Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY");
   ```
2. **QR-kód beállításainak konfigurálása:**
   ```java
   import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
   import com.groupdocs.signature.options.sign.QrCodeSignOptions;
   import java.util.UUID;

   DocumentSignatureData documentSignature = new DocumentSignatureData();
   documentSignature.setID(UUID.randomUUID().toString());
   documentSignature.setAuthor(System.getenv("USERNAME"));
   documentSignature.setDataFactor(new BigDecimal("11.22"));

   QrCodeSignOptions options = new QrCodeSignOptions();
   options.setData(documentSignature);
   options.setEncodeType(QrCodeTypes.QR);
   options.setDataEncryption(encryption); // Használja a titkosítási objektumot
   options.setHeight(100);
   options.setWidth(100);
   options.setVerticalAlignment(com.groupdocs.signature.domain.enums.VerticalAlignment.Bottom);
   options.setHorizontalAlignment(com.groupdocs.signature.domain.enums.HorizontalAlignment.Right);

   import com.groupdocs.signature.domain.Padding;
   Padding padding = new Padding();
   padding.setRight(10);
   padding.setBottom(10);
   options.setMargin(padding);
   ```
   - **Kódolás típusa:** Megadja a QR-kód formátumát.
   - **Igazítás és margó:** Szabja testre a QR-kód megjelenését a dokumentumon.

### Példahasználat
Dokumentum aláírása a konfigurált beállításokkal:
```java
signature.sign("YOUR_OUTPUT_DIRECTORY/QRCodeEncryptedObject.pdf\