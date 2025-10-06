---
"date": "2025-05-08"
"description": "Ismerje meg, hogyan írhatja alá biztonságosan a DICOM képeket a GroupDocs.Signature for Java segítségével. Növelje a dokumentumok biztonságát QR-kódok és metaadatok beágyazásával."
"title": "DICOM képek aláírása QR-kódokkal és metaadatokkal a GroupDocs.Signature for Java használatával"
"url": "/hu/java/image-signatures/sign-dicom-images-groupdocs-signature-java/"
"weight": 1
type: docs
---
# DICOM képek aláírása QR-kódokkal és metaadatokkal a GroupDocs.Signature for Java használatával

## Bevezetés

A gyorsan fejlődő digitális egészségügyi környezetben a betegadatok biztonságos kezelése kiemelkedő fontosságú. Ez az oktatóanyag végigvezeti Önt egy robusztus megoldás megvalósításán, amely a GroupDocs.Signature for Java segítségével QR-kódokkal és metaadatokkal írja alá az orvostudományban használt digitális képalkotási és kommunikációs (DICOM) képeket. Ezek a funkciók biztosítják a hitelességet, javítják a nyomon követhetőséget és fenntartják a megfelelőséget azáltal, hogy létfontosságú információkat ágyaznak be közvetlenül az orvosi képekbe.

### Amit tanulni fogsz:
- Hogyan integrálható a GroupDocs.Signature for Java a projektbe.
- DICOM képek QR-kódokkal történő aláírásának folyamata.
- XMP metaadatok hozzáadása a dokumentumbiztonság fokozása érdekében.
- Aláírások lekérése, ellenőrzése és keresése DICOM fájlokban.
- Aláírt DICOM képek előnézeteinek generálása.

Vágjunk bele! Mielőtt belekezdenénk, győződjünk meg róla, hogy minden megvan a rendelkezésedre a zökkenőmentes haladáshoz.

## Előfeltételek

A GroupDocs.Signature funkciók hatékony megvalósításához győződjön meg arról, hogy teljesülnek a következő előfeltételek:

### Szükséges könyvtárak és függőségek
- **GroupDocs.Signature Java-hoz**A függvénykönyvtár 23.12-es vagy újabb verziójára lesz szükséged.

### Környezeti beállítási követelmények
- **Java fejlesztőkészlet (JDK)**Győződjön meg arról, hogy a JDK telepítve van a rendszerén.
- **IDE**Használjon integrált fejlesztői környezetet, például IntelliJ IDEA-t vagy Eclipse-t.

### Ismereti előfeltételek
Alapvető ismeretek a következőkről:
- Java programozás és objektumorientált alapelvek.
- Maven vagy Gradle build eszközök függőségkezeléshez.

## GroupDocs.Signature beállítása Java-hoz

A GroupDocs.Signature használatának megkezdéséhez hozzá kell adnia azt függőségként a projektjéhez. Így teheti meg ezt különböző buildeszközök használatával:

### Szakértő
Add hozzá a következő kódrészletet a `pom.xml` fájl:
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Gradle
Vedd bele ezt a `build.gradle` fájl:
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### Közvetlen letöltés
Vagy letöltheti a legújabb verziót innen: [GroupDocs.Signature Java kiadásokhoz](https://releases.groupdocs.com/signature/java/).

#### Licencbeszerzés lépései
1. **Ingyenes próbaverzió**: Próbálja ki a funkciókat egy korlátozott ideig tartó ingyenes próbaidőszakkal.
2. **Ideiglenes engedély**Szerezzen be egy ideiglenes licencet a teljes funkcionalitás felfedezéséhez.
3. **Vásárlás**: Vásároljon előfizetést, ha hosszú távú hozzáférésre van szüksége.

#### Alapvető inicializálás és beállítás

A GroupDocs.Signature inicializálásához hozzon létre egy példányt a következőből: `Signature` osztály:
```java
import com.groupdocs.signature.Signature;

// Az aláírásobjektum inicializálása a DICOM fájl elérési útjával
Signature signature = new Signature(filePath);
```

## Megvalósítási útmutató

### DICOM kép aláírása QR-kóddal és metaadatokkal

#### Áttekintés
Ez a funkció lehetővé teszi a DICOM képek QR-kóddal történő aláírását és XMP metaadatok hozzáadását, ezáltal fokozva a dokumentum biztonságát.

#### 1. lépés: QR-kód aláírási beállításainak beállítása
```java
import com.groupdocs.signature.domain.Padding;
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.signatures.QrCodeSignOptions;

Padding padding = new Padding();
padding.setRight(5);
padding.setLeft(5);

QrCodeSignOptions options = new QrCodeSignOptions("Patient #36363393. R: No-Issues");
options.setAllPages(true);
options.setWidth(100);
options.setHeight(100);
options.setVerticalAlignment(VerticalAlignment.Bottom);
options.setHorizontalAlignment(HorizontalAlignment.Right);
options.setMargin(padding);
```
Itt konfiguráljuk a QR-kód megjelenését és pozícióját a DICOM képen.

#### 2. lépés: XMP metaadatok hozzáadása
```java
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomSaveOptions;
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomXmpEntry;
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomXmpType;

DicomSaveOptions dicomSaveOptions = new DicomSaveOptions();
List<DicomXmpEntry> xmpEntries = new ArrayList<>();
xmpEntries.add(new DicomXmpEntry(DicomXmpType.PatientName, "Patient #4"));
dicomSaveOptions.setXmpEntries(xmpEntries);
```
Ez a kódrészlet metaadatokat ad a DICOM fájlhoz, további beteginformációkat ágyazva be.

#### 3. lépés: A dokumentum aláírása
```java
String outputFilePath = YOUR_OUTPUT_DIRECTORY + "/SignDicomImageAdvanced/" + fileName;
signature.sign(outputFilePath, options, dicomSaveOptions);
```
A `sign` A metódus a QR-kódot és a metaadatokat a DICOM-fájlba írja, és a megadott helyre menti.

### Aláírt DICOM képadatok lekérése

#### Áttekintés
XMP metaadatok kinyerése aláírt DICOM képből ellenőrzési vagy auditálási célokra.
```java
import com.groupdocs.signature.domain.IDocumentInfo;
import com.groupdocs.signature.domain.signatures.MetadataSignature;

IDocumentInfo documentInfo = signature.getDocumentInfo();
for (MetadataSignature item : documentInfo.getMetadataSignatures()) {
    System.out.println(item.toString());
}
```
Ez a kód lekéri és kinyomtatja a DICOM fájlhoz társított összes metaadat-aláírást.

### Aláírt DICOM ellenőrzése

#### Áttekintés
Ellenőrizze, hogy van-e QR-kód aláírás az aláírt DICOM képen, hogy megerősítse annak hitelességét.
```java
import com.groupdocs.signature.domain.VerificationResult;
import com.groupdocs.signature.options.verify.QrCodeVerifyOptions;
import com.groupdocs.signature.domain.enums.TextMatchType;

QrCodeVerifyOptions verifyOptions = new QrCodeVerifyOptions();
verifyOptions.setAllPages(true);
verifyOptions.setText("Patient #36363393");
verifyOptions.setMatchType(TextMatchType.Contains);

VerificationResult result = signature.verify(verifyOptions);
if (result.isValid()) {
    System.out.println(filePath + " has successfully verified signatures!");
} else {
    System.out.println(filePath + " failed verification process.");
}
```
Ez az ellenőrzési lépés biztosítja, hogy a QR-kód megfeleljen a várt kritériumoknak, megerősítve a dokumentum integritását.

### Aláírások keresése aláírt DICOM fájlokban

#### Áttekintés
Keresse meg az összes QR-kód aláírást egy aláírt DICOM képen belül, hogy áttekinthesse vagy auditálhassa azokat.
```java
import com.groupdocs.signature.domain.signatures.QrCodeSignature;
import java.util.List;

List<QrCodeSignature> signatures = signature.search(QrCodeSignature.class);
for (QrCodeSignature qrCodeSignature : signatures) {
    System.out.println("QRCode signature found at page " +
        qrCodeSignature.getPageNumber() + ": " +
        qrCodeSignature.getEncodeType().getTypeName() + ": " +
        qrCodeSignature.getText());
}
```
Ez a funkció hasznos a dokumentumban található összes QR-kód aláírás beolvasásához, átfogó láthatóságot biztosítva.

### Aláírt DICOM előnézetének létrehozása

#### Áttekintés
Hozzon létre előnézeteket az aláírt DICOM kép minden oldalához, lehetővé téve a gyors vizuális ellenőrzést a teljes fájl megnyitása nélkül.
```java
import com.groupdocs.signature.options.PreviewOptions;
import java.io.File;
import java.io.FileOutputStream;
import java.nio.file.Paths;

PreviewOptions previewOption = new PreviewOptions(pageNumber -> {
    try {
        String pageFilePath = YOUR_OUTPUT_DIRECTORY + "/SignDicomImageAdvanced/image-" + pageNumber + ".jpg";
        return new FileOutputStream(Paths.get(pageFilePath).toFile());
    } catch (Exception e) {
        throw new RuntimeException(e.getMessage());
    }
});

signature.generatePreview(previewOption);
```
Ez a kódrészlet minden oldalhoz képelőnézetet generál, ami hasznos lehet a gyors ellenőrzéshez vagy megosztáshoz.

## Gyakorlati alkalmazások

A GroupDocs.Signature for Java számos valós alkalmazást kínál:
- **Orvosi képalkotás**Biztonságosan írja alá és kezelje a betegek DICOM képeit QR-kódokkal és metaadatokkal.
- **Jogi dokumentumkezelés**A dokumentumok hitelességének és megfelelőségének javítása jogi eljárások során.
- **Pénzügyi szolgáltatások**Biztonságos elektronikus aláírások alkalmazása érzékeny pénzügyi dokumentumokon.